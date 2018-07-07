---
title: 'Move a public folder mailbox to a different mailbox database: Exchange 2013 Help'
TOCTitle: Move a public folder mailbox to a different mailbox database
ms:assetid: 67601d45-4824-4ae6-9a7e-b645ec3af4d3
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ906434(v=EXCHG.150)
ms:contentKeyID: 50630967
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Move a public folder mailbox to a different mailbox database

 

_**Applies to:** Exchange Server 2013_


You may need to move a public folder mailbox to a different mailbox database for load balancing purposes or for moving resources closer to their geographical location. Similar to moving a regular mailbox, you use the **MoveRequest** cmdlets to move a public folder mailbox. For more information about moving mailboxes, see [Mailbox moves in Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

For additional management tasks related to public folders, see [Public folder procedures](public-folder-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete depends on the size of the public folder mailbox.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox move and migration permissions" section in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - You can’t perform this procedure in the EAC. You can only perform this procedure in the Shell.

  - Depending on the size of the public folder mailbox, the move may take several hours to complete. During that time, users won’t be able to access the public folders. Users also won’t have access to public folders for a brief period while the folder is in the “Completion in Progress” state.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Create a move request

The **New-MoveRequest** cmdlet queues the public folder mailbox into the Microsoft Exchange Mailbox Replication service queue. When the Microsoft Exchange Mailbox Replication service is available, it will pick up the move request and begin moving the public folder mailbox. It will complete the entire request from beginning to end.

This example begins the move request for the public folder mailbox PF\_SanFrancisco to the mailbox database MBX\_DB01.

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01

For detailed syntax and parameter information, see [New-MoveRequest](https://technet.microsoft.com/en-us/library/dd351123\(v=exchg.150\)).

## Create a move request to complete at a later time

During the final stage of the move request, when it’s in the `CompletionInProgress` phase, users may be temporarily locked out the public folder mailbox. If needed, you can suspend the move request before it reaches that phase and resume it at a time when users won’t be impacted.

This example begins the move request for the public folder mailbox PF\_SanFrancisco to the mailbox database MBX\_DB01, and suspends it when the move request is ready to complete.

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01 -SuspendWhenReadyToComplete

For detailed syntax and parameter information, see [New-MoveRequest](https://technet.microsoft.com/en-us/library/dd351123\(v=exchg.150\)).

This example retrieves the status of the ongoing mailbox move for the public folder mailbox PF\_SanFrancisco.

    Get-MoveRequest -Identity "PF_SanFrancisco"

For detailed syntax and parameter information, see [Get-MoveRequest](https://technet.microsoft.com/en-us/library/dd335227\(v=exchg.150\)).

When the move request reaches the status of Suspended, you can resume the request. This example resumes the move request for the public folder mailbox PF\_SanFrancisco.

    Resume-MoveRequest -Identity "PF_SanFrancisco"

For detailed syntax and parameter information, see [Resume-MoveRequest](https://technet.microsoft.com/en-us/library/ee332320\(v=exchg.150\)).

## How do you know this worked?

To verify that the move request was successfully created, run the following command:

    Get-MoveRequestStatistics -Identity PF_SanFrancisco | Format-List Status

A status of `Completed` indicates that the move request was successful.

If the move was unsuccessful, you may need to restore the public folder. For more information, see [Restore public folders and public folder mailboxes from failed moves](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md).

