---
title: 'Message filters: Exchange 2013 Help'
TOCTitle: Message filters
ms:assetid: 8e6187c1-76f0-49da-bc24-2ab57cfb3c2c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb123714(v=EXCHG.150)
ms:contentKeyID: 49286849
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Message filters

 

_**Applies to:** Exchange Server 2013_


Filtering generates different views of the messages in queues. By specifying filter criteria, you can quickly locate messages and take action on them. When an email message is sent to multiple recipients, the message may be located in multiple queues. When you filter by message properties, you can locate messages across all queues. The following scenarios are examples of how you might use message filtering to manage mail flow:

  - The Submission queue on the Mailbox server or Edge Transport server that receives email from the Internet has a high volume of messages that are queued for delivery. Many of the messages have the same subject. Therefore, you suspect that spam is being sent to your organization. You can create a filter to view all the messages that meet the subject criteria. If you determine that the messages are spam, you can select them all and delete them from the delivery queue without sending an NDR.

  - A user reports that mail flow is slow. You examine the queues and see that many messages that have random subjects appear to be coming from a single domain. You can create a filter to view all the queued messages from that domain. If you determine that the messages are spam, you can select them all and delete them from the queues without sending an NDR.

## Message properties as filters

You can use message properties to create a filter and locate messages that meet specified criteria. You can create filters in Queue Viewer, or by using the *Filter* parameter on the message management cmdlets. Note that the message management cmdlets support more filterable properties than the Queue Viewer. The following table lists the message properties by which you can filter and the values that are associated with those properties.

