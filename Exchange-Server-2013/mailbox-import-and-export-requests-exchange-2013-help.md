---
title: 'Mailbox import and export requests: Exchange 2013 Help'
TOCTitle: Mailbox import and export requests
ms:assetid: 157a7d88-d3aa-4056-9a50-df67451b14be
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee633455(v=EXCHG.150)
ms:contentKeyID: 49360508
ms.date: 06/04/2016
mtps_version: v=EXCHG.150
---

# Mailbox import and export requests

 

_**Applies to:** Exchange Server 2013_


Using the **MailboxImportRequest** or **MailboxExportRequest** cmdlet sets in the Exchange Management Shell, you can import data from or export data to .pst files. After you initiate a mailbox import or export request, the process is completed asynchronously by the Microsoft Exchange Mailbox Replication service (MRS). MRS resides on all Exchange 2010 Client Access servers and is the service responsible for moving mailboxes and importing and exporting .pst files.

**Contents**

Reasons to import or export mailbox data

Advantages to using import and export requests

Considerations

Importing mailbox data

Exporting mailbox data

## Reasons to import or export mailbox data

You may want to import or export mailbox data for the following reasons:

  - **Satisfy compliance requirements**   You can export mailbox content to a .pst file for legal discovery purposes. After the export is complete, you can import the content to a mailbox used specifically for compliance purposes.

  - **Create a point-in-time snapshot of a mailbox**   By creating a snapshot of specific mailboxes, you avoid having to retain an entire backup set for a mailbox database.

  - **Move a user's .pst file into his or her mailbox or personal archive**   Microsoft Outlook users can save their email locally as .pst files. Using the [New-MailboxImportRequest](https://technet.microsoft.com/en-us/library/ff607310\(v=exchg.150\)) cmdlet, you can move data from a user's .pst file to his or her mailbox or personal archive. This is an easy method for transferring email from a user's local computer to Exchange servers.

## Advantages to using import and export requests

Advantages to using import and export requests in Exchange 2013 include the following:

  - A .pst provider is included in Exchange 2013 that can read and write .pst files.

  - Import and export requests are asynchronous. The process is performed by MRS, which takes advantage of the queuing and throttling frameworks.

  - The .pst files can be imported directly to a user's personal archive.

  - Multiple .pst files can be imported or exported at the same time.

  - The .pst files can reside on any shared network drive accessible by your Exchange servers.

  - Exchange 2013 supports these .pst files: Unicode files created by Office Outlook 2007 and Outlook 2010

## Considerations

Before you import or export mailbox data, consider the following:

  - To import or export mailbox data, a network shared folder accessible by your Exchange servers must be set up. You must also grant read/write permissions to the Exchange Trusted Subsystem group so that the group can access the network share where you import and export mailbox data. If you don't grant this permission, you will receive an error message stating that Exchange is unable to establish a connection to the target mailbox.

  - The maximum .pst file size supported by Outlook is 50 gigabytes (GB). Therefore, we recommend that you don't import a .pst file larger than 50 GB. You can create multiple .pst files for mailboxes larger than 50 GB by specifying specific folders to include or exclude or by using a content filter.

  - Import and export requests are performed by MRS, which also processes move requests and mailbox restore requests. All requests are queued and throttled by MRS.

  - Importing and exporting mailbox data may take several hours depending on file size, network bandwidth, and MRS throttling.

  - Data can't be imported to a public folder or public folder database.

## Importing mailbox data

Use the **MailboxImportRequest** cmdlet set to import data from a .pst file to a mailbox or personal archive. The following is a list of options you can specify when importing mailbox data from a .pst file:


