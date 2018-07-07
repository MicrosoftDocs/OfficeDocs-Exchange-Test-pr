---
title: 'Default Retention Policy in Exchange Online and Exchange Server: Exchange 2013 Help'
TOCTitle: Default Retention Policy
ms:assetid: bcf31b2d-463b-4623-b488-c8ac40f14f62
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn775046(v=EXCHG.150)
ms:contentKeyID: 62755577
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Default Retention Policy in Exchange Online and Exchange Server

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Exchange creates the retention policy Default MRM Policy in your Exchange Online and on-premises Exchange organization. The policy is automatically applied to new users in Exchange Online. In on-premises organizations, the policy is applied when you create an archive for the mailbox. You can change the retention policy applied to a user at any time.

You can modify tags included in the Default MRM Policy, for example by changing the retention age or retention actions, disable a tag, or modify the policy by adding or removing tags from it. The updated policy is applied to mailboxes the next time they’re processed by the Managed Folder Assistant

## Retention tags linked to the Default MRM Policy

The following table lists the default retention tags linked to the Default MRM Policy.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Type</th>
<th>Retention age (days)</th>
<th>Retention action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Default 2 years move to archive</p></td>
<td><p>Default Policy Tag (DPT)</p></td>
<td><p>730</p></td>
<td><p>Move to Archive</p></td>
</tr>
<tr class="even">
<td><p>Recoverable Items 14 days move to archive</p></td>
<td><p>Recoverable Items folder</p></td>
<td><p>14</p></td>
<td><p>Move to Archive</p></td>
</tr>
<tr class="odd">
<td><p>Personal 1 year move to archive</p></td>
<td><p>Personal tag</p></td>
<td><p>365</p></td>
<td><p>Move to Archive</p></td>
</tr>
<tr class="even">
<td><p>Personal 5 year move to archive</p></td>
<td><p>Personal tag</p></td>
<td><p>1,825</p></td>
<td><p>Move to Archive</p></td>
</tr>
<tr class="odd">
<td><p>Personal never move to archive</p></td>
<td><p>Personal tag</p></td>
<td><p>Not applicable</p></td>
<td><p>Move to Archive</p></td>
</tr>
<tr class="even">
<td><p>1 Week Delete</p></td>
<td><p>Personal tag</p></td>
<td><p>7</p></td>
<td><p>Delete and Allow Recovery</p></td>
</tr>
<tr class="odd">
<td><p>1 Month Delete</p></td>
<td><p>Personal tag</p></td>
<td><p>30</p></td>
<td><p>Delete and Allow Recovery</p></td>
</tr>
<tr class="even">
<td><p>6 Month Delete</p></td>
<td><p>Personal tag</p></td>
<td><p>180</p></td>
<td><p>Delete and Allow Recovery</p></td>
</tr>
<tr class="odd">
<td><p>1 Year Delete</p></td>
<td><p>Personal tag</p></td>
<td><p>365</p></td>
<td><p>Delete and Allow Recovery</p></td>
</tr>
<tr class="even">
<td><p>5 Year Delete</p></td>
<td><p>Personal tag</p></td>
<td><p>1,825</p></td>
<td><p>Delete and Allow Recovery</p></td>
</tr>
<tr class="odd">
<td><p>Never Delete</p></td>
<td><p>Personal tag</p></td>
<td><p>Not applicable</p></td>
<td><p>Delete and Allow Recovery</p></td>
</tr>
</tbody>
</table>


## What you can do with the Default MRM Policy


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>You can…</th>
<th>In Exchange Online…</th>
<th>In Exchange Server…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Apply the Default MRM Policy automatically to new users</p></td>
<td><p>Yes, applied by default. No action is required.</p></td>
<td><p>Yes, applied by default if you also create an archive for the new user.</p>
<p>If you create an archive for the user later, the policy is applied automatically only if the user doesn’t have an existing Retention Policy.</p></td>
</tr>
<tr class="even">
<td><p>Modify the retention age or retention action of a retention tag linked to the policy</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="odd">
<td><p>Disable a retention tag linked to the policy</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="even">
<td><p>Add a retention tag to the policy</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="odd">
<td><p>Remove a retention tag from the policy</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="even">
<td><p>Set another policy as the default retention policy to be applied automatically to new users</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


## More information

  - A Retention Tag can be linked to more than one Retention Policy. For details about managing [Retention tags and retention policies](retention-tags-and-retention-policies-exchange-2013-help.md), see [Messaging Records Management Procedures](messaging-records-management-procedures-exchange-2013-help.md).

  - The Default MRM Policy doesn't include a DPT to automatically delete items (but it does contain personal tags with the delete retention action that users can apply to mailbox items). If you want to automatically delete items after a specified period, you can create a DPT with the required delete action and add it to the policy. For details, see [Create a Retention Policy](create-a-retention-policy-exchange-2013-help.md) and [Add retention tags to or remove retention tags from a retention policy](add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md).

  - Retention policies are applied to mailbox users. The same policy applies to the user’s mailbox and archive.

