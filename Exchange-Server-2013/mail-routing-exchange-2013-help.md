---
title: 'Mail routing: Exchange 2013 Help'
TOCTitle: Mail routing
ms:assetid: 6fd39079-9655-4fd9-9269-c7462c76e0a7
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998825(v=EXCHG.150)
ms:contentKeyID: 48385209
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Mail routing

 

_**Applies to:** Exchange Server 2013_


The primary task of the Transport service that exists on all Mailbox servers in your Microsoft Exchange Server 2013 organization is to route messages received from users and external sources to their ultimate destinations. Routing decisions are made during message categorization. The categorizer is a component of the Transport service on a Mailbox server that processes all incoming messages and determines what to do with the message based on information about their destinations.

Routing in Exchange 2013 is now fully aware of Database Availability Groups (DAGs), and uses DAG membership as a routing boundary. Why? In Exchange 2013, all Mailbox servers host the Transport service. Therefore, when a Mailbox server belongs to a DAG, the primary mechanism for routing messages is closely aligned with the DAG. And when a DAG spans multiple Active Directory sites, using the Active Directory site as the primary routing boundary is inefficient. Exchange 2013 also uses Active Directory site membership as a routing boundary for Mailbox servers that don't belong to DAGs, and for routing interoperability with previous versions of Exchange. Other notable changes to Exchange 2013 routing include:

  - The Transport service on a Mailbox server never communicates directly with a mailbox database. Instead, the Transport service communicates with the Mailbox Transport service on the Mailbox server. Only the Mailbox Transport service communicates with the mailbox database on the local Mailbox server. When the Mailbox server is a member of a DAG, only the Mailbox Transport service on the Mailbox server that holds the active copy of the mailbox database accepts the message for the destination recipient.

  - Remote procedure calls (RPCs) are only used by the Mailbox Transport service when sending messages to or receiving messages from the local mailbox database. When the Mailbox server is a member of a DAG, the Mailbox Transport service only uses RPCs to communicate locally with the active copies of the mailbox databases. In other words, RPC is never used for cross-server communication. Instead, the Mailbox Transport service and the Transport service on different Mailbox servers always communicate using SMTP.

  - Exchange 2013 uses more precise queuing for remote destinations. Instead of using one queue for all destinations in a remote Active Directory site, Exchange 2013 queues messages for specific destinations within the Active Directory site, such as individual Send connectors.

  - Linked connectors have been deprecated. A linked connector was a Receive connector that was linked to a Send connector. All messages received by the Receive connector were automatically forwarded to the Send connector.

**Contents**

Routing components

  - Routing destinations

  - Delivery groups

  - Queues

Routing messages

  - Routing messages between Active Directory sites

  - Routing in the Front End Transport service

  - Routing in the Mailbox Transport service

  - Routing in the Transport service on Edge Transport servers

## Routing components

When a message is received by the Transport service on an Exchange 2013 Mailbox server, the message must be categorized. The first phase of message categorization is recipient resolution. After the recipient has been resolved, the ultimate destination can be determined. The next phase, routing, determines how to best reach that destination. Routing in Exchange 2013 has been generalized for increased flexibility and decreased complexity by introducing the concepts of routing destinations and delivery groups.

## Routing destinations

In Exchange 2013, the ultimate destination for a message is called a *routing destination*. The following routing destinations exist in Exchange 2013:

  - **A mailbox database**   This is the routing destination for any recipient with a mailbox on a Mailbox server in the Exchange organization. In Exchange 2013, public folders are a type of mailbox, so routing messages to public folder recipients is the same as routing messages to mailbox recipients.

  - **A connector**   A connector is a Send connector for SMTP messages when used as a routing destination. A Delivery Agent connector or a Foreign connector is used as a routing destination for non-SMTP messages.

  - **A distribution group expansion server**   This is the routing destination when a distribution group has a designated expansion server that's responsible for expanding the membership list of the group. A distribution group expansion server is always a Hub Transport server or an Exchange 2013 Mailbox server.

