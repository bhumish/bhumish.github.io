---
title: "Your Eureka Forbes account can easily be hacked!"
date: 2020-04-11
draft: false
tags: ["vulnerability", "security", "eureka-forbes", "otp-bypass", "cybersecurity", "responsible-disclosure"]
categories: ["Security", "Vulnerability Research"]
---

I am a customer of Eureka Forbes, and last year I was accessing their website for making a payment. I own an Aquaguard Water Purifier by them and wanted to pay for the yearly maintenance contract (AMC).

For anything related to your account, you need to login via their website ([https://www.eurekaforbes.com/](https://www.eurekaforbes.com/)). There is currently only 1 mechanism available for login – **OTP Login**. You provide your phone-number (registered with Eureka Forbes) and they send an SMS OTP to your phone.

## The Vulnerability

There is a flaw in this mechanism. By using this flaw, anybody can login to anybody's Eureka Forbes account — just by entering their phone number (needs to be linked with Eureka Forbes). As per Eureka Forbes, they have 20 Million customers – means I can literally enter phone-numbers sequentially and login to many accounts.

## What's at Risk?

What's the harm (or profit) in entering someone else's account? By knowing/guessing a phone number, from their account I can view details like:

- Full name
- Email-id
- Address (Home/Office/Business)
- Order Details
- AMC Details
- Service Request Details
- Download Invoices

Not just view, I can also edit the customers details. Just a scenario – I am out of my AMC duration, so I login to some account who has paid for the AMC, change their address to my address and later log a Service-Request to do the servicing (for free)! Another scenario is, fraudsters can harvest this data for selling.

## Actions taken from my side:

As soon as I observed this flaw, I tried to inform Eureka Forbes regarding this issue. The initial point-of-contact (customer care – 18602661177) was useless – the Executive never connected me to someone technical. 

Next was to contact them over email – on Jan 17, I sent an email to:
- deepa.customercare@eurekaforbes.com
- customerservice@eurekaforbes.com (email-ids observed on their website)
- shailendrakulkarni@eurekaforbes.com
- suchetadadarkar@eurekaforbes.com (on LinkedIn, both have listed their jobs as IT Managers at Eureka Forbes)

I did not get a reply. Found a Regional Head over LinkedIn and messaged her, but she didn't reply.

Later I got information that **Quinnox** ([www.quinnox.com](https://www.quinnox.com)) was the one who manages the IT and Websites for Eureka Forbes. Tried contacting one of their employee over LinkedIn, asking him to connect me with someone who can look into this — never got a reply.

My last option was to contact **CERT-IN** (the Indian Gov's Computer Emergency Response Team) for this issue. I provided all the technical details (HTTP Traffic, steps to reproduce) over email on 25 Feb 2020. Earlier they were not able to reproduce the issue at their side, so I provided screenshots and more details in the subsequent communications. That day I got many OTPs trying to login to my account – I guessed someone at CERT-IN was trying to test the issue (in the steps and screenshots I had provided my phone number, so they might have tested using my number). I tried to check if they were able to test this and again a follow-up mail after a week, but they never replied.

## Current Status

The issue is still **OPEN** on the website (today, 11 April 2020). Anybody can login to someone's Eureka Forbes account by just knowing their phone number. If you know someone who works at Eureka Forbes or Quinnox, please ask them to contact me at bhumish[at]live[dot]com.

## Timeline

- **January 2020**: Discovered the vulnerability
- **January 17, 2020**: Contacted Eureka Forbes via multiple channels
- **February 25, 2020**: Reported to CERT-IN with technical details
- **April 11, 2020**: Vulnerability still exists, going public

## Key Takeaways

1. **OTP-based authentication** can have implementation flaws
2. **Responsible disclosure** doesn't always work - companies may ignore security researchers
3. **Customer data privacy** is at risk when companies don't prioritize security
4. **20 Million customers** potentially affected by this single vulnerability

*This is a case study in responsible disclosure and the challenges security researchers face when trying to help companies fix vulnerabilities.*