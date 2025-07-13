---
title: "A free gift with the dynamic IP"
date: 2013-09-30
draft: false
description: "Experience switching from Tata Docomo to Vodafone 3G and discovering my new IP address was blacklisted by Spamhaus due to previous Cutwail botnet activity"
tags: ["networking", "ISP", "dynamic-ip", "spamhaus", "blacklist", "3G", "internet"]
categories: ["Technology", "Networking"]
---

Hello! One more post for the day.

Until now, I have been using the 3G internet by Tata Docomo. They were generous and gave me IP addresses without any kind of conversion. Means whatever IP I get on my ppp0 interface with ipconfig, is the same IP I get by the Google search 'whats my ip'. Though they were dynamic IPs, they reached me without any translations.

Last week I switched to a new provider, Vodafone 3G. I don't know what kind of addressing scheme they are using, but definitely they gave me something more with the IP. Here on my laptop, on the ppp0 interface I have private IP address of 10.119.69.xx, which is further translated by NAT at their side and converted to 1.38.29.123. Mostly we (here 'we' refers to the whole group of people whose NAT address is converted to the specified IP, and you can consider the number of people in a class-A scheme) are given that IP address on the outside, while the inside address keeps changing.

Now, what's the problem with that IP? Because, Spamhaus has black-listed that IP. Here's the link: [Spamhaus haz my IP black-listed](http://cbl.abuseat.org/lookup.cgi?ip=1.38.29.123). Reason? Before some days/months/years, that IP was a member of [Cutwail spambot](http://en.wikipedia.org/wiki/Cutwail_botnet) and kept sending spam mails. My first reaction on reading this was – let me check if I am affected with that spyware/bot. Additionally, there are some cons of getting black-listed by the Spamhaus » online services (like port-scans, some forums) will block you, and the main problem will be with the SMTP.

Two things need to be done:

1. Spamhaus should have kind-of dynamic listing
2. Else ISPs should be taking actions for getting the IP out of Spamhaus' black-list.

Will be soon contacting my ISP for further discussions on the issue.

PS – I'm safe. 🙂 No cutwail here.