Note that these same routing destinations also existed in previous versions of Exchange.

Return to top

## Delivery groups

Each routing destination in Exchange 2013 has a collection of one or more transport servers that are responsible for delivering messages to that routing destination. This collection of transport servers is called a *delivery group*. A transport server could be an Exchange 2013 Mailbox server, or an Exchange 2010 server or Exchange 2007 server that has the Hub Transport server role installed. When the routing destination is a mailbox database, the transport servers in the delivery group are the same version of Exchange as the mailbox database. When the routing destination is a connector or a distribution group expansion server, the delivery group may contain a mixture of Exchange 2013 Mailbox servers and Exchange 2010 or Exchange 2007 Hub Transport servers. How the message is routed depends on the relationship between the source transport server and the destination delivery group:

  - If the source transport server is in the destination delivery group, the routing destination itself is the next hop for the message. The message is delivered by the source transport server to the mailbox database or connector on a transport server in the delivery group. Note that when a distribution group expansion server is the routing destination, the distribution group is already expanded by the time messages reach the routing stage of categorization on the distribution group expansion server. Therefore, the routing destination from the distribution group expansion server is always a mailbox database or a connector.

  - If the source transport server is outside the destination delivery group, the message is relayed along the least-cost routing path to the destination delivery group. Depending on the size and complexity of the Exchange topology, the message is relayed to other transport servers along the least cost routing path, or the message is relayed directly to a transport server in the destination delivery group.

The following types of delivery groups exist in Exchange 2013:

  - **Routable DAG**   This is a collection of Exchange 2013 Mailbox servers that belong to one DAG. The mailbox databases in the DAG are the routing destinations that are serviced by this delivery group. After the message arrives at the Transport service on a Mailbox server that belongs to the DAG, the Transport service routes the message to the Mailbox Transport service on the Mailbox server in the DAG that currently holds the active copy of the destination mailbox database. The Mailbox Transport service on the destination Mailbox server then delivers the message to the local mailbox database. Although a DAG may contain Mailbox servers located in different Active Directory sites, the DAG is the delivery group boundary.

  - **Mailbox delivery group**   This is a collection of Exchange servers of the same version located in one Active Directory site. The Active Directory site is the delivery group boundary. The routing destinations and the delivery groups that service them are separated by the major release versions of Exchange in the Active Directory site. The mailbox databases located on Exchange 2010 Mailbox servers are serviced by the Exchange 2010 Hub Transport servers located in the Active Directory site. The mailbox databases located on Exchange 2007 Mailbox servers are serviced by the Exchange 2007 Hub Transport servers located in the Active Directory site. The mailbox databases located on Exchange 2013 Mailbox servers in Active Directory site that don't belong to a DAG are serviced by the Transport service on Exchange 2013 Mailbox servers in the Active Directory site. How the message is delivered to the mailbox database depends on version of Exchange:
    
      - **Exchange 2013**   After the message arrives at the destination Mailbox server in the destination Active Directory site, the Transport service uses SMTP to transfer the message to the Mailbox Transport service. The Mailbox Transport service then delivers the message to the local mailbox database using RPC.
    
      - **Exchange 2010 or Exchange 2007**   After the message arrives at a random Hub Transport server of the same version in the destination Active Directory site, the store driver on the Hub Transport server uses RPC to write the message to the mailbox database.

  - **Connector source servers**   This is a mixed collection of Exchange 2010 or Exchange 2007 Hub Transport servers, or Exchange 2013 Mailbox servers that are scoped as the source server for a Send connector, a Delivery Agent connector or a Foreign connector. The connector is the routing destination that's serviced by this routing group. When a connector is scoped to a specific server, only that server is allowed to route messages to destination defined by the connector. This delivery group may contain Exchange 2010 or Exchange 2007 Hub Transport servers, or Exchange 2013 Mailbox servers located in different Active Directory sites.

  - **AD site**   In some circumstances, an Active Directory site isn't the ultimate destination of a message, but the message must pass through an Exchange 2010 or Exchange 2007 Hub Transport server or Exchange 2013 Mailbox server in that Active Directory site. Those circumstances include:
    
      - When the Active Directory site is configured as a hub site. When the hub site exists on the least-cost routing path for message delivery, the messages queue and are processed by a transport server in the hub site before they're relayed to their ultimate destination.
    
      - When an Edge Transport server is subscribed to the Active Directory site. These subscribed Edge Transport servers aren't directly accessible from other Active Directory sites. Note that the Edge Transport server could be Exchange 2013, Exchange 2010 or Exchange 2007.
    

    > [!NOTE]
    > Delayed fan-out is only used when the delivery group is an Active Directory site. Delayed fan-out attempts to reduce the number of message transmissions when multiple recipients share any part of the least-cost routing path.



  - **Server list**   This is a collection of one or more Exchange 2010 or Exchange 2007 Hub Transport servers or Exchange 2013 Mailbox servers that are configured as distribution group expansion servers. The distribution group expansion server is the routing destination serviced by this delivery group.

