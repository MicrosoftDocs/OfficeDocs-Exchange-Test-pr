---
title: 'Update the public folder hierarchy: Exchange 2013 Help'
TOCTitle: Update the public folder hierarchy
ms:assetid: a7b2fb51-0207-4d7d-938d-466ae110bb90
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ945055(v=EXCHG.150)
ms:contentKeyID: 51423389
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Update the public folder hierarchy

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You only need to update the public folder hierarchy if you want to manually invoke the hierarchy synchronizer and the mailbox assistant. Both these are invoked at least once every 24 hours for each public folder mailbox in the organization. The hierarchy synchronizer is invoked every 15 minutes if any users are logged on to a secondary mailbox through Microsoft Outlook or a Microsoft Exchange Web Services client.

For additional management tasks related to public folders in Exchange Online, see [Public folder procedures in Office 365 and Exchange Online](https://technet.microsoft.com/en-us/library/jj966272\(v=exchg.150\)).

For additional management tasks related to public folders in Exchange Server 2013, see [Public folder procedures](public-folder-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Sharing and collaboration permissions](sharing-and-collaboration-permissions-exchange-2013-help.md) topic.

  - You can’t perform this procedure in the EAC. You must use the Shell.

  - We recommend that when you run this command with the *InvokeSynchronizer* parameter, you use the *SuppressStatus* parameter. If you don't use this parameter in the command, the output will display status messages every 3 seconds for up to one minute. Until the minute passes, you can't use that instance of the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Update the public folder hierarchy

This example updates the public folder hierarchy on the public folder mailbox PF\_marketing and suppresses the command's output.

    Update-PublicFolderMailbox -Identity PF_marketing -InvokeSynchronizer -SuppressStatus

This example updates all public folder mailboxes and suppresses the command's output.

    Get-Mailbox -PublicFolder | Update-PublicFolderMailbox InvokeSynchronizer -SuppressStatus

