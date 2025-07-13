---
title: "Security Considerations for Smart Cameras"
date: 2021-06-30
tags: [Smart Cameras, IoT Security, Surveillance]
---

In this world of interconnected devices, smart cameras are everywhere — ubiquitous in modern times. Over the past decade, the camera industry has seen major innovation, with Gartner projecting around 15 million connected cameras by 2023.

With camera evolution, attackers have become more skilled. Recently, a security startup had nearly 150,000 cameras breached; cloud‑connected cameras of over 200 individuals were hacked, exposing four years of footage. Hackers once infiltrated casino cameras and used that access to win millions. It’s critical to secure every component — security is only as strong as the weakest link.

This article explains the key attack vectors and security considerations across the smart‑camera ecosystem.

## Architecture

Typical home smart-camera architecture:

- Wired or wireless cameras connect to a gateway
- Gateway connects to the Internet and developer’s server
- Users access cameras via mobile app:
  - Over local Wi‑Fi to gateway
  - Or via the Internet routed through servers

All eight components in this ecosystem (shown in the diagram) can be potential points of vulnerability.

{{< figure src="cam.png" alt="Alt text" caption="Architecture" align="center" >}}

### 1. Gateway

As the central controller, the gateway manages configuration, access, maintenance, and updates — from both internet and LAN sides. Firmware is a common attack vector.

Studies reveal nearly all home routers have severe unpatched flaws. A compromised gateway can lead to control over all connected devices.

**Security measures for the gateway:**

- Implement strong authentication and authorization
- Use secure/encrypted internal and external communication
- Follow robust coding practices
- Validate and sanitize input errors
- Employ strong cryptography
- Securely store sensitive data

### 2. Mobile‑to‑Gateway Connection

Even on a local network, mobile apps should require authentication.

- Protect against rogue devices (e.g., guests)
- Avoid default SSIDs—hide and rename them
- Disable guest Wi-Fi accounts
- Use WPA2 and defend against protocol-level attacks like KRACK

### 3. Camera‑to‑Gateway Link

Cameras communicate with the gateway via wired or wireless protocols.

- Ensure network protocol is resilient to DoS attacks
- Prevent Man‑in‑the‑Middle (MITM)—use strong encryption

### 4. Camera Device

As the focal device, the camera’s internal systems must be secured.

- Audit firmware regularly for bugs
- Avoid default credentials or hardcoded passwords
- Enforce multi-factor authentication (MFA) where possible

### 5. Gateway–Cloud Server Communication

This path travels over the public internet and must be secured end-to-end:

- Mutual authentication between gateway and cloud
- Ensure integrity and confidentiality of data
- Transmit only necessary data, minimum privacy exposure

### 6. Cloud Server

Cloud servers host streaming, storage, authentication, updates, logging, and more.

Key security controls:

- Audit server and service configurations
- Enforce MFA and strict access controls (IAM)
- Encrypt data at rest and in transit
- Monitor continuously and run vulnerability management
- Meet relevant compliance standards

### 7. Mobile App to Cloud

Users access their cameras anywhere via mobile app—this introduces remote access risks:

- Strong, rate-limited authentication with MFA
- Fine-grained authorization—prevent privilege escalation
- Use SSL pinning to avoid MITM
- Encrypt all communications

### 8. Mobile Application Security

The app itself requires scrutiny:

- Prevent other apps on the device from reading camera app data
- Protect authentication flows, even with physical access
- Defend against reverse-engineering—use code obfuscation
- Audit per OWASP Mobile Testing Guide
