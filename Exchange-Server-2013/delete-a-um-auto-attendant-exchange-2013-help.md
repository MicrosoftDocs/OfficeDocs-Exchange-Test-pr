---
title: 'Delete a UM auto attendant: Exchange 2013 Help'
TOCTitle: Delete a UM auto attendant
ms:assetid: 92846bbc-e6b9-45fc-8702-ef5c92eeb08f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb123780(v=EXCHG.150)
ms:contentKeyID: 49315460
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Delete a UM auto attendant

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


After you delete a Unified Messaging (UM) auto attendant, the incoming calls that were answered by the UM auto attendant must be answered by a human operator. A UM auto attendant can't be deleted if it's associated with a UM dial plan as the default UM auto attendant.

For additional management tasks related to UM auto attendants, see [UM auto attendant procedures](um-auto-attendant-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM auto attendants" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM auto attendant has been created. For detailed steps, see [Create a UM auto attendant](create-a-um-auto-attendant-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to delete a UM auto attendant

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to edit, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Auto Attendants**, select the UM auto attendant you want to delete. On the toolbar, click **Delete** ![Delete icon](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon"). On the **Warning** page, click **Yes**.

## Use the Shell to delete a UM auto attendant

This example deletes a UM auto attendant named `MyUMAutoAttendant`.

    Remove-UMAutoAttendant -Identity MyUMAutoAttendant

