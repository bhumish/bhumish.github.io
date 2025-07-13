---
title: "3 WAN Protocols you should know: HDLC, PPP, and Frame-Relay"
date: 2012-02-02
draft: false
tags: ["networking", "wan", "protocols", "hdlc", "ppp", "frame-relay", "cisco"]
categories: ["technology", "networking", "education"]
description: "A comprehensive guide to three essential WAN protocols: HDLC, PPP, and Frame-Relay, explaining their features, differences, and use cases"
---

## What is HDLC?

HDLC stands for High-Level Data Link Control protocol. Like the two other WAN protocols mentioned in this article, HDLC is a Layer 2 protocol. HDLC is a simple protocol used to connect point to point serial devices. For example, you have point to point leased line connecting two locations, in two different cities. HDLC would be the protocol with the least amount of configuration required to connect these two locations. HDLC would be running over the WAN, between the two locations. Each router would be de-encapsulating HDLC and turning dropping it off on the LAN.

HDLC performs error correction, just like Ethernet. Cisco's version of HDLC is actually proprietary because they added a protocol type field. Thus, Cisco HDLC can only work with other Cisco devices.

HDLC is actually the default protocol on all Cisco serial interfaces. If you do a `show running-config` on a Cisco router, your serial interfaces (by default) won't have any encapsulation. This is because they are configured to the default of HDLC.

## What is PPP?

You may have heard of the Point to Point Protocol (PPP) because it is used for most every dial up connection to the Internet. PPP is based on HDLC and is very similar. Both work well to connect point to point leased lines.

The differences between PPP and HDLC are:

- PPP is not proprietary when used on a Cisco router
- PPP has several sub-protocols that make it function.
- PPP is feature-rich with dial up networking features

Because PPP has so many dial-up networking features, it has become the most popular dial up networking protocol in use today. Here are some of the dial-up networking features it offers:

- Link quality management monitors the quality of the dial-up link and how many errors have been taken. It can bring the link down if the link is receiving too many errors.
- Multilink can bring up multiple PPP dialup links and bond them together to function as one.
- Authentication is supported with PAP and CHAP. These protocols take your username and password to ensure that you are allowed access to the network you are dialing in to.

## What is Frame-Relay?

Frame Relay is a Layer 2 protocol and commonly known as a service from carriers. For example, people will say "I ordered a frame-relay circuit". Frame relay creates a private network through a carrier's network. This is done with permanent virtual circuits (PVC). A PVC is a connection from one site, to another site, through the carrier's network. This is really just a configuration entry that a carrier makes on their frame relay switches.

Obtaining a frame-relay circuit is done by ordering a T1 or fractional T1 from the carrier. On top of that, you order a frame-relay port, matching the size of the circuit you ordered. Finally, you order a PVC that connects your frame relay port to another of your ports inside the network.

The benefits of frame-relay are:

- Ability to have a single circuit that connects to the "frame relay cloud" and gain access to all other sites (as long as you have PVCs). As the number of locations grow, you would save more and more money because you don't need as many circuits as you would if you were trying to fully-mesh your network with point to point leased lines.
- Improved disaster recovery because all you have to do is to order a single circuit to the cloud and PVC's to gain access to all remote sites.
- By using the PVCs, you can design your WAN however you want. Meaning, you define what sites have direct connections to other sites and you only pay the small monthly PVC fee for each connection.