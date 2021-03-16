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

  - No ads, no analytics or any 3rd-party SDK. Installed size on iOS 14 is less than 2MB.
  - No data is collected from you. Moreover, your connection log is only in the memory and never saved to the device.
  - Pure Swift implementation.
  - Native iOS TLS stack ensuring stability and security.

## Specifications

  - Transport layer: HTTPS (TCP) over IPv4 or IPv6
  - Simultaneous TCP connections: 1–32 (SoftEther only)
  - UDP acceleration: Requires at least iOS 13 and server build 9695 (SoftEther only)
  - Authentication (SSTP): Password (EAP-MSCHAPv2, MS-CHAPv2, CHAP and PAP)
  - Authentication (SoftEther): Password (including RADIUS / NT Domain)
  - Tunnel IP and DNS: Automatic (IPv4 and stateless IPv6) or static
  - Server platform: Microsoft Windows Server, SoftEther VPN (VPN Gate), MikroTik RouterOS etc.

## Support

[FAQ](help.html)

[よくある質問](help-ja.html)

[Privacy Policy](privacy.html)

© 2020 Domosekai Limited.  All rights reserved.
