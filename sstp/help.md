---
layout: default
title: SSTP Connect
description: SSTP / SoftEther VPN Client for iOS
---

[日本語はこちら](help-ja.html)

# FAQ

## General

### Q: Can I connect or disconnect via system VPN settings?

Yes, you can. Your VPN profiles are saved in the system. Therefore, you can connect and disconnect the VPN without opening this app.

### Q: What information do you collect from the app?

Nothing. Your profiles are saved locally (in system settings) and passwords are stored in keychain. Connection logs are only in the memory and never (even temporarily) saved to the device. We do not send or receive anything in the background.

### Q: Sometimes the WiFi icon goes off with the VPN icon for several seconds. What's going on?

This is an indication that VPN is reconnecting. You are not losing your WiFi connection. It's just how iOS responds to VPN reconnecting events.

### Q: I want to make sure traffic is blocked during reconnecting events (called "Seamless Tunnel" by OpenVPN). How can I do it?

This feature is already enabled and we do not offer a way to disable it.

However, please note that some system traffic does not go through VPN at all. (e.g. push notifications and some DNS requests)

This is controlled by iOS.

### Q: Sometimes automatic switch from mobile data does not happen even when the device has already connected to WiFi. Why is that?

The app relies on the system to notify it when alternative network path is available. It generally works but if the current connection is made over IPv6 and the new network (WiFI) does not support IPv6, there is chance that the notification will not arrive. 

You can learn from the connection log if a switch has occured. A manual reconnection may be necessary if the answer is no.

## Profile

### Q: What are the required items in a profile?

You need to provide at least these information:
  - A description of the connection
  - Server address
  - Username and password
  - Virutal hub name (SoftEther only)

### Q: What do I need to fill in as server address? An IP or a hostname?

Generally you should use a hostname (e.g. vpn.example.com), so that you don't need to take care of IP changes.

However, if your DNS provider is unreliable, or you want to enforce connecting via IPv4 or IPv6 (server is dual-stack), you can use an IP address instead. 
In that case, you need to put the hostname in the hostname field to pass TLS validation and for Windows servers to work.

## SSTP

### Q: Do you offer the same connectivity as the Windows SSTP client?

In most cases we provide the same connectivity as the official client. However in these situations our app does not work for you.
  - Connecting over HTTP / SOCKS proxy is required
  - Authentication method other than password is required
  - PEAP is required

## SoftEther

### Q: If I can connect using SoftEther Client for Windows, does that mean I can use this app as well?

In most cases we provide the same connectivity as the official client. However in these situations our app does not work for you.
  - NAT traversal or direct UDP connection is required to connect to the server
  - Connecting over HTTP / SOCKS proxy is required
  - Authentication method other than password is required

### Q: What is UDP acceleration and why is iOS 13 / server build 9695 required?

SoftEther by default connects via direct TCP and data packets are transferred over TCP as well. UDP acceleration enables sending and receiving data packets over UDP. 
Although it's named acceleration, the speed may or may not be better than TCP, depending heavily on your network condition.

SoftEther has historically implemented two versions of UDP acceleration. The original version encrypts data with RC4 cipher, which has been proved insecure and Apple has also ceased its support since iOS 10. 

The newer version was introduced in server build 9695 and uses ChaCha20-Poly1305 as cipher. Starting iOS 13, Apple has native support to it. 

### Q: How do I know whether I am using UDP or TCP? Why is UDP not working sometimes?

"UDP" sign will be displayed in the status bar when UDP is used. You can also know it from the connection log. 

UDP acceleration has two working mode:
  - Direct mode, in which certain ports on the server need to be opened, just as in TCP. This is the most reliable mode.
  - NAT traversal mode, where no ports are open but the external IPs of the client and the server are obtained from external servers. 
    Both ends need to be sitting on the public address or behind some specific type of NAT network (called "cone NAT") in order to establish UDP connection. 
    Many cellular network, for example, uses symmetric NAT in IPv4 which does not allow NAT traversal. UDP acceleration will not work in these situations.

IPv6 network does not use NAT and should be naturally supporting UDP acceleration.

### Q: After I switched the network, UDP acceleration seemd not working and why is that?

This is normal if the UDP acceleration works in NAT traversal mode, because according to the current SoftEther protocol there is no way to renegotiate a new endpoint for an existing session. 
Therefore the server has no way to know your new address and cannot reach the device after the network switch.

Once you switch back to the original network (provided that your IP address has not changed), the UDP will be probably working again.

