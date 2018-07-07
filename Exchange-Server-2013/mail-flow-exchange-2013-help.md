---
title: 'Mail flow: Exchange 2013 Help'
TOCTitle: Mail flow
ms:assetid: 14df5e1a-a5f7-4b0d-ba97-f53b76f0e7e0
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa996349(v=EXCHG.150)
ms:contentKeyID: 48384840
ms.date: 07/14/2016
mtps_version: v=EXCHG.150
---

# Mail flow

 

_**Applies to:** Exchange Server 2013_


In Microsoft Exchange Server 2013, mail flow occurs through the transport pipeline. The *transport pipeline* is a collection of services, connections, components, and queues that work together to route all messages to the categorizer in the Transport service on a Mailbox server inside the organization.

Looking for a list of all mail flow topics? See Mail flow documentation.

For information about how to configure mail flow in a new Exchange 2013 organization, see [Configure mail flow and client access](configure-mail-flow-and-client-access-exchange-2013-help.md).

**Contents**

The transport pipeline

The Transport service on a Mailbox server

Mail flow documentation

## The transport pipeline

The transport pipeline consists of the following services:

  - **Front End Transport service on Client Access servers**   This service acts as a stateless proxy for all inbound and (optionally) outbound external SMTP traffic for the Exchange 2013 organization. The Front End Transport service doesn't inspect message content, doesn't communicate with the Mailbox Transport service on Mailbox servers, and doesn't queue any messages locally.

  - **Transport service on Mailbox servers**   This service is virtually identical to the Hub Transport server role in previous versions of Exchange. The Transport service handles all SMTP mail flow for the organization, performs message categorization, and performs message content inspection. Unlike previous versions of Exchange, the Transport service never communicates directly with mailbox databases. That task is now handled by the Mailbox Transport service. The Transport service routes messages between the Mailbox Transport service, the Transport service, the Front End Transport service, and (depending on your configuration) the Transport service on Edge Transport servers. The Transport service on Mailbox servers is described in more detail later in this topic.

  - **Mailbox Transport service on Mailbox servers**   This service consists of two separate services: the Mailbox Transport Submission service and Mailbox Transport Delivery service. The Mailbox Transport Delivery service receives SMTP messages from the Transport service on the local Mailbox server or on other Mailbox servers, and connects to the local mailbox database using an Exchange remote procedure call (RPC) to deliver the message. The Mailbox Transport Submission service connects to the local mailbox database using RPC to retrieve messages, and submits the messages over SMTP to the Transport service on the local Mailbox server, or on other Mailbox servers. The Mailbox Transport Submission service has access to the same routing topology information as the Transport service. Like the Front End Transport service, the Mailbox Transport service also doesn't queue any messages locally.

  - **Transport service on Edge Transport servers**   This service is very similar to the Transport service on Mailbox servers. If you have an Edge Transport server installed in the perimeter network, all mail coming from the Internet or going to the Internet flows through the Transport service Edge Transport server. This service is described in more detail later in this topic.

The following figure shows the relationships among the components in the Exchange 2013 transport pipeline.

**Overview of the transport pipeline in Exchange 2013.**

![Transport pipeline overview diagram](images/Aa996349.6f548b64-6ac2-4e98-9098-69ad6cd9f569(EXCHG.150).gif "Transport pipeline overview diagram")

## Messages from external senders

Messages from outside the organization enter the transport pipeline through a Receive connector in the Front End Transport service on the Client Access server and are then routed to the Transport service on the Mailbox server.

If you have an Exchange 2013 Edge Transport server installed in the perimeter network, messages from outside the organization enter the transport pipeline through a Receive connector in the Transport service on the Edge Transport server. Where the messages go next depends on how your internal Exchange servers are configured.

  - **Mailbox server and Client Access server installed on the same computer**   In this configuration, the Client Access server is used for inbound mail flow. Mail flows from the Transport service on the Edge Transport server to the Front End Transport service on the Client Access server, and then to the Transport service on the Mailbox server.

  - **Mailbox server and Client Access server installed on different computers**   In this configuration, the Client Access server is bypassed for inbound mail flow. Mail flows from the Transport service on the Edge Transport server to the Transport service on the Mailbox server.


