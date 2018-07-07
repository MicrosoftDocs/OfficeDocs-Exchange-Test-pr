---
title: 'The local domain needs to be updated_LocalDomainPrep: Exchange 2013 Help'
TOCTitle: The local domain needs to be updated_LocalDomainPrep
ms:assetid: f33e6785-e85a-495e-a124-ebcb2b763e75
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.localdomainprep(v=EXCHG.150)
ms:contentKeyID: 46629174
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# The local domain needs to be updated\_LocalDomainPrep

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft Exchange Server 2007 setup cannot continue because the logged on user does not have the account permissions that are required for domain preparation.

Exchange setup requires that the user who is logged on when **Setup /PrepareDomain** is run be a member of the Domain Administrators and Exchange Organization Administrators groups, or the Enterprise Admins group.

To resolve this issue, grant the logged on user Domain Admins and Exchange Organization Administrator permissions, enroll them in the Enterprise Admins group, or log on with an account that has those permissions and rerun Exchange 2007 setup.

For more information about Active Directory permissions that are needed with Microsoft Exchange, see "Working with Active Directory Permissions in Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

