---
title: 'Checklist: Deploying retention policies: Exchange 2013 Help'
TOCTitle: 'Checklist: Deploying retention policies'
ms:assetid: 59e299fd-b6a8-48f5-88ae-dc20dbe32e90
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee364743(v=EXCHG.150)
ms:contentKeyID: 49318577
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Checklist: Deploying retention policies

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Use this checklist to deploy retention policies in your Microsoft Exchange Server 2013 organization. Before you start working with this checklist, make sure you're familiar with the concepts in the following topics:

  - [Messaging records management](messaging-records-management-exchange-2013-help.md)

  - [Retention tags and retention policies](retention-tags-and-retention-policies-exchange-2013-help.md)

## Checklist for deploying retention policies


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Done?</th>
<th>Tasks</th>
<th>Resources</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p> </p></td>
<td><p>Assess messaging records management (MRM) requirements for different sets of users.</p></td>
<td><p><a href="messaging-records-management-exchange-2013-help.md">Messaging records management</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Determine which Microsoft Outlook client versions are in use.</p></td>
<td><p>Parse the RPC Client Access log files located at <code>%ExchangeInstallPath%Logging\RPC Client Access</code>.</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Create retention tags.</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">Create a Retention Policy</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Create retention policies.</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">Create a Retention Policy</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Add retention tags to retention policies.</p></td>
<td><p><a href="add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md">Add retention tags to or remove retention tags from a retention policy</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Place mailboxes on retention hold.</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">Place a mailbox on retention hold</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Apply a retention policy to a single mailbox for testing purposes.</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">Apply a retention policy to mailboxes</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Optional: Implement client blocking to block legacy Outlook clients.</p></td>
<td><p><a href="configure-outlook-client-blocking-exchange-2013-help.md">Configure Outlook Client Blocking for Messaging Records Management</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Begin user communication and training activities. Include a deadline when retention policies will be processed, and items moved or deleted.</p></td>
<td><p>Not applicable</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Apply retention policy to additional mailboxes.</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">Apply a retention policy to mailboxes</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>A few days in advance, remind users about the deadline.</p></td>
<td><p>Not applicable</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>At the deadline, remove the retention hold from mailboxes.</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">Place a mailbox on retention hold</a></p></td>
</tr>
</tbody>
</table>