> [!NOTE]
> If you have an Exchange 2010 or Exchange 2007 Edge Transport server installed in your perimeter network, mail flow always occurs directly between the Edge Transport server and the Transport service on the Mailbox server. For more information, see <A href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">Use an Exchange 2010 or 2007 Edge Transport server in Exchange 2013</A>.



## Messages from internal senders

SMTP messages from inside the organization enter the transport pipeline through the Transport service on a Mailbox server in one of the following ways:

  - Through a Receive connector.

  - From the Pickup directory or the Replay directory.

  - From the Mailbox Transport service.

  - Through agent submission.

The message is routed based on the routing destination or delivery group. For more information, see [Mail routing](mail-routing-exchange-2013-help.md).

If the message has external recipients, the message is routed from the Transport service on the Mailbox server to the Internet, or from the Mailbox server to the Front End Transport service on a Client Access server and then to the Internet if the Send connector is configured to proxy outbound connections through the Client Access server. For more information, see [Create a Send connector for email sent to the Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md).

If you have an Edge Transport server installed in the perimeter network, messages that have external recipients are never routed through the Front End Transport service on a Client Access server. The message is routed from the Transport service on a Mailbox server to the Transport service on the Edge Transport server

## Transport service on Mailbox servers

Every message that's sent or received in an Exchange 2013 organization must be categorized in the Transport service on a Mailbox server before it can be routed and delivered. After a message has been categorized, it's put in a delivery queue for delivery to the destination mailbox database, the destination database availability group (DAG), Active Directory site, or Active Directory forest, or to the destination domain outside the organization.

The Transport service on a Mailbox server consists of the following components and processes:

  - **SMTP Receive**   When messages are received by the Transport service, message content inspection is performed, transport rules are applied, and anti-spam and anti-malware inspection is performed if they are enabled. The SMTP session has a series of events that work together in a specific order to validate the contents of a message before it's accepted. After a message has passed completely through SMTP Receive and isn't rejected by receive events, or by an anti-spam and anti-malware agent, it's put in the Submission queue.

  - **Submission**   Submission is the process of putting messages into the Submission queue. The categorizer picks up one message at a time for categorization. Submission happens in three ways:
    
      - From SMTP Receive through a Receive connector.
    
      - Through the Pickup directory or the Replay directory. These directories exist on Mailbox servers and Edge Transport servers. Correctly formatted message files that are copied into the Pickup directory or the Replay directory are put directly into the Submission queue.
    
      - Through a transport agent.

  - **Categorizer**   The categorizer picks up one message at a time from the Submission queue. The categorizer completes the following steps:
    
      - Recipient resolution, which includes top-level addressing, expansion, and bifurcation.
    
      - Routing resolution.
    
      - Content conversion.
    
    Additionally, mail flow rules that are defined by the organization are applied. After messages have been categorized, they're put into a delivery queue that's based on the destination of the message. Messages are queued by the destination mailbox database, DAG, Active Directory site, Active Directory forest or external domain.

  - **SMTP Send**   How messages are routed from the Transport service depends on the location of the message recipients relative to the Mailbox server where categorization occurred. The message could be routed to one of the following locations:
    
      - To the Mailbox Transport service on the same Mailbox server.
    
      - To the Mailbox Transport service on a different Mailbox server that's part of the same DAG.
    
      - To the Transport service on a Mailbox server in a different DAG, Active Directory site, or Active Directory forest.
    
      - For delivery to the Internet through a Send connector on the same Mailbox server, through the Transport service on a different Mailbox server, through the Front End Transport service on a Client Access server, or through the Transport service on an Edge Transport server in the perimeter network.

## Transport service on Edge Transport servers

