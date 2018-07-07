---
title: 'Message retry, resubmit, and expiration intervals: Exchange 2013 Help'
TOCTitle: Message retry, resubmit, and expiration intervals
ms:assetid: 03020e6f-4c01-4c6e-ae47-fd74d4c4f96a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ891103(v=EXCHG.150)
ms:contentKeyID: 50646229
ms.date: 07/14/2016
mtps_version: v=EXCHG.150
---

# Message retry, resubmit, and expiration intervals

 

_**Applies to:** Exchange Server 2013_


In Microsoft Exchange Server 2013, messages that can't be successfully delivered are subject to various retry, resubmit, and expiration deadlines based on the message's source and destination. *Retry* is a renewed connection attempt with the destination. *Resubmit* is the act of sending messages back to the Submission queue for the categorizer to reprocess. The message *expires* after all delivery efforts have failed over a specified period of time. After a message expires, the sender is notified of the delivery failure. Then the message is deleted from the queue.

In all three cases of retry, resubmit, or expire, you can manually intervene before the automatic actions are performed on the messages.

For instructions on how to configure these intervals, see [Configure message retry, resubmit, and expiration intervals](configure-message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md).

## Configuration options for message retry

When a transport server can't connect to the next hop, the queue is put in a status of Retry. Connection attempts continue until the queue expires or a connection is made.

## Configuration Options for Automatic Message Retry

The configuration options that are available for message retry intervals are described in the following table.

### Configuration options that are available for message retry intervals

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter or key name</th>
<th>Default value</th>
<th>Where to configure</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueGlitchRetryCount</em></p></td>
<td><p>4</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>This key specifies the number of connection attempts that are immediately tried when a transport server has trouble connecting with the destination server. Such connection problems are typically caused by very brief network outages.</p>
<p>Valid input for this key is an integer from 0 through 15.</p>
<p>Typically, you don't have to modify this key unless the network is unreliable and continues to experience many accidentally dropped connections.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueGlitchRetryInterval</em></p></td>
<td><p><code>00:01:00</code> or 1 minute</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>This key controls the connection interval between each connection attempt that's specified by the <em>QueueGlitchRetryCount</em> key.</p>
<p>Typically, you don't have to modify this parameter unless the network is unreliable and continues to experience many accidentally dropped connections.</p></td>
</tr>
<tr class="odd">
<td><p><em>TransientFailureRetryCount</em></p></td>
<td><p>6</p></td>
<td><p><strong>Set-TransportService</strong> cmdlet or server properties in the Exchange Administration Center (EAC)</p></td>
<td><p>This parameter specifies the number of connection attempts that are tried after the connection attempts that are controlled by the <em>QueueGlitchRetryCount</em> and <em>QueueGlitchRetryInterval</em> keys have failed. Connection problems that exhaust the <em>QueueGlitchRetryCount</em> and <em>QueueGlitchRetryInterval</em> keys can be caused by server restarts or cached DNS lookup failures.</p>
<p>Valid input for this parameter is an integer from 0 through 15. If you set this parameter to 0, the next connection attempt is controlled by the <em>OutboundConnectionFailureRetryInterval</em> parameter.</p></td>
</tr>
<tr class="even">
<td><p><em>TransientFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Transport service on Mailbox servers: <code>00:05:00</code> or 5 minutes</p></li>
<li><p>Edge Transport servers: <code>00:01:00</code> or 10 minutes</p></li>
</ul></td>
<td><p><strong>Set-TransportService</strong>cmdlet or server properties in the EAC</p></td>
<td><p>This parameter controls the connection interval between each connection attempt that's specified by the <em>TransientFailureRetryCount</em> parameter.</p>
<p>To specify a value, enter it as a time span: dd.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundConnectionFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Transport service on Mailbox servers: <code>00:10:00</code> or 10 minutes</p></li>
<li><p>Edge Transport Servers: <code>00:30:00</code> or 30 minutes</p></li>
</ul></td>
<td><p><strong>Set-TransportService</strong> cmdlet or server properties in the EAC</p></td>
<td><p>This parameter specifies the retry interval for outbound connection attempts that have previously failed. The previously failed connection attempts are controlled by the <em>TransientFailureRetryCount</em> and <em>TransientFailureRetryInterval</em> parameters.</p>
<p>To specify a value, enter it as a time span: dd.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.</p></td>
</tr>
<tr class="even">
<td><p><em>MessageRetryInterval</em></p></td>
<td><p><code>00:15:00</code> or15 minutes</p></td>
<td><p><strong>Set-TransportService</strong> cmdlet</p></td>
<td><p>This parameter specifies the retry interval for individual messages that have a status of Retry. We recommend that you don't modify the default value unless Microsoft Customer Service and Support advises you to do this.</p></td>
</tr>
<tr class="odd">
<td><p><em>MailboxDeliveryQueueRetryInterval</em></p></td>
<td><p><code>00:05:00</code> or 5 minutes</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>This key specifies how frequently the queues try to connect to the Mailbox Transport Delivery service for a destination mailbox database that can't be successfully reached.</p>
<p>To specify a value, enter it as a time span: dd.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.</p>
<p>Valid input for this key is from 00:00:01 through 1.00:00:00.</p></td>
</tr>
</tbody>
</table>


Return to top

## Configuration options for manual message retry

When a delivery queue is in the status of Retry, you can manually force an immediate connection attempt by using Queue Viewer in the Exchange toolbox or the **Retry-Queue** cmdlet in the Shell. The manual retry attempt overrides the next scheduled retry time. If the connection isn't successful, the retry interval timer is reset. The delivery queue must be in a status of Retry for this action to have any effect.

