---
title: 'Include text with the email message sent when a PIN Is reset: Exchange 2013 Help'
TOCTitle: Include text with the email message sent when a PIN Is reset
ms:assetid: f7a4d775-a588-412f-ac2c-11ab1a5c67eb
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb201750(v=EXCHG.150)
ms:contentKeyID: 49315563
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Include text with the email message sent when a PIN Is reset

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can include additional text in the email message that's sent to users when their Unified Messaging (UM) or voice mail PIN is reset. You do this by entering custom text in the **When a user’s Outlook Voice Access PIN is reset** box on a UM mailbox policy. The customized text can include, for example, security-related information for UM-enabled users.

By default, a PIN used for Outlook Voice Access is reset by the Unified Messaging or voice mail system if the number of failed sign-in attempts exceeds 5. Users can also reset their PINs using the UM features included with Outlook Web App or Outlook 2010 or later, or by using Outlook Voice Access from a telephone.


> [!NOTE]
> The text you enter in this box is limited to 512&nbsp;characters, and can include simple HTML text.



For additional tasks related to Outlook Voice Access PIN security, see [PIN security procedures](pin-security-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailbox policies" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to add text to the email message sent to users when their PIN is reset

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Mailbox Policies**, select the UM mailbox policy you want to manage, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Mailbox Policy** page \> **Message text**, in the text box for **When a user’s Outlook Voice Access PIN is reset**, enter the text you want to include in the email message that’s sent when a user’s PIN is reset.

4.  Click **Save**.

## Use the Shell to add text to the email message sent to users when their PIN is reset

This example includes the additional text, "Do not share your PIN with other users. Doing so may result in disciplinary action", in the email message sent to users who are associated with the UM mailbox policy `MyUMMailboxPolicy` when their PIN is reset.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ResetPINText "Do not share your PIN with other users. Doing so may result in disciplinary action."

