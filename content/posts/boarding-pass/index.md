---
title: "Never Post A Picture Of Your Boarding Pass On Social Media"
date: 2019-03-24
draft: false
tags: ["security", "privacy", "boarding-pass", "airlines", "social-media", "barcode", "travel"]
categories: ["security", "privacy", "travel-security"]
description: "Comprehensive analysis of security risks associated with posting boarding pass images on social media and recommendations for airlines to improve security"
---

Whenever I go on a trip I do the mandatory Check-in at Facebook, Twitter and Instagram, saying where I am going, who my travel-mates are, how many days I will be away and I post a picture of my Boarding-pass to prove it. I love doing it, its super cool for my friends and anyone who follow me! But sadly I am not aware of what an adversary can do with just my airplane boarding pass.

Let's see what an adversary can do with a photograph of my boarding pass:

- Get my full name
- Get my seat, flight time, destination
- Get my PNR and E-ticket number (starts to get bad from here)
- Login to the Airlines' website via my name and PNR
- See my email-id, phone number, home address, other booked flight details (worse coming up)
- Cancel my upcoming flights
- Modify my name, phone number, email-id

And now I am wondering, should I really cool to post pictures of my boarding pass over social media if these are the consequences? No, no you should not.

Most people, who are smarter than I am, would never publish the details of their PNR and E-ticket number and scribble over them in their picture. Smart people know that this will make them secure against the scenarios I describe above.

But wait, what about the barcode?

{{< figure src="one.png" alt="Boarding pass photo" align="center" >}}

People forget to hide the Barcode, not knowing that the barcode will give away all of the information which the person has scribbled over. These barcodes can be easily read on phone apps like Android ([PDF417 Barcode Scanner](https://play.google.com/store/apps/details?id=mobi.pdf417&hl=en_US)) or iOS ([BP Scanner](https://itunes.apple.com/us/app/bp-scanner/id1166018608)), or can be uploaded on a web-service ([ZXing](https://zxing.org/w/decode.jspx)) to fetch the data.

There has been research conducted around this subject ([Wonderhowto](https://null-byte.wonderhowto.com/how-to/hackers-use-hidden-data-airline-boarding-passes-hack-flights-0180728/) and [Kaspersky](https://www.kaspersky.com/blog/dont-post-boarding-pass-online/10495/)), but the Airlines have provided no solution to this, they do not even bother telling people not to post their boarding passes online. The problem with this is that most airlines still allow anyone to login with just their last-name and PNR!

Instead of educating the billions of flyers over not to post boarding-pass pictures, it would be better if the bunch of Airlines implement better security for their customers' data and start taking their travel privacy seriously.

It's not always the users' fault if they post pictures of their boarding passes. Some users may have a problem with their booking and quite naturally head over to their airlines twitter support, providing their PNR and flight details publicly. In this case the user was not trying to show off, but get some information or help with a booking.

{{< figure src="two.png" alt="Boarding pass photo" align="center" >}}

## Imagine some scenarios like this:

- I live in Tokyo. I create a script that will notify me whenever someone posts a boarding-pass or PNR and the keyword #tokyo, it will give me an alert. John Doe is traveling from London to Tokyo today and posts his boarding-pass. His next flight from Tokyo to Sydney is tomorrow. I can login to his account on the Airlines' website, cancel the ticket to Sydney and strand him in Tokyo airport. Since he is in flight, he will get no notification of his flight cancellation until he reaches Tokyo. If the website also allows me the option to update the flyer details I can change his name to my name, give my email address and print the ticket.
- I can change the meal preferences of a vegan passenger to non-vegan meal.
- Use the frequent-flyer miles to upgrade my own bookings.
- I can request a wheel chair for the flyer when he lands at the Tokyo airport.
- Competitor airlines can sell their tickets to this flyer by targeted advertisements, can sell cheaper deals (flyer's email and phone number are available).
- If a couple is traveling on the same PNR, I can select two seats at different ends of the plane (Seat # 1A and 30D) to annoy them.
- I can blackmail the flyer or sell their itinerary to business rivals or close relatives if I sniff that the flyer is traveling with someone important (maybe cheating).

{{< figure src="three.png" alt="Boarding pass photo" align="center" >}}

There are 109932 images tagged with #boardingpass on Instagram right now.

Attackers can use other tags to search for images, or use the location of an airport where there are chances of people posting their boarding-pass. Also, instead of posting it as a permanent picture, people are posting their boarding-pass as Instagram story. I can gradually start following tens, hundreds and then thousands of people on Instagram, who will make their story visible to me. A bot can be created to look for any possible image of boarding-pass in their stories. Similarly, a search on Twitter for boardingpass, PNR, flight, airport will give list of images and tweets containing the flyer's name and PNR number. It's a jungle out there!

## What should the airlines do to prevent this or minimize the impact:

**(a)** When you login they ask for the PNR and last-name/first-name. They should also ask for some data unique to the user which is cannot be normally present in a tweet or Instagram post - e.g. Date of Birth (I agree this can be easily obtained for some users, but not all), Phone number or email-address (somewhat tough to get, but not a full-proof solution), exact data and time of booking the ticket (user can get these details from the confirmation mail, while the attacker can't)

{{< figure src="four.png" alt="Boarding pass photo" align="center" >}}

**(b)** In case a traveler wants to make modifications to seat, meal preferences, up-gradation - the traveler may need to provide an OTP sent to their email (this should not be hard for the traveler to provide, since all airports are WiFi enable now). Other mechanisms to solve this can also be discussed

**(c)** Cancellation of tickets should not be very easy. A second factor of identification/authentication should be strictly enforced here. The Credit-card number or Bank account details used to book the ticket should be asked at this stage, which are not very easy to obtain.

Can we start an online campaign, asking the Airlines to implement something secure?

For getting the trends and to know the state of some local and international airlines, I took the liberty to go through the public posts of travelers and login to their accounts. I did not make any changes to the travelers' data or obtain them for personal/commercial use. I accessed the accounts for checking the authentication mechanisms using publicly available data only.

## Here is the list of airlines I could go through during my free time:

- Spicejet

{{< figure src="five.png" alt="Boarding pass photo" align="center" >}}

- Vistara

{{< figure src="six.png" alt="Boarding pass photo" align="center" >}}

- Spirit Airlines

{{< figure src="seven.png" alt="Boarding pass photo" align="center" >}}
{{< figure src="eight.png" alt="Boarding pass photo" align="center" >}}

- Jet Airways

{{< figure src="nine.png" alt="Boarding pass photo" align="center" >}}

- Go Air

{{< figure src="ten.png" alt="Boarding pass photo" align="center" >}}

- Aeroflot

{{< figure src="eleven.png" alt="Boarding pass photo" align="center" >}}
{{< figure src="twelve.png" alt="Boarding pass photo" align="center" >}}

- American Airlines

{{< figure src="thirteen.png" alt="Boarding pass photo" align="center" >}}