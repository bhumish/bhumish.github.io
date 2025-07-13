---
title: "Brute-Force Attack on Wordpress"
date: 2013-04-13
draft: false
tags: ["wordpress", "brute-force", "security", "botnet", "cybersecurity", "ddos"]
categories: ["security", "technology", "wordpress"]
description: "Analysis of distributed brute-force attacks targeting WordPress installations and security recommendations to protect against such attacks"
---

## Apparatus:

- Distributed botnet, around tens of thousands of bots with their respective IP addresses
- A pass file of around 1000 entries with some normal passwords
- Default username: 'admin'

## Steps:

- WordPress 3.0 release before 3 years, users going on with 'admin' as their default username, and some usual password
- A brute-force with username: 'admin' and password from the above mentioned file
- The botnet, tries this attack on each and every wordpress portal available over Internet

## Objective:

A well-planned distributed attack (just like [itsoknoproblembro](http://www.infosecurity-magazine.com/view/30053/dissection-of-itsoknoproblembro-the-ddos-tool-that-shook-the-banking-world/) shook the banking world) against some hot-spot over the Internet.

## How:

The wordpress web servers have very high bandwidth, practically unlimited. Any attack triggered from these servers will have a great impact. This can be done to create a better and huge zombie-net.

## Conclusion:

Save your wordpress! Change your password if the username is admin (and also, you need to change the username from admin to something else, for being secure).

## Some more tips:

If you are using the .com for your wordpress, change your password and enable the 2 step authentication.

If you are the admin of wordpress installation on your server, you have some more steps to follow – like creating a password for the .wpadmin file and some security modifications in the .htaccess file.

More description for making these changes is available here: [Hostgator Support for WP Attack](http://support.hostgator.com/articles/specialized-help/technical/wordpress/wordpress-login-brute-force-attack)