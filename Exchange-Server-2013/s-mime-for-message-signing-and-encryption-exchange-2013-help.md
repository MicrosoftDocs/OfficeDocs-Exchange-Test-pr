﻿---
title: 'S/MIME for message signing and encryption: Exchange 2013 Help'
TOCTitle: S/MIME for message signing and encryption
ms:assetid: 887c710b-0ec6-4ff0-8065-5f05f74afef3
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn626158(v=EXCHG.150)
ms:contentKeyID: 61212601
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# S/MIME for message signing and encryption

 

_**Applies to:** Exchange Online, Exchange Server 2013_


S/MIME (Secure/Multipurpose Internet Mail Extensions) is a widely accepted method, or more precisely a protocol, for sending digitally signed and encrypted messages. S/MIME allows you to encrypt emails and digitally sign them. When you use S/MIME with an email message, it helps the people who receive that message to be certain that what they see in their inbox is the exact message that started with the sender. It will also help people who receive messages to be certain that the message came from the specific sender and not from someone pretending to be the sender. To do this, S/MIME provides for cryptographic security services such as authentication, message integrity, and non-repudiation of origin (using digital signatures). It also helps enhance privacy and data security (using encryption) for electronic messaging. For a more complete background about the history and architecture of S/MIME in the context of email, see [Understanding S/MIME](https://go.microsoft.com/fwlink/?linkid=393948).

As an administrator, you can enable S/MIME-based security for your organization if you have mailboxes in either Exchange 2013 SP1 or Exchange Online, a part of Office 365. Use the guidance in the topics linked here along with the Exchange Management Shell to set up S/MIME. To use S/MIME in supported versions of Outlook or ActiveSync, with either Exchange 2013 SP1 or Exchange Online, the users in your organization must have certificates issued for signing and encryption purposes and data published to your on-premises Active Directory Domain Service (AD DS). Your AD DS must be located on computers at a physical location that you control and not at a remote facility or cloud-based service somewhere on the internet. For more information about AD DS, see [Active Directory Domain Services](https://go.microsoft.com/fwlink/?linkid=394064).

## Supported scenarios and technical considerations

If your organization uses either Exchange 2013 SP1 or Exchange Online, you can set up S/MIME to work with any of the following end points:

  - Outlook 2010

  - Outlook 2013

  - Outlook Web App

  - Exchange ActiveSync (EAS)

The steps that you follow to set up S/MIME with each of these end points is slightly different depending on which you choose. Generally, you will need to accomplish the following:

  - Install a Windows-based Certification Authority and set up a public key infrastructure to issue S/MIME certificates. Certificates issued by third-party certificate providers are also supported. For details, see [Active Directory Certificate Services Overview](https://technet.microsoft.com/library/hh831740.aspx).

  - Publish the user certificate in an on-premises AD DS account in the UserSMIMECertificate and/or UserCertificate attributes.

  - For Exchange Online organizations, synchronize the user certificates from AD DS to Azure Active Directory by using an appropriate version of DirSync. These certificates will then get synchronized from Azure Active Directory to Exchange Online directory and will be used when encrypting a message to a recipient.

  - Set up a virtual certificate collection in order to validate S/MIME. This information is used by OWA when validating the signature of an email and ensuring that it was signed by a trusted certificate.

  - Set up the Outlook or EAS end point to use S/MIME.

## Setup S/MIME with Outlook Web App

Setting up S/MIME for Exchange 2013 SP1 or Exchange Online with Outlook Web App involves the following key steps:

1.  [Configure S/MIME settings for Outlook Web App](configure-s-mime-settings-for-outlook-web-app-exchange-2013-help.md)

2.  [Set up virtual certificate collection to validate S/MIME](set-up-virtual-certificate-collection-to-validate-s-mime-exchange-2013-help.md)

3.  [Sync user certificates to Office 365 for S/MIME](https://technet.microsoft.com/en-us/library/dn626159\(v=exchg.150\)) This step applies to Exchange Online only.

## Related message encryption technologies

As message security becomes more important, administrators need to understand the principles and concepts of secure messaging. This understanding is especially important because of the growing variety of protection-related technologies, such as S/MIME, that have become available. To understand more about S/MIME and how it works in context of email, see [Understanding S/MIME](https://go.microsoft.com/fwlink/?linkid=393948). A variety of encryption technologies work together to provide protection for messages at rest and in-transit. S/MIME can work simultaneously with the following technologies but is not dependent on them:

  -  **Transport Layer Security (TLS)** encrypts the tunnel or the route between email servers in order to help prevent snooping and eavesdropping.

  -  **Secure Sockets Layer (SSL)** encrypts the connection between email clients and Office 365 servers.

  -  **BitLocker** encrypts the data on a hard drive in a datacenter so that if someone gets unauthorized access, they can’t read it.

## S/MIME compared with Office 365 Message Encryption

S/MIME requires a certificate and publishing infrastructure that is often used in business-to-business and business-to-consumer situations. The user controls the cryptographic keys in S/MIME and can choose whether to use them for each message they send. Email programs such as Outlook search a trusted root certificate authority location to perform digital signing and verification of the signature. Office 365 Message Encryption is a policy-based encryption service that can be configured by an administrator, and not an individual user, to encrypt mail sent to anyone inside or outside of the organization. It’s an online service that’s built on Azure Rights Management (RMS) and does not rely on a public key infrastructure. Office 365 Message Encryption also provides additional capabilities, such as the capability to customize the mail with organization’s brand. For more information about Office 365 Message Encryption, see [Office 365 Message Encryption](https://go.microsoft.com/fwlink/?linkid=392525).

## More information

[Outlook Web App](outlook-web-app-exchange-2013-help.md)

[Secure Mail (2000)](https://technet.microsoft.com/en-us/library/cc962043.aspx)