The components of the Transport service on Edge Transport servers are identical to the components of the Transport service on Mailbox servers. However, what actually happens during each stage of processing on Edge Transport servers is different. The differences are described in the following list.

  - **SMTP Receive**   When an Edge Transport server is subscribed to an internal Active Directory site, the default Receive connector is automatically configured to accept mail from internal Mailbox servers and from the Internet. When Internet messages arrive at the Edge Transport server, anti-spam agents filter connections and message contents, and help identify the sender and the recipient while the message is being accepted into the organization. The anti-spam agents are installed and enabled by default. Additional attachment filtering and connection filtering features are available, but built-in malware filtering is not. Also, transport rules are controlled by the Edge Rule agent. Compared to the Transport Rule agent on Mailbox servers, only a small subset of transport rule conditions are available on Edge Transport servers. But, there are unique transport rule actions related to SMTP connections that are available only on Edge Transport servers.

  - **Submission**   On an Edge Transport server, messages typically enter the Submission queue through a Receive connector. However, the Pickup directory and the Replay directory are also available.

  - **Categorizer**   On an Edge Transport server, categorization is a short process in which the message is put directly into a delivery queue for delivery to internal or external recipients.

  - **SMTP Send**   When an Edge Transport server is subscribed to an internal Active Directory site, two Send connectors are automatically created and configured. One is responsible for sending outbound mail to Internet recipients; the other is responsible for sending inbound mail from the Internet to internal recipients. Inbound mail is sent to the Transport service on an available Mailbox server in the subscribed Active Directory site.

## Mail flow documentation

The following table contains links to topics that will help you learn about and manage mail flow in Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Topic</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-routing-exchange-2013-help.md">Mail routing</a></p></td>
<td><p>Mail routing describes how messages are transmitted between messaging servers.</p></td>
</tr>
<tr class="even">
<td><p><a href="connectors-exchange-2013-help.md">Connectors</a></p></td>
<td><p>Connectors define where and how messages are transmitted to and from Exchange servers.</p></td>
</tr>
<tr class="odd">
<td><p><a href="domains-exchange-2013-help.md">Domains</a></p></td>
<td><p>Accepted domains define the SMTP address spaces that are used in the Exchange organization. Remote domains configure message formatting and encoding settings for messages sent to external domains.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-agents-exchange-2013-help.md">Transport agents</a></p></td>
<td><p>Transport agents act on messages as they travel through the Exchange transport pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-high-availability-exchange-2013-help.md">Transport high availability</a></p></td>
<td><p>Transport high availability describes how Exchange 2013 keeps redundant copies of messages during transit and after delivery.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-logs-exchange-2013-help.md">Transport logs</a></p></td>
<td><p>Transport logs record what happens to messages as they flow through the transport pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-message-approval-exchange-2013-help.md">Manage message approval</a></p></td>
<td><p>Moderated transport requires approval for messages sent to specific recipients.</p></td>
</tr>
<tr class="even">
<td><p><a href="content-conversion-exchange-2013-help.md">Content conversion</a></p></td>
<td><p>Content conversion controls the Transport Neutral encoding format (TNEF) message conversion options for external recipients, and the MAPI conversion options for internal recipients.</p></td>
</tr>
<tr class="odd">
<td><p><a href="dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md">DSNs and NDRs in Exchange 2013</a></p></td>
<td><p>Delivery status notifications (DSNs) are the system messages that are sent to message senders, for example, non-delivery reports (NDRs).</p></td>
</tr>
<tr class="even">
<td><p><a href="track-messages-with-delivery-reports-exchange-2013-help.md">Track messages with delivery reports</a></p></td>
<td><p>Delivery Reports is a message tracking tool that you can use to search for delivery status on email messages sent to or from users in your organization's address book, with a certain subject. You can track delivery information about messages sent by or received from any specific mailbox in your organization.</p></td>
</tr>
<tr class="odd">
<td><p><a href="message-size-limits-exchange-2013-help.md">Message size limits</a></p></td>
<td><p>This topic describes the size and individual component limits that are imposed on messages.</p></td>
</tr>
<tr class="even">
<td><p><a href="queue-viewer-exchange-2013-help.md">Queue Viewer</a></p></td>
<td><p>You use the Queue Viewer in the Exchange Toolbox to view and act upon queues and message in queues.</p></td>
</tr>
<tr class="odd">
<td><p><a href="pickup-directory-and-replay-directory-exchange-2013-help.md">Pickup directory and Replay directory</a></p></td>
<td><p>The pickup and replay directories are used to insert message files into the transport pipeline.</p></td>
</tr>
<tr class="even">
<td><p><a href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">Use an Exchange 2010 or 2007 Edge Transport server in Exchange 2013</a></p></td>
<td><p>This topic describes the considerations for using an Edge Transport server from previous versions of Exchange in Exchange 2013.</p></td>
</tr>
</tbody>
</table>

