---
title: 'How retention age is calculated: Exchange 2013 Help'
TOCTitle: How retention age is calculated
ms:assetid: a7daf7aa-0411-4b26-a422-eefd1b113f9f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb430780(v=EXCHG.150)
ms:contentKeyID: 49315253
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# How retention age is calculated

 

_**Applies to:** Exchange Online, Exchange Server 2013_


The Managed Folder Assistant (MFA) is one of many *mailbox assistant* processes that runs on mailbox servers. Its job is to process mailboxes that have a Retention Policy applied, add the Retention Tags included in the policy to the mailbox, and process items in the mailbox. If the items have a retention tag, the assistant tests the age of those items. If an item has exceeded its *retention age*, it takes the specified *retention action*. Retention actions include moving an item to the user’s archive, deleting the item and allowing recovery, or deleting the item permanently.

See [Retention tags and retention policies](retention-tags-and-retention-policies-exchange-2013-help.md) for more information.

## Determining the age of different types of items

The retention age of mailbox items is calculated from the date of delivery or in the case of items like drafts that aren't delivered but created by the user, the date an item was created. When the Managed Folder Assistant processes items in a mailbox, it stamps a start date and an expiration date for all items that have retention tags with the **Delete and Allow Recovery** or **Permanently Delete** retention action. Items that have an archive tag are also stamped with a move date.

Items in the Deleted Items folder and items which may have a start and end date, such as calendar items (meetings and appointments) and tasks, are handled differently as shown in this table.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>If the item type is…</th>
<th>And the item is…</th>
<th>The retention age is calculated based on…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Email message</p></li>
<li><p>Document</p></li>
<li><p>Fax</p></li>
<li><p>Journal item</p></li>
<li><p>Meeting request, response, or cancellation</p></li>
<li><p>Missed call</p></li>
</ul></td>
<td><p>Not in the Deleted Items folder</p></td>
<td><p>Delivery date or date of creation</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>Email message</p></li>
<li><p>Document</p></li>
<li><p>Fax</p></li>
<li><p>Journal item</p></li>
<li><p>Meeting request, response, or cancellation</p></li>
<li><p>Missed call</p></li>
</ul></td>
<td><p>In the Deleted Items folder</p></td>
<td><ul>
<li><p>Date of delivery or creation unless the item was deleted from a folder that does not have an inherited or implicit retention tag.</p></li>
<li><p>If an item is in a folder that doesn’t have an inherited or implicit retention tag applied, the item isn’t processed by the MFA and therefore doesn’t have a start date stamped by it. When the user deletes such an item, and the MFA processes it for the first time in the Deleted Items folder, it stamps the current date as the start date.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Calendar</p></td>
<td><p>Not in the Deleted Items folder</p></td>
<td><ul>
<li><p>Non-recurring calendar items expire according to their end date.</p></li>
<li><p>Recurring calendar items expire according to the end date of their last occurrence. Recurring calendar items with no end date don't expire.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Calendar</p></td>
<td><p>In the Deleted Items folder</p></td>
<td><ol>
<li><p>A calendar item expires according to its <code>message-received date</code>, if one exists.</p></li>
<li><p>If a calendar item doesn't have a <code>message-received date</code>, it expires according to its <code>message-creation date</code>.</p></li>
<li><p>If a calendar item has neither a <code>message-received date</code> nor a <code>message-creation date</code>, it doesn't expire.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Task</p></td>
<td><p>Not in the Deleted Items folder</p></td>
<td><ul>
<li><p>Non-recurring tasks:</p>
<ol>
<li><p>A non-recurring task expires according to its <code>message-received date</code>, if one exists.</p></li>
<li><p>If a non-recurring task doesn't have a <code>message-received date</code>, it expires according to its <code>message-creation date</code>.</p></li>
<li><p>If a non-recurring task has neither a <code>message-received date</code> nor a<code> </code><code>message-creation date</code>, it doesn't expire.</p></li>
</ol></li>
<li><p>A recurring task expires according to the <code>end date</code> of its last occurrence. If a recurring task doesn't have an <code>end date</code>, it doesn't expire.</p></li>
<li><p>A regenerating task (which is a recurring task that regenerates a specified time after the preceding instance of the task is completed) doesn't expire.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Task</p></td>
<td><p>In the Deleted Items folder</p></td>
<td><ol>
<li><p>A task expires according to its <code>message-received date</code>, if one exists.</p></li>
<li><p>If a task doesn't have a <code>message-received date</code>, it expires according to its <code>message-creation date</code>.</p></li>
<li><p>If a task has neither a <code>message-received date</code> nor a <code>message-creation date</code>, it doesn't expire.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Contact</p></td>
<td><p>In any folder</p></td>
<td><p>Contacts aren't stamped with a start date or an expiration date, so they're skipped by the Managed Folder Assistant and don't expire.</p></td>
</tr>
<tr class="even">
<td><p>Corrupted</p></td>
<td><p>In any folder</p></td>
<td><p>Corrupted items are skipped by the Managed Folder Assistant and don't expire.</p></td>
</tr>
</tbody>
</table>


## Examples


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>If the user..</th>
<th>The retention tags on folder…</th>
<th>The Managed Folder Assistant…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ol>
<li><p>Receives a message in the Inbox on 01/26/2013.</p></li>
<li><p>Deletes the message on 2/27/2013.</p></li>
</ol>
<p></p></td>
<td><ul>
<li><p>Inbox: Delete in 365 days</p></li>
<li><p>Deleted Items: Delete in 30 days</p></li>
</ul>
<p></p></td>
<td><ol>
<li><p>Processes the message in the Inbox on 1/26/2013, stamps it with a <em>start date</em> of 01/26/2013 and an <em>expiration date</em> of 01/26/2014.</p></li>
<li><p>Processes the message again in the Deleted Items folder on 2/27/2013. It recalculates the expiration date based on the same start date (01/26/2013).</p></li>
<li><p>Because the item is older than 30 days, it is expired immediately.</p></li>
</ol></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Receives a message in the Inbox on 01/26/2013.</p></li>
<li><p>Deletes the message on 2/27/2013.</p></li>
</ol></td>
<td><ul>
<li><p>Inbox: None (inherited or implicit)</p></li>
<li><p>Deleted Items: Delete in 30 days</p></li>
</ul></td>
<td><ol>
<li><p>Processes the message in the Deleted Items folder on 02/27/2013 and determines the item doesn't have a start date. It stamps the current date as the start date, and 03/27/2013 as the expiration date.</p></li>
<li><p>The item is expired on 3/27/2013, which is 30 days after the user deleted or moved it to the Deleted Items folder.</p></li>
</ol></td>
</tr>
</tbody>
</table>


## More Info

  - In Exchange Online, the Managed Folder Assistant processes a mailbox once in seven days. This might result in items being expired up to seven days after the expiration date stamped on the item.

  - Items in mailboxes placed on Retention Hold aren't processed by the Managed Folder Assistant until the Retention Hold is removed.

  - If a mailbox is placed on In-Place Hold or Litigation Hold, expiring items are removed from the Inbox but preserved in the Recoverable Items folder until the mailbox is removed from [In-Place Hold and Litigation Hold](in-place-hold-and-litigation-hold-exchange-2013-help.md).

  - In hybrid deployments, the same retention tags and retention policies must exist in your on-premises and Exchange Online organizations in order to consistently move and expire items across both organizations. See [Export and import retention tags](export-and-import-retention-tags-exchange-2013-help.md) for more information.

