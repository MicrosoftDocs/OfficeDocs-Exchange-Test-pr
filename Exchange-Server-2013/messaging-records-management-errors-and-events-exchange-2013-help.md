---
title: 'Messaging records management errors and events: Exchange 2013 Help'
TOCTitle: Messaging records management errors and events
ms:assetid: 8bc3f5ae-403b-45af-86c1-b2fccab34e63
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb310783(v=EXCHG.150)
ms:contentKeyID: 50873803
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Messaging records management errors and events

 

_**Applies to:** Exchange Server 2013_


Messaging records management (MRM) generates events that you can view in Event Viewer. This allows you to troubleshoot and verify the performance of the Managed Folder Assistant. Event Viewer tracks the following kinds of events in the following order, based on importance:

1.  Error events

2.  Warning events

3.  Informational events

## MRM Errors and Events

The following tables provide lists of events that you can use to troubleshoot MRM. The logging types include the following:

  - Events labeled as **LogAlways** are always logged individually.

  - Events labeled as **LogPeriodic** are logged only once in any five-minute period, not every time they occur. This helps to prevent excessive log entries.

### MRM events in the Managed Folder Assistant category

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Event ID</strong></th>
<th><strong>Category</strong></th>
<th><strong>Event type</strong></th>
<th><strong>Logging</strong></th>
<th><strong>Value or description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10003</p></td>
<td><p>Managed Folder Assistant</p></td>
<td><p>Error</p></td>
<td><p>LogPeriodic</p></td>
<td><p>Could not get the server configuration object from Active Directory. &lt;<em>Exception details</em>&gt;. Check for domain controller network connectivity issues or incorrect DNS configuration.</p></td>
</tr>
<tr class="even">
<td><p>10004</p></td>
<td><p>Managed Folder Assistant</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>The retention policy for folder &lt;<em>folder</em>&gt; in mailbox &lt;<em>mailbox</em>&gt; will not be applied. The managed folder assistant is unable to process managed content setting &lt;<em>content setting</em>&gt; for the managed folder &lt;<em>managed folder</em>&gt;. The RetentionAction is MoveToFolder but a destination folder was not specified. Please specify a destination folder.</p></td>
</tr>
<tr class="odd">
<td><p>10005</p></td>
<td><p>Managed Folder Assistant</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>Retention policy will not be applied to folder &lt;<em>folder</em>&gt; in mailbox &lt;<em>mailbox</em>&gt;. Unable to process Managed Content Setting &lt;<em>content setting</em>&gt; for the Managed Folder &lt;<em>managed folder</em>&gt;. The RetentionAction is MoveToFolder but the destination folder &lt;<em>folder</em>&gt; is the same as the source folder &lt;<em>folder</em>&gt;. Please specify a destination folder that is different from the source folder.</p></td>
</tr>
<tr class="even">
<td><p>10009</p></td>
<td><p>Managed Folder Assistant</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>The managed folder assistant skipped processing all databases on the local server because it could not read the audit log parameters from Active Directory. It will try again later in the schedule window. Current database: &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10010</p></td>
<td><p>Managed Folder Assistant</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>The managed folder assistant skipped processing all databases on the local server because the audit log is enabled but the path to the audit log is missing in Active Directory. It will try again later in the schedule window. Current database: &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10011</p></td>
<td><p>Managed Folder Assistant</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>The managed folder assistant could not configure the audit log. It will stop processing the current database: '%1'. It will try again later in the schedule window. Exception details: &lt;<em>details</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10012</p></td>
<td><p>Managed Folder Assistant</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>The managed folder assistant did not write to the audit log. It will stop processing the current database: &lt;<em>database</em>&gt;. It will try to write to the audit log again later in the schedule window. Exception details: &lt;<em>details</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10017</p></td>
<td><p>Managed Folder Assistant</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>An exception occurred in the Managed Folder Assistant while it was processing Mailbox: &lt;<em>mailbox</em>&gt; Folder: Name: &lt;<em>folder name</em>&gt; Id: &lt;<em>folder ID</em>&gt; Item: Ids: &lt;<em>IDs</em>&gt;. Exception: &lt;<em>exception</em>&gt;.</p></td>
</tr>
</tbody>
</table>


