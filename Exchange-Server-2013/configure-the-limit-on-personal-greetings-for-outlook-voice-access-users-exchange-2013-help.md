---
title: 'Configure the limit on personal greetings for Outlook Voice Access users: Exchange 2013 Help'
TOCTitle: Configure the limit on personal greetings for Outlook Voice Access users
ms:assetid: d400f250-0f55-45f5-9918-5f1d7819fbdf
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb201731(v=EXCHG.150)
ms:contentKeyID: 49315531
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure the limit on personal greetings for Outlook Voice Access users

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


The **Limit on personal greetings (minutes)** setting enables you to enter the maximum number of minutes that users associated with the Unified Messaging (UM) mailbox policy can use to record their voice mail greetings. This setting applies to both their standard voice mail and their Out of Office voice mail greetings. By default, the maximum greeting duration is set to 5 minutes. However, you can configure the maximum greeting duration to any setting between 1 and 10 minutes.

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

## Use the EAC to change the maximum greeting duration

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to modify, and then on the toolbar, click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Mailbox Policies**, select the UM mailbox policy you want to manage, and then on the toolbar, click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM mailbox policy** page \> **General**, under **Limit on personal greetings (minutes)**, enter the length of time, in minutes, allowed for personal greetings for voice mail users.

4.  Click **Save**.

## Use the Shell to change the maximum greeting duration

This example configures the maximum greeting duration on the UM mailbox policy `MyUMMailboxPolicy` to 3 minutes.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy MaxGreetingDuration 3

