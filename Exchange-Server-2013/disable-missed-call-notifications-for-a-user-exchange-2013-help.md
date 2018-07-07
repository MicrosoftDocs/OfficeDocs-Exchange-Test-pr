---
title: 'Disable missed call notifications for a user: Exchange 2013 Help'
TOCTitle: Disable missed call notifications for a user
ms:assetid: e54937d5-3074-454f-b561-e601fecfc6ad
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673570(v=EXCHG.150)
ms:contentKeyID: 49315540
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Disable missed call notifications for a user

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can enable or disable missed call notifications for a Unified Messaging (UM) mailbox policy by using the Shell or the EAC. A missed call notification is an email message that's sent to a user when the user doesn't answer an incoming call and the caller doesn’t leave a voice message. This is a different email message than the one that contains the voice message that's left for a user.

When you disable missed call notifications on a UM mailbox policy, you prevent all users associated with the UM mailbox policy from receiving an email message when they don't answer an incoming call and the caller doesn’t leave a voice message. By default, missed call notifications are enabled for each UM mailbox policy that's created. Also by default, a UM mailbox policy is created every time you create a UM dial plan.


> [!NOTE]
> When you’re integrating Unified Messaging and Microsoft Lync Server, missed call notifications aren’t available to users that have a mailbox located on an Exchange 2007 or Exchange 2010 Mailbox server when a user disconnects before the call is sent to a Mailbox server running the Microsoft Exchange Unified Messaging service.



For additional management tasks related to UM mailbox policies, see [Manage a UM mailbox policy](manage-a-um-mailbox-policy-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailbox policies" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to disable missed call notifications for a UM mailbox policy

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Mailbox Policies**, select the UM mailbox policy you want to manage, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Mailbox Policy** page \> **General**, clear the check box next to **Allow missed call notifications**.

4.  Click **Save**.

## Use the Shell to disable missed call notifications for a UM mailbox policy

This example disables missed call notifications for a UM mailbox policy named `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMissedCallNotifications $false

