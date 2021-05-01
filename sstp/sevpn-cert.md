---
layout: default
title: SSTP Connect
description: SSTP / SoftEther VPN Client for iOS
---

## Generate iOS-compatible SoftEther server certificates

### Note

*We recommend using certificates signed by public CAs which ensures maximum level of security. You can get them from free services such as Let's Encrypt.*

*Only use self-generated certificates if public CA certificates do not work for you. In that case, please follow this guide to regenerate certificates as certificates generated automatically by SoftEther Server do not meet iOS 13 requirements.*

**TLS Server Trust Evaluation is an advanced topic for server administrators. You must be responsible for any changes you made and their consequences.**

**PROCEED AT YOUR OWN RISK!**

### Overview

You will be generating two certificates according to this guide. The first one is called root certificate which is then used to generate the second one (called server or leaf certificate), used directly by the VPN server.

### Prerequisites

- SoftEther VPN Server v4.25 Build 9656 and later (older versions can not generate iOS-compatible certificates)

- Access to VPN server admin mode via SE-VPN Server Manager (GUI) or vpncmd (command line)

### Using SE-VPN Server Manager (GUI)

1. Connect to the VPN server in administration mode

1. Open *Encryption and Network*

1. Under *Server Certificate Settings*, click *New*.

1. Choose *Root Certificate* and fill in certificate information

    - Common Name: Any name EXCEPT your server hostname
    - Expires in: 3650 days (default) or other value you want
    - Strengthness: 2048 bits

    ![root-ca](https://user-images.githubusercontent.com/54519668/116781285-81982880-aab4-11eb-825d-a8038fa9eedd.JPG)

1. Click *OK*. The new root certificate is shown under *Server Certificate*.

    ![root-ca-overview](https://user-images.githubusercontent.com/54519668/116781287-8361ec00-aab4-11eb-9130-f9574d437dc2.JPG)

1. Choose *Export* to export as X509 certificate and private key. **Save the key to a safe place and never disclose to others.**

1. Now generate the server (leaf) certificate. Click *New*.

1. Choose *Certificate Signed by Other Certificate*

1. Click *Load Certificate and Private Key* and load the certificate and key you just exported

1. Fill in server certificate information

    - Common Name: Your server hostname (such as SoftEther DDNS hostname)
    - Expires in: 730 days (or any value less than 825 days)
    - Strengthness: 2048 bits

    ![server-cert](https://user-images.githubusercontent.com/54519668/116781290-852baf80-aab4-11eb-9011-a7569b057627.JPG)

1. Click *OK* to close *Create New Certificate*.

1. The new certificate is now shown under *Server Certificate*. It does not need to be exported.

    ![server-cert-overview](https://user-images.githubusercontent.com/54519668/116781291-865cdc80-aab4-11eb-9352-0d6738009289.JPG)

1. Click *OK* to close *Encryption and Network Settings*. VPN manager will prompt that you need to install the root certificate manually if you need OpenVPN connectivity.

1. (Optional) Copy the root certificate you exported (not the private key) to `chain_certs` sub-folder on the server and regenerate OpenVPN configuration. You don't need to do this if OpenVPN connectivity is not needed.

1. Upload the root certificate (not the private key) to your website or email it to yourself. Follow Apple's guide to install and trust the root certificate on your iOS device. 

    To install: https://support.apple.com/en-us/HT209435

    To trust: https://support.apple.com/en-us/HT204477

1. Repeat the above procedures to generate a new server certificate when the current one expires (in 730 days for example).

### Using vpncmd (command line)

1. Log into server admin mode

1. Run `makecert2048`, fill in root certificate information. Specify filenames to export the root certificate and private key. 

    - Name of Certificate (CN): Any name EXCEPT your server hostname
    - Expiration: 3650 days (default) or other value you want

    **Save the key to a safe place and never disclose to others.**

    Sample:

    ```
    VPN Server>makecert2048
    MakeCert2048 command - Create New X.509 Certificate and Private Key (2048 bit)
    Name of Certificate to Create (CN): debian

    Organization of Certificate to Create (O):

    Organization Unit of Certificate to Create (OU):

    Country of Certificate to Create (C):

    State of Certificate to Create (ST):

    Locale of Certificate to Create (L):

    Serial Number of Certificate to Create (Hexadecimal):

    Expiration Date of Certificate to Create (Days): 3650

    File Name to Save Certificate to Create: /root/debian.cer

    File Name to Save Private Key to Create: /root/debian.key

    The command completed successfully.
    ```

1. Run `makecert2048 /SIGNCERT:<Path to root certificate> /SIGNKEY:<Path to private key>`, fill in server certificate information.

    - Name of Certificate (CN): Your server hostname (such as SoftEther DDNS hostname)
    - Expiration: 730 days (or any value less than 825 days)

    Specify filenames to export the server certificate and private key.
    **Save the key to a safe place and never disclose to others.**

    Sample:

    ```
    VPN Server>makecert2048 /SIGNCERT:/root/debian.cer /SIGNKEY:/root/debian.key
    MakeCert2048 command - Create New X.509 Certificate and Private Key (2048 bit)
    Name of Certificate to Create (CN): vpn123456789.softether.net

    Organization of Certificate to Create (O):

    Organization Unit of Certificate to Create (OU):

    Country of Certificate to Create (C):

    State of Certificate to Create (ST):

    Locale of Certificate to Create (L):

    Serial Number of Certificate to Create (Hexadecimal):

    Expiration Date of Certificate to Create (Days): 730

    File Name to Save Certificate to Create: /root/server.cer

    File Name to Save Private Key to Create: /root/server.key

    The command completed successfully.
    ```

1. Run `servercertset`, provide path to the server certificate and private key. Do not provide path to the root certificate.

1. (Optional) Copy the root certificate you exported (not the private key) to `chain_certs` sub-folder on the server and regenerate OpenVPN configuration. You don't need to do this if OpenVPN connectivity is not needed.

1. Upload the root certificate (not the private key) to your website or email it to yourself. Follow Apple's guide to install and trust the root certificate on your iOS device. 

    To install: https://support.apple.com/en-us/HT209435

    To trust: https://support.apple.com/en-us/HT204477

1. Repeat the above procedures to generate a new server certificate when the current one expires (in 730 days for example).
