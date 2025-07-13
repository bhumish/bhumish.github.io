---
title: "Common Network Security Threats"
date: 2012-09-05
draft: false
description: "An overview of common network security threats including Smurf attacks, Ping of Death, DoS attacks, SYN Flood, viruses, and worms"
tags: ["network-security", "cybersecurity", "threats", "dos", "ddos", "virus", "worms", "smurf", "ping-of-death", "syn-flood"]
categories: ["Security", "Networking", "Cybersecurity"]
---

## Smurf

It's a version of Denial of Service attack – floods the victim with spoofed broadcast pings. A large number of pings are sent to the IP broadcast address of the victim, it responds back with broadcast to all the hosts – and these hosts simultaneously reply – causing a major lock in the network.

## Ping of Death

A funny ping – ICMP packet is sent to the victim – which floods its buffer, causing the system to reboot or the network getting hanged.

## DoS

The Denial of Service attack does exactly as the name suggests – prevents the users from the service. Can be generally implemented with ICMP spoofing.

## SYN Flood

The SYN packets are used for connection establishment – and these SYN packets are used here to take down a computer by sending a number of useless SYN packets, and the computer becomes too busy responding to the SYNs.

## Virus

Tiny programs creating a variety of bad things to computers – and they can replicate itself!

- **File virus** – contained in executables like .exe, .dll, and .com.
- **Macro virus** – A script to automatically carrying out a task – without the user initiating it.
- **Boot sector virus** – They damage the booting process of a computer by over-writing the boot sector, creating problems like hard disk error or missing OS.

## Worms

They are a lot like virus, and also they can actively replicate – without the user opening or executing them. They can propagate and destroy themselves.