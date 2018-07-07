---
title: 'Exchange Search: Exchange 2013 Help'
TOCTitle: Exchange Search
ms:assetid: 967e2a13-4e54-486a-ac22-08768674abbb
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb232132(v=EXCHG.150)
ms:contentKeyID: 51407269
ms.date: 06/04/2016
mtps_version: v=EXCHG.150
---

# Exchange Search

 

_**Applies to:** Exchange Server 2013_


With increasing mailbox sizes and increasing amounts of data being stored in mailboxes in the form of messages and attachments, it's crucial for users to be able to quickly search and locate the messages they need. [In-Place Archiving in Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md) helps you reduce or eliminate the use of .pst files by moving old and infrequently accessed items to the archive. This results in more mailbox data being stored by a user, and it makes searching across the user's primary and archive mailboxes an important productivity tool. [In-Place eDiscovery](in-place-ediscovery-exchange-2013-help.md) allows authorized users to search content in mailboxes across on-premises and cloud-based Exchange organizations to comply with electronic discovery (eDiscovery) requests, regulatory audits, or internal investigations. In-Place eDiscovery also uses the content indexes created by Exchange Search.

Exchange Search is different from full-text indexing available in Exchange Server 2003. Improvements were made to performance, content indexing, and search. New items are indexed in the transport pipeline or almost immediately after they're created or delivered to the mailbox, providing users with a fast, stable, and more reliable way of searching mailbox data. Content indexing is enabled by default, and there's no initial setup or configuration required.

For more information about Exchange Search, see:

  - [File formats indexed by Exchange Search](file-formats-indexed-by-exchange-search-exchange-2013-help.md)

  - [Message properties indexed by Exchange Search](message-properties-indexed-by-exchange-search-exchange-2013-help.md)

Looking for management tasks related to Exchange Search? See [Exchange Search procedures](exchange-search-procedures-exchange-2013-help.md).

## What’s New

Exchange 2013 introduces the following changes to Exchange Search:

  - The underlying content indexing engine has been replaced with Microsoft Search Foundation, which provides performance and functionality improvements and serves as the common underlying content indexing engine in Exchange and SharePoint. The management interface, however, remain the same.

  - By default, the Search Foundation handles the most common file formats in email attachments. You no longer need to install Microsoft Office Filter Packs for Exchange Search. For a list of the file formats handled by Exchange Search, see [File formats indexed by Exchange Search](file-formats-indexed-by-exchange-search-exchange-2013-help.md).
    
    You can add support for any additional file formats by install IFilters, as in previous versions of Exchange.

  - Content indexing is more efficient because it now processes messages in the transport pipeline. As a result, messages addressed to multiple recipients or distribution groups are processed only once. An annotation stream is attached to the message, significantly speeding up content indexing while consuming fewer resources.

