---
title: 'Enable or disable sending voice messages from Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Enable or disable sending voice messages from Outlook Voice Access
ms:assetid: 63544ae2-6a28-40b2-82fc-3df83e93ee56
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee423546(v=EXCHG.150)
ms:contentKeyID: 49315435
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Enable or disable sending voice messages from Outlook Voice Access

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can enable Outlook Voice Access users to send voice mail messages to other UM-enabled users who are associated with the same dial plan, or prevent them from doing so.

By default, this setting is enabled. If you disable this setting, Outlook Voice Access users that call into an Outlook Voice Access number won’t be able to send voice messages to users within the same dial plan.

For additional tasks related to UM dial plans, see [UM dial plan procedures](um-dial-plan-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM dial plans" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to enable or prevent Outlook Voice Access users sending voice messages to users in the same dial plan

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**.

2.  In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM dial plan** page, click **Configure**.

4.  In **Transfer & search**, under **Allow callers to**, select **Leave voice messages without ringing a user’s phone** to allow sending voice messages. If you want to prevent sending voice messages for users, clear this setting.

5.  Click **Save**.

## Use the Shell to enable or prevent Outlook Voice Access users sending voice messages to users in the same dial plan

This example enables Outlook Voice Access users associated with the UM dial plan named `MyUMDialPlan` to send voice messages to users associated with the same dial plan.

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $true

This example prevents Outlook Voice Access users associated with the UM dial plan named `MyUMDialPlan` from sending voice messages to users associated with the same dial plan.

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $false

