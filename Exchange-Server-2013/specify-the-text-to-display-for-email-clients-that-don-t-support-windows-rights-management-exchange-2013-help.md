---
title: "Specify the text to display for email clients that don't support Windows Rights Management: Exchange 2013 Help"
TOCTitle: Specify the text to display for email clients that don't support Windows Rights Management
ms:assetid: a9b2238a-b534-469c-a0c3-2768bc3d005b
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee423552(v=EXCHG.150)
ms:contentKeyID: 49315487
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Specify the text to display for email clients that don't support Windows Rights Management

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can specify the text that will be sent to a user when they receive a protected voice message but their email client doesn't support Information Rights Management (IRM) or Windows Rights Management.

Protected Voice Mail can be accessed only by email clients that support Windows Rights Management or when a UM–enabled user uses Outlook Voice Access to access a protected voice message.

Protected Voice Mail is encrypted. When a voice message is protected:

  - The message is marked as Private in Microsoft Outlook and Outlook Web App.

  - The voice message can be opened only by the intended recipient of the voice message.

  - The recipient can reply to the voice message, but can't forward it to someone who wasn't included on the original voice message.

If a protected voice message is sent to someone whose email client doesn't support Windows Rights Management and isn't accessing the message using Outlook Voice Access, an email message will be sent to them that includes the text you specify. This text should include instructions about what the called party should do to be able to receive the protected voice message.

For additional management tasks related to Protected Voice Mail procedures, see [Protected Voice Mail procedures](protected-voice-mail-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailbox policies" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use EAC to specify the text to display for email clients that don't support Windows Rights Management

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Mailbox Policies**, select the UM mailbox policy you want to manage, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Mailbox Policy** page \> **Protected voice mail**, under **Message to send to users who don’t have Windows Rights Management support**, type the message text in the text box.

4.  Click **Save**.

## Use the Shell to specify the text to display for email clients that don't support Windows Rights Management

This example specifies the text to display to users associated with the UM mailbox policy named `MyUMMailboxPolicy` who have email clients that don't support Windows Rights Management.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectedVoiceMailText "Your email client software does not support Protected Voice Mail. Please contact the Help Desk."

