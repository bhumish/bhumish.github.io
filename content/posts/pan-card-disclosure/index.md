---
title: "UTI ITSL – Data Disclosure through a single key"
date: 2017-03-18
draft: false
tags: ["security", "privacy", "vulnerability", "data-disclosure", "pan-card", "india"]
categories: ["Security Research"]
description: "A security vulnerability in UTI ITSL's PAN card tracking system that exposes personal information of millions of applicants through sequential application numbers."
---

NSDL and UTI are two bodies under the Indian Government which are the official PAN Card service providers. Recently I had the privilege to take services for PAN Updation through UTI ITSL.

After waiting for some time for the processing of my card, I went to the website of [UTI-ITSL](http://www.trackpan.utiitsl.com/PANONLINE/) for checking the status. I entered the application number, and instantly got the status of my query. Cool!

As a fuzzer, in the form-field for 'Application Coupon Number', I entered the next number (my application number + 1). And yes, it gave the results. Entered some more numbers in the sequence, got results for each query. I could get results for applications as early as 2011. This means that if someone runs a tiny script to scrape data of applicants for the last 8 years, they can easily get the details – Full name, PAN Number, Application Number.

{{< figure src="1.png" alt="Image" caption="Name, PAN No, Courier Tracking Details" align="center" >}}

As shown in the above image, all these details are visible to everyone without any kind of authentication, you need to just input a 9-digit application number.

And there is something more to that – you can look for the PIN Code and City of the applicant, through the Courier Tracking Number:

{{< figure src="2.png" alt="Image" caption="This PAN Card was delivered to some guy in RANPUR (Gujarat) on 09-03-2017, most probably he lives there" align="center" >}}

If you are more lucky, you will get the birth-date and spouse/father's name of the applicant:

{{< figure src="3.png" alt="Image" align="center" >}}

For the above applicant, he is having name mismatch between Income Tax Department's Data and the data provided in the application. So which fields are required to be shown to the applicant – only the field which is having some conflict, right? No, even if the DOB which is totally irrelevant in this case of name mismatch, it is shown. Proof below:

{{< figure src="4.png" alt="Image" caption="In case of Name mismatch (field highlighted by pink by the UTI guys), Father Name and DOB are also displayed" align="center" >}}

With some modification in the script to scrape all this data, we can fetch the DOBs for all the people who are having such mismatch in their application. Later through correlation, we can get the below details for a single applicant:

- Applicant's full name
- Applicant's Father's full name
- Applicant's DOB
- Applicant's PAN Number
- Applicant's PIN Code and City

This can count as a huge flaw in the design of their application which gives such golden data with very less efforts, and exposes the PII of millions of applicants.

Some suggestions for UTI developer guys:

- Randomize the application numbers, if possible, and
- Please do not allow anyone to query your database with a single key. At-least use two keys (e.g. 1. Application Number & Date – Time of application, 2. Application Number & UID Number)
- Don't provide the status if it has been a month after the PAN card is received by the applicant

(I tried to contact the people at UTI ITSL: their email ([utiitsl.gsd@utiitsl.com](mailto:utiitsl.gsd@utiitsl.com)) bounces back, no-one picks up the phone, and snail-mail I am not sure.)

Eti.