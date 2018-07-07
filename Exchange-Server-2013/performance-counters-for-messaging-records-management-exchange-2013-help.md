---
title: 'Performance counters for messaging records management: Exchange 2013 Help'
TOCTitle: Performance counters for messaging records management
ms:assetid: b59def6f-4249-4e0c-8057-8ae6eb7c5676
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb310790(v=EXCHG.150)
ms:contentKeyID: 50873808
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Performance counters for messaging records management

 

_**Applies to:** Exchange Server 2013_


The performance counters in this topic monitor the Managed Folder Assistant as it implements messaging records management (MRM) for Microsoft Exchange Server 2010. Because running the Managed Folder Assistant is a resource-intensive process, you should run it only when your server can tolerate the additional load. You should also monitor server performance when the Managed Folder Assistant is running. In addition to the performance counters listed in this topic, you may also want to monitor additional performance counters that monitor items such as disk performance and CPU usage.

For more information about monitoring computers running MRM, see [Monitoring messaging records management](monitoring-messaging-records-management-exchange-2013-help.md).

## Performance Counters for MRM

The following table describes performance counters for MRM.

### Performance counters, performance objects, and description

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Performance counter</th>
<th>Performance object</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Average Mailbox Processing Time In Seconds</p></td>
<td><p>MSExchange Assistants</p></td>
<td><p>Counts the average processing time of mailboxes for time-based assistants.</p></td>
</tr>
<tr class="even">
<td><p>Mailboxes Processed</p></td>
<td><p>MSExchange Assistants</p></td>
<td><p>Counts the number of mailboxes processed by time-based assistants since the service started.</p></td>
</tr>
<tr class="odd">
<td><p>Mailboxes processed/sec</p></td>
<td><p>MSExchange Assistants</p></td>
<td><p>Determines the rate of mailboxes processed by time-based assistants per second.</p></td>
</tr>
<tr class="even">
<td><p>Items Deleted but Recoverable</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Counts the number of items deleted by the Managed Folder Assistant since the start of the most recent schedule interval. (The items are still recoverable through the Recoverable Items folder.) The number includes items in the mailboxes scheduled for processing during the schedule interval and items in any mailboxes that you specified for processing. This counter is reset to zero at the start of each schedule interval.</p></td>
</tr>
<tr class="odd">
<td><p>Items Journaled</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Counts the number of items journaled by the Managed Folder Assistant since the start of the most recent schedule interval. The number includes items in the mailboxes scheduled for processing during the current work cycle and items in any mailboxes you specified for processing. This counter is reset to zero at the start of each work cycle.</p></td>
</tr>
<tr class="even">
<td><p>Items Marked as Past Retention Date</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Counts the number of items marked as past their retention date by the Managed Folder Assistant since the start of the most recent schedule interval. The number includes items in mailboxes scheduled for processing during the schedule interval and items in any mailboxes you specified for processing. This counter is reset to zero at the start of each schedule interval.</p></td>
</tr>
<tr class="odd">
<td><p>Items Moved</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Counts the number of items moved by the Managed Folder Assistant since the start of the most recent schedule interval. The number includes items in the mailboxes scheduled for processing during the schedule interval and items in any mailboxes you specified for processing. This counter is reset to zero at the start of each schedule interval.</p></td>
</tr>
<tr class="even">
<td><p>Items Permanently Deleted</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Counts the number of items permanently deleted by the Managed Folder Assistant since the beginning of the most recent schedule interval. The number includes items in the mailboxes scheduled for processing during the schedule interval and items in any mailboxes you specified for processing. This counter is reset to zero at the beginning of each schedule interval.</p></td>
</tr>
<tr class="odd">
<td><p>Items Subject to Retention Policy</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Counts the number of items subject to retention policy by the Managed Folder Assistant since the start of the most recent schedule interval. The number includes items in the mailboxes scheduled for processing during the schedule interval and items in any mailboxes you specified for processing. This counter is reset to zero at the start of each schedule interval. This counter is the sum of the following four expiration-related counters:</p>
<ul>
<li><p>Items Journaled</p></li>
<li><p>Items Marked as Past Retention Date</p></li>
<li><p>Items Moved</p></li>
<li><p>Items Permanently Deleted</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsExpired - Size of Items subject to Retention Policy (In Bytes)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Indicates the total size of items expired by the Managed Folder Assistant (SoftDelete, HardDelete, MoveToArchive).</p>
<p>The following items are included:</p>
<ul>
<li><p>Messages subject to deletion or move to a managed custom folder by a managed folder mailbox policy</p></li>
<li><p>Messages subject to deletion or move to archive by the user's retention policy</p></li>
<li><p>Messages expired by dumpster policy</p></li>
<li><p>Messages cleaned up by system cleanup tags</p></li>
</ul>
<p>This counter is reset to zero at every work cycle checkpoint of the Managed Folder Assistant work cycle.</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsSoftDeleted - Size of Items Deleted but Recoverable (In Bytes)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Indicates the total size of items soft deleted by the Managed Folder Assistant.</p>
<p>The following items are included:</p>
<ul>
<li><p>Messages soft deleted by a managed folder mailbox policy</p></li>
<li><p>Messages soft deleted by a retention policy</p></li>
</ul>
<p>This counter is reset to zero at every work cycle checkpoint of the Managed Folder Assistant work cycle.</p></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsPermanentlyDeleted - Size of Items Permanently Deleted (In Bytes)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Indicates the total size of items soft deleted by the Managed Folder Assistant.</p>
<p>The following items are included:</p>
<ul>
<li><p>Messages hard deleted by a managed folder mailbox policy</p></li>
<li><p>Messages hard deleted by a retention policy</p></li>
<li><p>Messages hard deleted by the Recoverable Items policy</p></li>
</ul>
<p>This counter is reset to zero at every work cycle checkpoint of the Managed Folder Assistant work cycle.</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsMoved - Size of Items Moved due to an Archive policy tag (In Bytes)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Indicates the total size of items moved to a folder or moved to archive by the Managed Folder Assistant.</p>
<p>The following items are included:</p>
<ul>
<li><p>Messages moved to a managed custom folder by a managed folder mailbox policy</p></li>
<li><p>Messages moved to the personal archive by a retention policy</p></li>
</ul>
<p>This counter is reset to zero at every work cycle checkpoint of the Managed Folder Assistant work cycle.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsWithPersonalTag - Items stamped with Personal Tag (Expiry or Archive)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Indicates the number of times a user tags items with a personal tag.</p>
<p>This includes both Deletion and Archive tags.</p>
<p>For example:</p>
<ul>
<li><p>An item is tagged with a personal tag.</p></li>
<li><p>An item with a personal tag is retagged with another personal tag.</p></li>
</ul>
<p>If a folder is tagged with a personal tag, the counter is incremented by the total number of items in the folder.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsWithDefaultTag - Items stamped with Default Tag (Expiry or Archive)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Indicates the number of items assigned a default policy tag (DPT) based on a user action, for example, when a user selects a message with a personal tag and selects <strong>Use folder policy</strong>.</p>
<p>If a new user is assigned a retention policy with a DPT, the counter is incremented by the number of items that will be assigned the DPT due to the retention policy.</p>

