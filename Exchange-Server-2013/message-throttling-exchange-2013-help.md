---
title: 'Message throttling: Exchange 2013 Help'
TOCTitle: Message throttling
ms:assetid: fba87902-2a79-42ac-b394-46a9016f667e
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb232205(v=EXCHG.150)
ms:contentKeyID: 49318513
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Message throttling

 

_**Applies to:** Exchange Server 2013_


*Message throttling* refers to a group of limits that are set on the number of messages and connections that can be processed by a Microsoft Exchange Server 2013 computer. These limits prevent the accidental or intentional exhaustion of system resources on the Exchange server.

**Contents**

Message throttling scope

Message cost and mail flow throttling

Message throttling on servers

Message throttling on Send connectors

Message throttling on Receive connectors

Message throttling policies

## Message throttling scope

Message throttling involves a variety of limits on message processing rates, SMTP connection rates, and SMTP session time-out values. These limits work together to protect an Exchange server from being overwhelmed by accepting and delivering messages. Although a large backlog of messages and connections may be waiting to be processed, the message throttling limits enable the Exchange server to process the messages and connections in an orderly manner.

In addition to message throttling, you can also put size limits on the individual components of messages, such as the number of recipients, the size of the message header, or the size of individual attachments. For more information about message size limits, see [Message size limits](message-size-limits-exchange-2013-help.md).

Another feature that helps avoid overwhelming the system resources of an Exchange transport server is *back pressure*. Back pressure is a system resource monitoring feature in the Transport service on Mailbox servers and on Edge Transport servers. When a monitored system resource, such as hard disk utilization or memory utilization, exceeds the specified threshold, the server reduces the rate at which it accepts new connections and messages, and focuses on delivering existing messages. When the utilization of the monitored system resources returns to normal levels, the server slowly increases the rate at which it accepts new connections and then establishes a normal level.

Return to top

## Message cost and mail flow throttling

To provide more consistent message throughput and predictable message delivery latency, Exchange 2013 establishes an accumulated cost for messages. This quality of service (QoS) feature was added in Microsoft Exchange Server 2010 SP1This cost is based on the following criteria:

  - Message size

  - Number of recipients

  - Frequency of transmission

Exchange 2013 transport servers track the average delivery cost of messages that are sent by individual users. By using message costs, Exchange 2013 provides a group of settings that can control the effect that a user or connection has on an Exchange organization. This group of settings is known as a *throttling policy*. When a user repeatedly sends costly messages, such as messages that have large attachments or messages that are sent to many recipients, the Exchange 2013-based transport servers use a throttling policy to assign a lower priority to higher-cost messages from the user while continuing to deliver lower-cost messages. This new behavior adds a “quality of service” aspect to the message throttling functionality in Exchange 2013.


> [!NOTE]
> Message throttling doesn’t affect the message priority from a user’s perspective. Messages still retain the original priority set by the user. For example, messages retain a setting of Important or Urgent, and so on.



To support this functionality, Exchange 2013 uses the following mechanisms:

  - **Internal prioritization agent**   This agent is triggered on the **OnResolvedMessage** event and assigns a lower priority to messages from the same sender that have a high accumulated cost. This cost is measured over a period of one minute and affects messages that have more than 500 recipients or that are larger than 1 megabyte (MB).

  - **Quota-based priority queuing for the MapiDelivery queue type**   This mechanism causes Exchange to deliver messages in a normal-priority queue more frequently than messages in a low-priority queue. By default, the normal-to-low message ratio is 20:1. However, new messages from a lower priority queue are never delivered sooner than new items from a higher priority queue. For example, consider the following scenario:
    
    1.  Twenty normal priority messages are delivered. By default, the next delivered message is a lower priority message.
    
    2.  Two new messages are received by the transport server: One message from a higher priority queue and one message from a lower priority queue.
    
    In this scenario, the message from the higher priority queue is delivered first. Then, the message from the lower priority queue is delivered.

  - **Throttle concurrent connections based on messaging database health**   This mechanism monitors the health of the Exchange messaging database (MDB) health and throttles concurrent connections to Exchange transport servers based on an assigned Health Measure value. The MDB is monitored by the Resource Health Monitor API in the Transport service on the Mailbox server and is assigned a health value from -1 through 100. This value is based on the RPC performance statistics that are included with each RPC response from the Store.exe process in the Mailbox Transport service. The Resource Health framework uses both the **Requests/Second** rate performance counter and the **Average RPC Latency** performance counter to calculate a health value for the database. To help maintain a consistent interactive user experience, Exchange reduces the number of concurrent connections as the health value decreases. The following health value ranges are available:
    
      - **-1:** This value indicates that the MDB health state is unknown. This value is assigned when the database starts. In this scenario, the database is considered healthy.
    
      - **0:** This value is assigned if the database is in an unhealthy state. In this state, the database should not be contacted.
    
      - **1 through 99:** These values represent a fair health state. A lower value represents a less healthy database.
    
      - **100:** This value represents a healthy database.

The Microsoft Exchange Throttling service provides the framework for mail flow throttling. The Microsoft Exchange Throttling service keeps track of mail flow throttling settings for a specific user and caches the throttling information in memory. Mail flow throttling settings are also known as a *budget*. Restarting the Microsoft Exchange Throttling service also resets mail flow throttling budgets.

You can use the throttling policy cmdlets that are available in Exchange 2013 to configure individual budget settings for a throttling policy. A budget is the amount of access that a user or application may have for a specific setting. A budget represents how many connections a user may have or how much activity a user may be permitted for each one-minute period. For example, a budget may be configured to set the amount of time that a user may spend using a specific feature in Exchange, such as ActiveSync, Outlook Web App, or Exchange Web Services. This threshold is stored in a throttling policy and defines the budget.

Time settings for a budget are set as a percentage of one minute. Therefore, a threshold of 100 percent represents 60 seconds. For example, assume that you want to specify Outlook Web App policy settings that limit the amount of time during which a user may run Outlook Web App code on a Client Access server and the amount of time the user may communicate with the Client Access server to 600 milliseconds over a one-minute period. To accomplish this, you need to set the value to 1 percent of one minute (600 milliseconds) for both of the following parameters:

  - **OWAPercentTimeInCAS:** 1

  - **OWAPercentTimeInMailboxRPC:** 1

A user who has this policy applied has a budget of OWAPercentTimeInCAS of 600 milliseconds and of OWAPercentageTimeInMailboxRPC of 600 milliseconds. In this scenario, when the user is logged into Outlook Web App, the user can run Client Access code for up to 600 milliseconds. After the 600 millisecond-period, the connection is considered over budget and the Exchange server doesn’t allow any further Outlook Web App action until one minute after the budget limit is reached. After the one-minute period, the user can run Outlook Web App client access code for another 600 milliseconds.

Return to top

## Message throttling on servers

You can set the message throttling options at the following locations:

  - In the transport service

  - On a Send connector

  - On a Receive connector

You can set all the message throttling options that are available in the Transport service on Mailbox servers, in the Mailbox Transport service on Mailbox servers, or in the Front End Transport service on Client Access servers using the Exchange Management Shell. You can also set some of the same options by configuring the transport server properties in the Exchange Administration Center (EAC).

The following table shows the message throttling options that are available on transport servers.

### Message throttling options on transport servers

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Source</th>
<th>Parameter</th>
<th>Default value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxDeliveries</em></p></td>
<td><p>20</p></td>
<td><p>This parameter specifies the maximum number of delivery threads that the transport service can have open at the same time to deliver messages to mailboxes. The valid input range for this parameter is from 1 through 256. We recommend that you don't modify the default value unless Microsoft Customer Service and Support advises you to do this.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxSubmissions</em></p></td>
<td><p>20</p></td>
<td><p>This parameter specifies the maximum number of submission threads that the transport service can have open at the same time to send messages from mailboxes. The valid input range for this parameter is from 1 through 256.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MaxConnectionRatePerMinute</em></p></td>
<td><p>1200</p></td>
<td><p>This parameter specifies the maximum rate that connections are allowed to be opened with the transport service. If many connections are attempted with the transport service at the same time, the <em>MaxConnectionRatePerMinute</em> parameter limits the rate that the connections are opened so that the server's resources aren't overwhelmed.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong> or</p>
<p>Transport server properties</p></td>
<td><p><em>MaxOutboundConnections</em></p></td>
<td><p>1000</p></td>
<td><p>This parameter specifies the maximum number of outbound connections that can be open at a time. If you enter a value of <code>unlimited</code>, no limit is imposed on the number of outbound connections. The value of this parameter must be greater than or equal to the value of the <em>MaxPerDomainOutboundConnections</em> parameter.</p>
<p>This value can also be configured using the EAC at <strong>Servers</strong> &gt; <strong>Servers</strong> &gt; <strong>Properties</strong> &gt; <strong>Transport limits</strong> &gt; <strong>Outbound connection restrictions</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong> or</p>
<p>Transport server properties</p></td>
<td><p><em>MaxPerDomainOutboundConnections</em></p></td>
<td><p>20</p></td>
<td><p>This parameter specifies the maximum number of concurrent connections to any single domain. If you enter a value of <code>unlimited</code>, no limit is imposed on the number of outbound connections per domain. The value of this parameter must be greater than or equal to the value of the <em>MaxOutboundConnections</em> parameter.</p>
<p>This value can also be configured using the EAC at <strong>Servers</strong> &gt; <strong>Servers</strong> &gt; <strong>Properties</strong> &gt; <strong>Transport limits</strong> &gt; <strong>Outbound connection restrictions</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>PickupDirectoryMaxMessagesPerMinute</em></p></td>
<td><p>100</p></td>
<td><p>This parameter specifies the maximum number of messages processed per minute by the Pickup directory and by the Replay directory. Each directory can independently process message files at the rate specified by this parameter.</p></td>
</tr>
</tbody>
</table>


