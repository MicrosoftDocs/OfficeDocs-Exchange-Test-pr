---
title: 'Digital certificates and SSL: Exchange 2013 Help'
TOCTitle: Digital certificates and SSL
ms:assetid: a9e2e08c-d46a-4135-a387-eb653212b676
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd351044(v=EXCHG.150)
ms:contentKeyID: 48385423
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Digital certificates and SSL

 

_**Applies to:** Exchange Server 2013_


Secure Sockets Layer (SSL) is a method for securing communications between a client and a server. For Exchange Server 2013, SSL is used to help secure communications between the server and clients. Clients include mobile phones, computers inside an organization's network, and computers outside an organization's network.

By default, when you install Exchange 2013, client communications are encrypted using SSL when you use Outlook Web App, Exchange ActiveSync, and Outlook Anywhere.

SSL requires you to use digital certificates. This topic summarizes the different types of digital certificates and information about how to configure Exchange 2013 to use these types of digital certificates.

**Contents**

Overview of digital certificates

Digital certificates and proxying

Digital certificates best practices

## Overview of digital certificates

Digital certificates are electronic files that work like an online password to verify the identity of a user or a computer. They're used to create the SSL encrypted channel that's used for client communications. A certificate is a digital statement that's issued by a certification authority (CA) that vouches for the identity of the certificate holder and enables the parties to communicate in a secure manner using encryption.

Digital certificates do the following:

  - They authenticate that their holders—people, websites, and even network resources such as routers—are truly who or what they claim to be.

  - They protect data that's exchanged online from theft or tampering.

Digital certificates can be issued by a trusted third-party CA or a Windows public key infrastructure (PKI) using Certificate Services, or they can be self-signed. Each type of certificate has advantages and disadvantages. Each type of digital certificate is tamper-proof and can't be forged.

Certificates can be issued for several uses. These uses include web user authentication, web server authentication, Secure/Multipurpose Internet Mail Extensions (S/MIME), Internet Protocol security (IPsec), Transport Layer Security (TLS), and code signing.

A certificate contains a public key and attaches that public key to the identity of a person, computer, or service that holds the corresponding private key. The public and private keys are used by the client and the server to encrypt the data before it's transmitted. For Windows-based users, computers, and services, trust in a CA is established when there's a copy of the root certificate in the trusted root certificate store and the certificate contains a valid certification path. For the certificate to be valid, the certificate must not have been revoked and the validity period must not have expired.

## Types of certificates

There are three primary types of digital certificates: self-signed certificates, Windows PKI-generated certificates, and third-party certificates.

## Self-signed certificates

When you install Exchange 2013, a self-signed certificate is automatically configured on the Mailbox servers. A self-signed certificate is signed by the application that created it. The subject and the name of the certificate match. The issuer and the subject are defined on the certificate. This self-signed certificate is used to encrypt communications between the Client Access server and the Mailbox server. The Client Access server trusts the self-signed certificate on the Mailbox server automatically, so no third-party certificate is needed on the Mailbox server. When you install Exchange 2013, a self-signed certificate is also created on the Client Access server. This self-signed certificate will allow some client protocols to use SSL for their communications. Exchange ActiveSync and Outlook Web App can establish an SSL connection by using a self-signed certificate. Outlook Anywhere won't work with a self-signed certificate on the Client Access server. Self-signed certificates must be manually copied to the trusted root certificate store on the client computer or mobile device. When a client connects to a server over SSL and the server presents a self-signed certificate, the client will be prompted to verify that the certificate was issued by a trusted authority. The client must explicitly trust the issuing authority. If the client confirms the trust, then SSL communications can continue.


> [!NOTE]
> By default, the digital certificate installed on the Mailbox server or servers is a self-signed certificate. You don’t need to replace the self-signed certificate on the Mailbox servers in your organization with a trusted third-party certificate. The Client Access server automatically trusts the self-signed certificate on the Mailbox server and no other configuration is needed for certificates on the Mailbox server.



