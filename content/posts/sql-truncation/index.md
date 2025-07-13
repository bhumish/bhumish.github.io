---
title: "SQL Truncation Vulnerability"
date: 2014-02-25
draft: false
tags: ["sql-injection", "sql-truncation", "web-security", "vulnerability", "owasp", "authentication-bypass"]
categories: ["Web Security"]
description: "Understanding SQL Truncation vulnerability - an often overlooked security flaw that can lead to authentication bypass and account takeover attacks."
---

**SQL Injection**. At the top in the [OWASP Top 10](https://www.owasp.org/index.php/Top_10_2013-Top_10) List.

I was going through some missions, and came across one with **SQL Truncation vulnerability**. It is an ignored vulnerability, and many have patched the vulnerability, but there are lots of websites which still have this vulnerability. Here I'm explaining you (ELI5) the basics of SQL Truncation and how the vulnerability is exploited.

## The Scenario

Let's take an example of a website where a user can register himself with a username and password, and later login with the same username-password combination. Let's name this website `pikachu.com`.

Whenever a user registers the username and password, using SQL they are stored in the table. For the table, there is some specific **maximum-length** for the username and password. Let's consider that the username and password should be **max 20 characters**.

In the HTML form, the following would be given:

```html
<td><label>Select an Username: </label></td>
<td align="right"><input type="text" name="username" value="" maxlength="20" /></td>

<td><label>Select a Password: </label></td>
<td align="right"><input type="text" name="password" value="" maxlength="20" /></td>

<td><label>Verify Password: </label></td>
<td align="right"><input type="text" name="password" value="" maxlength="20" /></td>
```

This enforces the user to have username-password of maximum length **20 characters** only.

## Normal Registration Process

Now, suppose the user enters `pokemon` as the username and some random password. It will be checked in the column of usernames whether a username `pokemon` exists or not. If the username does not exist, the table will store `pokemon` under the username column and the password for it in the password column. Here `pokemon` is the administrator of the website.

## The Attack

Now, we are the attackers and we want to login to that site with the username `pokemon`. Possible? Yeah, **possible if it is vulnerable to SQL Truncation**. The following scenario:

### Step 1: Bypass Client-Side Validation
- Use the add-on **Web Developer** (for Firefox) or something similar in your browser, to break the `maxlength=20` barrier.

### Step 2: Create Malicious Username  
- Create a new user `pokemon                    b`, which exceeds 20 characters. After `pokemon` you need to have **white spaces** filling the 20 characters and then some random characters.

### Step 3: Database Storage
- The application will search in the username column for `pokemon                    b`, and doesn't find any so will store it in the database with our password. 
- But since the **max limit is 20 characters**, it will store only `pokemon                    ` and since there are only white spaces, it becomes `pokemon`. 
- If we provide just `pokemon ` at the username registration, it will take only `pokemon` as it truncates the white spaces – and hence we gave `pokemon                    b` where the trailing character `b` will not let it truncate the white spaces.

### Step 4: Successful Account Takeover
- Thus we inserted the user `pokemon` into the database with **our password**, and now onward we can login with our own password and `pokemon` username.
- Whenever we use `pokemon` as the username, now it will check the two different cells in the table with the same username, and will validate our credentials.

## Visual Representation

Here's what happens during the attack:

```
Original Admin User:
Username: "pokemon"
Password: "admin_password"

Attacker Registration:
Input: "pokemon                    b" (pokemon + 20 spaces + b)
Stored: "pokemon                    " (truncated to 20 chars)
Final:  "pokemon" (spaces trimmed)
Password: "attacker_password"

Result: Two users with same username "pokemon" but different passwords
```

## Impact

**SQL Truncation** is a type of **SQL Injection**, which is a low hanging fruit. If it is not properly patched in the application, can cause a severe damage to the application data.

## Mitigation

To prevent SQL Truncation vulnerabilities:

1. **Server-side validation** - Don't rely only on client-side `maxlength` attributes
2. **Proper input sanitization** - Trim whitespace and validate input length on the server
3. **Database constraints** - Use proper database constraints and error handling
4. **Unique constraints** - Implement proper unique constraints in the database
5. **Input validation** - Validate all user inputs before processing

---

**Reference:** [MySQL and SQL Column Truncation Vulnerabilities](http://www.suspekt.org/2008/08/18/mysql-and-sql-column-truncation-vulnerabilities/)