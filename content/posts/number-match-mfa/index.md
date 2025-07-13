---
title: "MFA - Why do we match numbers to approve MFA sign-in?"
date: 2023-07-23
draft: false
tags: ["MFA", "cybersecurity", "authentication", "technology"]
categories: ["Security", "Technology"]
description: "Understanding why modern MFA systems require number matching instead of simple approve/deny buttons to prevent MFA fatigue attacks."
---

This post is mainly for users who use MFA authenticator apps on their smartphones. Earlier the process was to click either "Yes (Approve)" or "No (Deny)" and that would allow to login. Why is now one more step required to enter a value shown on the login page?

## Background

We have been using passwords since years to secure our digital accounts. Since people need to have passwords for several different services and it becomes tough to remember them, they started to either (a) reuse the same password, (b) use an easy password, (c) write down the different passwords.

It became easy for attackers/hackers/fraudsters to either guess these passwords or brute-force them (try millions of possible passwords), or maybe scan through your personal diary to check the password, or glance through your screen while you are typing. Hence the concept of 2FA was introduced, where you provide one more layer of identity (prove that you are the real owner of this account).

The most common technique for 2FA is an OTP sent over to the user via SMS (phone carrier's network). Attackers started abusing these functionality and there were many researches to prove that this option is not safe. Big companies came up with the authenticator applications (Authy, Google Authenticator, Microsoft Authenticator, PingID) which would send you a push notification to either approve or deny the authentication requests.

Attackers were able to bypass this by using a technique called '[MFA Fatigue](https://www.theregister.com/2022/11/03/mfa_fatigue_enterprise_threat/)' or '[MFA Bombing](https://portswigger.net/daily-swig/mfa-fatigue-attacks-users-tricked-into-allowing-device-access-due-to-overload-of-push-notifications)'. In case they get hold of your password, they would still need to have an Approval sent from your authenticator app, which you are not going to provide easily. They would bombard you with hundreds of such push-notifications (or maybe voice calls or other social-engineering techniques), hoping that you would click on 'Approve' at least once – and that would open the door to your account. Last year a networking giant company was breached by the same method.

What would you do if you received hundreds of such requests within a few minutes? Probably click Approve to get rid of that spam, thinking there is some glitch on the app's platform?

## Answer

Security is always a cat and mouse game. Researchers came up with a simple technique to avoid MFA Fatigue - the user needs to enter the number shown on her screen into her authenticator app. When this is implemented, the number for each MFA request would be different, meaning when the attacker tries to send several requests and hopes that the user would approve, it would not happen. The attacker would need to match the exact number for that particular action, and the possibility is near to zero (in an ideal world).

{{< figure src="mfa-number1.png" alt="Alt text" caption="Selected the Microsoft Authenticator app for MFA" align="center" >}}
{{< figure src="mfa-number2.png" alt="Alt text" caption="Need to enter 84 on my Authenticator app" align="center" >}}

Some months back, Microsoft enforced the number-matching for users who use Authenticator app, along with other vendors providing similar functionality (Duo, Okta). In case you are interested to read more, here is a [document from CISA](https://www.cisa.gov/sites/default/files/publications/fact-sheet-implement-number-matching-in-mfa-applications-508c.pdf). Also, if you are an Azure admin, [this guide](https://learn.microsoft.com/en-us/azure/active-directory/authentication/how-to-mfa-number-match) has some more details regarding the number matching functionality in Microsoft Authenticator.