Delivery group membership isn't mutually exclusive. For example, an Exchange 2013 Mailbox server that's a member of a DAG can also be the source server of a scoped Send connector. This Mailbox server would belong to the routable DAG delivery group for the mailbox databases in the DAG, and also a connector source server delivery group for the scoped Send connector.

The following table maps the routing destinations to the delivery group based on the version of Exchange involved:


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>Exchange 2013 Mailbox server</th>
<th>Exchange 2010 or Exchange 2007 Hub Transport server</th>
<th>Edge Transport server in the perimeter network</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mailbox database in a DAG</p></td>
<td><p>Routable DAG</p></td>
<td><p>Mailbox delivery group</p></td>
<td><p>n/a</p></td>
</tr>
<tr class="even">
<td><p>Mailbox database not in a DAG</p></td>
<td><p>Mailbox delivery group</p></td>
<td><p>Mailbox delivery group</p></td>
<td><p>n/a</p></td>
</tr>
<tr class="odd">
<td><p>Connector</p></td>
<td><p>Connector source servers</p></td>
<td><p>Connector source servers</p></td>
<td><p>AD site</p></td>
</tr>
<tr class="even">
<td><p>Distribution group expansion server</p></td>
<td><p>Server list</p></td>
<td><p>Server list</p></td>
<td><p>n/a</p></td>
</tr>
</tbody>
</table>


Return to top

## Queues

From the perspective of the sending server, each delivery queue represents the destination for a particular message. When the Transport service on the Exchange 2013 Mailbox server selects the destination for a message, the destination is stamped on the recipient as the **NextHopSolutionKey** attribute. If a single message is being sent to more than one recipient, each recipient has the **NextHopSolutionKey** attribute. The receiving server also performs message categorization and queues the message for delivery. After a message is queued, you can examine the delivery type for a particular queue to determine whether a message will be relayed again when it reaches the next hop destination. Every unique value of the **NextHopSolutionKey** attribute corresponds to a separate delivery queue.

For more information, see the "NextHopSolutionKey" section in the [Queues](queues-exchange-2013-help.md) topic.

Return to top

## Routing messages

When a message needs to be delivered to a remote delivery group, a routing path must be determined for the message. Exchange 2013 uses the following logic to select the routing path for a message. This logic is basically unchanged from Exchange 2010:

1.  Calculate the least-cost routing path by adding the cost of the IP site links that must be traversed to reach the destination. If the destination is a connector, the cost assigned to the address space is added to the cost to reach the selected connector. If multiple routing paths are possible, the routing path with the lowest aggregate cost is used.

2.  If more than one routing path has the same aggregate cost, the number of hops in each path is evaluated and the routing path with the least number of hops is used.

