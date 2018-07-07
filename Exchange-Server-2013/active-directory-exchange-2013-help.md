---
title: 'Active Directory: Exchange 2013 Help'
TOCTitle: Active Directory
ms:assetid: 8e8464df-2d1d-4d68-82de-b0c158c549c3
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb123715(v=EXCHG.150)
ms:contentKeyID: 49289336
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Active Directory

 

_**Applies to:** Exchange Server 2013_


Microsoft Exchange Server 2013 uses Active Directory to store and share directory information with Windows. Active Directory forest design for Exchange 2013 is similar to Exchange Server 2010, except in a few ways, which are discussed below.

## Active Directory driver

The Active Directory driver is the core Microsoft Exchange component that allows Exchange services to create, modify, delete, and query for Active Directory Domain Services (AD DS) data. In Exchange 2013, all access to Active Directory is done using the Active Directory driver itself. Previously, in Exchange 2010, DSAccess provided directory lookup services for components such as SMTP, message transfer agent (MTA), and the Exchange store.

The Active Directory driver also uses Microsoft Exchange Active Directory Topology (MSExchangeADTopology), which allows the Active Directory driver to use Directory Service Access (DSAccess) topology data. This data includes the list of available domain controllers and global catalog servers available to handle Exchange requests. For more information about the Active Directory Driver, see [Active Directory Domain Services](https://go.microsoft.com/fwlink/p/?linkid=110942).

## Active Directory schema changes

Exchange 2013 adds new attributes to the Active Directory domain service schema and also makes other modifications to existing classes and attributes. For more information about Active Directory changes when you install Exchange 2013, see [Exchange 2013 Active Directory schema changes](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

## For more information

To learn more about how Exchange 2013 stores and retrieves information in Active Directory so that you can plan access to it, see [Access to Active Directory](access-to-active-directory-exchange-2013-help.md).

For more information about Active Directory forest design, see [AD DS Design Guide](https://go.microsoft.com/fwlink/p/?linkid=264957).

To learn more about computers running Windows in an Active Directory domain and deploying Exchange 2013 in a domain that has a disjoint namespace, see [Disjoint namespace scenarios](disjoint-namespace-scenarios-exchange-2013-help.md).