Return to top

## Message throttling on Send connectors

The following table shows the message throttling option that's available on Send connectors. You need to use the Exchange Management Shell to configure this option.

### Message throttling option available on Send connectors

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Source</th>
<th>Parameter</th>
<th>Default value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-SendConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>10 minutes</p></td>
<td><p>This parameter specifies the maximum time that an open SMTP connection with a destination messaging server can remain idle before the connection is closed.</p></td>
</tr>
</tbody>
</table>


Return to top

## Message throttling on Receive connectors

The following table shows the message throttling options that are available on Receive connectors that are configured in the Transport service on a Mailbox server or on an Edge Transport server. You need to use the Exchange Management Shell to configure these options.

### Message throttling options available on Receive connectors

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Source</th>
<th>Parameter</th>
<th>Default value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>5 minutes in the Transport service on Mailbox servers</p>
<p>5 minutes in the Front End Transport service on Client Access servers.</p>
<p>1 minute on Edge Transport servers.</p></td>
<td><p>This parameter specifies the maximum time that an open SMTP connection with a source messaging server can remain idle before the connection is closed. The value of this parameter must be smaller than the value specified by the <em>ConnectionTimeout</em> parameter.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionTimeOut</em></p></td>
<td><p>10 minutes in the Transport service on Mailbox servers</p>
<p>10 minutes in the Front End Transport service on Client Access servers.</p>
<p>5 minutes on Edge Transport servers.</p></td>
<td><p>This parameter specifies the maximum time that an SMTP connection with a source messaging server can remain open, even if the source messaging server is transmitting data. The value of this parameter must be larger than the value specified by the <em>ConnectionInactivityTimeout</em> parameter.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnection</em></p></td>
<td><p>5000</p></td>
<td><p>This parameter specifies the maximum number of inbound SMTP connections that this Receive connector allows at the same time.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPercentagePerSource</em></p></td>
<td><p>100 percent on the Default Receive connector in the Transport service on a mailbox server</p>
<p>2 percent on the other Receive connectors in the Transport service on Mailbox servers, and in the Front End Transport service on Client Access servers.</p></td>
<td><p>This parameter specifies the maximum number of SMTP connections that a Receive connector allows at the same time from a single source messaging server. The value is expressed as the percentage of available remaining connections on a Receive connector. The maximum number of connections that are permitted by the Receive connector is defined by the <em>MaxInboundConnection</em> parameter.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPerSource</em></p></td>
<td><p>unlimited on the Default Receive connector in the Transport service on a mailbox server</p>
<p>20 on the other Receive connectors in the Transport service on Mailbox servers, and in the Front End Transport service on Client Access servers.</p></td>
<td><p>This parameter specifies the maximum number of SMTP connections that a Receive connector allows at the same time from a single source messaging server.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxProtocolErrors</em></p></td>
<td><p>5</p></td>
<td><p>This parameter specifies the maximum number of SMTP protocol errors that a Receive connector allows before the Receive connector closes the connection with the source messaging server.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>TarpitInterval</em></p></td>
<td><p>5 seconds</p></td>
<td><p>This parameter specifies the delay that's used in <em>tarpitting</em>. Tarpitting is the practice of artificially delaying SMTP responses for specific SMTP communication patterns that indicate a directory harvest attack or other unwelcome messages. A <em>directory harvest attack</em> is an attempt to collect valid e-mail addresses from a particular organization to use as a target for unsolicited commercial e-mail.</p>
<p>The delay that's specified by the <em>TarpitInterval</em> parameter only applies to anonymous connections.</p></td>
</tr>
</tbody>
</table>


Return to top

## Message throttling policies

In Exchange 2013, each mailbox has a *ThrottlingPolicy* setting. The default value for this setting is blank (`$null`). You can use the *ThrottlingPolicy* paramenter on the **Set-Mailbox** cmdlet to configure a throttling policy for a mailbox.

A default throttling policy exists to provide a default set budget configuration for users who connect to Exchange. To configure customized budget settings for one or more users, create a new throttling policy. Then, apply the policy to the appropriate user or group.


> [!IMPORTANT]
> We recommend that you don't modify the default throttling policy.



You can set all the message throttling options that are available on Mailbox servers in the Exchange Management Shell. The following cmdlets are available to manage throttling policies:

  - **Get-ThrottlingPolicy**

  - **Remove-ThrottlingPolicy**

  - **New-ThrottlingPolicy**

  - **Set-ThrottlingPolicy**

You can use the **New-ThrottlingPolicy** and **Set-ThrottlingPolicy** cmdlets to configure how much activity a user can perform against Exchange over a specific connection or time period. These settings make up a user’s budget. You can establish throttling policies to control access to the following Exchange features:

  - Exchange ActiveSync

  - Exchange Web Services

  - Outlook Web App

  - Unified Messaging

  - IMAP4

  - POP3

  - Outlook client connections (MAPI or RPC connections)

  - Mail flow settings

  - PowerShell commands

  - CPU usages

Return to top

