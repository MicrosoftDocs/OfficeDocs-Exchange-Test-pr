---
title: 'Create certificates for UM: Exchange 2013 Help'
TOCTitle: Create certificates for UM
ms:assetid: 66807ee7-3d3f-482d-a3ac-d4e9baca3271
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn205141(v=EXCHG.150)
ms:contentKeyID: 53908379
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Create certificates for UM

 

_**Applies to:** Exchange Server 2013_


You can use the New Exchange Certificate wizard in the EAC or the Shell to create self-signed certificates or certificate requests for an internal public key infrastructure (PKI) certificate. For Unified Messaging (UM), you can use one of these certificates for both the Microsoft Exchange Unified Messaging service and the Microsoft Exchange Unified Messaging Call Router services. You can use the same certificate for both services, or a different certificate for each service. You can also purchase and import a third-party commercial certificate for UM services. If you’re using a self-signed certificate for UM, you may need to include the name of your Client Access and Mailbox servers in the subject alternative name (SAN).

By default, when you install Exchange Server 2013, two self-signed certificates are created: **Microsoft Exchange Server Auth Certificate** and **Microsoft Exchange**. The **Microsoft Exchange** self-signed certificate can be used by UM to encrypt data, but you must assign the certificate to the UM and UM Call Router services. After you assign the certificate to the Unified Messaging services, it can be copied to and imported to the VoIP gateways, IP PBXs, and SIP-enabled PBXs. However, instead of using the default self-signed certificates, you may need to create another one specifically for Unified Messaging.


> [!WARNING]
> Self-signed certificates can’t be used when you’re integrating UM with Microsoft Lync Server.



For additional management tasks related to managing certificates for Unified Messaging, see [Deploying certificates for UM procedures](deploying-certificates-for-um-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Certificate management" entry in the [Exchange and Shell infrastructure permissions](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) topic and the "UM service" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic. You must also log on by using an account that's a member of the local Administrators group on that computer.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to create a certificate request for UM

1.  In the EAC, navigate to **Servers** \> **Certificates**, and then click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

2.  On the **New Exchange certificate** page, select **Create a request for a certificate from a certification authority**, and then click **Next**.

3.  Enter a friendly name for the certificate, and then click **Next**.

4.  If you don’t need a wildcard certificate, click **Next**. If you need a wildcard certificate, select **Request a wildcard certificate. A wildcard certificate can be used to secure all sub-domains under your root domain with a single certificate**, enter the name of the root domain, and then click **Next**.

5.  Under **Store certificate request on this server**, click **Browse** to go to the location where you want to store the file. You can store the certificate request on any Client Access or Mailbox server in your Exchange organization. Select the location, click **OK**, and then click **Next**.

6.  If you requested a wildcard certificate, skip to step 9.

7.  If you didn’t request a wildcard certificate, you’ll need to specify the domains you want to be included in your certificate. If you want to edit a domain, click **Edit**![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon"), and then click **Next**.

8.  Under **Based on your selections, the following domains will be included in your certificate. You can add additional domains here, or make changes**, you can add, edit, remove, or check the name of domains that are listed under **Domain**. Then click **Next**.

9.  Under **Specify information about your organization. This is required by the certification authority**, enter the following:
    
      - **Organization name**
    
      - **Department name**
    
      - **City/Locality**
    
      - **State/Province**
    
      - **County/Region name**   For this option, use the drop-down list to select the country or region.

10. Under **Save the certificate request to the following file**, enter the name of the certificate file, and then click **Finish**.

## Use the Shell to create a certificate request for UM

This example creates a new Exchange certificate request for a Mailbox server named `MyMailboxServer` with a friendly name of `CertUM`.

    New-ExchangeCertificate -FriendlyName 'CertUM' -GenerateRequest -PrivateKeyExportable $true -KeySize '2048' -DomainName '*.northwindtraders.com' -SubjectName 'C=US,S=wa,L=redmond,O=northwindtraders,OU=servers,CN= northwindtraders.com' -Server 'MyMailboxServer'

## Use the EAC to create a self-signed certificate for UM

1.  In the EAC, navigate to **Servers** \> **Certificates**, and then click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

2.  On the **New Exchange certificate** page, choose **Create a self-signed certificate**, and then select **Next**.

3.  Enter a friendly name for the certificate, and then select **Next**.

4.  Click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") to select the Exchange servers that you want to apply this certificate to, and then select **Next**.

5.  Specify the domains that you want to be included in your certificate, and then select **Next**. If you want to add a domain for a service, click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

6.  Verify that the domains you included are correct, and then select **Finish**.


> [!IMPORTANT]
> When you use the EAC to create a self-signed certificate, you won’t be prompted to enable services for the certificate. After the certificate has been created, you can use the EAC or the <STRONG>Enable-ExchangeCertificate</STRONG> cmdlet in the Shell to enable the Exchange services. For more information about how to assign a certificate to UM services, see <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Assign a certificate to the UM and UM Call Router services</A>.



## Use the Shell to create a self-signed certificate for UM

This example creates a new Exchange self-signed certificate for a Mailbox server named `MyMailboxServer` with a friendly name of `UMCert`.

    New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true


> [!TIP]
> When you specify the services you want to enable by using the <EM>Services</EM> parameter, you’ll be prompted to assign those services. In this example, you’ll be prompted to enable the certificate for the UM and UM Call Router services. For more information about how to enable a certificate for services, see <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Assign a certificate to the UM and UM Call Router services</A>.


