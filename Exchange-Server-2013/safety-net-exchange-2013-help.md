---
title: 'Safety Net: Exchange 2013 Help'
TOCTitle: Safety Net
ms:assetid: d0abb807-3b12-4c7d-bc7e-769b87c84ccb
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ657495(v=EXCHG.150)
ms:contentKeyID: 49289415
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Safety Net

 

_**Applies to:** Exchange Server 2013_


In Microsoft Exchange Server 2013, the primary mechanism of mailbox high availability is the database availability group (DAG). For more information about DAGs, see [Managing database availability groups](managing-database-availability-groups-exchange-2013-help.md). The *transport dumpster* was first introduced in Exchange 2007, and was further improved in Exchange 2010 to provide redundant copies of messages after they're successfully delivered to mailboxes in DAGs. In Exchange 2010, the transport dumpster helped protect against data loss by maintaining a queue of successfully delivered messages that hadn't replicated to the passive mailbox database copies in the DAG. When a mailbox database or server failure required the promotion of an out-of-date copy of the mailbox database, the messages in the transport dumpster were automatically resubmitted to the new active copy of the mailbox database.

The transport dumpster has been improved in Exchange 2013 and is now called *Safety Net*.

Here's how Safety Net is similar to the transport dumpster in Exchange 2010:

  - Safety Net is a queue that's associated with the Transport service on a Mailbox server. This queue stores copies of messages that were successfully processed by the server.

  - You can specify how long Safety Net stores copies of the successfully processed messages before they expire and are automatically deleted. The default is 2 days.

Here's how Safety Net is different in Exchange 2013:

  - Safety Net doesn't require DAGs. For Mailbox servers that don't belong to a DAGs, Safety Net stores copies of the delivered messages on other Mailbox servers in the local Active Directory site.

  - Safety Net itself is now redundant, and is no longer a single point of failure. This introduces the concept of the *Primary Safety Net* and the *Shadow Safety Net*. If the Primary Safety Net is unavailable for more than 12 hours, resubmit requests become shadow resubmit requests, and messages are re-delivered from the Shadow Safety Net.

  - Safety Net takes over some responsibility from shadow redundancy in DAG environments. Shadow redundancy doesn't need to keep another copy of the delivered message in a shadow queue while it waits for the delivered message to replicate to the passive copies of mailbox database on the other Mailbox servers in the DAG. The copy of the delivered message is already stored in Safety Net, so the message can be resubmitted from Safety Net if necessary.

  - In Exchange 2013, transport high availability is more than just a best effort for message redundancy. Exchange 2013 attempts to guarantee message redundancy. Because of this, you can't specify a maximum size limit for Safety Net. You can only specify how long Safety Net stores messages before they're automatically deleted.

**Contents**

How Safety Net works

Message resubmission from Safety Net

Message resubmission from Shadow Safety Net

## How Safety Net works

Shadow redundancy keeps a redundant copy of the message while the message is in transit. Safety Net keeps a redundant copy of a message after the message is successfully processed. So, Safety Net begins where shadow redundancy ends. The same concepts about shadow redundancy, including the transport high availability boundary, primary messages, primary servers, shadow messages and shadow servers also apply to Safety Net. For more information, see [Shadow redundancy](shadow-redundancy-exchange-2013-help.md).

The Primary Safety Net exists on the Mailbox server that held the primary message before the message was successfully processed by the Transport service. This could mean the message was delivered to the Mailbox Transport service on the destination Mailbox server. Or, the message could have been relayed through the Mailbox server in an Active Directory site that's designated as a hub site on the way to the destination DAG or Active Directory site. After the primary server processes the primary message, the message is moved from the active queue into the Primary Safety Net on the same server.

The Shadow Safety Net exists on the Mailbox server that held the shadow message. After the shadow server determines the primary server has successfully processed the primary message, the shadow server moves the shadow message from the shadow queue into the Shadow Safety Net on the same server. Although it may seem obvious, the existence of the Shadow Safety Net requires shadow redundancy to be enabled, and shadow redundancy is enabled by default in Exchange 2013.

