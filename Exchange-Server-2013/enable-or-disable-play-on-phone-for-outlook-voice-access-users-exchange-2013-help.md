---
title: 'Enable or disable Play on Phone for Outlook Voice Access users: Exchange 2013 Help'
TOCTitle: Enable or disable Play on Phone for Outlook Voice Access users
ms:assetid: d3281a97-6fc6-42a3-855f-1af1184a644a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd351161(v=EXCHG.150)
ms:contentKeyID: 49315530
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Enable or disable Play on Phone for Outlook Voice Access users

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can enable or disable the Play on Phone feature for users associated with a Unified Messaging (UM) mailbox policy. This option is enabled by default and allows users to play their voice mail messages over any phone. This option isn't available to UM-enabled users who have a mailbox on a Microsoft Exchange Server 2007 server.

For additional management tasks related to UM mailbox policies, see [UM mailbox policy procedures](um-mailbox-policy-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 2 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailbox policies" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to enable or disable Play on Phone

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Mailbox Policies**, select the UM mailbox policy you want to manage, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Mailbox Policy** page, select or clear the check box next to **Allow Play on Phone for voice mail**.

4.  Click **Save**.

## Use the Shell to enable or disable Play on Phone

This example enables the Play on Phone feature for users who are associated with the UM mailbox policy `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowPlayOnPhone $true

This example disables the Play on Phone feature for users who are associated with the UM mailbox policy `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowPlayOnPhone $false

