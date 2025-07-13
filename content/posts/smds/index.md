---
title: "Switched Multimegabit Data Service"
date: 2012-05-06
draft: false
description: "An overview of SMDS (Switched Multimegabit Data Service), its addressing scheme, frame structure, and comparison with LAN technologies like Ethernet and Token-Ring"
tags: ["smds", "networking", "atm", "wan", "switched-networks", "telecommunications", "data-service", "bellcore"]
categories: ["Networking", "Technology", "Telecommunications"]
---

SMDS, or Switched Multimegabit Data Service, has not yet gained significant market penetration, although it has begun to experience some growth. SMDS was viewed as a stepping stone to ATM, since some of the communications equipment and media are common to the two technologies. As SMDS is not available everywhere, and there is more interest in ATM, SMDS has had a hard time getting into the mainstream.

SMDS does, however, have some penetration; if your long-distance carrier is MCI, you may have cause to use this technology. The attraction of SMDS is that it has the potential to provide high-speed, link-level connections (initially in the 1 to 34 Mbps range) with the economy of a shared public network, and exhibits many of the qualities of a LAN.

## SMDS Addressing Scheme

In an SMDS network, each node has a unique 10-digit address. Each digit is in binary-coded decimal, with 4 bits used to represent values 0 through 9. Bellcore, the "keeper" of the SMDS standard, assigns a 64-bit address for SMDS, which has the following allocation:

- The most significant 4 bits are either 1100 to indicate an individual address, or 1110 to indicate a group address.
- The next 4 most significant bits are used for the country code, which is 0001 for the United States.
- The next 40 bits are the binary-coded decimal bits representing the 10-decimal digit station address.
- The final 16 bits are currently padded with ones.

To address a node on the SMDS network, all you need do is put the node's SMDS address in the destination field of the SMDS frame.

## Frame Handling and Comparison with LAN Technologies

In this way, SMDS behaves in a fashion similar to Ethernet or Token-Ring, which delivers frames according to MAC addresses. A key difference between SMDS and these LAN technologies, however, is the maximum frame size allowed. Ethernet allows just over 1500 bytes, and Token-Ring just over 4000 bytes, but SMDS allows up to 9188 bytes. These SMDS frames are segmented into ATM-sized 53-byte cells for transfer across the network. A large frame size gives SMDS the ability to encapsulate complete LAN frames, such as Ethernet, Token-Ring, and FDDI, for transportation over the SMDS network.