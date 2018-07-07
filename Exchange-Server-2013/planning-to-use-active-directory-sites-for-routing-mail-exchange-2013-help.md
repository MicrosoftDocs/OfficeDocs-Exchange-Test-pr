---
title: 'Planning to use Active Directory sites for routing mail: Exchange 2013 Help'
TOCTitle: Planning to use Active Directory sites for routing mail
ms:assetid: 0f697cee-bcaa-4c69-b80c-7a2afd1817d2
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa996299(v=EXCHG.150)
ms:contentKeyID: 49289169
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Planning to use Active Directory sites for routing mail

 

_**Applies to:** Exchange Server 2013_


Microsoft Exchange Server 2013 recognizes Active Directory sites and database availability groups (DAGs) as routing boundaries. However, Exchange 2013 still uses Active Directory site topology to determine how messages are transported between Exchange servers in different DAGs or sites within the organization. For more information, see [Mail routing](mail-routing-exchange-2013-help.md).

The Transport service on a Mailbox server provides message transport inside the Exchange organization. When you're deploying a pure Exchange 2013 organization, or introducing Exchange 2013 into a pure Exchange Server 2010 organization, no additional configuration is required to establish routing in the forest.

**Contents**

How Exchange 2013 uses Active Directory site membership

Determine Active Directory site membership

Overview of IP site links

Exchange 2013 server placement in Active Directory sites

## How Exchange 2013 uses Active Directory site membership

Exchange 2013 is a site-aware application. Site-aware applications can determine their own Active Directory site membership and the site membership of other servers by querying Active Directory. Exchange 2013 uses site membership to determine which domain controllers and global catalog servers to use for processing Active Directory queries. Additionally, when a server running Exchange has to determine the Active Directory site membership of another Exchange server, it can query Active Directory to retrieve the site name.

In Exchange 2013, the Microsoft Exchange Active Directory Topology service is responsible for updating the site attribute of the Exchange server object. Because the Active Directory site membership is a server object attribute, Exchange doesn't have to query DNS to resolve a server address to a subnet associated with an Active Directory site. Stamping the Active Directory site attribute on an Exchange server object also enables Active Directory site membership to be assigned to a server that isn't a domain member, such as a subscribed Edge Transport server.

The Exchange 2013 servers use Active Directory site membership information as follows:

  - **Mail submission**   The Mailbox Transport Submission service on an Exchange 2013 Mailbox server uses Active Directory site membership information to determine the other Exchange 2013 Mailbox servers that are located in the same Active Directory site. If the source Mailbox server doesn't belong to a DAG, or if the DAG doesn't span multiple Active Directory sites, the Mailbox Transport Submission service on the source Mailbox server submits messages for routing and transport to the Transport service on an Exchange 2013 Mailbox server in the same Active Directory site.

  - **Mail delivery**   The Transport service on an Exchange 2013 Mailbox server performs recipient resolution and queries Active Directory to match an email address to a recipient account. The recipient account information includes the fully qualified domain name (FQDN) of the user's mailbox database. The Transport service queries Active Directory to determine the Active Directory site of the user's mailbox database. If the mailbox database doesn't belong to a DAG, it will deliver the message to that Mailbox server. Otherwise, it will relay the message to another Mailbox server in the same site as the target Mailbox server for delivery.

  - **Message routing**   The Transport service on Exchange 2013 Mailbox servers retrieves information from Active Directory to determine how mail should be routed inside the organization. Exchange 2013 uses the concept of *delivery groups* to determine where and how to route messages. Depending on the destination, the message could be routed to the Transport service or the Mailbox Transport Delivery service on an Exchange 2013 Mailbox server, or to a Hub Transport server that's running a previous version of Exchange. For more information, see [Mail routing](mail-routing-exchange-2013-help.md).

  - **Unified Messaging message submission**   The Unified Messaging service on Exchange 2013 Mailbox servers uses Active Directory site membership information to find the other Mailbox servers that are located in the same Active Directory site. The Unified Messaging service submits messages for routing to the Transport service on a Mailbox server within the same Active Directory site. The Transport service server performs recipient resolution and queries Active Directory to match a telephone number, E.164 number, or a SIP address to a recipient account. After the recipient resolution completes, the Transport service delivers the message to the target mailbox in the same way as a regular email message.

  - **Client connections to Client Access server**   When the Client Access server receives a user connection request, it queries Active Directory to determine which Mailbox server is hosting the user's mailbox. The Client Access server then retrieves the Active Directory site membership of that Mailbox server and proxies the connection to the Mailbox server.

## Determine Active Directory site membership

Active Directory clients assume site membership by matching their assigned IP address to a subnet defined in Active Directory Sites and Services and associated with an Active Directory site. The client then uses this information to determine which domain controllers and global catalog servers exist in that site and communicates with those directory servers for authentication and authorization purposes. Exchange 2013 takes advantage of this relationship by also preferring to retrieve information about recipients from directory servers in the same site as the Exchange 2013 server.

All computers that are part of the same Active Directory site are considered well connected, with a high-speed, reliable network connection. By default, when an Active Directory forest is first deployed, there's a single site named `Default-First-Site-Name`. If no other sites are manually configured by the administrator, all server and client computers in the forest are considered members of `Default-First-Site-Name`.

When more than one site is defined, the Active Directory administrator must define the subnets present in the organization and associate those subnets with Active Directory sites.