### Message properties to use when filtering messages

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Queue Viewer message property</th>
<th>Shell message property</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Date Received</strong></p></td>
<td><p><code>DateReceived</code></p></td>
<td><p>The date/time when the message was placed in the queue.</p></td>
</tr>
<tr class="even">
<td><p>n/a</p></td>
<td><p><code>DeferReason</code></p></td>
<td><p>This property identifies why the message was deferred. If the message wasn't deferred, this property has the value <code>None</code>. A deferred message is returned to the Submission queue because of transient errors that were encountered during recipient resolution. For more information about deferred messages, see <a href="recipient-resolution-exchange-2013-help.md">Recipient resolution</a>. The possible values are:</p>
<p><code>AD Transient Failure During Content Conversion</code></p>
<p><code>AD Transient Failure During Resolve</code></p>
<p><code>Agent</code></p>
<p><code>Ambiguous Recipient</code></p>
<p><code>Loop Detected</code></p>
<p><code>Marked As Retry Delivery If Rejected</code></p>
<p><code>Rerouted By Store Driver</code></p>
<p><code>Storage Transient Failure During Content Conversion</code></p>
<p><code>Transient Failure</code></p>
<p><code>Target Site Inbound Mail Disabled</code></p>
<p><code>Recipient Thread Limit Exceeded</code></p>
<p><code>Transient Attribution Failure</code></p>
<p><code>Transient Accepted Domains Load Failure</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Expiration Time</strong></p></td>
<td><p><code>ExpirationTime</code></p></td>
<td><p>This property contains the date/time when the message will expire and be deleted from the queue if the message can't be delivered.</p></td>
</tr>
<tr class="even">
<td><p><strong>From Address</strong></p></td>
<td><p><code>FromAddress</code></p></td>
<td><p>This property contains the SMTP address of the sender.</p></td>
</tr>
<tr class="odd">
<td><p>n/a</p></td>
<td><p><code>Identity</code></p></td>
<td><p>This property is the identity of the message in the form of <em>&lt;Server&gt;\&lt;Queue&gt;\&lt;MessageInteger&gt;</em>. For more information see the &quot;Message identity&quot; section in the <a href="queues-exchange-2013-help.md">Queues</a> topic.</p></td>
</tr>
<tr class="even">
<td><p><strong>Internet Message ID</strong></p></td>
<td><p><code>InternetMessageId</code></p></td>
<td><p>This property contains the value of the <code>Message-ID:</code> header field that's located in the message header. The value is expressed as an email address that contains a GUID and the FQDN the sending SMTP server. For example:</p>
<p><code>&lt;67D754D6103DC4FB3BA6BC7205DACABA61231@mailbox01.contoso.com&gt;</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Last Error</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>This property contains the text of the last error that was recorded for a message. For example, <code>A matching connector cannot be found to route the external recipient</code>.</p></td>
</tr>
<tr class="even">
<td><p>n/a</p></td>
<td><p><code>MessageLatency</code></p></td>
<td><p>This property contains the amount of time elapsed between when the message first entered the Submission queue on the server, and when the message was placed in the queue. The value uses the syntax <em>hh:mm:ss.ff</em>, where <em>hh</em> = hour, <em>mm</em> = minute, <em>ss</em> = second, and <em>ff</em> = fractions of a second.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Message Source Name</strong></p></td>
<td><p><code>MessageSourceName</code></p></td>
<td><p>This property contains a text string that indicates the name of the transport component that submitted the message to the queue. For example, if the message came in through a Receive connector, the value is: <code>SMTP:</code><em>&lt;ConnectorName&gt;</em>. If the message is a delivery status notification (DSN), the value is <code>DSN</code>.</p></td>
</tr>
<tr class="even">
<td><p>n/a</p></td>
<td><p><code>Priority</code></p></td>
<td><p>This property contains the priority of the message that's assigned by the user in Outlook or Outlook Web App. The possible values are <code>Low</code>, <code>Normal</code>, and <code>High</code>. For more information, see <a href="priority-queuing-exchange-2013-help.md">Priority queuing</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Queue ID</strong></p></td>
<td><p><code>Queue</code></p></td>
<td><p>This property is the identity of the queue that holds the message. The queue identity uses the syntax <em>&lt;Server&gt;\&lt;Queue&gt;</em>. For more information, see the &quot;Queue identity&quot; section in the <a href="queues-exchange-2013-help.md">Queues</a> topic.</p></td>
</tr>
<tr class="even">
<td><p>n/a</p></td>
<td><p><code>RetryCount</code></p></td>
<td><p>This property identifies the number of times that delivery of the message to the destination was tried, either automatically or manually.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SCL</strong></p></td>
<td><p><code>SCL</code></p></td>
<td><p>The value of the spam confidence level (SCL) property specifies the SCL of the message. Valid SCL entries are integers from 0 through 9. An empty SCL property value indicates that the message hasn't been processed by the Content Filter agent.</p>
<p>This property contains the spam confidence level (SCL) value of the message. Valid SCL entries are integers from 0 through 9 and -1. For more information, see <a href="spam-confidence-level-threshold-exchange-2013-help.md">Spam Confidence Level Threshold</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Size (KB)</strong></p></td>
<td><p><code>Size</code></p></td>
<td><p>This property indicates the size of the message.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Source IP</strong></p></td>
<td><p><code>SourceIP</code></p></td>
<td><p>This property contains the IP address of the server that submitted the message to the Exchange server that holds the message in the queue. The address could be the IP address of a remote SMTP server, or the IP address of the local Exchange server.</p></td>
</tr>
<tr class="even">
<td><p><strong>Status</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>This property indicates the current message status. A message can have one of the following status values:</p>
<p><code>Active</code></p>
<p><code>Locked</code></p>
<p><code>None</code></p>
<p><code>Pending Remove</code></p>
<p><code>Pending Suspend</code></p>
<p><code>Ready</code></p>
<p><code>Retry</code></p>
<p><code>Suspended</code></p>
<p>For more information, see the &quot;Message properties&quot; section in the <a href="queues-exchange-2013-help.md">Queues</a> topic.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Subject</strong></p></td>
<td><p><code>Subject</code></p></td>
<td><p>This property indicates the subject of a message that's found in the <code>Subject:</code> header field in the message header.</p></td>
</tr>
</tbody>
</table>

