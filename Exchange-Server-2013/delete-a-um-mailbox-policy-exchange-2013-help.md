---
title: 'Delete a UM mailbox policy: Exchange 2013 Help'
TOCTitle: Delete a UM mailbox policy
ms:assetid: c8758464-3c52-4dd3-b2a6-142a99bb0628
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124536(v=EXCHG.150)
ms:contentKeyID: 49315520
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Delete a UM mailbox policy

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


When you delete a Unified Messaging (UM) mailbox policy, the UM mailbox policy will no longer be available to be associated with recipients who are being enabled for UM. You can’t delete a UM mailbox policy if it's referenced by any UM-enabled mailboxes, and you can’t delete a UM dial plan if a UM mailbox policy is associated with it.

For additional management tasks related to UM mailbox policies, see [UM mailbox policy procedures](um-mailbox-policy-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailbox policies" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to delete a UM mailbox policy

1.  
    
    In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM dial plan** page, under **UM Mailbox Policies**, on the toolbar, click **Delete** ![Delete icon](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon").

## Use the Shell to delete a UM mailbox policy

This example deletes a UM mailbox policy named `MyUMMailboxPolicy`.

    Remove-UMMailboxPolicy -Identity MyUMMailboxPolicy

