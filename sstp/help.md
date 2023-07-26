---
layout: default
title: SSTP Connect
description: SSTP / SoftEther VPN Client for iOS
---

[日本語版はこちら](help-ja.html)

# FAQ

## General

### Q: How to start?

To use SSTP Connect, you need to create a profile first.

These items are needed for a profile:
  - A description of the connection
  - Server address
  - Username and password (or certificate)
  - Virtual Hub name (SoftEther only)

If you have an existing SSTP Connect configuration file or a connection setting file from SoftEther VPN Client Manager,
you can import it by either:
  - clicking + and choose *Import From File*, *Import From URL*, or
  - opening / sharing the file to the app.

### Q: How to edit or delete a profile?

Swipe right to edit and swipe left to delete a profile.

You can also tap Edit to enter the edit mode. You will find edit and delete buttons at the bottom.

### Q: What are the items in a profile and what do they mean?

- **Protocol**

  Select the VPN protocol you want to use. We currently support SSTP and SoftEther.

- **Description** 

  *Required*

  Fill in anything that helps you to identify the connection. It will also become the name shown in the system VPN list.

- **Server** 

  *Required*

  VPN server address in either hostname or IP address.

  Generally you should use a hostname (e.g. `vpn.example.com`), so that you don't need to take care of IP changes.

  However, if your DNS provider is unreliable, or you want to enforce connecting via IPv4 or IPv6 (if the server is dual-stack), you can use an IP address instead. 

- **Hostname**

  Server hostname that will be used in the TLS server verification.

  If you entered a hostname in the server field, you don't need to fill in the same hostname again.
  
  If you entered an IP address in the server field, please fill in the hostname here that matches the server certificate, otherwise TLS verification will fail.

- **Port**

  Port number of the server. By default it's `443`.
  
- **TLS Server Verification**

  TLS verification examines the server's identity and protects you from MITM (man-in-the-middle) attacks. We **STRONGLY RECOMMEND** you enable it at all times.

  For servers using non-public certificates, additional steps may be needed to pass TLS verification. See below for more information.
  
  If the server fails the verification, you will be asked whether to ignore the error and continue.
  You can also save the certificate so that no questions will be asked next time, provided the certificate remains unchanged.
  
  We **STRONGLY RECOMMEND** you fix the certificate issue in the first place and use the above method as the last resort only.
  
- **Virtual Hub**

  *SoftEther only*

  Enter the Virtual Hub name.
  
  The common default hub names are `default` and `vpn`. If you are using VPN Gate service, the hub name is `vpngate`.
  
- **Connections**

  *SoftEther only*

  The number of TCP connections for a SoftEther VPN session.
  
  We support 32 connections at most but you are recommended to start from 2. More connections consume more memory. Do not use under heavy load.
  
- **UDP Acceleration**

  *SoftEther only and requires iOS 12+*

  Whether to enable the UDP acceleration feature. 
  
- **NAT Traversal (NAT-T)**

  *SoftEther only and requires iOS 12+*

  Whether to enable the NAT traversal feature. NAT-T is helpful when the server cannot open ports or does not have a public IP address.
  
  However, NAT-T does not work in all cases. Please refer to the [official explanation](https://www.softether.org/4-docs/2-howto/6.VPN_Server_Behind_NAT_or_Firewall/1.Dynamic_DNS_and_NAT_Traversal) from SoftEther.
  
- **Authentication Method**

  Choose either password or certificate. 
  
  Authentication with certificate in SSTP is supported on iOS 12 and above.
  
  If you are using TEAP (EAP chaining), select the primary method. A secondary method can be configured in EAP Configuration.
  
- **Username** 

  *Required*

  Fill in the account name of the VPN.

  For SSTP users with certificate-based authentication, username can be omitted if it matches the certificate's User Principal Name (UPN).

  For SoftEther users connecting with SSTP protocol, the Virtual Hub name should be appended to the account in the form `user@HUB`, unless the default Virtual Hub is being used.
  
- **Password** 

  Fill in your password. Passwords are saved in the keychain, protected by iOS.
  
  If nothing is entered, you will be asked for the password upon connecting.
  
- **Certificate** 

  *Required for certificate-based authentication*

  Import and select the certificate you want to use. Certificates (including private keys) are saved in the keychain, protected by iOS.
  
  See below for how to import certificates. SoftEther VPN supports RSA certificates only.
  
- **EAP Configuration**

  *SSTP only*

  Advanced EAP configuration settings.
    
- **Enable PAP / CHAP**

  *SSTP only*

  Enable if the server only supports these obsolete authentication methods.
  
- **Tunnel IP Version**

  Choose the IP version inside the VPN tunnel. For IPv6 tunnels, only stateless configuration is currently supported (DHCPv6 not supported).

- **Static IP / DNS**

  Specify manual IP and DNS settings if instructed by your administrator.
  
- **MTU**

  Tunnel MTU size. By default it's 1400 for SSTP or 1500 for SoftEther.
  
  Generally it has little to do with the client's network environment and does not need to be changed.
  
- **Add Default Route**

  Select whether to add the default route so that Internet traffic will be routed via VPN.
  
  In iOS built-in VPN the option is called *Send All Traffic*.

  Please note that the DNS servers of the VPN interface may not be used if a default route is not in place.
  You may need to use IP addresses directly or add an internal DNS domain to access the remote LAN.

- **Advanced Routing**

  By default, SSTP Connect takes static routes pushed by the remote DHCP server. You can disable the function if it causes any trouble.
  If you are the server administrator, please note that not all SSTP VPN servers support this function. We have confirmed its operation on Windows Server RRAS and SoftEther VPN Server.

  You can also add your own routes, by defining the destinations that should be routed to the VPN and those should not, with each category holding up to
  1024 characters.

  Destinations can be specified in the following formats.

  - `IP` *a single address, e.g. 8.8.8.8*
  - `IP/Mask len` *a subnet, e.g. 10.0.0.0/8*
  - `IP/Mask len/Gateway` *a subnet with gateway (next hop), e.g. 192.168.2.0/24/192.168.1.254*

  Although you can add default routes, please note that it's still controlled by the *Add Default Route* switch.

  Gateways only affect SoftEther VPN. For SSTP VPN, gateways are ignored and determined by the server.

- **Proxy**

  Specify the proxy settings inside the VPN tunnel.
  
- **On Demand Rules**

  Edit VPN On Demand rules. See below for more information.
  
- **Disable TLS 1.0 & 1.1**

  TLS 1.0 and 1.1 are obsolete versions. The app will use the highest TLS version (up to 1.3) that the server accepts. But you can also explicitly disable these old versions here.
  
- **Auto Reconnect**

  Select whether to reconnect the VPN if interrupted.
  
- **Retry Times**

  Number of times to retry if the connection fails.
  
- **Temporary IPv6 Address**

  Use temporary IPv6 addresses every time connected if allowed by the server. If disabled, the same IPv6 address will be used for a profile.
  
- **Switch to Wi-Fi When Available**

  When an existing VPN session is on mobile network and the device connects to Wi-Fi, by default the session will stay on mobile. Enable this option to allow upgrading to Wi-Fi.
  
  Note that the upgrade is controlled by iOS and might not always work. For example, if the current mobile connection is made over IPv6 but the Wi-Fi is IPv4 only, there is chance that the upgrade will not occur. 
  
  We also noticed that NAT-T connections (SoftEther VPN) often need a manual switch to Wi-Fi.

- **Stay Connected During Sleep**

  Choose whether to disconnect the VPN as the device goes to sleep.
  
  Disabling the option saves battery but reconnection may take some time.

  Even with the option set to on, the VPN is not guaranteed to survive a sleep as the sleep and wake-up is handled by iOS. 
  In particular we have noticed that when both mobile data and WiFi is on, connections over WiFi may not stay on during sleep. Switching off mobile data may help.
  
### Q: Can I connect or disconnect via system VPN settings?

Yes, you can. Your profiles are saved in the system with your credentials in the keychain. Therefore, you can connect and disconnect the VPN without opening the app.

Please turn on notifications so that in case there are errors you will be notified immediately when the app is not in the foreground. (Requiring iOS 10+)

## TLS Server Verification

### Q: What requirements should a server certificate meet in order to pass TLS server verification?

iOS has implemented more strict rules on server certificates since iOS 13. See below link for more information.

https://support.apple.com/en-us/HT210176

The most important requirements are:

- RSA key size must be at least 2048 bits
- Hash algorithm should be in the SHA-2 family (such as SHA256)
- DNS name should be presented in Subject Alternative Name (SAN) (Common Name is no longer used)
- Validity period must be 825 days or fewer
- Leaf certificate can't be self-signed (must be signed by a CA)

### Q: What should I do if I want to use certificates generated by SoftEther VPN Server?

Certificates automatically generated by SoftEther VPN Server do not meet the above requirements. Please follow this [guide](sevpn-cert.html) to regenerate.

### Q: What should I do if the server uses a self-signed certificate or a certificate not signed by a public CA?

For security reasons, certificates signed by public CAs should be used. However if that’s not possible, you can ask your administrator for the root CA certificate and both install and trust it on your device. 

Note that the certificate still needs to meet the above requirements.

### Q: How to install and trust a certificate?

Email the certificate to yourself or download it from the web, then open it on your device. 
iOS should prompt you that a profile is now ready to install.

To install it: https://support.apple.com/en-us/HT209435

To trust it: https://support.apple.com/en-us/HT204477

## Authentication with Certificates

### Q: How to import my certificates?

The first step of using certificate-based authentication is importing your certificates. Currently the app only accepts certificates packed in PKCS #12 format (.p12 or .pfx files). 

PKCS #12 is the default format on Windows platform and also supported by SoftEther VPN Server.

You need to obtain the P12 file from your administrator and place it on your device. This can be done in several ways:

- Via Finder or iTunes File Sharing on a computer (see links below)
- Email the file to yourself, long press the attachment and choose *Save to Files*
- Save in iCloud Drive or other cloud drive that can be accessed by the Files app

When the certificate is on your device, import it into the app by tapping *Import* and navigate to the folder. You need to enter the password and give the certificate a distinct description. 

The certificate (and its private key) will be saved in the keychain. For security reasons, please delete the file after import or keep it in a secure place.

A certificate can be used by multiple profiles.

**Guide on using the Finder to share files from a computer**

*For macOS Catalina or later*

https://support.apple.com/en-us/HT210598

**Guide on using iTunes to share files from a computer**

*For macOS Mojave or earlier or a Windows PC*

https://support.apple.com/en-us/HT201301

### Q: How to remove a certificate?

In *Select Certificate*, you can swipe to remove certificates.

Note that under current iOS, if you remove the app without removing all the certificates, they may still be kept in the keychain (Don't worry. They are always protected by iOS). Once you reinstall the app, you can use them again.

### Q: I want to import a new certificate but the app complains it's already in the keychain. How is that possible?

According to iOS policy, certificates with the same serial number from the same issuer are considered the same, even if the names are different. Please ask the administrator to generate the certificate with a new serial number.

### Q: I have certificates installed in the system. Why can't I see them in the app?

As a third-party app, we can't access certificates installed in the system like built-in VPN does. You have to import them using the app.

## VPN On Demand

### Q: What is VPN On Demand and how to use it?

VPN On Demand is an advanced iOS feature that allows a VPN connection to be connected / disconnected if some rule matches.

You must first define a set of rules. iOS will try to match them in order and only the first matched rule will be applied. 
The matching process is completely handled by iOS and the app has no way to alter the behavior.

**Important:** Only the rules of the current enabled (selected) VPN profile are assessed.

### Q: How to write an on demand rule?

A rule has one action and a number of conditions. If all conditions are met, the action is taken.

There are four types of actions:

- Connect
- Disconnect
- Evaluate Connection (see below)
- Ignore

You can specify these types of conditions:

- Current Interface Type (Wi-Fi, Cellular, or any)
- Wi-Fi SSID (multiple allowed)
- DNS Search Domain (multiple allowed)
- DNS Servers (multiple allowed)
- Probe URL (matches if the specified HTTP or HTTPS URL can be reached)

If no condition is specified, the rule matches all situations and any rule after it will never be matched.

### Q: If I want the VPN to be connected when I am away from a WiFi network but disconnected on that network, how should I setup the rules?

You need to create two rules in the following order.

- Rule 1

```
  Action: Disconnect 
  Interface: Wi-Fi 
  SSID: (your Wi-Fi SSID)
```

- Rule 2

```
  Action: Connect  
  No need to input any condition
```

Then, click *Enable VPN On Demand* and save the profile.

**Note 1:** Make sure the profile is selected (showing a checkmark). It will not work if the profile is not selected.

**Note 2:** The order is important. If you place Rule 2 before Rule 1, Rule 1 will never run because Rule 2 matches any condition.
You can change the order by tapping *Edit* and drag rules into your desired order.

### Q: What does the action type "Evaluate Connection" do?

Evaluate Connection is a special action that further assesses the action to take based on the current connection's destination.

If the destination can't be resolved on the current network, one of these actions can be taken.

- Connect If Needed
- Do Not Connect (Ignore)

For example, you can setup the following rule that if some internal website is being requested (not resolvable on the current network), VPN is automatically started.

```
Action: Connect If Needed
Domain Being Evaluated: companyinternal.com (this will match *.companyinternal.com)
```

### Q: What kind of shortcuts do you support?

As of version 3.8, we support the following shortcuts via the Shortcuts app.

- Turn VPN On / Off
  
  Specify the VPN profile you want to use. If nothing is specified and the action is Turn Off, the active VPN connection will be turned off.
  
- Toggle the state of VPN
  
  Specify the VPN profile you want to use. 
  
- Check the state of VPN
  
  Specify the VPN profile you want to use. If nothing is specified, the active connection (if any) will be reported.
  
- Get VPN log
  
  Return the log (text file) of the active connection. Do nothing if no active connection.

## SSTP Questions

### Q: Do you offer the same connectivity as the Windows built-in SSTP client?

In most cases we provide the same connectivity as the official client. All password and certificate-based authentication methods available in Windows 11 are supported.

In the case that you authenticate with a certificate installed on your Windows device, make sure you can export it including the private key.

If you think you might have a special case, please discuss with us.

## SoftEther Questions

### Q: If I can connect using the official SoftEther Client, does that mean I can use this app too?

In most cases we provide the same connectivity as the official client. Both direct (TCP) and NAT-T connections are supported.

However, connections via ICMP or DNS are not supported.

If you think you might have a special case, please discuss with us.

### Q: What is UDP acceleration?

SoftEther by default connects via direct TCP and data packets are transferred over TCP as well. UDP acceleration enables sending and receiving data packets over UDP. 
Although it's called acceleration, the speed may or may not be better than TCP, depending heavily on your network condition.

### Q: How do I know whether I am using UDP or TCP? Why is UDP not working sometimes?

"UDP" sign will be displayed in the status bar when UDP is used. You can also know it from the connection log. 

UDP acceleration has two working mode:
  - Direct mode, in which certain ports on the server need to be opened, just as in TCP. This is the most reliable mode.
  - NAT traversal mode, where no ports are open but the external IPs of the client and the server are obtained from external servers. 
    Both ends need to be sitting on the public address or behind some specific type of NAT network (called "cone NAT") in order to establish UDP connection. 
    Many cellular network, for example, uses symmetric NAT in IPv4 which does not allow NAT traversal. UDP acceleration will not work in these situations.

IPv6 network does not use NAT and should be naturally supporting UDP acceleration.

### Q: After I switch the network, UDP acceleration seems not working and why is that?

This is normal if the UDP acceleration works in NAT traversal mode, because according to the current SoftEther protocol there is no way to renegotiate a new endpoint for an existing session. 
Therefore the server has no way to know your new address and cannot reach the device after the network switch.

Once you switch back to the original network (provided that your IP address has not changed), the UDP will be probably working again.

You have two options to solve this problem:
  - Open the relevant UDP ports on the server side just like you have done for TCP (i.e. Direct mode), or
  - Manually reconnect in the new network.

### Q: Can I connect to the VPN Azure service?

Yes, you can. Make sure that you use the hostname (xx.vpnazure.net) as the server address. It will not work if you enter an IP address.

Also please note that VPN Azure has two modes: 
  - Relay mode, which is pure TCP and should work in most occasions but might be slower.
  - Direct mode, where data packets are transferred directly to the real server using UDP acceleration.

iOS version, server build and NAT types need to be satisfying the UDP acceleration requirements for direct mode to work.

### Q: Can I connect to the VPN Gate service?

Yes. Use these information when you connnect to VPN Gate servers.
  - Server: `xx.opengw.net` (or IP address)
  - Hostname: `xx.opengw.net` (only required if an IP is entered as server)
  - Port: TCP port number (UDP is not supported)
  - Virtual Hub: `vpngate`
  - Username: `vpn`
  - Password: `vpn`

CAUTION: VPN Gate servers are provided by various contributors around the world. We do not have any affiliation with them or the project, 
nor do we ensure connectivity or security in any form. 

USE THESE SERVERS AT YOUR OWN RISK!

## Import & Export

### Q: What are the file formats supported?

You can import from a SSTP Connect configuration file, or a SoftEther VPN connection setting file.
They are both ended in `.vpn` but are not compatible with each other.

A SSTP Connect configuration file can contain multiple VPN profiles.

The export format is always SSTP Connect. We do not support exporting in SoftEther VPN format.

### Q: Can I edit a SSTP Connect configuration file?

SSTP Connect configuration files use the JSON format.
You are not encouraged to edit by hand but if you wish to, you can do it with a JSON editor at your own risk.

### Q: How is my sensitive information saved in the configuration file if I do not add a password?

Passwords and private keys are saved in base64 encoding if not protected by passwords.
Anyone can reveal the plain text by using a base64 decoder.

### Q: How is my sensitive information encrypted if I add a password?

Passwords and private keys are encrypted using AEAD_AES_256_CBC_HMAC_SHA_384,
as described in [draft-mcgrew-aead-aes-cbc-hmac-sha2-05](https://datatracker.ietf.org/doc/draft-mcgrew-aead-aes-cbc-hmac-sha2/).

The base64-encoded AEAD ciphertexts ("C", as defined in 2.1) are saved in the corresponding fields.

AEAD_AES_256_CBC_HMAC_SHA_384 requires a key ("K") and associated data ("A") in order to work.

The associated data is the username to the password.
If a username is not available for a private key, the certificate label is used instead.

### Q: How is the encryption key ("K") derived?

Key derivation uses the PBKDF2 algorithm, with the following inputs:

- Password: From user input
- Salt: Randomly generated 128 bits
- PRF: HMAC-SHA1
- Iterations: 10000

The derived key is 56-octet in length, as required by AEAD_AES_256_CBC_HMAC_SHA_384.

A different key is generated for each export file. The random salt is included in the file.

With the above information, you can independently verify the encryption result.

### Q: Is the encryption secure enough?

It depends. No encryption is secure unless your password is strong.

## Other

### Q: Sometimes the WiFi icon goes off with the VPN icon for several seconds. What's going on?

This is an indication that VPN is reconnecting. You are not losing your WiFi connection. It's just how iOS responds to VPN reconnecting events.

### Q: I want to make sure traffic is blocked during reconnecting events (called "Seamless Tunnel" by OpenVPN). How can I do it?

This feature is already enabled and we do not offer a way to disable it.

However, please note that some system traffic does not go through VPN at all, including push notifications and some DNS requests. This is controlled by iOS.

### Q: Can you help with setting up a server?

We don't make server-side products, but we can provide general advice to you. 
If special assistance is needed, we will evaluate the situation and (in the case that we can help) may give you a quote.

### Q: What if I have more questions?

Send an email to support@domosekai.com and we will look into it. 
If it's a connection issue, please set log level to "debug" and send the connection log along with your mail.