3.  If more than one routing path is still available, the name assigned to the Active Directory sites before the destination is considered. The routing path where the Active Directory site nearest the destination is lowest in alphanumeric order is used. If the site nearest the destination is the same for all routing paths being evaluated, an earlier site name is considered.

In Exchange 2010, each message recipient is always associated with only one Active Directory site, and there is only one least cost routing from the source Active Directory site to the destination Active Directory site. In Exchange 2013, a delivery group may span multiple Active Directory sites, and there may be multiple least-cost routing paths to those multiple Active Directory sites. Exchange 2013 designates a single Active Directory site in the destination delivery group as the *primary site*. The primary site is closest Active Directory site based on the routing logic described earlier. To successfully route messages between delivery groups, Exchange 2013 takes the following issues into consideration:

  - **The presence of one or more hub sites along the least-cost routing path**   If the least-cost routing path to the primary site contains any hub sites, the message must be routed through the hub sites. The closest hub site along the least-cost routing path is selected as a new delivery group of the type **AD site**, which includes all transport servers in the hub site. After the message traverses the hub site, routing of the message along the least-cost routing path continues. If the primary site happens to be a hub site, the primary site is still considered a hub site for the following reasons:
    
      - If the destination delivery group spans multiple Active Directory sites, the source server should only attempt to connect to the servers in the hub site.
    
      - The servers in the hub site that actually belong to the target delivery group are preferred.
    
    As in previous version of Exchange, any hub sites that aren't in the least-cost routing path to the primary site are ignored.

  - **The target Exchange server to select in the destination routing group**   When the destination delivery group spans multiple Active Directory sites, the routing path to specific servers within the delivery group may have different costs. Servers located in the closest Active Directory site are selected as the target servers for the delivery group based on the least-cost routing path, and the Active Directory site those servers are in is selected as the primary site.

  - **Fallback options when connection attempts to all servers in the destination routing group fail**   If the destination delivery group spans multiple Active Directory sites, the first fallback option is all other servers in the destination delivery group in other Active Directory sites that aren't selected as target servers. Server selection is made based on the cost of the routing path to those other Active Directory sites. If the destination delivery group has any servers in the local Active Directory site, there are no other fallback options because the message is already as close to the target routing destination as possible. If the destination delivery group has servers in remote Active Directory sites, the option is to try to connect to all other servers in the primary site. If that fails, a backoff path in the least-cost routing path to the primary site is used. Exchange 2013 tries to deliver the message as close to the destination as possible by backing off, hop by hop, along the least-cost routing path until a connection is made.

Return to top

## Routing messages between Active Directory sites

The way that Exchange 2013 routes messages between Active Directory sites is virtually the same as Exchange 2010. For more information, see [Route mail between Active Directory sites](route-mail-between-active-directory-sites-exchange-2013-help.md).

Return to top

## Routing in the Front End Transport service on Client Access servers

This acts as a stateless proxy for all inbound and (optionally) outbound external SMTP traffic for the Exchange 2013 organization. For outgoing messages, the Transport service uses Send connectors to communicate with the Front End Transport service on a Client Access server. Specifically, outgoing messages are proxied through the Front End Transport service when the *FrontEndProxyEnabled* parameter on an applicable Send connector is set to `$true`, or when the **Proxy through Client Access server** option is selected in the Send Connector properties in the Exchange admin center (EAC). Any Client Access server in the local Active Directory site will be selected. Note that the Front End Transport service doesn't have Send connectors.

For incoming messages, the Front End Transport service must quickly find a single, healthy Transport service on a Mailbox server to receive the message transmission, regardless of the number or type of recipients. Failure to do so results in the email service being perceived as unavailable by the external senders. Like the Transport service, the Front End Transport service loads routing tables based on information from Active Directory, and uses delivery groups to determine how to route messages. However, the routing tables used by the Front End Transport service have the following unique characteristics:

  - The Front End Transport service is never considered a member of a delivery group, even when the Mailbox server and the Client access server are installed on the same physical server. This forces the Front End Transport service to communicate with the Transport service only.

  - The routing tables don't contain any Send connector routes.

  - The routing tables contain a special list of Mailbox servers in the local Active Directory site for fast fail-over purposes.

