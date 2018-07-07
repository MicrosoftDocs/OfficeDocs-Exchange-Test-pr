---
title: 'Client Access server: Exchange 2013 Help'
TOCTitle: Client Access server
ms:assetid: 87e206ab-7a7b-4b4f-be1a-5035713c74d2
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd298114(v=EXCHG.150)
ms:contentKeyID: 48385301
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Client Access server

 

_**Applies to:** Exchange Server 2013_


For Microsoft Exchange 2013, there have been major architectural changes to the Exchange server roles. Instead of the five server roles that were present in Exchange 2010 and Exchange 2007, in Exchange 2013, the number of server roles has been reduced to three: the Client Access server and the Mailbox server, and with Service Pack 1, the Edge Transport server role.


> [!NOTE]
> Exchange 2013 can also work with the Exchange 2010 Edge Transport server role.



The Exchange 2013 Mailbox server includes all many of the server components found in Exchange 2010: client access protocols, transport services, mailbox databases, and Unified Messaging services (the Client Access server redirects SIP traffic generated from incoming calls to the Mailbox server). For more information about the Exchange 2013 Mailbox server, see [Mailbox server](mailbox-server-exchange-2013-help.md).

The Client Access server provides authentication, proxy, and limited redirection services, and offers all the usual client access protocols: HTTP, POP, IMAP, and SMTP. The Client Access server is a thin and stateless server that doesn’t do any data rendering. There’s never anything queued or stored on the Client Access server. For more information about the new Exchange 2013 architecture, see [What's new in Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).


> [!WARNING]
> Client Access servers are not supported in perimeter networks, and they must be deployed within your internal Active Directory environment. Every Active Directory site that contains a Mailbox server must also contain a Client Access server.



As a result of these architectural changes, there have been some changes to client connectivity. First, RPC/TCP is no longer a supported direct access protocol. This means that all Outlook connectivity must occur using RPC over HTTPS (also known as Outlook Anywhere), or with Exchange 2013 SP1 and Outlook 2013 SP1, MAPI over HTTP. As a result of these changes, there’s no need to have the RPC Client Access service on the Client Access server. In addition, fewer namespaces are required for a site-resilient solution than were required in Exchange 2010, and it’s no longer necessary to provide affinity for the RPC Client Access service. Also, Outlook clients no longer connect to a server fully qualified domain name (FQDN) as they’ve done in all previous versions of Exchange. Using Autodiscover, Outlook finds a new connection point made up of the user’s mailbox GUID + @ + the domain portion of the user’s primary SMTP address. This change makes it much less likely that users will see the dreaded message “Your administrator has made a change to your mailbox.” Only Outlook 2007 and later versions are supported with Exchange 2013.

## Client Access server functionality

The Client Access server in Exchange 2013 functions much like a front door, admitting all client requests and routing them to the correct active Mailbox database. The Client Access server provides network security functionality such as Secure Sockets Layer (SSL) and client authentication, and manages client connections through redirection and proxy functionality. The Client Access server authenticates client connections and, in most cases, will proxy a request to the Mailbox server that houses the currently active copy of the database that contains the user's mailbox. In some cases, the Client Access server might redirect the request to a more suitable Client Access server, either in a different location or running a more recent version of Exchange Server.

The Client Access server has the following features:

  - **Stateless server** In previous versions of Exchange, many of the Client Access protocols required session affinity. For example, Outlook Web App required that all requests from a particular client be handled by a specific Client Access server within a load balanced array of Client Access servers. In Exchange 2013, the Client Access server is stateless. In other words, because all processing for the mailbox happens on the Mailbox server, it doesn’t matter which Client Access server in an array of Client Access servers receives each individual client request. This change in functionality means that session affinity is no longer required at the load balancer level. This allows inbound connections to Client Access servers to be balanced using simple techniques provided by load balancing technology such as DNS round-robin. It also allows hardware load balancing devices to support significantly more concurrent connections.

  - **Connection pooling** The Client Access servers handle client authentication and send the AuthN data to the Mailbox server. The account used by the Client Access servers to connect to the Mailbox servers is a privileged account that’s a member of the Exchange Servers group. This allows the Client Access servers to pool connections to the Mailbox servers effectively. An array of Client Access servers can handle millions of client connections from the Internet, but far fewer connections are used to proxy the requests to the Mailbox servers than in previous releases of Exchange. This improves processing efficiency and end-to-end latency.

## Management tasks on the Client Access server

In Exchange 2013, there are several key tasks that can be performed on the Client Access server. The management of digital certificates is primarily performed on the Client Access server and some of the client protocol management for Exchange ActiveSync, POP3, and IMAP4 is also handled on the Client Access server.

