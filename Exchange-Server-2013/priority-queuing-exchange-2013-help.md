---
title: 'Priority queuing: Exchange 2013 Help'
TOCTitle: Priority queuing
ms:assetid: 6edbd826-fe55-435b-9c63-48e6365c3d09
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb691107(v=EXCHG.150)
ms:contentKeyID: 50646236
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Priority queuing

 

_**Applies to:** Exchange Server 2013_


*Priority queuing* is a feature of Microsoft Exchange Server 2013 that enables the sender-defined priority of a message to influence the processing of the message by the Transport service on the Mailbox server.

The message priority is assigned by the sender in Microsoft Outlook when the sender creates and sends the message. The sender can set any of the following message priority values in Outlook:

  - Low importance

  - Normal importance

  - High importance

The default priority for a message created in Outlook or Outlook Web App is Normal priority. The message priority is stored in the `X-Priority` header field in the message header.

Every message sent or received in an Exchange 2013 organization must be categorized by the Transport service on a Mailbox server before it can be routed and delivered. The categorizer in the Transport service on a Mailbox server picks up one message at a time from the Submission queue and performs recipient resolution, routing resolution, and content conversion on the message before putting the message in a delivery queue. For more information, see [Mail flow](mail-flow-exchange-2013-help.md).

Delivery queues are dynamically created based on the destination of a message. For more information, see [Queues](queues-exchange-2013-help.md).

All messages that have the same destination are put in the same delivery queue. Priority queuing affects the transmission of messages from a delivery queue to the destination messaging server. When priority queuing is enabled, High priority messages are transmitted to their destinations before Normal priority messages, and Normal priority messages are transmitted to their destinations before Low priority messages. The prioritized delivery of messages based on the message priority can help you define specific service level agreement (SLA) requirements for message delivery times.

## Options for configuring priority queuing

Support for priority queuing is controlled by keys in the `%ExchangeInstallPath%bin\EdgeTransport.exe.config` XML application configuration file. For instructions on how to configure priority queuing, see [Enable and configure priority queuing](enable-and-configure-priority-queuing-exchange-2013-help.md).

The following table explains each key in more detail.

