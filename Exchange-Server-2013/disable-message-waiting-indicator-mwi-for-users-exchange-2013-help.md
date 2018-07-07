---
title: 'Disable Message Waiting Indicator (MWI) for users: Exchange 2013 Help'
TOCTitle: Disable Message Waiting Indicator (MWI) for users
ms:assetid: 51cd6dc4-11d1-4eb9-a6c6-1965fcd24267
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673525(v=EXCHG.150)
ms:contentKeyID: 49315416
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Disable Message Waiting Indicator (MWI) for users

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can enable or disable Message Waiting Indicator for users associated with a Unified Messaging (UM) mailbox policy. Message Waiting Indicator is a feature found in most legacy voice mail systems. In its most common form, it lights a lamp on a voice mail subscriber’s phone to indicate the presence of a new voice mail message. Message Waiting Indicator can also send a text message to a UM-enabled user's mobile phone. The default setting is enabled.

If Message Waiting Indicator is disabled on the UM IP gateway, the feature isn't available to UM-enabled users associated with the UM mailbox policy.

For additional management tasks related to UM mailbox policies, see [UM mailbox policy procedures](um-mailbox-policy-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailbox policies" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to disable Message Waiting Indicator

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  Under **UM Mailbox Policies**, select the UM mailbox policy you want to manage, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Mailbox Policy** page, clear the check box next to **Allow Message Waiting Indicator**.

4.  Click **Save**.

## Use the Shell to disable Message Waiting Indicator

This example disables Message Waiting Indicator for users associated with the UM mailbox policy named `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMessageWaitingIndicator $false

