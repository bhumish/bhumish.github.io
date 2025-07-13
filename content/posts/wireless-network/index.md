---
title: "Wireless Network Development"
date: 2012-02-22
draft: false
description: "Developing and configuring a secure wireless network for a medium-sized office, including NAT, firewall, site blocking, and DHCP configuration on Cisco equipment"
tags: ["wireless", "networking", "cisco", "security", "nat", "firewall", "dhcp", "access-points", "project", "network-development"]
categories: ["Networking", "Projects", "Technology"]
---

As part of my college project work, I am developing a secure network at a medium sized office. Last week I completed the configuring of the wi-fi router with the normal protocols as well as some security features. Prior to developing the physical network, I tested the network with all its preferences in two different network simulators for its successful working (mainly for the IP address assigning). Let me describe you the techniques which I used in the router configuration –

## Network Address Translation

Yes, the protocol which changes the Class C private address of the company's computers to some Class A public addresses provided by the service provider. For the company I have configured the addresses as 192.x.x.x and the outside addresses will be 117.x.x.x (IP not displayed because of security reasons, you know!)

## Firewall

Configured the firewall inside the router (as there was no Demilitarized Zone for the company). The firewall works with the Access Control Lists, filtering the packets of data with insecure protocols. Oh yes, it is a stateless firewall.

## Site Blocking

This is the easiest security mechanism – to block the http sites with the words or tags used in the site content. Also, the sites are blocked with their categories – music streaming, proxy, adult and gaming.

## DHCP

Oh yes, it's not that tough to configure a DHCP on a Cisco router – but it is, when the router also works as a gateway – connecting the IP addresses of class A and class C.

This is what I configured in the router during this time. The access points that are used for the wireless networks are Cisco WRT54GL APs. The whole network for the authorities is working efficiently, and the next steps are to configure the catalyst switch and install the routers.

Along with the project work, I am preparing for networking certifications – CompTIA Network+ and CCNA. Planning to appear for Network+ during May, after completing my Engineering exams.