The parameters used by Safety Net are described in the following table.


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
<td><p><em>SafetyNetHoldTime</em> on <strong>Set-TransportConfig</strong></p></td>
<td><p>2 days</p></td>
<td><p>The length of time successfully processed primary messages are stored in Primary Safety Net, and acknowledged shadow messages are stored in Shadow Safety Net.</p>
<p>You can also specify this value in the Exchange Administration Center (EAC) at <strong>Mail flow</strong> &gt; <strong>Receive connectors</strong> &gt; <strong>More options</strong> <img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="More Options Icon" alt="More Options Icon" /> &gt; <strong>Organization transport settings</strong> &gt; <strong>Safety Net</strong> &gt; <strong>Safety Net hold time</strong>.</p>
<p>Unacknowledged shadow messages eventually expire from Shadow Safety Net after the sum of <em>SafetyNetHoldTime</em> and <em>MessageExpirationTimeout</em> on <strong>Set-TransportService</strong>.</p>
<p>To avoid data loss during Safety Net resubmits, the value of <em>SafetyNetHoldTime</em> must be greater than or equal to the value of <em>ReplayLagTime</em> on <strong>Set-MailboxDatabaseCopy</strong> for the lagged copy of the mailbox database.</p></td>
</tr>
<tr class="even">
<td><p><em>ReplayLagTime</em> on <strong>Set-MailboxDatabaseCopy</strong></p></td>
<td><p>Not configured</p></td>
<td><p>The amount of time that the Microsoft Exchange Replication service should wait before replaying log files that have been copied to the passive database copy. Setting this parameter to a value greater than 0 creates a lagged copy of the mailbox database. The maximum value is 14 days.</p>
<p>To avoid data loss during Safety Net resubmits, the value of <em>ReplayLagTime</em> must be less than or equal to the value of <em>SafetyNetHoldTime</em> on <strong>Set-TransportConfig</strong> for the lagged copy of the mailbox database.</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageExpirationTimeout</em> on <strong>Set-TransportService</strong></p></td>
<td><p>2 days</p></td>
<td><p>How long a message can remain in a queue before it expires.</p></td>
</tr>
<tr class="even">
<td><p><em>ShadowRedundancyEnabled</em> on <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> enables shadow redundancy on all transport servers in the organization.</p></li>
<li><p><code>$false</code> disables shadow redundancy on all transport servers in the organization.</p></li>
</ul>
<p>A redundant Safety Net requires shadow redundancy to be enabled.</p></td>
</tr>
</tbody>
</table>


Return to top

## Message resubmission from Safety Net

Message resubmissions from Safety Net are initiated by the Active Manager component of the Microsoft Exchange Replication service that manages DAGs and mailbox database copies. No manual actions are required to resubmit messages from Safety Net. For more information about Active Manager, see [Active Manager](active-manager-exchange-2013-help.md).

There are two basic Safety Net message resubmission scenarios:

  - After the automatic or manual failover of a mailbox database in a DAG.

  - After you active a lagged copy of a mailbox database.

A *lagged mailbox database copy* or *lagged copy* is a passive copy of a mailbox database where updates to the database are intentionally delayed to protect against logical corruption of the mailbox database. For more information, see [Managing mailbox database copies](managing-mailbox-database-copies-exchange-2013-help.md).

The only significant difference between the two scenarios is how far back in time to go to resubmit messages from Safety Net. Typically, for failover in a DAG, the new active copy of the mailbox database is typically several minutes to several hours behind the old active copy. A lagged copy of a mailbox database is typically several days behind the old active copy.

The main requirement for successful resubmission from Safety Net for a lagged copy is the amount of time messages are stored in Safety Net must be greater than or equal to the lag time of lagged copy of the mailbox database. In other words, the value of *SafetyNetHoldTime* on **Set-TransportConfig** must be greater than or equal to the value of the *ReplayLagTime* on **Set-MailboxDatabaseCopy** for the lagged copy.

Return to top

## Message resubmission from Shadow Safety Net

Like message resubmission from Primary Safety Net, message resubmissions from Shadow Safety Net are fully automated, and require no manual intervention.

When the Active Manager requests message resubmission from Safety Net over a specific time period, the request goes to the Transport service on the Mailbox servers where Primary Safety Net is holding the message copies for the required time period. In large Exchange organizations, it's likely that the required messages exist in Safety Net on multiple Mailbox servers, particularly if the required time period is large.

Without optimization, resubmitting messages from Safety Net would result in potentially large numbers of duplicate deliveries. Duplicate deliveries within the Exchange organization aren't a problem, because duplicate message detection prevents mailbox users from seeing duplicate copies of a message. But duplicate message delivery to recipients outside the Exchange organization will result in duplicate copies of messages. Fortunately, the resubmission of messages from Safety Net has been optimized in Exchange 2013 to reduce duplicate message delivery.

