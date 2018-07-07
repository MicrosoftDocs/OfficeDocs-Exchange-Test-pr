---
title: 'Run a non-owner mailbox access report: Exchange Online Help'
TOCTitle: Run a non-owner mailbox access report
ms:assetid: dbbef170-e726-4735-abf1-2857db9bb52d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150575(v=EXCHG.150)
ms:contentKeyID: 47560119
ms.date: 04/16/2018
mtps_version: v=EXCHG.150
---

# Run a non-owner mailbox access report

 

_**Applies to:** Exchange Online_


The Non-Owner Mailbox Access Report in the Exchange Administration Center (EAC) lists the mailboxes that have been accessed by someone other than the person who owns the mailbox. When a mailbox is accessed by a non-owner, Microsoft Exchange logs information about this action in a mailbox audit log that’s stored as an email message in a hidden folder in the mailbox being audited. Entries from this log are displayed as search results and include a list of mailboxes accessed by a non-owner, who accessed the mailbox and when, the actions performed by the non-owner, and whether the action was successful. By default, entries in the mailbox audit log are retained for 90 days.

When you enable mailbox audit logging for a mailbox, Microsoft Exchange logs specific actions by non-owners, including both administrators and users, called *delegated users*, who have been assigned permissions to a mailbox. You can also narrow the search to users inside or outside your organization.

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox audit logging" entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Enable mailbox audit logging

You have to enable mailbox audit logging for each mailbox that you want to run a non-owner mailbox access report for. If mailbox audit logging isn't enabled, you won't get any results when you run a report.

To enable mailbox audit logging for a single mailbox, run the following Shell command.

    Set-Mailbox <Identity> -AuditEnabled $true

For example, to enable mailbox auditing for a user named Florence Flipo, run the following command.

    Set-Mailbox "Florence Flipo" -AuditEnabled $true

To enable mailbox auditing for all user mailboxes in your organization, run the following commands.

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}

    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

## How do you know this worked?

Run the following command to verify that you’ve successfully configured mailbox audit logging.

    Get-Mailbox | FL Name,AuditEnabled

A value of `True` for the *AuditEnabled* property verifies that audit logging is enabled.

Return to top

## Run a non-owner mailbox access report

1.  In the EAC, navigate to **Compliance Management** \> **Auditing**.

2.  Click **Run a non-owner mailbox access report**.
    
    By default, Microsoft Exchange runs the report for non-owner access to any mailboxes in the organization over the past two weeks. The mailboxes listed in the search results have been enabled for mailbox audit logging.

3.  To view non-owner access for a specific mailbox, select the mailbox from the list of mailboxes. View the search results in the details pane.


> [!TIP]
> Want to narrow the search results? Select the start date, end date, or both, and select specific mailboxes to search. Click <STRONG>Search</STRONG> to re-run the report.



## Search for specific types of non-owner access

You can also specify the type of non-owner access, also called the logon type, to search for. Here are your options:

  - **All non-owners**   Search for access by administrators and delegated users inside your organization. Also includes access user outside of your organization.

  - **External users**   Search for access by users outside of your organization.

  - **Administrators and delegated users**   Search for access by administrators and delegated users inside your organization.

  - **Administrators**   Search for access by administrators in your organization.

Return to top

## How do you know this worked?

To verify that you’ve successfully run a non-owner mailbox access report, check the search results pane. Mailboxes that you ran the report for are displayed in this pane. If there are no results for a specific mailbox, it’s possible there hasn’t been access by a non-owner or that non-owner access hasn’t taken place within the specified date range. As previously described, be sure to verify that audit logging has been enabled for the mailboxes you want to search for access by non-owners.

Return to top

## What gets logged in the mailbox audit log?

When you run a non-owner mailbox access report, entries from the mailbox audit log are displayed in the search results in the EAC. Each report entry contains this information:

  - Who accessed the mailbox and when

  - The actions performed by the non-owner

  - The affected message and its folder location

  - Whether the action was successful

The following table lists the actions performed by non-owners that can be logged by mailbox audit logging. In the table, a **Yes** indicates that the action can be logged for that logon type, and a **No** indicates that an action can't be logged. An asterisk (**\***) indicates that the action is logged by default when mailbox audit logging is enabled for the mailbox. If you want to track actions that aren't logged by default, you have to use PowerShell to enable logging of those actions.


> [!NOTE]
> An administrator who has been assigned the Full Access permission to a user's mailbox is considered a delegated user.




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Action</th>
<th>Description</th>
<th>Administrator</th>
<th>Delegated user</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Copy</strong></p></td>
<td><p>A message was copied to another folder.</p></td>
<td><p>Yes</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><strong>Create</strong></p></td>
<td><p>An item is created in the Calendar, Contacts, Notes, or Tasks folder in the mailbox; for example, a new meeting request is created. Note that message or folder creation isn't audited.</p></td>
<td><p>Yes*</p></td>
<td><p>Yes*</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderBind</strong></p></td>
<td><p>A mailbox folder was accessed.</p></td>
<td><p>Yes*</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="even">
<td><p><strong>Hard-delete</strong></p></td>
<td><p>A message was purged from the Recoverable Items folder.</p></td>
<td><p>Yes*</p></td>
<td><p>Yes*</p></td>
</tr>
<tr class="odd">
<td><p><strong>MessageBind</strong></p></td>
<td><p>A message was viewed in the preview pane or opened.</p></td>
<td><p>Yes</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><strong>Move</strong></p></td>
<td><p>A message was moved to another folder.</p></td>
<td><p>Yes*</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="odd">
<td><p><strong>Move To Deleted Items</strong></p></td>
<td><p>A message was moved to the Deleted Items folder.</p></td>
<td><p>Yes*</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="even">
<td><p><strong>Send as</strong></p></td>
<td><p>A message was sent using SendAs permission. This means another user sent the message as though it came from the mailbox owner.</p></td>
<td><p>Yes*</p></td>
<td><p>Yes*</p></td>
</tr>
<tr class="odd">
<td><p><strong>Send on behalf of</strong></p></td>
<td><p>A message was sent using SendOnBehalf permission. This means another user sent the message on behalf of the mailbox owner. The message will indicate to the recipient who the message was sent on behalf of and who actually sent the message.</p></td>
<td><p>Yes*</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="even">
<td><p><strong>Soft-delete</strong></p></td>
<td><p>A message was deleted from the Deleted Items folder.</p></td>
<td><p>Yes*</p></td>
<td><p>Yes*</p></td>
</tr>
<tr class="odd">
<td><p><strong>Update</strong></p></td>
<td><p>A message was changed.</p></td>
<td><p>Yes*</p></td>
<td><p>Yes*</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> *&nbsp; Audited by default if auditing is enabled for a mailbox.



Return to top

