---
title: "Login Bypass Vulnerability on a famous Indian Restaurant chain"
date: 2018-08-30
draft: false
tags: ["MFA", "bug-bounty", "authentication", "security"]
description: "Story on how easily anyone could have logged in to your foodie account."
---

**TLDR**: While ordering dinner for me, I came across a bug where I could login to anybody's account and view their details (like name, email address, home address, order details). This issue was fixed on the same day of reporting to the concerned technical team.

Let's name the company **FoodieExpress**, which serves fast-food in their restaurants, allows take-away of food and does home-delivery of food (when ordered over call, mobile app or website).

## The Authentication System

For login to their website/mobile-app, there is only one method – **OTP login**. You have to enter your registered mobile number, you will receive an OTP and enter it on the screen – you will be logged in. In case the number is not registered, OTP will be sent to the number and you have to provide your details (name, email-id, delivery address, etc).

## The Vulnerability

The issue was here – **you can bypass this OTP and login into anybody's account**. If the user is not registered then you can create their account without any consent.

## Normal Login Flow

For trying one happy/valid scenario, let's order some food from FoodieExpress. My number `1234512345` is already registered with them.

1. When I click on 'Sign In / Register' button on FoodieExpress website's Homepage, it takes me to the Login page (https://foodieexpress.co.in/login).
2. Page asks me to provide my mobile number, where I provide `1234512345` as my number.
3. I receive an OTP on my phone, lets say `9876`.
4. I provide OTP `0000` on the next page – it says 'Invalid OTP!'
5. Correct OTP `9876` is provided, and it allows me to login. After login, I am able to go through my profile to see my personal details, saved addresses, order history, track and existing order, etc.

## Technical Details

Something technical, what happens at the back-end in the above scenario:

An API call, named `api/cart/validate-cust-otp` is made to the server `foodieexpress.co.on:443`, which contains the OTP entered by the user. For example:

```json
{
  "otp": "9876"
}
```

Server checks the OTP, either it is correct or incorrect and responds to the browser accordingly. The HTTP response can be either of these two:

### (a) If the OTP is incorrect
```json
{
  "messageCode": 1015,
  "Message": "OTP is Invalid or Expired",
  "ErrorCode": 0
}
```

### (b) If the OTP is correct
```json
{
  "messageCode": 1001,
  "Message": "Successful",
  "ErrorCode": 0
}
```

The browser proceeds on the basis of this response from server. If we make changes to this response message by using a Proxy tool (e.g. Burp suite), the browser will be unaware of that and may allow us to proceed considering the modified response from proxy.

Both these above responses are used to exploit the security issue.

## How to exploit

1. Setup your browser to use a proxy for HTTP/S request-responses
2. Enter your desired mobile number (can be your friend's number, or any unknown victim's number)
3. OTP will be sent to that number, and you are not aware about the OTP
4. Enter the OTP as any random 4 digit number (e.g. `0000`, `1234`, `2521`, `0914`) and intercept its HTTP response
5. This HTTP response will be similar to **(a)** mentioned above, replace the text with the content given for **(b)** – successful
6. This will tell the browser that authentication is successful and later all the further process will take place considering the authentication of victim user
7. **You will be logged in to the victim's account!**

## Resolution

Logging in to someone else's account is this easy – by just changing the authentication response! Later I had a discussion with the security team managing the website, they understood the issue and fixed it on the same day – a very quick response from their side.

---

*Here I am not providing any details about the Restaurant chain or the Web-development company, as requested by the stakeholders.*