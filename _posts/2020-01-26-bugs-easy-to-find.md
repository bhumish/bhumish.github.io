---
layout: post
title:  Bugs — Easy To Find, Tough To Report
date:   2020-01-26 14:01:35 +0300
image:  '/assets/img/bugs-01.png'
tags:   security, infosec
---

A common complaint that you often hear in Infosec is how hard it can be to report vulnerabilities sometimes. This story tells of my journey using OSINT tools to find the right person to responsibly report a bug to. Of course, I enjoyed the journey more than the destination.

---

#### The story of my bug: 

Even today, you can still find lots of misconfigured S3 buckets chock full of juicy data. I recently found one which contained a lot of personal documents belonging to the employees of a electric vehicle startup, lets refer to them with a made up name to save them some face. Lets call them EVzap.

EVzap provides their electric vehicles to cab companies along with their own trained drivers for the vehicle. These drivers need to provide their documents, things like their driving license, proof of ID, tax documents, proof of address and so on to the company for their background verification. Later EVzap provides their own EV driving permit to these drivers, along with the report of background verification. All these documents were publicly available in their poorly configured bucket.

Finding the bucket was very easy, a few keyword searches for the filenames and you get your data. The tough part for me was what comes next, how to contact this company and responsibly report the vulnerable bucket leaking personal data.

---

#### How I got to the right person: 

I took my first step and checked the Contact page on their website to shoot then an email and I instantly got a reply, there was no such email address and my mail had bounced. At that moment I felt pity for EVzap, they couldn’t even setup a simple email, one which was their primary contact listed on their website. Later I searched for the email-id of some employees, but happened to find only one, the email-id of their CEO. I thought it was alright to mail him for this issue, since I couldn’t find any other contacts and the issue was critical. I sent him an email, but nothing happened for 3 months. I almost forgot about that bucket full of data.

But then last week I remember them and realized that I had to find someone at EVzap and ask them to remove the (still publicly available) personal data. After an intensive search on Google I found a phone number for their office. Ironically, this number was not om their Contact page, I found the number from an article I stumbled across which talked about a partnership between EVzap and a cab company.

I called their office but the receptionist was clueless about ‘who handles their software’ or ‘who the IT person was’. She did gave me the number of a person handling their engineering division though, so I called the engineer who was helpful,  he said “Oh, so you need to contact Alvin for that. Wait, I can share his email address after confirming with him. Call me in the second half of today.“

I thanked him and felt relieved, I then tried searching for Alvin on LinkedIn, he was there but was not very active. I sent him a connection request, hoping I would connect with him and I called the engineer later in the day but he didn’t pick up my call. I texted him but never got a reply. I started to feeling pity as their bucket still leaked.

The next day I looked for more employees of EVzap on LinkedIn and found some people from their tech department. I knew that the domain of their emails would be “@evzap.co” so tried to guess the email-id like “name@evzap.co”, “name.lastname@evzap.co”, “name-initial+lastname@evzap.co”. Some emails bounced, some never saw a reply. I added one more guy from EVzap on LinkedIn, and he was quick to accept. I messaged him about the issue and he also said the same thing – you need to contact Alvin, here’s the LinkedIn profile of Alvin. I mentioned that Alvin doesn’t seem to be active on LinkedIn, and requested him to give Alwin’s official email-id. He quickly shared Alwin’s official address and I was very thankful!

So now I had the official email address of the right guy. End of the story? Nope!

I mailed Alvin, but he didn’t reply. I waited a day, sent a follow-up but still no reply. I wanted Alvin’s phone number, so I went to his LinkedIn profile and saw something interesting – he was the founder of an IT consulting company.

Tried searching for that company, found their website which proudly displayed the message “Under Maintenance”. More research told me that the company had been permanently closed since 2018. Now the Wayback machine (archive.org) ccame to my rescue – I went to the last snapshot of that company’s website. That snapshot also contained their Contact page, which this time had a phone number listed. How to know if this number belonged to some HR person or Marketing guy or the Receptionist? Truecaller comes to my help. When I entered that number in Truecaller, the search result said – Alvin Philip. Now I got a feeling of achievement which was was even better than the moment when I have found that open bucket with all the PII data.

Quickly I gave a call to Alwin on that number, he picked up and I told him about the bug. He was totally unaware that such mis-configurations happen in S3. I explained him all the details – how I found the bug, what documents were exposed, what he needed to fix. He confirmed everything with his laptop in front of him, thanked me and said that he would reply to my mail. Next day the bucket stopped being leaky.

I still haven’t received an email reply from Alvin though.

The moral of the story is that the tools that we use in our daily life can be super helpful, we just need to tweak them according to our need.

Also that bugs remain hard to report and ours can be a thankless job sometimes 🙂