For more information, see the "Retry queues" section in [Manage queues](manage-queues-exchange-2013-help.md).

Return to top

## Configuration options for delay DSN messages

After each message delivery failure, the Edge Transport server or the Transport service on the Mailbox server generates a delay delivery status notification (DSN) message and queues it for delivery to the sender of the undeliverable message. This delay DSN message is sent only after a specified delay notification timeout interval, and only if the failed message wasn't successfully delivered during that time. By default, the delay notification timeout interval is 4 hours. This delay prevents the sending of unnecessary delay DSN messages that may be caused by temporary message transmission failures. The sending of delay DSN notification messages can be selectively enabled or disabled for messages that originate inside or outside the Exchange organization.

The configuration options that are available for delay DSN notification messages are described in the following table.

### Configuration options that are available for delay DSN notification messages

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter name</th>
<th>Default value</th>
<th>Location</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code>4 hours</p></td>
<td><p><strong>Set-TransportService</strong> or server properties in the EAC</p></td>
<td><p>This parameter specifies how long the server waits before it sends a delay DSN message to the sender. The value of this parameter should always be greater than the value of the <em>TransientFailureRetryCount</em> parameter multiplied by the value of the <em>TransientFailureRetryInterval</em> parameter.</p>
<p>To specify a value, enter it as a time span: dd.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>This parameter specifies whether delay DSN messages can be sent to message senders who are outside the Exchange organization.</p>
<p>Valid input for this parameter is <code>$true</code> or <code>$false</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>This parameter specifies whether delay DSN messages can be sent to message senders who are inside the Exchange organization.</p>
<p>Valid input for this parameter is <code>$true</code> or <code>$false</code>.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> On Exchange 2007 Hub Transport servers, all <EM>ExternalDSN*</EM> and <EM>InternalDSN*</EM> parameters are available on the <STRONG>Set-TransportServer</STRONG> cmdlet, not the <STRONG>Set-TransportConfig</STRONG> cmdlet. If you have any Exchange 2007 Hub Transport servers in your organization, you need to make changes to these values using the <STRONG>Set-TransportServer</STRONG> cmdlet on each Exchange 2007 Hub Transport server.



Return to top

## Configuration options for message resubmission

Message resubmission sends undelivered messages back to the Submission queue to be reprocessed by the categorizer.

## Automatic message resubmission

Undelivered messages are automatically resubmitted if the delivery queue is in the status of Retry and has been unable to successfully deliver any messages for a specified period of time. That period of time is controlled by the *MaxIdleTimeBeforeResubmit* key in the EdgeTransport.exe.config application configuration file. Only messages in delivery queues are candidates for automatic resubmission.

To specify a value, enter it as a time span: dd.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.

The default value is `12:00:00` or 12 hours.

## Manual Message Resubmission

You can manually resubmit messages that have the following status in the Transport service on a Mailbox server or an Edge Transport server:

  - Delivery queues that have the status of Retry. The messages in the queues must not be in the Suspended state.

  - Messages that are in the Unreachable queue and aren't in the Suspended state.

  - Messages that are in the poison message queue.

For more information about the poison message queue and the Unreachable queue, see "About the Poison Message Queue and the Unreachable Queue" in the topic [Queues](queues-exchange-2013-help.md).

If you want to manually resubmit messages that are located in delivery queues or the Unreachable queue without waiting for the time that's specified by the *MaxIdleTimeBeforeResubmit* parameter to pass, you need to use the **Retry-Queue** cmdlet with the *Resubmit* parameter. To manually resubmit messages that are located in the poison message queue, you can use Queue Viewer or the **Resume-Message** cmdlet to resume the message. For more information, see the "Resubmit messages in queues" section in [Manage queues](manage-queues-exchange-2013-help.md).

Another way that you can manually resubmit messages is to suspend the messages, export the messages to text files that have the .eml file name extension, and then copy the .eml files to the Replay directory on any Mailbox server or Edge Transport server. This resubmission method works for messages that are located in delivery queues or the Unreachable queue. Messages that are located in the poison message queue are already in the Suspended state. Messages that are located in the Submission queue can't be suspended or exported.


> [!NOTE]
> When you export messages from a queue, you don't remove the messages from the queue. After you export the messages and successfully resubmit them by using the Replay directory, you should remove the suspended messages to avoid duplicate message delivery.



For more information, see [Export messages from queues](export-messages-from-queues-exchange-2013-help.md).

Return to top

## Configuration options for message expiration

The *message expiration timeout interval* specifies the maximum length of time that an Edge Transport server or the Transport service on a Mailbox server tries to deliver a failed message. If the message can't be successfully delivered before the expiration timeout interval has passed, an NDR that contains the original message or the message headers is delivered to the sender.

## Automatic message expiration

The message expiration timeout interval is controlled by the *MessageExpirationTimeOut* parameter in the **Set-TransportService** cmdlet or in the server properties in the EAC.

To specify a value, enter it as a time span: dd.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.

The default value is `2.00:00:00` or 2 days. The valid input range for this parameter is from `00:00:05` through `90.00:00:00`.

## Manual Message Expiration

Although you can't manually force messages to expire, you can manually remove messages from any queue, except the Submission queue, with or without an NDR.

For more information, see the "Remove messages from queues" section in [Manage messages in queues](manage-messages-in-queues-exchange-2013-help.md).

Return to top

