---
layout: default
title: SSTP Connect
description: SSTP / SoftEther VPN Client for iOS
---

## Generate iOS-compatible SoftEther server certificates

### Note

*We recommend using certificates signed by public CAs which ensures maximum level of security. You can get them from free service like Let's Encrypt.*

*Only use self-generated certificates if the above option does not work for you. In that case, please follow this guide to regenerate certificates as certificates generated automatically by SoftEther Server does not meet iOS 13 requirements.*

**TLS Server Trust Evaluation is an advanced topic for server administrators. You must be responsible for any changes you made and their consequences.**

**PROCEED AT YOUR OWN RISK!**

### Overview

You will be generating two certificates in this guide. The first is called root certificate which is then used to generate the second certificate (leaf certificate), used directly by the VPN server.

### Prerequisites

- SoftEther VPN Server v4.25 Build 9656 and later (older versions can not generate iOS-compatible certificates)

- Access to VPN server via SE-VPN Server Manager (GUI) or vpncmd (command line)

### Using SE-VPN Server Manager (GUI)

1. Connect to the VPN server in administration mode

1. Open *Encryption and Network*

1. Under *Server Certificate Settings*, click *New*.

1. Choose *Root Certificate* and fill in details

    - Common Name: Any name EXCEPT your server hostname
    - Expires in: 3650 days (default) or other value you want
    - Strenthness: 2048 bits

1. Click *OK*

1. Choose *Export* to export as X509 certificate and private key. **Save the key to a safe place and never disclose to others.**

1. Now generate the server (leaf) certificate. Click *New*.

1. Choose *Certificate Signed by Other Certificate*

1. Click *Load Certificate and Private Key* and load the certificate and key you just exported

1. Fill in server certificate details

    - Common Name: Your server hostname (such as SoftEther DDNS hostname)
    - Expires in: 730 days (or any value less than 825 days)
    - Strenghness: 2048 bits

1. Click *OK* to close *Create New Certificate*.

1. The new certificate is now shown under *Server Certificate*. It does not need to be exported.

1. Click *OK* to close *Encryption and Network Settings*. VPN manager will prompts you that you need to install the root certificate manually if you need OpenVPN connectivity.

1. (Optional) Copy the root certificate you exported (not the private key) to `chain_certs` sub-folder on the server and regenerate OpenVPN configuration. You don't need to do this if OpenVPN connectivity is not needed.

1. Upload the root certificate (not the private key) to your website or email it to yourself. Follow Apple's guide to install and trust the root certificate on your iOS device. 

    To install: https://support.apple.com/en-us/HT209435

    To trust: https://support.apple.com/en-us/HT204477

1. Repeat the above procedures to generate a new server certificate when the current one expires (in 730 days for example).

### Using vpncmd (command line)

1. Log into server admin mode

1. Run `makecert2048`, fill in root certificate detals. Specify filenames to export the root certificate and private key. 

    - Name of Certificate (CN): Any name EXCEPT your server hostname
    - Expiration: 3650 days (default) or other value you want

    **Save the key to a safe place and never disclose to others.**

1. Run `makecert2048 /SIGNCERT:<PATH TO ROOT CERTIFICATE> /SIGNKEY:<PATH TO PRIVATE KEY>`, fill in server certificate details

    - Name of Certificate (CN): Your server hostname (such as SoftEther DDNS hostname)
    - Expiration: 730 days (or any value less than 825 days)

    Specify filenames to export the server certificate and private key.
    **Save the key to a safe place and never disclose to others.**

1. Run `servercertset`, provide path to the server certificate and private key. Do not provide path to the root certificate.

1. (Optional) Copy the root certificate you exported (not the private key) to `chain_certs` sub-folder on the server and regenerate OpenVPN configuration. You don't need to do this if OpenVPN connectivity is not needed.

1. Upload the root certificate (not the private key) to your website or email it to yourself. Follow Apple's guide to install and trust the root certificate on your iOS device. 

    To install: https://support.apple.com/en-us/HT209435

    To trust: https://support.apple.com/en-us/HT204477

1. Repeat the above procedures to generate a new server certificate when the current one expires (in 730 days for example).