> [!NOTE]
> If a user has a retention policy with a DPT, new messages that arrive through transport get a default tag, and this isn't tracked by this counter.


</td>
</tr>
<tr class="even">
<td><p>TotalItemsWithSystemCleanupTag - Items stamped with System Cleanup Tag</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Indicates the number of items tagged with the system cleanup tag. This includes mailbox metadata items that aren't visible to users.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsExpiredByDefaultExpiryTag - Items expired due to a default Expiry Tag</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Indicates the number of items expired (soft or hard deleted) by the Managed Folder Assistant due to any non-personal (default or system) tag in a retention policy.</p>
<p>This doesn't include the items expired by Recoverable Items clean up or system clean up.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsExpiredByPersonalExpiryTag - Items expired due to a personal Expiry Tag</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Indicates the number of items expired (soft or hard deleted) by the Managed Folder Assistant due to a personal tag in the retention policy.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsMovedByDefaultArchiveTag - Items moved due to a default Archive Tag</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Indicates the number of items moved to the archive by the Managed Folder Assistant due to any non-personal (default or system) archive tag in a retention policy.</p>
<p>This doesn't include the items moved to the Recoverable Items folder in archive by Recoverable Items cleanup.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsMovedByPersonalArchiveTag - Items Moved due to an Archive Tag</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Indicates the number of items moved to the archive by the Managed Folder Assistant due to a personal archive tag in a retention policy.</p></td>
</tr>
<tr class="odd">
<td><p>TotalMovedDumpsterItems - Mailbox Dumpsters Moved Items</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>Indicates the number of items moved to the Recoverable Items folder in the archive by Recoverable Items cleanup.</p></td>
</tr>
</tbody>
</table>