### MRM events in the Assistants category

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Event ID</strong></th>
<th><strong>Category</strong></th>
<th><strong>Event type</strong></th>
<th><strong>Logging</strong></th>
<th><strong>Value or description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9004</p></td>
<td><p>Assistants</p></td>
<td><p>Warning</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; failed to process mailbox &lt;<em>mailbox</em>&gt;. The following exception caused the failure: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9014</p></td>
<td><p>Assistants</p></td>
<td><p>Warning</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. Unable to process schedule changes. The following exception caused the failure: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9017</p></td>
<td><p>Assistants</p></td>
<td><p>Information</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; for database &lt;<em>database</em>&gt; is entering a scheduled time window. There are &lt;<em>number</em>&gt; mailboxes to process.</p></td>
</tr>
<tr class="even">
<td><p>9018</p></td>
<td><p>Assistants</p></td>
<td><p>Information</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; for database &lt;<em>database</em>&gt; is exiting a scheduled time window. &lt;<em>number</em>&gt; out of &lt;<em>number</em>&gt; mailboxes were successfully processed. &lt;<em>number</em>&gt; mailboxes were skipped due to errors. &lt;<em>number</em>&gt; mailboxes were processed separately. &lt;<em>number</em>&gt; mailboxes were not processed due to insufficient time.</p>

> [!NOTE]
> The Managed Folder Assistant will resume where it left off the next time it runs.


</td>
</tr>
<tr class="odd">
<td><p>9019</p></td>
<td><p>Assistants</p></td>
<td><p>Warning</p></td>
<td><p>LogPeriodic</p></td>
<td><p>Service &lt;<em>service</em>&gt;. Unable to save progress for &lt;<em>service</em>&gt; on database &lt;<em>database</em>&gt;. (The assistant was unable to save where it stopped so that it could resume there when it restarts.) The following exception caused the failure: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9020</p></td>
<td><p>Assistants</p></td>
<td><p>Warning</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>assistant name</em>&gt; failed to start for database &lt;<em>database</em>&gt;. The following exception caused the failure: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9021</p></td>
<td><p>Assistants</p></td>
<td><p>Information</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; for database &lt;<em>database</em>&gt; is processing an on-demand request. There are &lt;<em>number</em>&gt; mailboxes to process.</p></td>
</tr>
<tr class="even">
<td><p>9022</p></td>
<td><p>Assistants</p></td>
<td><p>Information</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; for database &lt;<em>database</em>&gt; has finished an on-demand request. &lt;<em>number</em>&gt; out of &lt;<em>number</em>&gt; mailboxes were successfully processed. &lt;<em>number</em>&gt; mailboxes were skipped due to errors.</p></td>
</tr>
<tr class="odd">
<td><p>9023</p></td>
<td><p>Assistants</p></td>
<td><p>Warning</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; failed to start time window processing on database &lt;<em>database</em>&gt;. The following exception caused the failure: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9025</p></td>
<td><p>Assistants</p></td>
<td><p>Information</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; skipped &lt;<em>number</em>&gt; mailboxes on database &lt;<em>database</em>&gt;. Mailboxes: &lt;<em>mailboxes</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9026</p></td>
<td><p>Assistants</p></td>
<td><p>Warning</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; failed to start on-demand processing on database &lt;<em>database</em>&gt;. The following exception caused the failure: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9027</p></td>
<td><p>Assistants</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; caused the process to terminate &lt;<em>number</em>&gt; times while processing mailbox &lt;<em>mailbox</em>&gt; on database &lt;<em>database</em>&gt;. This mailbox will no longer be processed in the requested time window or on-demand request. The following exception caused the failure: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9028</p></td>
<td><p>Assistants</p></td>
<td><p>Warning</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; caused the process to terminate &lt;<em>number</em>&gt; times while processing mailbox &lt;<em>mailbox</em>&gt; on database &lt;<em>database</em>&gt;. The following exception caused the failure: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9033</p></td>
<td><p>Assistants</p></td>
<td><p>Warning</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; for database &lt;<em>database</em>&gt; received an on-demand request. However, there are no mailboxes to process.</p></td>
</tr>
<tr class="odd">
<td><p>9034</p></td>
<td><p>Assistants</p></td>
<td><p>Information</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt; halted time based operations for managed folder assistant on database &lt;<em>database</em>&gt;.</p></td>
</tr>
<tr class="even">
<td><p>9035</p></td>
<td><p>Assistants</p></td>
<td><p>Warning</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>assistant name</em>&gt; was unable to process &lt;<em>number</em>&gt; mailboxes because insufficient time.</p></td>
</tr>
<tr class="odd">
<td><p>9037</p></td>
<td><p>Assistants</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. An exception was encountered while processing a RPC. Method: &lt;<em>method</em>&gt;, Exception: &lt;<em>exception</em>&gt;</p></td>
</tr>
</tbody>
</table>