The Microsoft Exchange Active Directory Topology service checks the site membership attribute on the Exchange server object when the server starts. If the site attribute has to be updated, the Microsoft Exchange Active Directory Topology service stamps the attribute with the new value. The Microsoft Exchange Active Directory Topology service verifies the site attribute value every 15 minutes and updates the value if site membership has changed. The Microsoft Exchange Active Directory Topology service uses the Net Logon service to obtain current site membership. The Net Logon service updates site membership every five minutes. This means that up to a 20 minute latency period may pass between the time that site membership changes and the new value is stamped on the site attribute.

## Overview of IP site links

Relationships between Active Directory sites are defined by IP site links. The IP site link consists of two or more Active Directory sites. All Active Directory sites that are part of the link communicate at the same cost. The IP site link properties include a cost assignment, a schedule, and an interval. The schedule and interval properties are only used for determining Active Directory replication frequency. Exchange 2013 uses the cost assignment to determine the lowest cost route for traffic to follow when multiple paths exist to the destination. The cost of the route is determined by aggregating the cost of all site links in a transmission path. The Active Directory administrator assigns the cost to a link based on relative network speed and available bandwidth compared to other available connections.

By default, the Transport service on a Mailbox server always tries a direct connection to the Transport service or the Mailbox Transport Delivery service on a Mailbox server in another Active Directory site. Messages in transport don't relay through the Transport service on each Mailbox server in a site link path. However, Mailbox servers in intermediate Active Directory sites along the routing path may perform message relay in the following scenarios:

  - Direct relay between Mailbox servers won't occur when a hub site exists along the least cost routing path. You can configure an Active Directory site as a hub site so that messages are routed through the hub site before the messages are relayed to the target server. Hub sites are discussed later in this topic.

  - Exchange 2013 uses the routing path derived from IP site link information when communication to the destination Active Directory site fails. If no Mailbox server in the destination Active Directory site responds, message delivery backs off along the least cost routing path until a connection is made to a Mailbox server in an Active Directory site along the routing path. The messages are queued in that Active Directory site and the queue will be in a retry state. This behavior is called *queue at point of failure*.

  - In Exchange 2013 organizations without DAGs, the Transport service on a Mailbox server can also use the IP site link information to optimize routing of messages sent to multiple recipients. The Mailbox server delays bifurcation of messages until it reaches a fork in the routing paths to the recipients. The bifurcated message is relayed to each recipient destination by a Mailbox server in the Active Directory site that represents the fork in the individual routing paths. This functionality is called *delayed fan-out*.

## Designate hub sites

You can use the **Set-AdSite** cmdlet to configure an Active Directory site as a hub site. When a hub site exists along the least cost routing path between two transport servers, messages are routed through the hub site for processing before they are relayed to the destination server. For this routing behavior to occur, the hub site must exist along the least cost routing path between two transport servers. This configuration should only be used when it's required by the network topology, such as when firewalls exist between Active Directory sites and prevent direct relay of SMTP communications. For more information, see [Configure Exchange mail routing settings in Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

## Set an Exchange-specific cost on an IP site link

You can use the **Set-AdSiteLink** cmdlet in the Exchange Management Shell to configure an Exchange-specific cost to an Active Directory IP site link. The Exchange-specific cost is a separate attribute used instead of the Active Directory-assigned cost to determine the Exchange routing path. This configuration is useful when the Active Directory IP site link costs don't result in an optimal Exchange message routing topology. For more information, see [Configure Exchange mail routing settings in Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

## Set message size restrictions on IP site links

By default, Exchange 2013 doesn't impose a maximum message size limit on messages relayed between Mailbox servers in different Active Directory sites. If you use the **Set-AdSiteLink** cmdlet to configure a maximum message size on an Active Directory IP site link, routing generates a non-delivery report (NDR) for any message that has a size larger than the maximum message size limit configured on any Active Directory site link in the least cost routing path. This configuration is useful for restricting the size of messages sent to remote Active Directory sites that must communicate over low-bandwidth connections.

## Exchange 2013 server placement in Active Directory sites

For message routing between Exchange 2013 servers to occur correctly, all Exchange servers deployed in the forest must belong to an Active Directory site. Make sure that the IP addresses that you have assigned are in subnets that are correctly associated with Active Directory sites.

The first step in planning the placement of Exchange 2013 servers in the Active Directory site topology is to document the current topology. Your documentation should include the following:

  - Sites

  - Subnets and their site association

  - IP site links and their member sites

  - IP site link costs

  - Directory servers in each site

  - Physical network connections

  - Firewall locations

After you have diagrammed these objects, plan the placement of Exchange servers. Consider the following information when deciding where to put servers:

  - A Mailbox server needs to communicate directly with a global catalog server to perform Active Directory lookups.

  - We recommend that you deploy more than one Mailbox server in each Active Directory site to provide load balancing and fault tolerance.

  - DAGs and site resilience

  - The Unified Messaging service on Mailbox servers submits voice mail messages to the Transport service on Mailbox servers for delivery to mailboxes. The Client Access server that's running the Unified Messaging Call Router service may be located in a hub site or near the IP or Voice over IP (VoIP) gateway, IP Private Branch eXchange (IP PBX), SIP-enabled PBX, or session border controllers (SBC). The Transport service on a Mailbox server that has the same site membership as the Client Access server will receive voice mail messages for transport and route the messages to the Transport service on other Mailbox servers in the organization.

  - Client Access servers provide a connectivity point to the Exchange organization for users who are accessing Exchange remotely. A Client Access server must be deployed in each Active Directory site that contains Mailbox servers.

After you plan your Exchange 2013 server placement, you may identify areas where you can modify the Active Directory site topology to improve communication flow. You may want to adjust IP site links and site link costs to optimize mail delivery. An efficient Active Directory topology doesn't require any changes to support Exchange 2013

