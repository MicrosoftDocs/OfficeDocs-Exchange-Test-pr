---
title: 'Place a mailbox on retention hold: Exchange 2013 Help'
TOCTitle: Place a mailbox on retention hold
ms:assetid: 2baac4a7-3402-4142-bfb3-1649a950e677
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd335168(v=EXCHG.150)
ms:contentKeyID: 49318575
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Place a mailbox on retention hold

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Placing a mailbox on retention hold suspends the processing of a retention policy or managed folder mailbox policy for that mailbox. Retention hold is designed for situations such as a user being on vacation or away temporarily.

During retention hold, users can log on to their mailbox and change or delete items. When you perform a mailbox search, deleted items that are past the deleted item retention period aren't returned in search results. To make sure items changed or deleted by users are preserved in legal hold scenarios, you must place a mailbox on legal hold. For more information, see [Create or remove an In-Place Hold](create-or-remove-an-in-place-hold-exchange-2013-help.md).

You can also include retention comments for mailboxes you place on retention hold. The comments are displayed in supported versions of Microsoft Outlook.

For additional management tasks related to messaging records management (MRM), see [Messaging Records Management Procedures](messaging-records-management-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Messaging records management" entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

  - You can’t use the Exchange Administration Center (EAC) to place a mailbox on retention hold. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to place a mailbox on retention hold

This example places Michael Allen's mailbox on retention hold.

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $true

For detailed syntax and parameter information, see [Set-Mailbox](https://technet.microsoft.com/en-us/library/bb123981\(v=exchg.150\)).

## Use the Shell to remove retention hold for a mailbox

This example removes the retention hold from Michael Allen's mailbox.

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $false

For detailed syntax and parameter information, see [Set-Mailbox](https://technet.microsoft.com/en-us/library/bb123981\(v=exchg.150\)).

## How do you know this worked?

To verify that you have successfully placed a mailbox on retention hold, use the [Get-Mailbox](https://technet.microsoft.com/en-us/library/bb123685\(v=exchg.150\)) cmdlet to retrieve the *RetentionHoldEnabled* property of the mailbox.

This command retrieves the *RetentionHoldEnabled* property for Michael Allen’s mailbox.

    Get-Mailbox "Michael Allen" | Select RetentionHoldEnabled

This command retrieves all mailboxes in the Exchange organization, filters the mailboxes that are placed on retention hold, and lists them along with the retention policy applied to each.


> [!IMPORTANT]
> Because <EM>RetentionHoldEnabled</EM> isn’t a filterable property in Exchange 2013, you can’t use the <EM>Filter</EM> parameter with the <STRONG>Get-Mailbox</STRONG> cmdlet to filter mailboxes that are placed on retention hold on the server-side. This command retrieves a list of all mailboxes and filters on the client running the Shell session. In large environments with thousands of mailboxes, this command may take a long time to complete.



    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionHoldEnabled -eq $true} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto

