---
title: 'Shadow redundancy: Exchange 2013 Help'
TOCTitle: Shadow redundancy
ms:assetid: a40dbe61-2a18-48a8-b2e0-4e81a6678d11
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd351027(v=EXCHG.150)
ms:contentKeyID: 49289359
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Shadow redundancy

 

_**Applies to:** Exchange Server 2013_


Shadow redundancy was introduced in Microsoft Exchange Server 2010 to provide redundant copies of messages before they're delivered to mailboxes. In Exchange 2010, shadow redundancy delayed deleting a message from the transport database on a transport server until the server verified the next hop in the message delivery path completed delivery. If the next hop failed before reporting successful delivery back to the transport server, the transport server resubmitted the message to that next hop. Exchange 2010 servers used the XSHADOW verb to advertise their shadow redundancy support. If an SMTP server didn't support shadow redundancy, Exchange 2010 used delayed acknowledgement based on a configured time interval on the Receive connector to make a redundant copy of the message.

The major improvement to shadow redundancy in Microsoft Exchange Server 2013 is that the transport server now makes a redundant copy of any messages it receives before it acknowledges successfully receiving the message back to the sending server. The sending server's support or lack of support for shadow redundancy doesn't matter. This helps to ensure that all messages in the Exchange 2013 transport pipeline are made redundant while they're in transit. If Exchange 2013 determines the original message was lost in transit, the redundant copy of the message is redelivered.

**Contents**

Shadow redundancy components

Requirements for shadow redundancy

Shadow redundancy is enabled by default

How shadow messages are created

SMTP timeouts

How shadow messages are maintained

Message processing after an outage

## Shadow redundancy components

The following table describes the components of shadow redundancy. These terms are used throughout the topic.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Term</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Transport server</p></td>
<td><p>An Exchange server that has message queues and is responsible for routing messages. In Exchange 2013, a transport server is a Mailbox server (the Transport service on the Mailbox server).</p></td>
</tr>
<tr class="even">
<td><p>Transport database</p></td>
<td><p>The message queue database on an Exchange 2013 transport server. Shadow queues and Safety Net are also stored in the transport database.</p></td>
</tr>
<tr class="odd">
<td><p>Transport high availability boundary</p></td>
<td><p>A database availability group (DAG) in DAG environments, or an Active Directory site in non-DAG environments. When a message arrives on a transport server in the transport high availability boundary, Exchange tries to maintain 2 redundant copies of the message on transport servers within the boundary. When a message leaves the transport high availability boundary, Exchange stops maintaining redundant copies of the message.</p></td>
</tr>
<tr class="even">
<td><p>Primary message</p></td>
<td><p>The message submitted into the transport pipeline for delivery.</p></td>
</tr>
<tr class="odd">
<td><p>Shadow message</p></td>
<td><p>The redundant copy of the message that the shadow server retains until it confirms the primary message was successfully processed by the primary server.</p></td>
</tr>
<tr class="even">
<td><p>Primary server</p></td>
<td><p>The transport server that's currently processing the primary message.</p></td>
</tr>
<tr class="odd">
<td><p>Shadow server</p></td>
<td><p>The transport server that holds the shadow message for the primary server. A transport server may be the primary server for some messages and the shadow server for other messages simultaneously.</p></td>
</tr>
<tr class="even">
<td><p>Shadow queue</p></td>
<td><p>The delivery queue where the shadow server stores shadow messages. For messages with multiple recipients, each next hop for the primary message requires separate shadow queues.</p></td>
</tr>
<tr class="odd">
<td><p>Discard status</p></td>
<td><p>The information a transport server maintains for shadow messages that indicate the primary message has been successfully processed.</p></td>
</tr>
<tr class="even">
<td><p>Discard notification</p></td>
<td><p>The response a shadow server receives from a primary server indicating a shadow message is ready to be discarded.</p></td>
</tr>
<tr class="odd">
<td><p>Safety Net</p></td>
<td><p>The Exchange 2013 improved version of the transport dumpster. Messages that are successfully processed or delivered to a mailbox recipient by the Transport service on a Mailbox server are moved into Safety Net. For more information, see <a href="safety-net-exchange-2013-help.md">Safety Net</a>.</p></td>
</tr>
<tr class="even">
<td><p>Shadow Redundancy Manager</p></td>
<td><p>The transport component that manages shadow redundancy.</p></td>
</tr>
<tr class="odd">
<td><p>Heartbeat</p></td>
<td><p>The process that allows primary servers and shadow servers to verify the availability of each other.</p></td>
</tr>
</tbody>
</table>


Return to top

## Requirements for shadow redundancy

Although it may seem obvious, shadow redundancy requires multiple Exchange 2013 Mailbox servers. The Mailbox server can be standalone servers, or Mailbox servers and Client Access servers installed on the same computer.

  - If the Mailbox server isn't a member of a DAG, the other Mailbox servers must be in the local Active Directory site.

  - If the Mailbox server is a member of a DAG, the other Mailbox servers must belong to the same DAG. The other Mailbox servers that belong to the DAG can be in the local Active Directory site or in a remote Active Directory site. If the DAG spans multiple Active Directory sites, shadow redundancy prefers creating a redundant copy of the message in a remote Active Directory site for site resiliency.

These are the situations where shadow redundancy can't protect messages in transit:

  - In single Exchange server environments.

  - In under-provisioned DAGs.

  - During the simultaneous failure of two or more transport servers involved in the shadow redundancy of a message.

Return to top

## Shadow redundancy is enabled by default

By default, shadow redundancy is enabled globally in the Transport service on all Mailbox servers by using the *ShadowRedundancyEnabled* parameter on the **Set-TransportConfig** cmdlet. By default, if the Transport service on a Mailbox server can't create a redundant copy of a message, the message is not rejected. However, you can configure Exchange 2013 to reject a message if a redundant copy of the message isn't created by using the *RejectMessageOnShadowFailure* parameter on the **Set-TransportConfig** cmdlet. The message is rejected with a transient failure, but the sending server can transmit the message again. The SMTP response code is `451 4.4.0 Message failed to be made redundant.` You should configure Exchange 2013 to reject messages that can't be made redundant only when your organization has multiple Exchange 2013 Mailbox servers available.

The following table describes the parameters that enable shadow redundancy.

### Parameters that enable shadow redundancy

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Default value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowRedundancyEnabled</em> on <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> enables shadow redundancy on all transport servers in the organization.</p></li>
<li><p><code>$false</code> disables shadow redundancy on all transport servers in the organization.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>RejectMessageOnShadowFailure</em> on <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$false</code></p></td>
<td><ul>
<li><p><code>$false</code>   When a shadow copy of the message can't be created, the primary message is accepted anyway by transport servers in the organization. Those messages aren't redundantly persisted while they're in transit.</p></li>
<li><p><code>$true</code>   No message is accepted or acknowledged by any transport server in the organization until a shadow copy of the message is successfully created. If a shadow copy of the message can't be created, the primary message is rejected with a transient error. All messages in the organization are redundantly persisted while they're in transit.</p>
<p>You should set this value to <code>$true</code> only if you have multiple Exchange 2013 Mailbox servers in a DAG or Active Directory site where a shadow copy of the message can be created.</p></li>
</ul>
<p>This parameter is only meaningful when <em>ShadowRedundancyEnabled</em> is <code>$true</code>.</p></td>
</tr>
</tbody>
</table>


Return to top

## How shadow messages are created

The main goal of shadow redundancy is to always have two copies of a message within a transport high availability boundary while the message is in transit. Where and when the redundant copy of the message is created depends on where the message came from and where the message is going. There are three major determining factors:

  - Messages received from outside a transport high availability boundary.

  - Messages sent outside a transport high availability boundary.

  - Messages received from the Mailbox Transport Submission service from a Mailbox server within the transport high availability boundary.

A *transport high availability boundary* is one of the following:

  - A DAG, for Mailbox servers that are members of a DAG. This includes a DAG that spans multiple Active Directory sites.

  - An Active Directory site, for Mailbox servers that don't belong to a DAG.

Shadow redundancy never tracks shadow messages across a transport high availability boundary. When a message crosses the transport high availability boundary, shadow redundancy begins or restarts. This reduces shadow message maintenance traffic and prevents shadow message resubmissions from occurring across the transport high availability boundary. Exchange 2010 Hub Transport servers are a special case, and are discussed later in this topic.

## Messages received from outside a transport high availability boundary

When the Transport service on an Exchange 2013 Mailbox server receives a message from outside the transport high availability boundary, the Mailbox server isn't concerned about the support or lack of support for shadow redundancy by the sending server. As long as shadow redundancy is enabled, the Mailbox server that receives the message makes a redundant copy of the message on another Mailbox server within the transport high availability boundary before acknowledging receipt of the message back to the sending server. Here's an example of how the process works:

![Shadow message creation](images/Dd351027.a97d383b-6ae4-458d-af3a-1ac0a41cd52b(EXCHG.150).gif "Shadow message creation")

1.  An SMTP server transmits a message to the Transport service on a Mailbox server. The Mailbox server is the primary server, and the message is the primary message.

2.  While the original SMTP session with the SMTP server is still active, the Transport service on primary server opens a new, simultaneous SMTP session with the Transport service on a different Mailbox server in the organization to create a redundant copy of the message.
    
      - If the primary server is a member of a DAG, the primary server connects to a different Mailbox server in the same DAG. If the DAG spans multiple Active Directory sites, a Mailbox server in a different Active Directory site is preferred by default. This setting is controlled by the *ShadowMessagePreference* parameter on the **Set-TransportService** cmdlet. The default value is `PreferRemote`, but you can change it to `RemoteOnly` or `LocalOnly`.
    
      - If the primary server isn't a member of a DAG, the primary server connects to a different Mailbox server in the same Active Directory Site, regardless of the value of the *ShadowMessagePreference* parameter.

3.  The primary server transmits a copy of the message to the Transport service on other Mailbox server, and Transport service on the other Mailbox server acknowledges that the copy of the message was created successfully. The copy of the message is the shadow message, and the Mailbox server that holds it is the shadow server for the primary server. The message exists in a shadow queue on the shadow server.

4.  After the primary server receives acknowledgement from the shadow server, the primary server acknowledges the receipt of the primary message to the original SMTP server in the original SMTP session, and the SMTP session is closed.

## Messages sent outside a transport high availability boundary

When an Exchange 2013 transport server transmits a message outside the transport high availability boundary, and the SMTP server on the other side acknowledges successful receipt of the message, the transport server moves the message into Safety Net. No resubmission of the message from Safety Net can occur after the primary message has been successfully transmitted across the transport high availability boundary. For more information about Safety Net, see [Safety Net](safety-net-exchange-2013-help.md).

## Messages transmitted within a transport high availability boundary

Message routing is optimized in Exchange 2013 so that when the ultimate destination is in a DAG or Active Directory site, multiple hops between the Transport service on Mailbox servers in that DAG or Active Directory site aren't typically required. Once the message is accepted by the Transport service on a Mailbox server in the DAG or Active Directory site that holds the ultimate destination for the message, the next hop for the message is typically the ultimate destination itself. Shadow redundancy's goal of keeping two copies of a message in transit is fulfilled when one shadow copy of the message exists anywhere within the DAG or Active Directory site. Typically, only failover scenarios in a DAG that require the **Redirect-Message** cmdlet to drain the active queues on a Mailbox server would require multiple hops within the same transport high availability boundary.

## Shadow redundancy with Exchange 2010 Hub Transport servers in the same Active Directory site

When an Exchange 2010 Hub Transport server transmits a message to an Exchange 2013 Mailbox server in the same Active Directory site, the Exchange 2010 Hub Transport server advertises support for shadow redundancy using the XSHADOW command, but the Mailbox server doesn't advertise support for shadow redundancy. This prevents the Exchange 2010 Hub Transport server from creating a shadow copy of the message on an Exchange 2013 Mailbox server.

When the Transport service on an Exchange 2013 Mailbox server transmits a message to an Exchange 2010 Hub Transport in the same Active Directory site, the Exchange 2013 Mailbox server shadows the message for the Exchange 2010 Hub Transport server. After the Exchange 2013 Mailbox server receives acknowledgement from the Exchange 2010 Hub Transport server that the message was successfully received, the Exchange 2013 Mailbox server moves the successfully processed message into Safety Net. However, the successfully processed messages stored in Safety Net by Exchange 2013 Mailbox are never resubmitted to the Exchange 2010 Hub Transport servers.

Return to top

## SMTP timeouts

During the attempt to make a redundant copy of the message, the SMTP connection between the sending SMTP server and the primary server, or the SMTP session between the primary server and the shadow server could timeout. Receive connectors and Send connectors both have a *ConnectionInactivityTimeOut* parameter for when data is actually being transmitted on the connector. Receive connectors also have an absolute *ConnectionTimeOut* parameter.

If any of the SMTP sessions time out before the shadow copy of the message is successfully created and acknowledged, the result is controlled by the *RejectMessageOnShadowFailure* parameter on the **Set-TransportConfig** cmdlet. By default, the value of this parameter is `$false`, which means the primary message is accepted without a shadow copy being created. If the value of this parameter is `$true` the primary message is rejected with the transient error `451 4.4.0`.

If the shadow copy of a message is successfully created, but the SMTP session between the sending SMTP server and the primary server times out, the primary server accepts and processes the primary message. The sending SMTP server will re-deliver the unacknowledged message, but duplicate message detection will prevent Exchange mailbox users from seeing the duplicate messages. When the sending SMTP server resubmits the message, the primary server will create another shadow copy of the message. There's no relationship between the shadow messages created during message resubmissions by the sending SMTP server.

The following table describes the parameters that control the creation of shadow messages

### Shadow message creation parameters

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Source</th>
<th>Default value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowMessagePreferenceSetting</em> on <strong>Set-TransportConfig</strong></p></td>
<td><p><code>PreferRemote</code></p></td>
<td><ul>
<li><p><code>PreferRemote</code>   Try to make a shadow copy of the message on a Mailbox server in a different Active Directory site. If the operation fails, try make a shadow copy of the message on a server in the local Active Directory site.</p></li>
<li><p><code>LocalOnly</code>   A shadow copy of the message should only be made on a transport server in the local Active Directory site.</p></li>
<li><p><code>RemoteOnly</code>: A shadow copy of the message should only be made on a transport server in a different Active Directory site.</p></li>
</ul>
<p>This parameter is only meaningful when the primary server that's trying to make a shadow copy of the message is a Mailbox server that's a member of a DAG that spans multiple Active Directory sites.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxRetriesForRemoteSiteShadow</em> on <strong>Set-TransportConfig</strong></p></td>
<td><p>4</p></td>
<td><p>This parameter is used when the Mailbox server is a member of a DAG that spans multiple Active Directory sites.</p>
<ul>
<li><p>If <em>ShadowMessagePreferenceSetting</em> is set to <code>PreferRemote</code>, first the Mailbox server tries to create a shadow copy of the message on another Mailbox server in a remote Active directory site up to the number of times specified by <em>MaxRetriesForRemoteSiteShadow</em>. If this fails, the Mailbox server tries to create a shadow copy of the message on a different Mailbox server in the local Active Directory site up to the number of times specified by <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
<li><p>If <em>ShadowMessagePreferenceSetting</em> is set to <code>RemoteOnly</code>, the Mailbox server only tries to create a shadow copy of the message on a Mailbox server in a remote Active Directory site up to the number of times specified by <em>MaxRetriesForRemoteSiteShadow</em>.</p></li>
<li><p>The</p></li>
</ul>
<p>When a shadow copy of the message can't be successfully created:</p>
<ul>
<li><p>If <em>RejectMessageOnShadowFailure</em> is <code>$true</code>, the primary message is rejected with a transient error.</p></li>
<li><p>If <em>RejectMessageOnShadowFailure</em> is <code>$false</code>, the primary message is accepted anyway, but isn't redundantly persisted.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>MaxRetriesForLocalSiteShadow</em> on <strong>Set-TransportConfig</strong></p></td>
<td><p>2</p></td>
<td><p>This parameter is used in the following circumstances:</p>
<ul>
<li><p>If the Mailbox server is a member of a DAG that spans multiple Active Directory sites.</p>
<ol>
<li><p>If <em>ShadowMessagePreferenceSetting</em> is set to <code>PreferRemote</code>, first the Mailbox server tries to create a shadow copy of the message on another Mailbox server in a remote Active directory site up to the number of times specified by <em>MaxRetriesForRemoteSiteShadow</em>. If this fails, the Mailbox server tries to create a shadow copy of the message on a different Mailbox server in the local Active Directory site up to the number of times specified by <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
<li><p>If <em>ShadowMessagePreferenceSetting</em> is set to <code>LocalOnly</code>, the Mailbox server only tries to create a shadow copy of the message on a different Mailbox server in the local Active Directory site up to the number of times specified by the <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
</ol></li>
<li><p>If the Mailbox server isn't a member of a DAG, or if the Mailbox server is a member of a DAG that's in one Active Directory site, the Mailbox server only tries to create a shadow copy of the message on a different Mailbox server in the local Active Directory site up to the number of times specified by <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
</ul>
<p>When a shadow copy of the message can't be successfully created:</p>
<ul>
<li><p>If <em>RejectMessageOnShadowFailure</em> is <code>$true</code>, the primary message is rejected with a transient error.</p></li>
<li><p>If <em>RejectMessageOnShadowFailure</em> is <code>$false</code>, the primary message is accepted anyway, but isn't redundantly persisted.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ConnectionInactivityTimeout</em> on <strong>Set-ReceiveConnector</strong></p></td>
<td><p>5 minutes in the Transport service on Mailbox servers</p>
<p>5 minutes in the Front End Transport service on Client Access servers.</p>
<p>1 minute on Edge Transport servers.</p></td>
<td><p>This parameter specifies the maximum time that an open SMTP connection with a source messaging server can remain idle before the connection is closed. The value of this parameter must be smaller than the value specified by the <em>ConnectionTimeout</em> parameter.</p></td>
</tr>
<tr class="odd">
<td><p><em>ConnectionTimeout</em> on <strong>Set-ReceiveConnector</strong></p></td>
<td><p>10 minutes in the Transport service on Mailbox servers</p>
<p>10 minutes in the Front End Transport service on Client Access servers.</p>
<p>5 minutes on Edge Transport servers.</p></td>
<td><p>This parameter specifies the maximum time that an SMTP connection with a source messaging server can remain open, even if the source messaging server is transmitting data. The value of this parameter must be larger than the value specified by the <em>ConnectionInactivityTimeout</em> parameter.</p></td>
</tr>
<tr class="even">
<td><p><em>ConnectionInactivityTimeOut</em> on <strong>Set-SendConnector</strong></p></td>
<td><p>10 minutes</p></td>
<td><p>This parameter specifies the maximum time that an open SMTP connection with a destination messaging server can remain idle before the connection is closed.</p></td>
</tr>
</tbody>
</table>


