---
title: 'Configure the time zone: Exchange 2013 Help'
TOCTitle: Configure the time zone
ms:assetid: 30d769e1-3657-4622-bc9a-643c63cf46d9
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997162(v=EXCHG.150)
ms:contentKeyID: 49315381
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure the time zone

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


By default, the Unified Messaging (UM) auto attendant uses the time zone of the Mailbox server on which it's created. However, there are situations where you may have to change the time zone for a UM auto attendant to a different time zone. For example, if you have two UM dial plans and each dial plan represents a different time zone, you must configure one UM auto attendant to have the same time zone as the Mailbox server and the other UM auto attendant to have a time zone that differs from the Mailbox server.

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

## Use the EAC to configure the time zone

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Auto Attendants**, select the UM auto attendant for which you want to set the time zone, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Auto Attendant** page, click **Business Hours**, and then, under **Time zone**, select the time zone from the drop-down list.

4.  To save your changes, click **OK**, and then click **Save**.

## Use the Shell to configure the time zone

This example sets the time zone to the Pacific time zone on a UM auto attendant named `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -TimeZoneName Pacific

