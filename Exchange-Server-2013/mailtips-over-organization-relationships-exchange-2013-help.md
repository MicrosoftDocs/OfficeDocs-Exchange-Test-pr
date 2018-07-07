---
title: 'MailTips over organization relationships: Exchange 2013 Help'
TOCTitle: MailTips over organization relationships
ms:assetid: 1784256f-abe1-4503-b8c4-26d544b73452
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ670165(v=EXCHG.150)
ms:contentKeyID: 49527749
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# MailTips over organization relationships

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Microsoft Exchange Server 2013 allows you to configure organization relationships with Microsoft Exchange Online or other Exchange organizations. Establishing an organization relationship allows you to enhance the user experience when dealing with the other organization. For example, you can share free or busy data, configure secure message flow, and enable message tracking across both organizations.

## Controlling the MailTips access level

You may want to restrict certain types of MailTips. You can either allow all MailTips to be returned or allow only a limited set that would prevent NDRs. You can configure this setting with the *MailTipsAccessLevel* parameter on the **Set-OrganizationRelationship** cmdlet. The following table shows which MailTips are returned over the organization relationship.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>MailTip</th>
<th>Is the MailTip available when the access level is set to All?</th>
<th>Is the MailTip available when the access level is set to Limited?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Large Audience</p></td>
<td><p>Yes</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Automatic Replies</p></td>
<td><p>Yes</p>
<p>If the remote domain of the recipient is specified as internal, the internal automatic reply is displayed. Otherwise, the external automatic reply is displayed.</p></td>
<td><p>Yes</p>
<p>The external automatic reply is displayed.</p></td>
</tr>
<tr class="odd">
<td><p>Moderated Recipient</p></td>
<td><p>Yes</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Oversize Message</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="odd">
<td><p>Restricted Recipient</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="even">
<td><p>Mailbox Full</p></td>
<td><p>Yes</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Custom MailTips</p></td>
<td><p>Yes</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>External Recipients</p></td>
<td><p>Yes</p>
<p>If the remote domain of the recipient is specified as internal, this MailTip is suppressed. Otherwise, the external MailTip is returned.</p></td>
<td><p>Yes</p>
<p>If the remote domain of the recipient is specified as internal, this MailTip is suppressed. Otherwise, the external MailTip is returned.</p></td>
</tr>
</tbody>
</table>


For detailed steps about how to configure MailTips access levels, see [Manage MailTips for organization relationships](manage-mailtips-for-organization-relationships-exchange-2013-help.md).

## Controlling the MailTips access scope

When you enable MailTips over an organization relationship and set the access level to `All`, the recipient-specific MailTips, Mailbox Full, Automatic Replies, and custom MailTips, are returned for all users. However, you may only want to allow these MailTips for a specific set of users. For example, if you set up an organization relationship with a partner, you may want to allow these MailTips only for the users that work with that partner.

To achieve this, you need to first create a group and add all users for whom you want to share recipient-specific MailTips to that group. You can then specify that group on the organization relationship.

After you implement this restriction, your Client Access servers will first verify whether the recipient for whom they received a MailTips query is part of this group. If the recipient is a member of this group, the Client Access servers will proxy back all MailTips including the recipient-specific MailTips. Otherwise they won't include the recipient-specific MailTips in their response.

For detailed steps about how to configure MailTips access levels, see [Manage MailTips for organization relationships](manage-mailtips-for-organization-relationships-exchange-2013-help.md).

