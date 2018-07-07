---
title: 'Active Directory does not exist or cannot be contacted: Exchange 2013 Help'
TOCTitle: Active Directory does not exist or cannot be contacted
ms:assetid: 56adb6fe-ecb8-4a7f-b440-89aa401c28b7
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.cannotaccessad(v=EXCHG.150)
ms:contentKeyID: 46628912
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Active Directory does not exist or cannot be contacted

 

_**Applies to:** Exchange Server_


Microsoft Exchange Server 2013 Setup can’t continue because it can't contact a valid Active Directory directory service site. Setup requires that the server you’re installing Exchange on is able to locate the configuration naming context in Active Directory.

To resolve this issue, verify that the user account running Exchange Setup is an Active Directory user and then run Setup again. If this doesn’t resolve the issue, follow the guidance about using the dcdiag.exe and repadmin.exe support tools from the topics below to further diagnose the problem.

For more information about Active Directory troubleshooting and configuration for Exchange, see the following topics:

  - [Prepare Active Directory and domains](prepare-active-directory-and-domains-exchange-2013-help.md)

  - [Troubleshooting Active Directory Domain Services](https://go.microsoft.com/fwlink/p/?linkid=272144)

  - [Configuring a Computer for Troubleshooting](https://go.microsoft.com/fwlink/p/?linkid=272141)

  - [Troubleshooting Active Directory Replication Problems](https://go.microsoft.com/fwlink/p/?linkid=272142)

  - [Monitoring and Troubleshooting Active Directory Replication Using Repadmin](https://go.microsoft.com/fwlink/p/?linkid=272143)

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Did you find what you’re looking for? Please take a minute to [send us feedback](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) about the information you were hoping to find.

