---
title: 'Queue filters: Exchange 2013 Help'
TOCTitle: Queue filters
ms:assetid: fbfbdcab-e0d2-4ed9-8f7f-e5fa2c87360d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb125237(v=EXCHG.150)
ms:contentKeyID: 49286856
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Queue filters

 

_**Applies to:** Exchange Server 2013_


Filtering generates different views of queues. You use the queue properties as filter options. By specifying filter criteria, you can quickly locate queues and take action on them. The following scenarios are examples of how you might use queue filtering to manage mail flow:

  - You receive a message from the Microsoft System Center Operations Manager that indicates that a queue length has exceeded the established threshold. You want to investigate whether a server-wide mail flow problem exists.
    
    You can create a filter to view all the queues that have a message count that exceeds what you consider typical. If a mail flow problem is indicated, you can select all the queues in the filter results and suspend the queues while you continue to investigate.

  - You suspend several queues to investigate the cause of mail flow problems. You determine that the problem was caused by an incorrect connector configuration and is now fixed.
    
    You can create a filter to view all the queues that have a status of Suspended, and then select all the queues in the filter results and resume the queues.

## Queue properties to use when filtering queues

You can use the queue properties to create a filter and locate queues that meet specified criteria. You can create filters in Queue Viewer, or by using the *Filter* parameter on the queue management cmdlets. Note that the queue management cmdlets support more filterable properties than the Queue Viewer. The following table lists the queue properties by which you can filter and the valid values for those properties.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Queue Viewer queue property</th>
<th>Shell queue property</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>n/a</p></td>
<td><p><code>DeferredMessageCount</code></p></td>
<td><p>This property identifies the number of messages that were returned to the Submission queue because of transient errors that were encountered during recipient resolution. For more information about deferred messages, see <a href="recipient-resolution-exchange-2013-help.md">Recipient resolution</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Delivery Type</strong></p></td>
<td><p><code>DeliveryType</code></p></td>
<td><p>The valid values for <strong>DeliveryType</strong> are explained in the &quot;NextHopSolutionKey&quot; section in the <a href="queues-exchange-2013-help.md">Queues</a> topic.</p></td>
</tr>
<tr class="odd">
<td><p>n/a</p></td>
<td><p><code>Identity</code></p></td>
<td><p>This property is the identity of the queue in the form of <em>&lt;Server&gt;\&lt;Queue&gt;</em>. For more information see the &quot;Queue identity&quot; section in the <a href="queues-exchange-2013-help.md">Queues</a> topic.</p></td>
</tr>
<tr class="even">
<td><p>n/a</p></td>
<td><p><code>IncomingRate</code></p></td>
<td><p>This property is a calculated number that indicates how quickly messages are entering the queue. For more information, see &quot;IncomingRate, OutgoingRate, and Velocity&quot; section in the <a href="queues-exchange-2013-help.md">Queues</a> topic.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Last Error</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>This property indicates the text string of the last error that was recorded for the queue.</p></td>
</tr>
<tr class="even">
<td><p><strong>Last Retry Time</strong></p></td>
<td><p><code>LastRetryTime</code></p></td>
<td><p>This property indicates the date/time of the last connection attempt for a queue that has a status of <code>Retry</code>.</p></td>
</tr>
<tr class="odd">
<td><p>n/a</p></td>
<td><p><code>LockedMessageCount</code></p></td>
<td><p>This property is reserved for internal Microsoft use, and isn't used in on-premises Exchange 2013 organizations.</p></td>
</tr>
<tr class="even">
<td><p><strong>Message Count</strong></p></td>
<td><p><code>MessageCount</code></p></td>
<td><p>This property indicates the number of messages in the queue.</p></td>
</tr>
<tr class="odd">
<td><p>n/a</p></td>
<td><p><code>NextHopCategory</code></p></td>
<td><p>This property designates the next hop of the queue as <code>Internal</code> or <code>External</code> and is based on the value of the <strong>DeliveryType</strong> property of the queue. For more information, see the &quot;NextHopSolutionKey&quot; section in the <a href="queues-exchange-2013-help.md">Queues</a> topic.</p></td>
</tr>
<tr class="even">
<td><p>n/a</p></td>
<td><p><code>NextHopConnector</code></p></td>
<td><p>This property is the GUID of the next hop and is based on the value of the <strong>DeliveryType</strong> property of the queue. For more information, see the &quot;NextHopSolutionKey&quot; section in the <a href="queues-exchange-2013-help.md">Queues</a> topic.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Next Hop Domain</strong></p></td>
<td><p><code>NextHopDomain</code></p></td>
<td><p>This property is the name of next hop and is based on the value of the <strong>DeliveryType</strong> property of the queue . For more information, see the &quot;NextHopSolutionKey&quot; section in the <a href="queues-exchange-2013-help.md">Queues</a> topic.</p></td>
</tr>
<tr class="even">
<td><p><strong>Next Retry Time</strong></p></td>
<td><p><code>NextRetryTime</code></p></td>
<td><p>This property indicates the date/time of the next connection attempt for a queue that has a status of <code>Retry</code>.</p></td>
</tr>
<tr class="odd">
<td><p>n/a</p></td>
<td><p><code>OutgoingRate</code></p></td>
<td><p>This property is a calculated number that indicates how quickly messages are leaving the queue. For more information, see &quot;IncomingRate, OutgoingRate, and Velocity&quot; section in the <a href="queues-exchange-2013-help.md">Queues</a> topic.</p></td>
</tr>
<tr class="even">
<td><p>n/a</p></td>
<td><p><code>RiskLevel</code></p></td>
<td><p>This property is reserved for internal Microsoft use, and isn't used in on-premises Exchange 2013 organizations.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Status</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>This property indicates the current queue status. A queue can have one of the following status values Active, Connecting, None, Suspended, Ready, or Retry. For more information, see the &quot;Queue status&quot; section in the <a href="queues-exchange-2013-help.md">Queues</a> topic.</p></td>
</tr>
<tr class="even">
<td><p>n/a</p></td>
<td><p><code>TlsDomain</code></p></td>
<td><p>This property contains the FQDN of the destination domain if the domain is configured for Domain Security.</p></td>
</tr>
<tr class="odd">
<td><p>n/a</p></td>
<td><p><code>Velocity</code></p></td>
<td><p>This property contains a calculated number that indicates how effectively the queue is draining. For more information, see &quot;IncomingRate, OutgoingRate, and Velocity&quot; section in the <a href="queues-exchange-2013-help.md">Queues</a> topic.</p></td>
</tr>
</tbody>
</table>