### Priority queuing keys in the EdgeTransport.exe.config file

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Key</th>
<th>Default value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>PriorityQueuingEnabled</em></p></td>
<td><p><code>false</code></p></td>
<td><p>This key enables or disables priority queuing in the Transport service on the Mailbox server. Valid input for this key is <code>true</code> or <code>false</code>.</p>
<p>When this key is <code>false</code>, priority queuing is disabled, and all the priority queuing message limits that exist in the EdgeTransport.exe.config file are ignored.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxHighPriorityMessageSize</em></p></td>
<td><p><code>250KB</code></p></td>
<td><p>This key specifies the maximum allowed size of a High priority message. If a High priority message is larger than the value specified by this key, the message is automatically downgraded from High priority to Normal priority.</p>
<p>The value of this key should be significantly less than the value of the <em>MaxSendMessageSize</em> parameter on the <strong>Set-TransportConfig</strong> cmdlet. The default value of this parameter is <code>10 MB</code>. The difference in these two values helps ensure consistent and predictable delivery times for High priority messages.</p>
<p>When you enter a value, qualify the value with one of the following units:</p>
<ul>
<li><p>KB (kilobytes)</p></li>
<li><p>MB (megabytes)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>LowPriorityDelayNotificationTimeout</em></p>
<p><em>NormalPriorityDelayNotificationTimeout</em></p>
<p><em>HighPriorityDelayNotificationTimeout</em></p></td>
<td><p><strong>Low</strong>   <code>8:00:00</code> (8 hours)</p>
<p><strong>Normal</strong>   <code>4:00:00</code> (4 hours)</p>
<p><strong>High</strong>   <code>00:30:00</code> (30 minutes)</p></td>
<td><p>These keys specify the timeout interval for delay delivery status notification (DSN) messages based on the message priority.</p>
<p>After each message delivery failure, the Transport service generates a delay DSN message and queues it for delivery to the sender of the undeliverable message. This delay DSN message is sent only after a specified delay notification time-out interval, and only if the failed message wasn't successfully delivered during that time. This delay prevents the sending of unnecessary delay DSN messages that may be caused by temporary message transmission failures.</p>
<p>To specify a value, enter it as a time span: dd.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.</p></td>
</tr>
<tr class="even">
<td><p><em>LowPriorityMessageExpirationTimeout</em></p>
<p><em>NormalPriorityMessageExpirationTimeout</em></p>
<p><em>HighPriorityMessageExpirationTimeout</em></p></td>
<td><p><strong>Low</strong>   <code>2.00:00:00</code> (2 days)</p>
<p><strong>Normal</strong>   <code>2.00:00:00</code> (2 days)</p>
<p><strong>High</strong>   <code>8:00:00</code> (8 hours)</p></td>
<td><p>These keys specify the maximum length of time that the Transport service tries to deliver a failed message. If the message can't be successfully delivered before the expiration time-out interval has passed, a non-delivery report (NDR) that contains the original message or the message headers is delivered to the sender.</p>
<p>To specify a value, enter it as a time span: dd.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxPerDomainLowPriorityConnections</em></p>
<p><em>MaxPerDomainNormalPriorityConnections</em></p>
<p><em>MaxPerDomainHighPriorityConnections</em></p></td>
<td><p><strong>Low</strong>   2</p>
<p><strong>Normal</strong>   15</p>
<p><strong>High</strong>   3</p></td>
<td><p>These keys specify the maximum number of connections that the Transport service can have open to any single remote domain. The outgoing connections to remote domains occur by using the delivery queues and Send connectors that exist on the Mailbox server.</p>
<p>The sum these three keys should be less than or equal to the value of the <em>MaxPerDomainOutboundConnections</em> parameter on the <strong>Set-TransportService</strong> cmdlet. The default value of this parameter is <code>20</code>.</p></td>
</tr>
</tbody>
</table>


## How priority queuing affects other message limits on Mailbox servers

All messages that pass through the Transport service are subject to a variety of message retry, resubmit, and expiration limits. For more information, see [Message size limits](message-size-limits-exchange-2013-help.md).

Some message limits available in the **Set-TransportService** cmdlet have corresponding priority queuing message limits available in the EdgeTransport.exe.config application configuration file. The following table shows these corresponding message limits.

### Message limits in the Set-TransportService cmdlet that correspond to priority queuing message limits in the EdgeTransport.exe.config file

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Source</th>
<th>Parameter or key</th>
<th>Default value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code> (4 hours)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityDelayNotificationTimeout</em></p></td>
<td><p><code>4:00:00</code> (4 hours)</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MessageExpirationTimeOut</em></p></td>
<td><p><code>2.00:00:00</code> (2 days)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityMessageExpirationTimeout</em></p></td>
<td><p><code>2.00:00:00</code> (2 days)</p></td>
</tr>
</tbody>
</table>


When priority queuing is disabled, all the priority queuing message limits that exist in the EdgeTransport.exe.config configuration file are ignored. All the message limits on the **Set-TransportService** cmdlet apply to all messages that travel through the Transport service on the Mailbox server.

When priority queuing is enabled, the priority queuing message limits in the EdgeTransport.exe.config configuration file override the corresponding message limits in the **Set-TransportService** cmdlet. All other message limits in the **Set-TransportService** cmdlet still apply to Low priority, Normal priority, and High priority messages that travel through the Transport service on the Mailbox server.

## User Settings for Priority Queuing

The **Set-Mailbox** cmdlet has the *DowngradeHighPriorityMessagesEnabled* parameter. The default value is `$false`. When this parameter is set to `$true`, any High priority messages sent from the mailbox are automatically downgraded to Normal priority.

