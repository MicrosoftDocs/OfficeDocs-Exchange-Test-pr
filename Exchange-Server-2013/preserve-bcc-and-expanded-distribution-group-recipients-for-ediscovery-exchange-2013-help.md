---
title: 'Preserve Bcc and expanded distribution group recipients for eDiscovery: Exchange 2013 Help'
TOCTitle: Preserve Bcc and expanded distribution group recipients for eDiscovery
ms:assetid: eb8ddf15-0080-457e-9d83-e73e193da334
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn770225(v=EXCHG.150)
ms:contentKeyID: 62629952
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Preserve Bcc and expanded distribution group recipients for eDiscovery

 

_**Applies to:** Exchange Online, Exchange Server 2013, Office 365 Enterprise_


In-Place Hold, Litigation Hold, and [Office 365 retention policies](http://go.microsoft.com/fwlink/?linkid=827811) (created in the Office 365 Security & Compliance Center) allow you to preserve mailbox content to meet regulatory compliance and eDiscovery requirements. Information about recipients directly addressed in the To and Cc fields of a message is included in all messages by default, but your organization may require the ability to search for and reproduce details about all recipients of a message. This includes:

  - **Recipients addressed using the Bcc field of a message**   Bcc recipients are stored in the message in the sender’s mailbox, but not included in headers of the message delivered to recipients.

  - **Expanded distribution group recipients**   Recipients who receive the message because they’re members of a distribution group to which the message was addressed, either in the To, Cc or Bcc fields.

Exchange Online and Exchange Server 2013 (Cumulative Update 7 and later versions) retain information about Bcc and expanded distribution group recipients. You can search for this information by using an In-Place eDiscovery search in the Exchange admin center (EAC) or a Content Search in the Security & Compliance Center.

## How Bcc recipients and expanded distribution group recipients are preserved

As stated earlier, information about Bcc’ed recipients is stored with the message in the sender’s mailbox. This information is indexed and available to eDiscovery searches and holds.

Information about expanded distribution group recipients is stored with the message after you place a mailbox on In-Place Hold or Litigation Hold. In Office 365, this information is also stored when an Office 365 retention policy is applied to a mailbox. Distribution group membership is determined at the time the message is sent. The expanded recipients list stored with the message is not impacted by changes to membership of the group after the message is sent.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Information about…</th>
<th>Is stored in…</th>
<th>Is stored by default?</th>
<th>Is accessible to…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>To and Cc recipients</p></td>
<td><p>Message properties in the sender and recipients’ mailboxes.</p></td>
<td><p>Yes</p></td>
<td><p>Sender, recipients, and compliance officers</p></td>
</tr>
<tr class="even">
<td><p>Bcc recipients</p></td>
<td><p>Message property in the sender’s mailbox.</p></td>
<td><p>Yes</p></td>
<td><p>Sender and compliance officers</p></td>
</tr>
<tr class="odd">
<td><p>Expanded distribution group recipients</p></td>
<td><p>Message properties in the sender’s mailbox.</p></td>
<td><p>No. Expanded distribution group recipient information is stored after a mailbox is placed on In-Place Hold or Litigation Hold, or assigned to an Office 365 retention policy.</p></td>
<td><p>Compliance officers</p></td>
</tr>
</tbody>
</table>


## Searching for messages sent to Bcc and expanded distribution group recipients

When searching for messages sent to a recipient, eDiscovery search results now include messages sent to a distribution group that the recipient is a member of. The following table shows the scenarios where messages sent to Bcc and expanded distribution group recipients are returned in eDiscovery searches.

Scenario 1: John is a member of the US-Sales distribution group. This table shows eDiscovery search results when Bob sends a message to John directly or indirectly via a distribution group.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>When you search Bob’s mailbox for messages sent…</th>
<th>And the message is sent with…</th>
<th>Results include message?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>To:John</p></td>
<td><p>John on TO</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="even">
<td><p>To:John</p></td>
<td><p>US-Sales on TO</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="odd">
<td><p>To:US-Sales</p></td>
<td><p>US-Sales on TO</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="even">
<td><p>Cc:John</p></td>
<td><p>John on CC</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="odd">
<td><p>Cc:John</p></td>
<td><p>US-Sales on CC</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="even">
<td><p>Cc:US-Sales</p></td>
<td><p>US-Sales on CC</p></td>
<td><p>Yes</p></td>
</tr>
</tbody>
</table>


Scenario 2: Bob sends an email to John (To/Cc) and Jack (Bcc directly, or indirectly via a distribution group). The table below shows eDiscovery search results.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>When you search…</th>
<th>For messages sent…</th>
<th>Results include message?</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bob’s mailbox</p></td>
<td><p>To/Cc:John</p></td>
<td><p>Yes</p></td>
<td><p>Presents an indication that Jack was Bcc’ed.</p></td>
</tr>
<tr class="even">
<td><p>Bob’s mailbox</p></td>
<td><p>Bcc:Jack</p></td>
<td><p>Yes</p></td>
<td><p>Presents an indication that Jack was Bcc’ed.</p></td>
</tr>
<tr class="odd">
<td><p>Bob’s mailbox</p></td>
<td><p>Bcc:Jack (via distribution group)</p></td>
<td><p>Yes</p></td>
<td><p>List of members of the Bcc’ed distribution group, expanded when the message was sent, is visible in eDiscovery search preview, export and logs.</p></td>
</tr>
<tr class="even">
<td><p>John’s mailbox</p></td>
<td><p>To/Cc:John</p></td>
<td><p>Yes</p></td>
<td><p>No indication of Bcc recipients.</p></td>
</tr>
<tr class="odd">
<td><p>John’s mailbox</p></td>
<td><p>Bcc:Jack (directly or via distribution group)</p></td>
<td><p>No</p></td>
<td><p>Bcc information is not stored in the message delivered to recipients. You must search the sender’s mailbox.</p></td>
</tr>
<tr class="even">
<td><p>Jack’s mailbox</p></td>
<td><p>To/Cc:John (directly or via distribution group)</p></td>
<td><p>Yes</p></td>
<td><p>To/Cc information is included in message delivered to all recipients.</p></td>
</tr>
<tr class="odd">
<td><p>Jack’s mailbox</p></td>
<td><p>Bcc:Jack (directly or via distribution group)</p></td>
<td><p>No</p></td>
<td><p>Bcc information is not stored in the message delivered to recipients. You must search the sender’s mailbox.</p></td>
</tr>
</tbody>
</table>


## Frequently asked questions

**Q. When and where is Bcc recipient information stored?**  
A. Bcc recipient information is preserved by default in the original message in sender’s mailbox. If the Bcc recipient is a distribution group, distribution group membership is only expanded if the sender’s mailbox is on hold or assigned to an Office 365 retention policy.

**Q. When and where is the list of expanded distribution group recipients stored?**  
A. Group membership is expanded at the time the message is sent. The list of expanded distribution group members is stored in the original message in the sender’s mailbox. The sender’s mailbox must be on In-Place Hold, Litigation Hold, or assigned to an Office 365 retention policy.

**Q. Can the To/Cc recipients see which recipients were Bcc’ed?**  
A. No. This information is not included in message headers, and isn't visible to To/Cc recipients. The sender can see the Bcc field stored in the original message stored in their mailbox. Compliance officers can see this information when searching the sender’s mailbox.

**Q. How can I ensure expanded distribution group recipients are always preserved?**  
A. To ensure expanded distribution group members are always preserved with a message, [Place all mailboxes on hold](place-all-mailboxes-on-hold-exchange-2013-help.md) or create an organization-wide Office 365 retention policy.

**Q. Which types of groups are supported?**  
A. Distribution groups, mail-enabled security groups, and dynamic distribution groups are supported.

**Q. Is there a limit on the number of distribution group recipients that are expanded and stored in the message?**  
A. Up to 10,000 members of a distribution group is preserved.

**Q. Are nested distribution groups supported?**  
A. Yes, 25 levels of nested distribution groups are expanded.

**Q. Where is the Bcc and expanded distribution group recipient information visible?**  
A. Bcc and expanded distribution group recipients information is visible to Compliance officers when performing an eDiscovery search. Bcc and expanded distribution group recipients are included in search results copied to a Discovery mailbox or exported to a PST file and in the eDiscovery log included in search results. Bcc recipient information is also available in search preview.

**Q. What happens if a member of a distribution group is hidden from the organization's global address list (GAL)?**  
A. There's no impact. If recipients are hidden from the GAL, they're still included in the list of recipients for the expanded distribution group.

