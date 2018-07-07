---
title: "Installation of the first Exchange server in the organization can't be delegated: Exchange 2013 Help"
TOCTitle: Installation of the first Exchange server in the organization can't be delegated
ms:assetid: 4cf9f1a1-aeac-455b-a5c3-efcd4185a467
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.delegatedclientaccessfirstinstall(v=EXCHG.150)
ms:contentKeyID: 46628932
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Installation of the first Exchange server in the organization can't be delegated

 

_**Applies to:** Exchange Server_


Microsoft Exchange Server 2013 Setup can’t continue because the logged-on user doesn’t have the account permissions that are required to install the first Exchange 2013 server in the organization.

Although Exchange 2013 Setup allows using delegation to install successive server roles, Setup requires that the user who is logged on is a member of the Enterprise Admins Windows security group when the first Exchange 2013 server in the organization is installed. This is required because Exchange 2013 Setup creates and configures objects in the Exchange Organization container in Active Directory during installation.


> [!NOTE]
> If you haven’t prepared the Active Directory schema for Exchange 2013, the logged-on user must also be a member of the Schema Admins Windows security group. Alternately, another user who’s a member of the Schema Admins Windows group can prepare the Active Directory schema before Exchange 2013 is installed.



To resolve this issue, add the logged-on user as a member of the Enterprise Admins security group. Or, log on to an account that’s a member of the Enterprise Admins security group. Then run Exchange 2013 Setup again.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Did you find what you’re looking for? Please take a minute to [send us feedback](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) about the information you were hoping to find.