> [!NOTE]
> The mailbox to which you import the data must exist. You can't import data to a user account that doesn't have a mailbox.



  - You can import data to a different user account than the one from which it was exported. For example, you can export data from john@contoso.com and import it to legaldiscovery@contoso.com.

  - You can import items to only the user's personal archive by specifying the *IsArchive* parameter.

  - If associated folder messages exist in the .pst file, you can import them using the *AssociatedMessagesCopyOption* parameter. Associated messages contain hidden data with information about rules, views, and forms. If they exist in the .pst file, all messages from the safety net are imported.

  - You can include or exclude specific folders using the *IncludeFolders* or *ExcludeFolders* parameter.

  - You can exclude the Recoverable Items folder using the *ExcludeDumpster* parameter. By default, an import request includes the user's Recoverable Items folder if it's present in the .pst file.

## Mailbox import request cmdlets

Use the following cmdlets for mailbox import requests.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607310(v=exchg.150)">New-MailboxImportRequest</a></p></td>
<td><p>Starts the process of importing a .pst file to a mailbox or personal archive. You can create more than one import request per mailbox. Each request must have a unique name.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607317(v=exchg.150)">Set-MailboxImportRequest</a></p></td>
<td><p>Changes import request options after the request is created or recover from a failed request.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607309(v=exchg.150)">Suspend-MailboxImportRequest</a></p></td>
<td><p>Suspends an import request any time after the request is created but before the request reaches the status of Completed.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607306(v=exchg.150)">Resume-MailboxImportRequest</a></p></td>
<td><p>Resumes an import request that's suspended or failed.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607311(v=exchg.150)">Remove-MailboxImportRequest</a></p></td>
<td><p>Removes fully or partially completed import requests. Completed import requests aren't automatically cleared. You must use this cmdlet to remove them.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607368(v=exchg.150)">Get-MailboxImportRequest</a></p></td>
<td><p>View general information about an import request.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607315(v=exchg.150)">Get-MailboxImportRequestStatistics</a></p></td>
<td><p>View detailed information about an import request.</p></td>
</tr>
</tbody>
</table>


## Exporting mailbox data

Use the **MailboxExportRequest** cmdlet set to export mailbox data to a .pst file. You can export one mailbox or several mailboxes, but only one request is written to each .pst file at a time. The following is a list of options you can specify when exporting mailbox data to a .pst file:

  - You can export personal archive data using the *IsArchive* parameter.

  - You can filter the messages that are exported using the *ContentFilter* parameter. You can filter by message content, attachment, senders, recipients, Inbox category, importance, message type, message size, and when the message was sent, received, or expired.

  - You can specify folders to include or exclude using the *IncludeFolders* or *ExcludeFolders* parameter. If exporting data from an Exchange 2013 mailbox, you can also exclude the Recoverable Items folder using the *ExcludeDumpster* parameter.

  - You can export associated messages using the *AssociatedMessagesCopyOption* parameter. Associated messages contain hidden data with information about rules, views, and forms. By default, associated items aren't copied to the .pst file.

## Mailbox export request cmdlets

Use the following cmdlets for mailbox export requests.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607299(v=exchg.150)">New-MailboxExportRequest</a></p></td>
<td><p>Starts the process of exporting data from a primary mailbox or personal archive to a .pst file. You can create more than one export request per mailbox. Each request must have a unique name.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607312(v=exchg.150)">Set-MailboxExportRequest</a></p></td>
<td><p>Changes export request options after the request is created or recover from a failed request.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607305(v=exchg.150)">Suspend-MailboxExportRequest</a></p></td>
<td><p>Suspends an export request any time after the request is created but before the request reaches the status of Completed.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607476(v=exchg.150)">Resume-MailboxExportRequest</a></p></td>
<td><p>Resumes an export request that's suspended or failed.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607464(v=exchg.150)">Remove-MailboxExportRequest</a></p></td>
<td><p>Removes fully or partially completed export requests. Completed export requests aren't automatically cleared. You must use this cmdlet to remove them.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607479(v=exchg.150)">Get-MailboxExportRequest</a></p></td>
<td><p>View general information about an export request.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/en-us/library/ff607316(v=exchg.150)">Get-MailboxExportRequestStatistics</a></p></td>
<td><p>View detailed information about an export request.</p></td>
</tr>
</tbody>
</table>