Routing in the Front End Transport service resolves message recipients to mailbox databases. The list of Mailbox servers used by the Front End Transport service is based on the mailbox databases of the message recipients. Note that it's possible that none of the recipients have mailboxes, for example, if the recipient is a distribution group or a mail user. For each mailbox database, the Front End Transport service looks up the delivery group and the associated routing information. The delivery groups used by the Front End Transport service are:

  - Routable DAG

  - Mailbox delivery group

  - AD site

Depending on the number and type of recipients, the Front End Transport service performs one of the following actions:

  - For messages with a single mailbox recipient, select a Mailbox server in the target delivery group, and give preference to the Mailbox server based on the proximity of the Active Directory site. Routing the message to the recipient may involve routing the message through a hub site.

  - For messages with multiple mailbox recipients, use the first 20 recipients to select a Mailbox server in the closest delivery group, based on the proximity of the Active Directory site. Note that message bifurcation doesn't occur in Front-End Transport, so only one Mailbox server is ultimately selected, regardless of number of recipients in a message.

  - If the message has no mailbox recipients, select a random Mailbox server in the local Active Directory site.

Return to top

## Routing in the Mailbox Transport service on Mailbox servers

This consists of two separate services: the Mailbox Transport Submission service and Mailbox Transport Delivery service. For incoming messages, the Mailbox Transport Delivery service receives SMTP messages from the Transport service, and connects to the local mailbox database using RPC to deliver the message. For outgoing messages, the Mailbox Transport Submission service connects to the local mailbox database using RPC to retrieve messages, and submits the messages over SMTP to the Transport service. The Mailbox Transport service is stateless, and doesn't queue any messages locally.

Like the Transport service, the Mailbox Transport service loads routing tables based on information from Active Directory, and uses delivery groups to determine how to route messages. However, there are routing aspects that are unique to the Mailbox Transport service:

  - Because the Transport service and the Mailbox Transport service exist on the same Exchange 2013 Mailbox server, the Mailbox Transport service always belongs to the same delivery group as the Mailbox server. This delivery group is referred to as the *local delivery group*.

  - The Mailbox Transport Submission service doesn't automatically send messages to the Transport service on the local Mailbox server or on other Mailbox servers in its own local delivery group. The Mailbox Transport Submission service has access to the same routing topology information as the Transport service, so the Mailbox Transport submission service can send messages to the Transport service on Mailbox servers outside the delivery group. The Mailbox servers in the local delivery group are used as fallback options, and for delivery to non-mailbox recipients.

  - The Mailbox Transport service only communicates with the Transport service on Exchange 2013 Mailbox servers.

  - The Mailbox Transport service only communicates with mailbox databases on the local Exchange 2013 Mailbox server. The Mailbox Transport service never communicates with mailbox databases on other Mailbox servers.

When a user sends a message from their mailbox, the Mailbox Transport Submission service resolves the message recipients to mailbox databases. The list of Mailbox servers used by the Mailbox Transport Submission service is based on the mailbox databases of the message recipients. Note that it's possible that none of the recipients have mailboxes, for example, if the recipient is a distribution group or a mail user. For each mailbox database, the Mailbox Transport Submission service looks up the delivery group and the associated routing information. The delivery groups used by the Mailbox Transport Submission service are:

  - Routable DAG

  - Mailbox delivery group

  - AD site

Depending on the number and type of recipients, the Mailbox Transport Submission service performs one of the following actions:

  - For messages with a single mailbox recipient, select a Mailbox server in the target delivery group, and give preference to the Mailbox server based on the proximity of the Active Directory site. Routing the message to the recipient may involve routing the message through a hub site.

  - For messages with multiple mailbox recipients, use the first 20 recipients to select a Mailbox server in the closest delivery group, based on the proximity of the Active Directory site.

  - If the message has no mailbox recipients, select a Mailbox server in the local delivery group.

