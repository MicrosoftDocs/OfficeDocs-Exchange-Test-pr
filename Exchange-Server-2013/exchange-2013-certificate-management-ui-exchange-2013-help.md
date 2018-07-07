---
title: 'Exchange 2013 certificate management UI: Exchange 2013 Help'
TOCTitle: Exchange 2013 certificate management UI
ms:assetid: 8975848d-07f0-4643-9eac-20aece69945f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ984582(v=EXCHG.150)
ms:contentKeyID: 51541779
ms.date: 07/14/2016
mtps_version: v=EXCHG.150
---

# Exchange 2013 certificate management UI

 

_**Applies to:** Exchange Server 2013_


Managing certificates in an Exchange Server deployment is one of the most important administrative tasks. Ensuring that certificates are appropriately set up and configured is key to delivering a secure messaging infrastructure for the enterprise. In Exchange 2010, the Exchange Management Console (EMC) was the primary method of managing certificates. In Exchange 2013, certificate management functionality is provided in the Exchange Administration Console (EAC), the new Exchange 2013 administrative user interface. In Exchange 2013, the focus is on minimizing the number of certificates that an administrator must manage, minimizing the interaction the administrator must have with certificates, and allowing management of certificates from a central location.

## Client Access server certificates

The Client Access server in Exchange 2013 is a stateless thin server designed to accept incoming client connections and proxy them to the correct Mailbox server. The Exchange Certificate Management UI on the Client Access server can help you with a variety of tasks, including requesting new certificates and renewing expired or soon–to-expire certificates.

## Understanding the Certificate Management UI

You can access the Exchange Certificate Management UI through the EAC by selecting **Servers** and then **Certificates**. Using the management UI you can perform the following actions:

  - **Create a new certificate**   Selecting **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") launches the New Exchange Certificate wizard.

  - **Edit an existing certificate**   Selecting **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon") on a valid certificate allows you to see the certificate’s property page.

  - **Delete a certificate**   Selecting **Delete** ![Delete icon](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon") when a certificate is selected launches the delete confirmation dialog box.

  - **Perform additional actions**   Selecting **More options** ![More Options Icon](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "More Options Icon") allows you to export or import a certificate. If you want to export a certificate, the certificate must be valid.

## Certificate expiration

In previous versions of Microsoft Exchange, you couldn’t easily see when a digital certificate was nearing expiration. In Exchange 2013, the Notifications center displays warnings when a certificate stored on any Exchange 2013 Client Access server is about to expire.

## Mailbox server certificates

One key difference between Exchange 2010 and Exchange 2013 is that the certificates that are used on the Exchange 2013 Mailbox server are self-signed certificates. Because all clients connect to an Exchange 2013 Mailbox server through an Exchange 2013 Client Access server, the only certificates that you need to manage are those on the Client Access server. The Client Access server automatically trusts the self-signed certificate on the Mailbox server, so clients will not receive warnings about a self-signed certificate not being trusted, provided that the Client Access server has a non-self-signed certificate from either a Windows certification authority (CA) or a trusted third party. There are no tools or cmdlets available to manage self-signed certificates on the Mailbox server. After the server has been properly installed, you should never need to worry about the certificates on the Mailbox server.

## Self-signed certificate expiration

By default, the self-signed certificate that is installed on the Exchange 2013 Mailbox server will expire five years from the date of installation.

## Certificate cmdlets

You can use the following cmdlets to manage digital certificates on an Exchange Client Access server:

  - Import-ExchangeCertificate   This cmdlet is used to import certificates to a server. You can import a CA-signed certificate (to complete a pending certificate signing request (CSR)) or a certificate with a private key (PKCS \#12 files, generally with a .pfx extension, previously exported from a server along with the private key).

  - Remove-ExchangeCertificate   This cmdlet is used to remove certificates from a server.

  - Enable-ExchangeCertificate   This cmdlet is used to assign services to a certificate.

  - Get-ExchangeCertificate   This cmdlet is used to retrieve an Exchange certificate based on a variety of criteria.

  - New-ExchangeCertificate   This cmdlet is used to create a new self-signed certificate or a CSR.

