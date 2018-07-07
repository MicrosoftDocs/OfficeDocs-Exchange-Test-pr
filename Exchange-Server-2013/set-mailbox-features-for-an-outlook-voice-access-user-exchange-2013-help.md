---
title: 'Set mailbox features for an Outlook Voice Access user: Exchange 2013 Help'
TOCTitle: Set mailbox features for an Outlook Voice Access user
ms:assetid: a56bfd75-7bc5-49b9-b098-06855a720dcd
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124030(v=EXCHG.150)
ms:contentKeyID: 49315476
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Set mailbox features for an Outlook Voice Access user

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


Telephone user interface (TUI) settings are used when a user accesses the Unified Messaging (UM) system by using Outlook Voice Access. When you modify a UM-enabled user's TUI configuration settings, you modify properties and their values on the UM-enabled user's mailbox.

You can change the following TUI settings for a UM-enabled user:

  - Allow subscriber access

  - Allow TUI access to the calendar

  - Allow TUI access to email

  - Allow Automatic Speech Recognition

For additional management tasks related to UM users, see [Set mailbox features for an Outlook Voice Access user](set-mailbox-features-for-an-outlook-voice-access-user-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailboxes" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that the existing Exchange recipient is enabled for Unified Messaging and voice mail. For detailed steps, see [Enable a user for voice mail](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Use the Shell to modify a single UM-enabled user's TUI settings

This example enables calendar and email access using the TUI for a UM-enabled user named Tony Smith.

    Set-UMMailbox -Identity tony@contoso.com TUIAccessToCal True -TUIAccessToEmail True -OperatorNumber 111111 -DisableMissedCallNotification False -AnonCallBlock True


> [!NOTE]
> TUI settings for users are also available on UM mailbox policies. Modifying TUI settings on a UM mailbox policy affects all users who are associated with the UM mailbox policy. For more information about how to modify TUI settings on a UM mailbox policy, see <A href="set-mailbox-features-for-outlook-voice-access-users-exchange-2013-help.md">Set mailbox features for Outlook Voice Access users</A>.