Frequently, small organizations decide not to use a third-party certificate or not to install their own PKI to issue their own certificates. They might make this decision because those solutions are too expensive, because their administrators lack the experience and knowledge to create their own certificate hierarchy, or for both reasons. The cost is minimal and the setup is simple when you use self-signed certificates. However, it's much more difficult to establish an infrastructure for certificate life-cycle management, renewal, trust management, and revocation when you use self-signed certificates.

## Windows public key infrastructure certificates

The second type of certificate is a Windows PKI-generated certificate. A PKI is a system of digital certificates, certification authorities, and registration authorities (RAs) that verify and authenticate the validity of each party that's involved in an electronic transaction by using public key cryptography. When you implement a PKI in an organization that uses Active Directory, you provide an infrastructure for certificate life-cycle management, renewal, trust management, and revocation. However, there is some additional cost involved in deploying servers and infrastructure to create and manage Windows PKI-generated certificates.

Certificate Services are required to deploy a Windows PKI and can be installed through **Add Or Remove Programs** in Control Panel. You can install Certificate Services on any server in the domain.

If you obtain certificates from a domain-joined Windows CA, you can use the CA to request or sign certificates to issue to your own servers or computers on your network. This enables you to use a PKI that resembles a third-party certificate vendor, but is less expensive. These PKI certificates can't be deployed publicly, as other types of certificates can be. However, when a PKI CA signs the requestor's certificate by using the private key, the requestor is verified. The public key of this CA is part of the certificate. A server that has this certificate in the trusted root certificate store can use that public key to decrypt the requestor's certificate and authenticate the requestor.

The steps for deploying a PKI-generated certificate resemble those required for deploying a self-signed certificate. You must still install a copy of the trusted root certificate from the PKI to the trusted root certificate store of the computers or mobile devices that you want to be able to establish an SSL connection to Microsoft Exchange.

A Windows PKI enables organizations to publish their own certificates. Clients can request and receive certificates from a Windows PKI on the internal network. The Windows PKI can renew or revoke certificates.

## Trusted third-party certificates

Third-party or commercial certificates are certificates that are generated by a third-party or commercial CA and then purchased for you to use on your network servers. One problem with self-signed and PKI-based certificates is that, because the certificate is not automatically trusted by the client computer or mobile device, you must make sure that you import the certificate into the trusted root certificate store on client computers and devices. Third-party or commercial certificates do not have this problem. Most commercial CA certificates are already trusted because the certificate already resides in the trusted root certificate store. Because the issuer is trusted, the certificate is also trusted. Using third-party certificates greatly simplifies deployment.

For larger organizations or organizations that must publicly deploy certificates, the best solution is to use a third-party or commercial certificate, even though there is a cost associated with the certificate. Commercial certificates may not be the best solution for small and medium-size organizations, and you might decide to use one of the other certificate options that are available.

Return to top

## Choosing a certificate type

When you choose the type of certificate to install, there are several things to consider. A certificate must be signed to be valid. It can be self-signed or signed by a CA. A self-signed certificate has limitations. For example, not all mobile devices let a user install a digital certificate in the trusted root certificate store. The ability to install certificates on a mobile device depends on the mobile device manufacturer and the mobile service provider. Some manufacturers and mobile service providers disable access to the trusted root certificate store. In this case, neither a self-signed certificate nor a certificate from a Windows PKI CA can be installed on the mobile device.

## Default Exchange certificates

By default, Exchange installs a self-signed certificate on both the Client Access server and the Mailbox server so that all network communication is encrypted. Encrypting all network communication requires that every Exchange server have an X.509 certificate that it can use. You should replace this self-signed certificate on the Client Access server with one that is automatically trusted by your clients.

“Self-signed” means that a certificate was created and signed only by the Exchange server itself. Because it wasn't created and signed by a generally trusted CA, the default self-signed certificate won't be trusted by any software except other Exchange servers in the same organization. The default certificate is enabled for all Exchange services. It has a subject alternative name (SAN) that corresponds to the server name of the Exchange server that it's installed on. It also has a list of SANs that include both the server name and the fully qualified domain name (FQDN) of the server.

Although other Exchange servers in your Exchange organization trust this certificate automatically, clients like web browsers, Outlook clients, mobile phones, and other email clients in addition to external email servers won't automatically trust it. Therefore, consider replacing this certificate with a trusted third-party certificate on your Exchange Client Access servers. If you have your own internal PKI, and all your clients trust that entity, you can also use certificates that you issue yourself.

## Certificate requirements by service

Certificates are used for several things in Exchange. Most customers also use certificates on more than one Exchange server. In general, the fewer certificates you have, the easier certificate management becomes.

## IIS

All the following Exchange services use the same certificate on a given Exchange Client Access server:

  - Outlook Web App

  - Exchange Administration Center (EAC)

  - Exchange Web Services

  - Exchange ActiveSync

  - Outlook Anywhere

  - Autodiscover

  - Outlook Address Book distribution

Because only a single certificate can be associated with a website, and because all these services are offered under a single website by default, all the names that clients of these services use must be in the certificate (or fall under a wildcard name in the certificate).

## POP/IMAP

Certificates that are used for POP or IMAP can be specified separately from the certificate that's used for IIS. However, to simplify administration, we recommend that you include the POP or IMAP service name in your IIS certificate and use a single certificate for all these services.

## SMTP

A separate certificate can be used for each receive connector that you configure. The certificate must include the name that SMTP clients (or other SMTP servers) use to reach that connector. To simplify certificate management, consider including all names for which you have to support TLS traffic in a single certificate.

## Digital certificates and proxying

Proxying is the method by which one server sends client connections to another server. In the case of Exchange 2013, this happens when the Client Access server proxies an incoming client request to the Mailbox server that contains the active copy of the client’s mailbox.

When Client Access servers proxy requests, SSL is used for encryption but not for authentication. The self-signed certificate on the Mailbox server encrypts the traffic between the Client Access server and the Mailbox server.

## Reverse proxies and certificates

Many Exchange deployments use reverse proxies to publish Exchange services on the Internet. Reverse proxies can be configured to terminate SSL encryption, examine the traffic in the clear on the server, and then open a new SSL encryption channel from the reverse proxy servers to the Exchange servers behind them. This is known as SSL bridging. Another way to configure the reverse proxy servers is to let the SSL connections pass straight through to the Exchange servers behind the reverse proxy servers. With either deployment model, the clients on the Internet connect to the reverse proxy server using a host name for Exchange access, such as mail.contoso.com. Then the reverse proxy server connects to Exchange using a different host name, such as the machine name of the Exchange Client Access server. You don't have to include the machine name of the Exchange Client Access server on your certificate because most common reverse proxy servers are able to match the original host name that's used by the client to the internal host name of the Exchange Client Access server.

## SSL and split DNS

Split DNS is a technology that allows you to configure different IP addresses for the same host name, depending on where the originating DNS request came from. This is also known as split-horizon DNS, split-view DNS, or split-brain DNS. Split DNS can help you reduce the number of host names that you must manage for Exchange by allowing your clients to connect to Exchange through the same host name whether they're connecting from the Internet or from the intranet. Split DNS allows requests that originate from the intranet to receive a different IP address than requests that originate from the Internet.

Split DNS is usually unnecessary in a small Exchange deployment because users can access the same DNS endpoint whether they're coming from the intranet or the Internet. However, with larger deployments, this configuration will result in too high of a load on your outgoing Internet proxy server and your reverse proxy server. For larger deployments, configure split DNS so that, for example, external users access mail.contoso.com and internal users access internal.contoso.com. Using split DNS for this configuration ensures that your users won't have to remember to use different host names depending on where they're located.

## Remote Windows PowerShell

Kerberos authentication and Kerberos encryption are used for remote Windows PowerShell access, from both the Exchange Administration Center (EAC) and the Exchange Management Shell. Therefore, you won't have to configure your SSL certificates for use with remote Windows PowerShell.

Return to top

## Digital certificates best practices

Although the configuration of your organization's digital certificates will vary based on its specific needs, information about best practices has been included to help you choose the digital certificate configuration that's right for you.

## Best practice: Use a trusted third-party certificate

