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

- **Lightweight**

  No ads, analytics or other 3rd-party SDK
  
- **Privacy**

  No data is collected from you. Log only exists in the memory and is never saved to the device.
  
  Passwords and certificates are saved in the keychain, protected by iOS.
  
- **Native**

  Standard iOS TLS stack ensuring stability and security
  
- **Security**

  Authentication with password or certificate
  
  Certificates packed in PKCS #12 format (.p12, .pfx) are required. SSTP requires iOS 12+.
  
- **IPv6**

  Support IPv6 network and tunnel (stateless tunnel only, DHCPv6 not supported)
  
- **UDP**

  Support SoftEther UDP acceleration (requires iOS 13+ and SoftEther Server 4.30+)

- **Import**

  Support SoftEther VPN Client Manager connection setting files (.vpn)

## Server Platforms

- Microsoft Windows Server RRAS
- Microsoft Azure P2S VPN
- MikroTik RouterOS*
- SoftEther VPN Server
- VPN Azure

\* Servers configured without certificates are not supported.

## Support

[FAQ](help.html)

[よくある質問](help-ja.html)

[Privacy Policy](privacy.html)

## Legal

Since version 3.0, SSTP Connect uses [SwiftNIO](https://github.com/apple/swift-nio), an Apple project released under Apache License 2.0.
  
© 2020–2021 Domosekai Limited.  All rights reserved.
