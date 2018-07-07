---
title: 'Enable or disable Outlook Voice Access for users: Exchange 2013 Help'
TOCTitle: Enable or disable Outlook Voice Access for users
ms:assetid: c0c244a0-ad2f-4adf-bc1f-1d55fd7ea2d5
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd351106(v=EXCHG.150)
ms:contentKeyID: 49315514
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Enable or disable Outlook Voice Access for users

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can enable or disable access to Outlook Voice Access for UM-enabled users who are associated with a Unified Messaging (UM) mailbox policy. Outlook Voice Access is a feature used by UM-enabled users to access their mailbox over a phone. By default, this setting is enabled.

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

## Use the EAC to enable or disable Outlook Voice Access

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  Under **UM Mailbox Policies**, select the UM mailbox policy you want to manage, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Mailbox Policy** page, select or clear the check box next to **Allow Outlook Voice Access**.

4.  Click **Save**.

## Use the Shell to enable or disable Outlook Voice Access

This example allows users who are associated with the UM mailbox policy `MyUMMailboxPolicy` to use Outlook Voice Access.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowSubscriberAccess $true

This example prevents users who are associated with the UM mailbox policy `MyUMMailboxPolicy` from using Outlook Voice Access.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowSubscriberAccess $false

