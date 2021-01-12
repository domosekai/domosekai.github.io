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
  - Server address (either a hostname or an IP address)
  - Username and password

### Q: What do I need to fill in as server address? An IP or a hostname?

Generally you should use a hostname (e.g. vpn.example.com), so that you don't need to take care of IP changes.

However, if your DNS provider is unreliable, or you want to enforce connecting via IPv4 or IPv6 (server is dual-stack), you can use an IP address instead. 
In that case, you might need to put the hostname in the hostname field to pass TLS validation.

### Q: When should I fill in the hostname field?

A hostname is used to verify the identity of the server. If the name in the server’s certificate does not match the hostname, an error occurs and TLS validation fails.

In most cases, the hostname is the same as the address of the server and you don’t need to provide twice. 
However, in these situations, you may need to explicitly provide a hostname:
  - You have entered an IP address as the server address.
  - The server has a hostname (as in its certificate) different from the address you are connecting to.

## TLS validation

### Q: What is server trust evaluation and when should I disable it?

Server trust evaluation (or TLS validation) verifies the identity of the server. Every SSTP server must provide its certificate to the client and by verifying the validity of it you are more protected from someone who might hijack the network and try to steal your information (known as the man-in-the-middle attack).

Generally speaking, you should never disable TLS validation. However, in some circumstances you may want to do that (e.g. the server uses an obsolete or weak certificate and you can’t change it). Only use it as the last resort and always consult your server administrator first.

### Q: What requirements should a server certificate meet in order to pass TLS validation?

Rule of thumb: Add https:// to your server address and open in Safari (e.g. https://yourserveraddress). If it reports a 403 or 404 error, you are good to go (it's normal for an SSTP server since it's not a website). 
If you encounter some certificate error, you know that TLS validation has failed.

iOS has implemented more strict rules on server certificates since iOS 13. See below links for more information.

https://support.apple.com/en-us/HT210176

https://support.apple.com/en-us/HT211025

### Q: What should I do if the server uses a self-signed certificate or a certificate not signed by a public CA?

For security reasons, certificates signed by public CAs should be used. However if that’s not possible, you can ask your administrator for the root CA certificate and both install and trust it in your device. Note that the certificate still needs to meet iOS requirements, and depending on the certificates and your iOS version, it may not always work. Only disable server trust evaluation as the last resort.

### Q: How to install and trust a certificate?

In iOS, a certificate (usually the root CA) is known as a profile. Email the certificate to your mailbox or download it from the web, then open it on your device. 
iOS should tell you that the profile is now ready to install.

To install it: https://support.apple.com/en-us/HT209435

To trust it: https://support.apple.com/en-us/HT204477

## General

### Q: Can I connect or disconnect via system VPN settings?

Yes, you can. Your VPN profiles are saved in the system. Therefore, you can connect and disconnect the VPN without opening this app.

### Q: What information do you collect from the app?

Nothing. Your profiles are saved locally (in system settings) and passwords are stored in keychain. Connection logs are only in the memory and never (even temporarily) saved to the device. We do not send or receive anything in the background.

### Q: Your app is draining my battery?

In the default profile, VPN stays on when your device goes to sleep. You can turn it off in the profile so that VPN reconnects when the phone wakes up. Note that reconnection may take some time.

However, sometimes the phone just refuses to go to sleep and you can confirm it through the connection log (no "Entering sleep mode" shown in the log). 
This is normal if the phone is charging or something is working in the background (e.g. music is playing). If there is nothing special, try restarting your device.

### Q: Why are there many "entering sleep mode" and "wake up" messages in the log?

This is normal. Sleep and wake-up is controlled by the system, not by the app. Usually you don't need to care about that.

The expected behavior is, if "Stay connected during sleep" is on, the app does nothing when phone sleeps, or disconnects the VPN if the option is off.

### Q: I have set "Stay connected during sleep" to on but the connections still get disconnected sometimes. Why is that?

As we mentioned above, sleep and wake-up is controlled by the system, of which the exact mechanism is unknown. 
If the system considers necessary to shut down network connections, the app has no way to keep connected. Sometimes a reboot helps.

### Q: What if I have more questions?

Send an email to support@domosekai.com and we will look into it. 
If it's a connection issue, please set log level to "debug" and send the connection log along with your mail.

### Q: Can you help with setting up a server?

We don't make server-side products, but we can provide general advice to you. 
If special assistance is needed, we will evaluate the situation and (in the case that we can help) may give you a quote.