When the Mailbox Transport Delivery service receives a message from the Transport service, it accepts or rejects the message for delivery to a local mailbox database. The Mailbox Transport Delivery service can deliver the message if the recipient resides in an active copy of a local mailbox database. But, if the recipient doesn't reside in an active copy of a local mailbox database, the Mailbox Transport Delivery service can't deliver the message, and must provide a non-delivery response to the Transport service. For example, if the active copy of the mailbox database recently moved to another server, the Transport service might erroneously transmit a message to a Mailbox server that now holds an inactive copy of the mailbox database. The non-delivery responses that the Mailbox Transport Delivery service returns to the Transport service include:

  - Retry delivery

  - Generate an NDR

  - Reroute the message

Return to top

## Routing in the Transport service on Edge Transport servers

If you have an Edge Transport server installed in your perimeter network, the Transport service on the Edge Transport server provides SMTP relay and smart host services for all Internet-facing mail flow. Messages that come and go from the Internet are queued locally on the Edge Transport server. The queues correspond to external domains or Send connectors. For more information, see the "NextHopSolutionKey" section in the [Queues](queues-exchange-2013-help.md) topic.

Typically, when you install an Edge Transport server in your perimeter network, you subscribe the Edge Transport server to an Active Directory site. The Active Directory site contains the Mailbox servers that will relay messages to and from the Edge Transport server. The Edge Subscription process creates an Active Directory site membership affiliation for the Edge Transport server. The site affiliation enables the Mailbox servers in the Active Directory site to relay messages to the Edge Transport server for delivery to the Internet without having to configure explicit Send connectors.

In multi-site configurations, outbound mail from internal recipients to external recipients is first routed to the subscribed Active Directory site. The target Active Directory site is the delivery group. The routing destination is the intra-organization Send connector in the Transport service on any of the Mailbox servers in the subscribed Active Directory site. The *intra-organization Send connector* is special Send connector that exists in the Transport service on every Mailbox server. This Send connector is implicitly created, invisible, requires no management, and is used to relay messages between Exchange servers.

Outbound mail for external recipients is routed from the Mailbox server to the Edge Transport server. The Client Access server is not involved in routing mail to a subscribed Edge Transport server. Mail is transmitted from the intra-organization Send connector in the Transport service on the Mailbox server to a Receive connector in the Transport service on the Edge Transport server. On a subscribed Edge Transport server, the default Receive connector is configured to listen for connections from internal Mailbox servers in the subscribed Active Directory site and anonymous connections from the Internet. After the message is categorized by the Transport service on the Edge Transport server, the message is queued locally for delivery to the Internet by using the dedicated Send connector that's created during the Edge Subscription.

Inbound mail from external recipients arrives on the Edge Transport through the default Receive connector, and the messages are categorized and queued for delivery. The messages are relayed through the dedicated Send connector that's created by the Edge Subscription to send mail into the Exchange organization. Where the messages go next depends on how the internal Exchange servers are configured.

  - **Mailbox server and Client Access server installed on the same computer**   In this configuration, the Client Access server is used for inbound mail flow. Mail flows from the Send connector in the Transport service on the Edge Transport server to the default Receive connector in the Front End Transport service on the Client Access server, and then to the default Receive connector in the Transport service on the Mailbox server.

  - **Mailbox server and Client Access server installed on different computers**   In this configuration, the Client Access server is bypassed for inbound mail flow. Mail flows from the Send connector in the Transport service on the Edge Transport server to the default Receive connector in the Transport service on the Mailbox server.

If you have an Exchange 2007 or Exchange 2010 Edge Transport server installed in the perimeter network, inbound and outbound mail flow always occurs directly between the Edge Transport server and the Mailbox server. The Client Access server isn't used.

Return to top

