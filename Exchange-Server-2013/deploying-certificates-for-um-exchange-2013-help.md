---
title: 'Deploying certificates for UM: Exchange 2013 Help'
TOCTitle: Deploying certificates for UM
ms:assetid: 95658f6f-eac2-4674-90e7-f2d3f25c5242
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee681661(v=EXCHG.150)
ms:contentKeyID: 51439481
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Deploying certificates for UM

 

_**Applies to:** Exchange Server 2013_


You can use mutual Transport Layer Security (mutual TLS) to enable Unified Messaging (UM) to encrypt data sent between your Microsoft Exchange 2013 servers and VoIP gateways, IP PBXs, session border controllers (SBCs), and Microsoft Lync Server. Certificates bind the identity of the certificate owner to a pair of electronic keys (public and private) that are used to encrypt and sign information digitally.

If you’re using SIP secured or Secured dial plans in your Exchange 2010 organization, you’ll need to import the certificates that were used to your Exchange 2013 Client Access servers running the Microsoft Exchange UM Call Router service and Mailbox servers running the Microsoft Exchange UM service. You can use one of the following certificates for the UM and UM Call Router services:

  - A self-signed (Exchange) certificate

  - An internal public key infrastructure (PKI) certificate

  - A third-party commercial certificate

By default, when you install Unified Messaging, a self-signed certificate is created and used. This self-signed certificate can be used with VoIP gateways, IP PBXs, and SBCs, but not when you’re integrating UM with Lync Server. If you’re deploying certificates to be used with Lync Server, you need to use the Exchange certificate wizard or the **New-ExchangeCertificate** cmdlet to obtain a certificate that was issued by an internal or PKI certification authority (CA), or purchase a commercial or third-party certificate that is mutually trusted by Unified Messaging and Lync Server.

## Deploying certificates for VoIP gateways, IP PBXs, and SBCs

To enable UM to encrypt data that's sent between VoIP gateways, IP PBXs, and SBCs you need to do the following:

  - Use the self-signed UM certificate, create a new Exchange certificate request and obtain an internal PKI certificate, or purchase a third-party commercial certificate that you can use for mutual TLS between UM and VoIP gateways, IP PBXs, and SBCs.

  - Import the certificate that will be used on all Client Access and Mailbox servers in your organization.

  - Enable the certificate to be used by UM services.

  - Import the certificate on your VoIP gateways, IP PBXs, and SBCs.

  - Configure the UM dial plan as SIP secured or Secured.

  - Configure the UM startup mode on Client Access and Mailbox servers in your organization.

  - Create the required UM IP gateways with a fully qualified domain name (FQDN).

  - Configure the listening port on the UM IP gateways to use TLS port 5061.

  - Restart the Unified Messaging Call Router service on all Client Access servers and restart the Microsoft Exchange Unified Messaging service on all Mailbox servers.

## Deploying certificates for Lync Server

To encrypt data that's sent between UM and Lync Server, you need to do the following:

  - Create a new Exchange certificate request and obtain an internal PKI certificate, or purchase a third-party commercial certificate. The certificate must be mutually trusted by UM and Lync Server.

  - Import the certificate that will be used on all Client Access and Mailbox servers in your organization.

  - Enable the certificate to be used by UM services.

  - Import the certificate on the computers running Lync Server.

  - Configure the SIP URI UM dial plan as SIP secured or Secured.

  - Configure the UM startup mode on Client Access and Mailbox servers in your organization.

  - Run OcsUmUtil.exe from a Lync Server computer.

  - Restart the Unified Messaging Call Router service on all Client Access servers and restart the Microsoft Exchange Unified Messaging service on all Mailbox servers in your organization. For details, see [UM services procedures](um-services-procedures-exchange-2013-help.md).

  - Restart the Lync Server Front-End service on all Lync Servers that are part of an Enterprise Edition Front End pool or restart the Standard Edition Front End Servers. You can use the **Stop-CsWindowsService** cmdlet to stop Lync Server services and the **Start-CsWindowsService** cmdlet to start Lync Server services.
    
    The **Start-CsWindowsService** and **Stop-CsWindowsService** cmdlets are similar to the generic Windows PowerShell cmdlets **Start-Service** and **Stop-Service**. If you want, you could use the **Start-Service** or **Stop-Service** cmdlets to start and stop a Lync Server service. However, the **Start-CsWindowsService** **Stop-CsWindowsService** cmdlets include a *ComputerName* parameter that makes it easy to stop and start a Lync Server service on a remote computer. To do this, you include the *ComputerName* parameter followed by the fully qualified domain name (FQDN) of the remote computer. The **Start-Service** and **Stop-Service** cmdlets don’t have a comparable parameter.
    

    > [!NOTE]
    > To fully integrate UM and Lync Server, you must also run the ExchUcUtil.ps1 script on any Client Access or Mailbox server in your organization


