# FAQ

## Profile

### Q: What are the required items in a profile?

You need to provide at least these information:
  - A description of the connection
  - Server address (either domain name or IP)
  - Username and password

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

### Q: What are the limitations in the trial mode?

Trial mode limits each session to 10 minutes. It gives you an option to test your connections before purchase.

### Q: What information do you collect from the app?

Nothing. Your profiles are saved locally (in system settings) and passwords are stored in keychain. Connection logs are only in the memory and never (even temporarily) saved to the device. 

Moreover, the app has these features:

  - Zero 3rd-party SDK. This means no ads, no analytics etc. On iOS 14 devices the installed size can be as low as about 1MB.
  - Pure Swift implementation. 
  - System native TLS stack (including trust evaluation) for connecting to your servers. This ensures better security and updates automatically with the system.
  - Zero network connection other than those made to your specified servers. We do not send or receive anything in the background.

### Q: What if I have more questions?

Send an email to support@domosekai.com and we will look into it.