Return to top

## How shadow messages are maintained

After a shadow message is successfully created, the work of shadow redundancy has only just begun. The primary server and the shadow server need to stay in contact with each other to track the progress of the message.

When the primary server successfully transmits the message to the next hop, and the next hop acknowledges receipt of the message, the primary server updates the *discard status* of the message as delivery complete. The discard status is basically a message that contains of list of messages that are being monitored. A successfully delivered message doesn't need to be kept in a shadow queue, so once the shadow server knows the primary server has successfully transmitted the message to the next hop, the shadow server moves the shadow message from the shadow queue into Safety Net.

The shadow server determines the discard status of the shadow messages in its shadow queues by querying the primary server. If the shadow server opens an SMTP session with the primary server for any reason, including the transmission of other unrelated messages, the shadow server issues the **XQDISCARD** command to determine the discard status of the primary messages. If the shadow server hasn't opened an SMTP session with the primary server after a preconfigured time interval, the shadow server will open an SMTP session with the primary server and issue the **XQDISCARD** command. The time interval is controlled by the *ShadowHeartbeatFrequentcy* parameter on the **Set-TransportConfig** cmdlet. The default value is 2 minutes. After the shadow server opens an SMTP session with the primary server, the primary server responds with the *discard notifications* for messages that apply to the querying shadow server. In Exchange 2013, discard notifications are stored on disk, not in memory. Therefore, if the Microsoft Exchange Transport service restarts, the discard notifications are persisted. After the service starts, the primary server still knows about the messages it successfully processed, and that information is available to the shadow server.

The SMTP communication between the shadow server and the primary server is used as the *heartbeat* that determines the availability of the servers. If the shadow server can't open an SMTP session with the primary server after a preconfigured time interval, or if the transport database of the primary server has a different database ID, the shadow server promotes itself as the primary server, promotes the shadow messages as primary messages, and transmits the messages to the next hop. The time interval is controlled by the *ShadowResubmitTimeSpan* parameter on the **Set-TransportConfig** cmdlet. The default value is 3 hours.

*Shadow Redundancy Manager* is the core component of an Exchange 2013 transport server that's responsible for managing shadow redundancy. Shadow Redundancy Manager is responsible for maintaining the following information for all the primary messages that a server is currently processing:

  - The shadow server for each primary message being processed.

  - The discard status to be sent to shadow servers.

