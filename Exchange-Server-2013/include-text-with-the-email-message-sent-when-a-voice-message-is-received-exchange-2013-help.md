---
title: 'Include text with the email message sent when a voice message Is received: Exchange 2013 Help'
TOCTitle: Include text with the email message sent when a voice message Is received
ms:assetid: b2eec29c-e5eb-4263-80d8-0b9813dd56dc
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb201718(v=EXCHG.150)
ms:contentKeyID: 49315500
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Include text with the email message sent when a voice message Is received

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can include additional text in the email message that's sent when a voice mail message is received by a user who is enabled for Unified Messaging (UM) voice mail. By default, the text that's included with a voice message indicates only that the user has received a voice message. However, you can create a custom message by adding text in the **When a user receives a voice message** box on a UM mailbox policy. For example, the text can include information about system security policies and describe the correct way to handle voice messages in your organization. After you add the text, it will be included in each email message that's sent when UM-enabled users associated with the UM mailbox policy receive a voice message.


> [!NOTE]
> The custom text that accompanies a voice message is limited to 512&nbsp;characters, and can include simple HTML text.



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

## Use the EAC to change the text included with a voice message

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Mailbox Policies**, select the UM mailbox policy you want to manage, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Mailbox Policy** page \> **Message text**, in the text box for **When a user receives a voice message**, enter the text you want to include in the email message that’s sent when users receive a voice message.

4.  Click **Save**.

## Use the Shell to change the text included with a voice message

This example includes the additional text, "Do not forward voice messages to users outside this organization", with voice messages sent to users who are associated with the UM mailbox policy named `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailText "Do not forward voice messages to users outside this organization."

