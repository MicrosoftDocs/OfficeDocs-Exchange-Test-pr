---
title: 'Enable or prevent transferring calls from Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Enable or prevent transferring calls from Outlook Voice Access
ms:assetid: b80c57f1-394c-4608-8ad3-52a3e6d697db
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee423554(v=EXCHG.150)
ms:contentKeyID: 49315507
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Enable or prevent transferring calls from Outlook Voice Access

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can enable Outlook Voice Access users to transfer calls to a user who's associated with a Unified Messaging (UM) dial plan, or prevent them from doing so. By default, both this option and the **Leave voice messages without ringing a user’s phone** option are enabled, so that Outlook Voice Access users can transfer calls to users in the same UM dial plan and leave voice messages for them. This setting only applies to Outlook Voice Access users who have entered their PIN and are authenticated.

For additional tasks related to UM dial plans, see [UM dial plan procedures](um-dial-plan-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM dial plans" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to enable or prevent Outlook Voice Access users from transferring calls

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan that you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, click **Configure**.

3.  In **transfer & search**, under **Allow callers to**, select the check box next to **transfer to users** to enable callers to transfer calls to other users within the dial plan. If you want to prevent Outlook Voice Access users from transferring calls to users, clear this check box.

4.  Click **Save**.

## Use the Shell to enable or prevent Outlook Voice Access users from transferring calls

This example enables Outlook Voice Access users to transfer calls to users in the same dial plan on a UM dial plan named `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $true

This example prevents Outlook Voice Access users from transferring calls to users in the same dial plan on a UM dial plan named `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $false