Shadow Redundancy Manager is responsible for the following for all the shadow messages that a shadow server has in its shadow queues:

  - Maintaining the list of primary servers for each shadow message.

  - Comparing the original database ID and the current database ID of the queue database where the primary copy of the message is stored.

  - Checking the availability of each primary server for which a shadow message is queued.

  - Processing discard notifications from primary servers.

  - Removing the shadow messages from the shadow queues after all expected discard notifications are received.

  - Deciding when the shadow server should take ownership of shadow messages, becoming a primary server.

  - Tracking message bifurcations and other side-effect messages like delivery status notifications (DSNs) and journal reports to verify the redundant copy of the message isn't released until all forks of the message are fully processed.

The following table describes the parameters that control how shadow messages are maintained.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Default value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowHeartbeatFrequency</em> on <strong>Set-TransportConfig</strong></p></td>
<td><p>2 minutes</p></td>
<td><p>The maximum amount of time a shadow server waits before opening an SMTP connection to the primary server to check the discard status of messages.</p></td>
</tr>
<tr class="even">
<td><p><em>ShadowResubmitTimeSpan</em> on <strong>Set-TransportConfig</strong></p></td>
<td><p>3 hours</p></td>
<td><p>How long a server waits before deciding that a primary server has failed and assumes ownership of shadow messages in the shadow queue for the primary server that's unreachable.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShadowMessageAutoDiscardInterval</em> on <strong>Set-TransportConfig</strong></p></td>
<td><p>2 days</p></td>
<td><p>How long a server retains discard events for successfully delivered messages. A primary server queues discard events until queried by the shadow server. However, if the shadow server doesn't query the primary server for the duration specified in this parameter, the primary server deletes the queued discard events.</p></td>
</tr>
<tr class="even">
<td><p><em>SafetyNetHoldTime</em> on <strong>Set-TransportConfig</strong></p></td>
<td><p>2 days</p></td>
<td><p>How long successfully processed messages are retained in Safety Net. Unacknowledged shadow messages eventually expire from Safety Net after the sum of <em>SafetyNetHoldTime</em> and <em>MessageExpirationTimeout</em> on <strong>Set-TransportService</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageExpirationTimeout</em> on <strong>Set-TransportService</strong></p></td>
<td><p>2 days</p></td>
<td><p>How long a message can remain in a queue before it expires.</p></td>
</tr>
</tbody>
</table>


Return to top

## Message processing after an outage

Shadow redundancy minimizes message loss due to server outages. When a transport server comes back online after an outage, there are two scenarios:

  - **The server comes back online with a new transport database**   In this scenario, the transport database is unrecoverable due to data corruption or hardware failure. In this case, because the transport server will have a new database ID, it will be recognized as a new route by the other transport servers in the organization. This also applies to the situation where a server couldn't be recovered, and a new server was provisioned as a replacement.

  - **The server comes back online with the same transport database**   In this scenario, the particular transport server didn't fail, but was offline long enough for the shadow server to assume ownership of the messages and resubmit them. For example, a network card failure, or a long maintenance on the server would cause this scenario.

The following table summarizes how shadow redundancy reacts to these two scenarios. For clarity, assume that the server that had an outage is named Mailbox01.

### Message processing in recovery scenarios

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recovery scenario</th>
<th>Actions taken</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mailbox01 comes back online with a new database.</p></td>
<td><p>When Mailbox01 becomes unavailable, each server that has shadow messages queued for Mailbox01 will assume ownership of those messages and resubmit them. The messages then get delivered to their destinations.</p>
<p>The maximum delay for messages is the value of the <em>ShadowHeartbeatFrequency</em> parameter on the <strong>Set-TransportConfig</strong> cmdlet. The default value is 2 minutes.</p></td>
</tr>
<tr class="even">
<td><p>Mailbox01 comes back online with the same database.</p></td>
<td><p>After Mailbox01 comes back online, it will deliver the messages in its queues, which have already been delivered by the servers that hold shadow copies of messages for Mailbox01. This will result in duplicate delivery of these messages. Exchange mailbox users won't see duplicate messages due to duplicate message detection. However, recipients on non-Exchange messaging systems may receive duplicate copies of messages.</p>
<p>The maximum delay for messages is the value of the <em>ShadowResubmitTimeSpan</em> parameter on the <strong>Set-TransportConfig</strong> cmdlet. The default value is 3 hours.</p></td>
</tr>
</tbody>
</table>


Return to top

