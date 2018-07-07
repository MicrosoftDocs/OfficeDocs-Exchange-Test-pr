---
title: 'Create a digital certificate request: Exchange 2013 Help'
TOCTitle: Create a digital certificate request
ms:assetid: efb00de7-070b-46bf-a2fc-00d07ae085c1
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb125165(v=EXCHG.150)
ms:contentKeyID: 51492809
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Create a digital certificate request

 

_**Applies to:** Exchange Server 2013_


In Exchange Server 2013, you can manage certificates using the EAC or the Shell. The EAC includes a new certificate management user interface. Through this new UI, you can create a new certificate, edit an existing certificate, or remove a certificate.

## What do you need to know before you begin?

  - Estimated time to complete: 10 minutes plus time for the certification authority response.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Client Access server security" entry in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to create a new certificate request

1.  In the EAC, navigate to **Servers** \> **Certificates**.

2.  In the **Select server** list, select the server for which you want to create a certificate, and then click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

3.  In the **New Exchange certificate** wizard, choose either **Create a request for a certificate from a certification authority** or **Create a self-signed certificate**, and then select **Next**.

4.  Enter a friendly name for the certificate and select **Next**.

5.  If you didn’t choose a self-signed certificate and you want a wildcard certificate, select the box marked **Request a wildcard certificate**, enter the root domain, for example \*.contoso.com, and then select **Next**. If you chose a self-signed certificate, skip this step.

6.  Select the servers that you want to apply this certificate to and select **Next**.

7.  Specify the domains you want to be included in your certificate and then select **Next**.

8.  Verify that the included domains are correct. If you chose a self-signed certificate, select **Finish**. Otherwise select **Next**.

9.  Enter your organization name, department name, city or locality, state or province, and country or region, and then select **Next**.

10. Enter a location to save the certificate request and select **Finish**.

If you didn’t select a self-signed certificate, you’ll need to send the certificate request file to the certification authority for processing.

## Use the Shell to create a new certificate request

Run the following commands.

    $reqfile = New-ExchangeCertificate -GenerateRequest -SubjectName "C=US,o=Contoso,cn=contosotocert" -DomainName "contoso.com" -PrivateKeyExportable $true

    $reqfile | out-file c:\certreq.txt

## How do you know this worked?

If you created a self-signed certificate, the newly created certificate will appear in the certificate management UI. If you created a certificate request from a certification authority, the certificate request file will be in the location you specified. Send this file to the certification authority.

