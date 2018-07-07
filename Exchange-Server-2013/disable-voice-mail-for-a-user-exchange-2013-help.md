---
title: 'Disable voice mail  for a user: Exchange 2013 Help'
TOCTitle: Disable voice mail  for a user
ms:assetid: cecc9c0d-377d-489e-9db4-d487e9c0b552
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124691(v=EXCHG.150)
ms:contentKeyID: 49315525
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Disable voice mail for a user

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can disable Unified Messaging (UM) for a UM-enabled user. When you do this, the user can no longer use the voice mail features found in Unified Messaging. If you prefer, when you disable UM for a user, you can keep the UM settings for the user.

For additional management tasks related to users who are enabled for voice mail, see [Voice mail-enabled user procedures](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailboxes" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform this procedure, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform this procedure, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Before you perform these procedures, confirm that the existing user is currently enabled for Unified Messaging. For detailed steps, see [Enable a user for voice mail](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to disable Unified Messaging and voice mail for a user

1.  In the EAC, click **Recipients**.

2.  In the list view, select the user whose mailbox you want to disable for Unified Messaging.

3.  In the Details pane, under **Phone and Voice Features**, under **Unified Messaging**, click **Disable**.

4.  In the **Warning** box, click **Yes** to confirm that Unified Messaging will be disabled for the user.

## Use the Shell to disable Unified Messaging and voice mail for a user

This example disables Unified Messaging and voice mail for the user tonysmith@contoso.com, but keeps the UM mailbox settings.

    Disable-UMMailbox -Identity tonysmith@contoso.com -KeepProperties $True

