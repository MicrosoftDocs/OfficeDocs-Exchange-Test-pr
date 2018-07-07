---
title: 'Include text with the email message sent when a fax message is received: Exchange 2013 Help'
TOCTitle: Include text with the email message sent when a fax message is received
ms:assetid: 48244e58-b7d6-4f0e-bbae-d22bf0fc11ff
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb201684(v=EXCHG.150)
ms:contentKeyID: 49315409
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Include text with the email message sent when a fax message is received

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can include additional text in the email message that's sent when a fax message is received by a user who is enabled for Unified Messaging (UM) voice mail and is fax-enabled, and when the UM mailbox policy has been configured correctly to use a fax partner provider. By default, the text included when a UM-enabled user receives a fax message indicates only that the user has received a fax message. However, you can create a custom message by adding text in the **When a user receives a fax message** box on a UM mailbox policy. For example, the text can include information about system security policies and describe the correct way to handle fax messages in your organization. After you add the text, it will be included in each email message that's sent when UM-enabled users who are associated with the UM mailbox policy receive a fax message.


> [!NOTE]
> The custom text that accompanies a fax message is limited to 512&nbsp;characters, and can include simple HTML text.



For more information about fax partners, see [Microsoft PinPoint for Fax Partners](https://go.microsoft.com/fwlink/?linkid=190238).

For additional management tasks related to faxing, see [Faxing procedures](faxing-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailbox policies" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to change the text included with a fax message

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Mailbox Policies**, select the UM mailbox policy you want to manage, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Mailbox Policy** page \> **Message text**, in the text box for **When a user receives a fax message**, enter the text you want to include in the email message that’s sent when users receive a fax message in their mailbox.

4.  Click **Save**.

## Use the Shell to change the text included with a fax message

This example enables UM-enabled users who are associated with a UM mailbox policy to receive additional instructions on how to open a fax message that they've received in their mailbox.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -FaxMessageText "To open this fax message, double-click the file attachment."

