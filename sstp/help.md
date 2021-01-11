---
layout: default
title: SSTP Connect
description: SSTP VPN Client for iOS
---

# FAQ

## Profile

### Q: What are the required items in a profile?

You need to provide at least these information:
  - A description of the connection
  - Server address (either domain name or IP)
  - Username and password

### Q: What do I need to fill in as server address? An IP or hostname?

Generally you should use hostnames (domain name) as server addresses, so that you don't need to take care of IP changes.

However, if you are using unreliable DNS service, or you want to enforce IPv4 / IPv6 connections (server is dual-stack), you can fill in IPs instead. 
In that case, you might also need to fill in the hostname field (server name) to pass TLS validation.

### Q: What is a hostname and when should I provide it?

In most cases, the hostname is the same as the domain name of the server and you don’t need to provide twice. A hostname is used to verify the identity of the server. If the name in the server’s certificate does not match the hostname, an error occurs and TLS validation fails.

In these situations, you may need to explicitly provide a hostname:
  - You have entered an IP address as the server address.
  - The server has a hostname different from its domain name.

## TLS validation

### Q: What is server trust evaluation and when should I disable it?

Server trust evaluation (or TLS validation) verifies the identity of the server. Every SSTP server must provide its certificate to the client and by verifying the validity of it you are more protected from someone who might hijack the network and try to steal your information (known as the man-in-the-middle attack).

Generally speaking, you should never disable TLS validation. However, in some circumstances you may want to do that (e.g. the server uses an obsolete or weak certificate and you can’t change it). Only use it as the last resort and always consult your server administrator first.

### Q: What requirements should a server certificate meet in order to pass TLS validation?

Rule of thumb: If you can open the server in Safari (an SSTP server should report 404 and it’s normal) instead of encountering some certificate error, you are good to go.

iOS has implemented more strict rules on server certificates since iOS 13. See below links for more information.

https://support.apple.com/en-us/HT210176

https://support.apple.com/en-us/HT211025

### Q: What should I do if the server uses a self-signed certificate or a certificate not signed by a public CA?

For security reasons, certificates signed by public CAs should be used. However if that’s not possible, you can ask your administrator for the root CA certificate and both install and trust it in your device. Note that the certificate still needs to meet iOS requirements, and depending on the certificates and your iOS version, it may not always work. Only disable server trust evaluation as the last resort.

## General

### Q: Can I connect or disconnect via system VPN settings?

Yes, you can. Your VPN profiles are saved in the system. Therefore, you can connect and disconnect the VPN without opening this app.

### Q: What information do you collect from the app?

Nothing. Your profiles are saved locally (in system settings) and passwords are stored in keychain. Connection logs are only in the memory and never (even temporarily) saved to the device. We do not send or receive anything in the background.

### Q: What if I have more questions?

Send an email to support@domosekai.com and we will look into it. 
If it relates to a potential bug, please set log level to "debug" and send the connection log along with your mail.

### Q: Can you help with setting up a server?

We don't make server-side products, but we can provide general advice to you. 
If special assistance is needed, we will evaluate the situation and (in the case that we can help) may give you a quote.
