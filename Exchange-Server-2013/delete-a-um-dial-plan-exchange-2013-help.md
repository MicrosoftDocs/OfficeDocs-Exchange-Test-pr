---
title: 'Delete a UM dial plan: Exchange 2013 Help'
TOCTitle: Delete a UM dial plan
ms:assetid: c9b32ef6-432c-45ca-b94c-31bbcc973128
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124546(v=EXCHG.150)
ms:contentKeyID: 49315522
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Delete a UM dial plan

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can delete an existing Unified Messaging (UM) dial plan. When you delete the UM dial plan, it will no longer be available for UM IP gateways, UM mailbox policies, and UM hunt groups. You can’t delete a UM dial plan if it's referenced by or associated with UM mailbox policies, UM auto attendants, UM IP gateways, or UM hunt groups.

For additional management tasks related to UM dial plans, see [UM dial plan procedures](um-dial-plan-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM dial plans" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to delete an existing dial plan

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**.

2.  In the list view, select the UM dial plan you want to delete, and then click **Delete** ![Delete icon](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon").

3.  On the warning page, click **Yes**.

## Use the Shell to delete an existing dial plan

This example deletes a UM dial plan named `MyUMDialPlan`.

    RemoveUMDialplan -identity MyUMDialPlan

