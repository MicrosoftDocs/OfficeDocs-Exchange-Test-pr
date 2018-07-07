---
title: 'Insufficient permissions to prepare Active Directory_DomainPrepWithoutADUpdate: Exchange 2013 Help'
TOCTitle: Insufficient permissions to prepare Active Directory_DomainPrepWithoutADUpdate
ms:assetid: 4283c4b9-983f-460e-a5de-42b2772eae0d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.domainprepwithoutadupdate(v=EXCHG.150)
ms:contentKeyID: 46628878
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Insufficient permissions to prepare Active Directory\_DomainPrepWithoutADUpdate

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft Exchange Server 2007 setup cannot continue because the attempted domain preparation failed.

Exchange setup requires that the Active Directory directory service be modified for Exchange Server 2007 before domains in the Active Directory can be prepared.

The account being used to run the **setup /PrepareAD** command has insufficient permissions to execute this command even though it appears to belong to the Enterprise Admins group. The account may have expired.

To resolve this issue, verify that the logged-on user account is valid and belongs to the Enterprise Admins group, or log on with an account that has those permissions and rerun **setup /PrepareAD**.

For more information about how to perform the PrepareAD process, see "How to Prepare Active Directory and Domains" ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453)).

For more information about Active Directory permissions that are needed with Microsoft Exchange, see "Working with Active Directory Permissions in Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

