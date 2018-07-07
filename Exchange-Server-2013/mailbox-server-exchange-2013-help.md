---
title: 'Mailbox server: Exchange 2013 Help'
TOCTitle: Mailbox server
ms:assetid: 1aacc1c9-c81b-47d4-b222-ee73956cf968
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150491(v=EXCHG.150)
ms:contentKeyID: 47559954
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Mailbox server

 

_**Applies to:** Exchange Server 2013_


In Microsoft Exchange Server 2010, the Mailbox server role hosted both mailbox and public folder databases and also provided email message storage. Now, in Exchange Server 2013, the Mailbox server role also includes the Client Access protocols, Transport service, mailbox databases, and Unified Messaging components.

In Exchange 2013, the Mailbox server role interacts directly with Active Directory, the Client Access server, and Microsoft Outlook clients in the following process:

  - The Mailbox server uses LDAP to access recipient, server, and organization configuration information from Active Directory.

  - The Client Access server sends requests from clients to the Mailbox server and returns data from the Mailbox server to the clients. The Client Access server also accesses online address book (OAB) files on the Mailbox server through NetBIOS file sharing. The Client Access server sends messages, free/busy data, client profile settings, and OAB data between the client and the Mailbox server.

  - Outlook clients inside your firewall access the Client Access server to send and retrieve messages. Outlook clients outside the firewall can access the Client Access server by using Outlook Anywhere (which uses the RPC over HTTP Proxy component).

  - Public folder mailboxes are accessible via RPC over HTTP, regardless of whether the client is outside or inside the firewall.

  - The administrator-only computer retrieves Active Directory topology information from the Microsoft Exchange Active Directory Topology service. It also retrieves email address policy information and address list information.

  - The Client Access server uses LDAP or Name Service Provider Interface (NSPI) to contact the Active Directory server and retrieve users' Active Directory information.

**Mailbox and Client Access server interaction and architecture**

![Client Access and Mailbox server interaction](images/JJ150491.d14577bf-14f9-40fa-bd49-a92932eb003a(EXCHG.150).gif "Client Access and Mailbox server interaction")

For more details, see the “Exchange 2013 architecture” section in [What's new in Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).

## New Mailbox features

The following list briefly describes some new and some improved features in the Mailbox role for Exchange 2013:

  - Evolution of the Exchange 2010 database availability group (DAG):
    
      - Transaction log code has been refactored for fast failover with deep checkpoint on passive database copies.
    
      - To support enhanced site resiliency, servers can be in different locations.

  - Exchange 2013 now hosts some Client Access components, the Transport components, and the Unified Messaging components.

  - The Exchange Store has been re-written in managed code to improve performance in additional I/O reduction and reliability.

  - Each Exchange 2013 database now runs under its own process.

  - Smart Search has replaced the Exchange 2010 multi-mailbox search infrastructure.

## Securing Mailbox servers

By default, HTTP, Microsoft Exchange ActiveSync, POP3, and IMAP4 communication between the Mailbox servers and other Exchange server roles, domain controllers, and global catalog servers is encrypted. In addition, make sure that your Mailbox servers aren't accessible to the Internet.

## For more information

[Unified Messaging](unified-messaging-exchange-2013-help.md)

[Mail flow](mail-flow-exchange-2013-help.md)

[High availability and site resilience](high-availability-and-site-resilience-exchange-2013-help.md)

[Messaging policy and compliance](messaging-policy-and-compliance-exchange-2013-help.md)

[Mailbox moves in Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

[Manage mailbox databases in Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)

[Messaging policy and compliance](messaging-policy-and-compliance-exchange-2013-help.md)

[Recipients](recipients-exchange-2013-help.md)

[Collaboration](collaboration-exchange-2013-help.md)

