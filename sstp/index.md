---
layout: default
title: SSTP Connect
description: SSTP / SoftEther VPN Client for iOS
---

## Introduction

SSTP Connect is a VPN client that supports two HTTPS-based protocols, SSTP and SoftEther VPN.

SSTP (MS-SSTP) is developed by Microsoft and supported on Windows Server 2008 and later. It encapsulates IP traffic (layer 3) over HTTPS.

SoftEther VPN is developed by Daiyuu Nobori and SoftEther Corporation. It encapsulates Ethernet frames (layer 2) over HTTPS.

This is a third-party implementation based on Microsoft Open Specifications and SoftEther VPN source code. 
We do not have any affiliation with either Microsoft Corporation or SoftEther Corporation.

<a href='https://apps.apple.com/us/app/sstp-connect/id1543667909?itsct=apps_box&itscg=30200'><img alt='Download on the App Store' height="50" hspace="20" src='Download_on_the_App_Store_Badge_US-UK_RGB_blk_092917.svg'/></a>

## Features

- **Simplicity**

  VPN clients ought to be small and simple. Therefore we don't place ads, analytics or other 3rd-party SDK in the app. Size can tell.

- **Native**

  To the extent possible, native iOS libraries are used, including most importantly the TLS stack. We believe this ensures best stability and security. (Apple's SwiftNIO framework is also used.)
  
  Unlike some apps, SSTP Connect saves connections natively so that you can start a connection from the system. No need to open the app and it will work just the same.

- **Privacy**

  Please read our privacy policy. We promise that no data is collected from you. Moreover, connection log only exists in the memory and is never saved to the device.

- **Authentication Methods**

  Password and certificate-based authentication is supported for both protocols. (iOS 12+ required for certificate authentication in SSTP)
  
  SSTP authentication methods: PEAP, EAP-TLS, EAP-MSCHAPv2, MSCHAPv2, CHAP, PAP
  
  SoftEther authentication methods: Password (including RADIUS / NT Domain), Certificate

- **Security**

  Your passwords and certificates are only stored in the iOS keychain. SSTP Connect never saves them locally for convenience or other reasons.
  
- **IPv6 Ready**

  IPv6 is not the next generation. It's now and SSTP Connect is ready for that.
  
  Of course server connections are IPv6 ready but there is more. VPN tunnel is also IPv6 capable (stateless only, DHCPv6 not yet supported), provided the server has IPv6 configured.

- **More than TCP**  *SoftEther Only*

  You can use the advanced NAT traversal (NAT-T) and UDP acceleration technology, just like you do with the official client. (iOS 12+ required)

- **Easy Import**  *SoftEther Only*

  Wondering how to copy VPN connections from the official SoftEther client? SSTP Connect can read connection setting files (.vpn) so import work is a piece of cake.

## Supported Server Platforms

- Microsoft Windows Server 2008 and later
- Microsoft Azure P2S VPN
- MikroTik RouterOS (servers configured without certificates are not supported)
- SoftEther VPN Server
- VPN Azure

## Support

[FAQ](help.html)

[よくある質問](help-ja.html)

[Privacy Policy](privacy.html)

## Legal

Since version 3.0, SSTP Connect uses [SwiftNIO](https://github.com/apple/swift-nio), a network framework released by Apple under Apache License 2.0.
  
© 2020–2022 Domosekai Limited.  All rights reserved.
