---
title: 'Database portability: Exchange 2013 Help'
TOCTitle: Database portability
ms:assetid: 387b727a-ce51-4910-b5c4-613c693fa5bd
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd876873(v=EXCHG.150)
ms:contentKeyID: 50873792
ms.date: 01/30/2017
mtps_version: v=EXCHG.150
---

# Database portability

 

_**Applies to:** Exchange Server 2013_


Database portability is a feature that enables a Microsoft Exchange Server 2013 mailbox database to be moved to or mounted on any other Mailbox server in the same organization running Exchange 2013 that has databases with the same database schema version. Mailbox databases from previous versions of Exchange can't be moved to a Mailbox server running Exchange 2013. By using database portability, reliability is improved by removing several error-prone, manual steps from the recovery processes. In addition, database portability reduces the overall recovery times for various failure scenarios.

When using database portability to recover a mailbox database, the operating system version and the Exchange Server version on the source and target Exchange servers must be the same. For example, if an Exchange 2013 mailbox database was previously mounted on a server running Windows Server 2012, database portability will only work when migrating the database to a server also running Windows Server 2012 and Exchange 2013.

For information about how to perform a database recovery using the database portability feature, see [Move a mailbox database using database portability](move-a-mailbox-database-using-database-portability-exchange-2013-help.md).

