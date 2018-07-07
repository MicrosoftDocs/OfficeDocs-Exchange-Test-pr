---
title: 'Disable a UM auto attendant: Exchange 2013 Help'
TOCTitle: Disable a UM auto attendant
ms:assetid: ad79f374-f68f-430b-8b9c-2c841e1c55ae
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124228(v=EXCHG.150)
ms:contentKeyID: 49315491
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Disable a UM auto attendant

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


By default, when a Unified Messaging (UM) auto attendant is created, its status is set to disabled. After you create the UM auto attendant, you can change its status to control whether it can answer incoming calls. For example, you might want to disable the UM auto attendant when you're recording or re-recording customized prompts and messages.

For additional management tasks related to UM auto attendants, see [UM auto attendant procedures](um-auto-attendant-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM auto attendants" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM auto attendant has been created. For detailed steps, see [Create a UM auto attendant](create-a-um-auto-attendant-exchange-2013-help.md). Also confirm that the status of the UM auto attendant is set to enabled.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to disable a UM auto attendant

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the dial plan you want to change, and on the toolbar, click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Auto Attendants**, select the UM auto attendant you want to disable. On the toolbar, click **Down arrow** ![Down Arrow Icon](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Down Arrow Icon")

3.  On the **Warning** page, click **Yes**.

## Use the Shell to disable a UM auto attendant

This example disables a UM auto attendant named `MyUMAutoAttendant`.

    Disable-UMAutoAttendant -Identity MyUMAutoAttendant