To prevent clients from receiving errors regarding untrusted certificates, the certificate that's used by your Exchange server must be issued by someone that the client trusts. Although most clients can be configured to trust any certificate or certificate issuer, it's simpler to use a trusted third-party certificate on your Exchange server. This is because most clients already trust their root certificates. There are several third-party certificate issuers that offer certificates configured specifically for Exchange. You can use the EAC to generate certificate requests that work with most certificate issuers.

## How to select a certification authority

A certification authority (CA) is a company that issues and ensures the validity of certificates. Client software (for example, browsers such as Microsoft Internet Explorer, or operating systems such as Windows or Mac OS) have a built-in list of CAs they trust. This list can usually be configured to add and remove CAs, but that configuration is often cumbersome. Use the following criteria when you select a CA to buy your certificates from:

  - Ensure the CA is trusted by the client software (operating systems, browsers, and mobile phones) that will connect to your Exchange servers.

  - Choose a CA that says it supports “Unified Communications certificates” for use with Exchange server.

  - Make sure that the CA supports the kinds of certificates that you’ll use. Consider using subject alternative name (SAN) certificates. Not all CAs support SAN certificates, and other CAs don't support as many host names as you might need.

  - Make sure that the license you buy for the certificates allows you to put the certificate on the number of servers that you intend to use. Some CAs only allow you to put a certificate on one server.

  - Compare certificate prices between CAs.

## Best practice: Use SAN certificates

Depending on how you configure the service names in your Exchange deployment, your Exchange server may require a certificate that can represent multiple domain names. Although a wildcard certificate, such as one for \*.contoso.com, can resolve this problem, many customers are uncomfortable with the security implications of maintaining a certificate that can be used for any subdomain. A more secure alternative is to list each of the required domains as SANs in the certificate. By default, this approach is used when certificate requests are generated by Exchange.

## Best practice: Use the Exchange certificate wizard to request certificates

There are many services in Exchange that use certificates. A common error when requesting certificates is to make the request without including the correct set of service names. The certificate wizard in the Exchange Administration Center will help you include the correct list of names in the certificate request. The wizard lets you specify which services the certificate has to work with and, based on the services selected, includes the names that you must have in the certificate so that it can be used with those services. Run the certificate wizard when you've deployed your initial set of Exchange 2013 servers and determined which host names to use for the different services for your deployment. Ideally you'll only have to run the certificate wizard one time for each Active Directory site where you deploy Exchange.

Instead of worrying about forgetting a host name in the SAN list of the certificate that you purchase, you can use a certification authority that offers, at no charge, a grace period during which you can return a certificate and request the same new certificate with a few additional host names.

## Best practice: Use as few host names as possible

In addition to using as few certificates as possible, you should also use as few host names as possible. This practice can save money. Many certificate providers charge a fee based on the number of host names you add to your certificate.

The most important step you can take to reduce the number of host names that you must have and, therefore, the complexity of your certificate management, is not to include individual server host names in your certificate's subject alternative names.

The host names you must include in your Exchange certificates are the host names used by client applications to connect to Exchange. The following is a list of typical host names that would be required for a company named Contoso:

  - **Mail.contoso.com**   This host name covers most connections to Exchange, including Microsoft Outlook, Outlook Web App, Outlook Anywhere, the Offline Address Book, Exchange Web Services, POP3, IMAP4, SMTP, Exchange Control Panel, and ActiveSync.

  - **Autodiscover.contoso.com**   This host name is used by clients that support Autodiscover, including Microsoft Office Outlook 2007 and later versions, Exchange ActiveSync, and Exchange Web Services clients.

  - **Legacy.contoso.com**   This host name is required in a coexistence scenario with Exchange 2007 and Exchange 2013. If you'll have clients with mailboxes on Exchange 2007 and Exchange 2013, configuring a legacy host name prevents your users from having to learn a second URL during the upgrade process.

## Understanding wildcard certificates

A wildcard certificate is designed to support a domain and multiple subdomains. For example, configuring a wildcard certificate for \*.contoso.com results in a certificate that will work for mail.contoso.com, web.contoso.com, and autodiscover.contoso.com.

Return to top

