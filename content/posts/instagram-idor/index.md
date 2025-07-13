---
title: "Instagram - Your posts are not really private"
date: 2016-02-25
draft: false
tags: ["security", "privacy", "instagram", "idor", "access-control", "social-media"]
categories: ["Security Research"]
description: "A privacy vulnerability in Instagram where private posts can be accessed by anyone with the direct link, bypassing follower-only restrictions."
---

You are using Instagram, right? And you might have kept your posts private, so that only your followers can view your posts. Yes, even I have ticked the option to allow only my followers to view my posts.

{{< figure src="1.jpg" alt="Image" align="center" >}}

That option works well if you are browsing through Instagram only. But what if you post your Instagram picture's link like this:

{{< figure src="2.png" alt="Image" align="center" >}}

The post on your Instagram profile was limited only to your followers (maybe 150, 1500 or 150k), but now your tweet has made that picture available to millions of people who are on the Internet. Anybody can click on the link and see your picture.

{{< figure src="3.png" alt="Image" caption="My Instagram picture, as viewed in logged-out mode (https://www.instagram.com/p/BB4FvaowiZvxmolkohvwNRpf97HWls0Rel9wZI0/)" align="center" >}}

Although, when you visit my profile, you will see that my account is private!

{{< figure src="4.jpg" alt="Image" align="center" >}}

I was not trying for any bug-bounty, accidentally discovered this from my Twitter when I clicked the link.
Instagram should follow one rule- if an user opts to have a private profile, you need to make sure (from server side) that the posts remain visible only to the followers on Instagram. Need to have better access control.