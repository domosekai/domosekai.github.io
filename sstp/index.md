---
layout: default
title: SSTP Connect
description: SSTP / SoftEther VPN Client for iOS and macOS
appid: 1543667909
---

## Introduction

SSTP Connect is a VPN client that supports two HTTPS-based protocols, SSTP and SoftEther VPN.

SSTP (MS-SSTP) is developed by Microsoft and supported on Windows Server 2008 and later. It encapsulates IP traffic (layer 3) over HTTPS.

SoftEther VPN is developed by Daiyuu Nobori and SoftEther Corporation. It encapsulates Ethernet frames (layer 2) over HTTPS.

<a href='https://apps.apple.com/us/app/sstp-connect/id1543667909?itsct=apps_box&itscg=30200'><img alt='Download on the App Store' height="50" hspace="20" src='Download_on_the_App_Store_Badge_US-UK_RGB_blk_092917.svg'/></a>

*Available on both iOS and Mac App Store*

## News

  Some users are experiencing timeouts after upgrading to iOS 18.4 / macOS 15.4.
  Please see [here](ios184.html) for details.
  
## Features

- **Native**

  Only native libraries are used in the core function, including the TLS stack. No OpenSSL.
  
  Connections are saved natively so that you can start a connection from the system settings.

- **Simple**
  
  VPN clients ought to be small and simple. No ads, analytics or other 3rd-party SDK are included.

- **Privacy**

  No data is collected from you. Connection log only exists in the memory and is never saved to the device.

- **Complete**
  
  Support all password and certificate-based authentications available in Windows 11.
  
  Support authenticating by password and certificate at the same time with TEAP (EAP chaining).
  
  Protocol details below.

- **Security**
  
  Passwords and certificates are stored in the keychain. SSTP Connect never saves them locally for convenience.

- **IPv6 Ready**

  Support both IPv6 connections and stateless IPv6 configuration in the VPN tunnels.
  
  *DHCPv6 not supported*

- **More than TCP** *SoftEther Only*

  Support NAT traversal (NAT-T) and UDP acceleration just like the official SoftEther client.
  
- **Easy Import and Export**

  Not only from SSTP Connect, reading connection settings from SoftEther Client Manager is also a piece of cake.

- **Routing**

  Accept static routes pushed from the server or add your own entries.
  
- **Shortcut**

  Control VPN state and create automation with Shortcuts.

## SSTP Authentication Methods

- PEAP
- EAP-TTLS
- TEAP (EAP chaining)
- EAP-TLS
- EAP-MSCHAPv2
- MSCHAPv2
- CHAP
- PAP

## SoftEther Authentication Methods

- Password
- RADIUS / NT Domain Password
- Certificate
- Anonymous

## Supported Server Platforms

- Microsoft Windows Server 2008 and later
- Microsoft Azure P2S VPN
- MikroTik RouterOS  *Servers configured without certificates are not supported.*
- SoftEther VPN Server
- VPN Azure

## Support

[FAQ](help.html)

[よくある質問](help-ja.html)

[Privacy Policy](privacy.html)

## Legal

Since version 3.0, SSTP Connect uses [SwiftNIO](https://github.com/apple/swift-nio), a network framework released by Apple under Apache License 2.0.

SSTP Connect is a third-party implementation based on Microsoft Open Specifications and SoftEther VPN source code. 
We do not have any affiliation with either Microsoft Corporation or SoftEther Corporation.
  
© 2020–2024 Domosekai Limited.  All rights reserved.