You have two options to solve this problem:
  - Open the relevant UDP ports on the server side just like you have done for TCP (i.e. Direct mode), or
  - Manually reconnect in the new network.

### Q: Can I connect to VPN Azure service?

Yes, you can. Make sure that you use the hostname (xx.vpnazure.net) as the server address. It will not work if you enter an IP address.

Also please note that VPN Azure has two modes: 
  - Relay mode, which is pure TCP and should work in most occasions but might be slower.
  - Direct mode, where data packets are transferred directly to the real server using UDP acceleration.

iOS version, server build and NAT types need to be satisfying the above requirements for direct mode to work.

### Q: Can I connect to VPN Gate service?

Yes. Use these information when you connnect to VPN Gate servers.
  - Server: xx.opengw.net (or IP address)
  - Hostname: xx.opengw.net (only required if an IP is entered as server)
  - Port: TCP port number (UDP is not supported)
  - Virtual Hub: vpngate
  - Username: vpn
  - Password: vpn

CAUTION: VPN Gate servers are provided by various contributors around the world. We do not have any affiliation with them or the project, 
nor do we ensure connectivity or security in any form. 

USE THESE SERVERS AT YOUR OWN RISK!

## TLS validation

### Q: What is server trust evaluation and when should I disable it?

Server trust evaluation (or TLS validation) verifies the identity of the server. Every SSTP server must provide its certificate to the client and by verifying the validity of it you are more protected from someone who might hijack the network and try to steal your information (known as the man-in-the-middle attack).

Generally speaking, you should never disable TLS validation. However, in some circumstances you may want to do that (e.g. the server uses an obsolete or weak certificate and you can’t change it). Only use it as the last resort and always consult your server administrator first.

### Q: What requirements should a server certificate meet in order to pass TLS validation?

Rule of thumb: Add https\:// to your server address and open in Safari (e.g. https\://yourserveraddress). If it reports a 403 or 404 error, you are good to go (it's normal for an SSTP server since it's not a website). 

If you encounter some certificate error, you know that TLS validation has failed.

iOS has implemented more strict rules on server certificates since iOS 13. See below links for more information.

https://support.apple.com/en-us/HT210176

https://support.apple.com/en-us/HT211025

### Q: What should I do if I want to use certificates generated by SoftEther VPN Server?

Certificates automatically generated by SoftEther VPN Server do not meet iOS 13 requirements. Please follow this [guide](sevpn-cert.html) to regenerate.

### Q: What should I do if the server uses a self-signed certificate or a certificate not signed by a public CA?

For security reasons, certificates signed by public CAs should be used. However if that’s not possible, you can ask your administrator for the root CA certificate and both install and trust it in your device. Note that the certificate still needs to meet iOS requirements, and depending on the certificates and your iOS version, it may not always work. Only disable server trust evaluation as the last resort.

### Q: How to install and trust a certificate?

In iOS, a certificate (usually the root CA) is known as a profile. Email the certificate to your mailbox or download it from the web, then open it on your device. 
iOS should tell you that the profile is now ready to install.

To install it: https://support.apple.com/en-us/HT209435

To trust it: https://support.apple.com/en-us/HT204477

## Other

### Q: The app is draining my battery?

In the default profile, VPN stays on when your device goes to sleep. You can turn it off in the profile so that VPN only reconnects when the phone wakes up. This saves battery but reconnection may take some time.

However, sometimes the phone just refuses to go to sleep no matter how you set the option. You can know this from the connection log (no "Entering sleep mode" shown in the log). 
This is normal if the phone is charging or something is working in the background (e.g. music is playing). If there is nothing special, try restarting your device.

### Q: I have set "Stay connected during sleep" to on but the connections still get disconnected sometimes. Why is that?

As we mentioned above, sleep and wake-up is controlled by the system, of which the exact mechanism is unknown. 
If the system considers necessary to shut down network connections, the app has no way to keep connected. Sometimes a reboot may help.

We have also noticed that when both mobile data and WiFi is on, connections over WiFi might not survive during sleep. Try turning off mobile data.

### Q: Can you help with setting up a server?

We don't make server-side products, but we can provide general advice to you. 
If special assistance is needed, we will evaluate the situation and (in the case that we can help) may give you a quote.

### Q: What if I have more questions?

Send an email to support@domosekai.com and we will look into it. 
If it's a connection issue, please set log level to "debug" and send the connection log along with your mail.