If the Primary Safety Net is initially unresponsive, or becomes unresponsive during message resubmission, Active Manager continues to attempt to contact it for 12 hours before giving up. After 12 hours, a broadcast is sent to the Transport service on all the Mailbox servers in the transport high availability bound requesting resubmission of message from Safety Net for the required time interval for the required mailbox database. When a Shadow Safety Net responds, it resubmits the messages for the required mailbox database during the required time interval only.

There are some important considerations for the shadow messages stored in Shadow Safety Net:

  - Shadow Safety Net doesn't know where the primary server transmitted the primary message.

  - The shadow messages in Shadow Safety Net only contain original message envelope recipients, not the actual recipients where the primary message was delivered. For example, the message envelope recipient may be a distribution group that requires expansion.

  - The messages in Shadow Safety net don't have any of the message updates that occurred after the primary server processed the message. For example, message encoding or content conversion.

Shadow message resubmitted from Shadow Safety Net require full categorization and processing through the Transport service on the Mailbox server. Resubmission of large numbers of shadow messages from Shadow Safety Net can be expensive in terms of Mailbox server resources. Fortunately, resubmission of shadow messages from Shadow Safety Net is also optimized so only messages in the Shadow Safety Net for the requested time interval and the requested mailbox database are resubmitted.

The interaction of Primary Safety Net and Shadow Safety Net during message resubmission is described in the following scenario.

1.  Active Manager requests a resubmission of messages from Safety Net for a mailbox database for the time interval 5:00 to 9:00. However, the Mailbox server that holds the Primary Safety Net has crashed due to a hardware failure. Active Manager repeatedly tries to contact the Primary Safety Net for 12 hours.

2.  After 12 hours, Active Manager sends a broadcast message to the Transport service on all Mailbox servers in the transport high availability boundary looking for other Safety Nets that contain messages for the target mailbox database for the time interval 5:00 to 9:00. The Shadow Safety Net responds are resubmits messages for the mailbox database for the time interval 5:00 to 9:00.

An interesting interaction occurs if the Primary Safety Net was offline during part of the requested resubmit interval as described in the following scenario.

1.  The queue database on Mailbox server that holds the Primary Safety Net is corrupt, and a new queue database is created at 7:00. All of the primary messages stored in the Primary Safety Net from 1:00 to 7:00 are lost, but the server is able to store copies of successfully delivered messages in Safety Net starting at 7:00.

2.  Active Manager requests a resubmission of messages from Safety Net for a mailbox database for the time interval 1:00 to 9:00.

3.  The Primary Safety Net resubmits messages for the time interval 7:00 to 9:00.

4.  The Primary Safety Net sends a broadcast message to the Transport service on all Mailbox servers in the transport high availability boundary looking for other Safety Nets that contain messages for the target mailbox database for the time interval 1:00 to 7:00 for which the Primary Safety Net has no message. The Shadow Safety Net generates a second resubmit request on behalf of the Primary Safety Net for resubmitting the shadow messages for the target mailbox database for the time interval 1:00 to 7:00.

There are some other issues to consider when messages are resubmitted from Safety Net.

1.  All delivery status notifications (DSNs) and non-delivery reports (NDRs) are suppressed for Safety Net resubmits. For example, if the primary message resulted in an NDR, the NDR for the resubmitted message won't be delivered.

2.  Users removed from a distribution group may not receive a resubmitted message when the Shadow Safety Net resubmits the message. For example, a message is sent to a group containing User A and User B, and both recipients receive the message. User B is subsequently removed from the group. Later, a resubmit request from Primary Safety Net is made for the mailbox database that holds User B's mailbox. However, the Primary Safety Net is unavailable for more than 12 hours, so the Shadow Safety Net server responds and resubmits the affected message. During resubmission when the distribution group is expanded, User B isn't a member of the group, and won't receive a copy of the resubmitted message.

3.  New Users added to a distribution group may receive an old resubmitted message when the Shadow Safety Net resubmits the message. For example, a message is sent to a group containing User A and User B, and both recipients receive the message. User C is subsequently added to the group. Later, a resubmit request from Primary Safety Net is made for the mailbox database that holds User C's mailbox. However, the Primary Safety Net server is unavailable for more than 12 hours, so the Shadow Safety Net server responds and resubmits the affected messages. During resubmission when the distribution group is expanded, User C is a member of the group, and will receive a copy of the resubmitted message.

Return to top

