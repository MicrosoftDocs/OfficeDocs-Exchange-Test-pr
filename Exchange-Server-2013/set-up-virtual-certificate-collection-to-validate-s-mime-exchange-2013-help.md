---
title: 'Set up virtual certificate collection to validate S/MIME: Exchange 2013 Help'
TOCTitle: Set up virtual certificate collection to validate S/MIME
ms:assetid: 04a616e6-197c-490c-ae8c-c8d5f0f0b3dd
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn626155(v=EXCHG.150)
ms:contentKeyID: 61212602
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Set up virtual certificate collection to validate S/MIME

 

_**Applies to:** Exchange Online, Exchange Server 2013_


As a tenant administrator you will need to configure a virtual certificate collection that will be used to validate S/MIME certificates. This virtual certificate collection is set up as a certificate store file type with an SST filename extension. The SST file contains all the root and intermediate certificates that are used when validating an S/MIME certificate.

## Create and save an SST

You can only use the Shell to perform this procedure. To learn how to open the Exchange Management Shell in your on-premises Exchange organization, see [Open the Shell](https://technet.microsoft.com/en-us/library/dd638134\(v=exchg.150\)). To learn how to use Windows PowerShell to connect to Exchange Online, see [Connect to Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

As an administrator, you can create this SST file by exporting the certificates from a trusted machine using the `Export-Certificate` cmdlet and specifying the type as SST. For more information the `Export-Certificate` cmdlet, see the [Export-Certificate](https://technet.microsoft.com/en-us/library/hh848628.aspx) reference topic.

Once the SST file is generated, use the `Set-Smimeconfig` cmdlet to save it in the virtual certificate store by using the *-SMIMECertificateIssuingCA* parameter. For example: `Set-SmimeConfig -SMIMECertificateIssuingCA (Get-Content filename.sst -Encoding Byte)`

## Ensuring a certificate is valid

Exchange 2013 SP1 first checks for the SST file and validates the certificate. If the validation fails, it will look at the local machine certificate store to validate the certificate. This behavior is new for Exchange 2013 SP1 and different from prior versions of Exchange. In Exchange Online only the SST will be used for validation.

## More Information

[S/MIME for message signing and encryption](s-mime-for-message-signing-and-encryption-exchange-2013-help.md)

[Get-SmimeConfig](https://technet.microsoft.com/en-us/library/dn554257\(v=exchg.150\))

