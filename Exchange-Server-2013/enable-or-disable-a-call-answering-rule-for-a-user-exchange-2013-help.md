---
title: 'Enable or disable a call answering rule for a user: Exchange 2013 Help'
TOCTitle: Enable or disable a call answering rule for a user
ms:assetid: f9e40ac3-117f-44f6-9ab1-dc9f4c72e8ac
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn140252(v=EXCHG.150)
ms:contentKeyID: 54010237
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Enable or disable a call answering rule for a user

 

_**Applies to:** Exchange Server 2013, Exchange Server 2016_


You can use the Shell to enable or disable one or more call answering rules for a user. You can also use the **Enable-UMCallAnsweringRule** or **Disable-UMCallAnsweringRule** cmdlets in an Exchange Management Shell script to enable or disable one or more call answering rules for multiple users.

Call answering rules are applied to incoming calls similar to the way Inbox rules are applied to incoming email messages. By default, when a user is enabled for Unified Messaging (UM), no call answering rules are configured. Even so, incoming calls are answered by the mail system and callers are prompted to leave a voice message.

For additional management tasks related to call answering rules, see [Forwarding calls procedures](forwarding-calls-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM call answering rules" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform this procedure, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform this procedure, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Before you perform this procedure, confirm that the user's mailbox has been UM-enabled. For detailed steps, see [Enable a user for voice mail](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - You can only use the Shell to perform this procedure. To learn how to open the Exchange Management Shell in your on-premises Exchange organization, see [Open the Shell](https://technet.microsoft.com/en-us/library/dd638134\(v=exchg.150\)). To learn how to use Windows PowerShell to connect to Exchange Online, see [Connect to Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the Shell to enable a call answering rule

When a call answering rule is created, it's enabled. You can use the Shell to enable a call answering rule that was previously disabled. Enabling a call answering rule enables the **Enable-UMCallAnsweringRule** cmdlet to retrieve the call answering rule, including the conditions and actions for a specified call answering rule.

This example enables the call answering rule `MyUMCallAnsweringRule` in the mailbox for Tony Smith.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

The example uses the *WhatIf* switch to test whether the call answering rule `MyUMCallAnsweringRule` in the mailbox for Tony Smith is ready to be enabled and if there are any errors within the command.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

This example enables the call answering rule `MyUMCallAnsweringRule` in the mailbox for Tony Smith and prompts the signed-in user to confirm that the call answering rule is to be enabled.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm

## Use the Shell to disable a call answering rule

Disabling a call answering rule prevents it from being retrieved and processed when an incoming call is received. When you create a call answering rule, you should disable it while you're setting up conditions and actions. This prevents the call answering rule from being processed when an incoming call is received before you've correctly configured the call answering rule.

This example disables the call answering rule `MyUMCallAnsweringRule` in the mailbox for Tony Smith.

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

This example uses the *WhatIf* switch to test whether the call answering rule `MyUMCallAnsweringRule` in the mailbox for Tony Smith is ready to be disabled and if there are any errors within the command.

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

This example disables the call answering rule `MyUMCallAnsweringRule` in the mailbox for Tony Smith and prompts the signed-in user to confirm that they're disabling the call answering rule.

    Disable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm

