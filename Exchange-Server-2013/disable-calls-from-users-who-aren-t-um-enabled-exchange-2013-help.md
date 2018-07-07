---
title: "Disable calls from users who aren't UM-enabled: Exchange 2013 Help"
TOCTitle: Disable calls from users who aren't UM-enabled
ms:assetid: 272ff4ab-b4d9-4647-98e2-7c171f9dfc3f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673516(v=EXCHG.150)
ms:contentKeyID: 49315376
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Disable calls from users who aren't UM-enabled

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can enable or disable calls from users who aren't enabled for Unified Messaging (UM). By default, Unified Messaging allows incoming calls from unauthenticated callers through an auto attendant to be transferred to UM-enabled users. With this setting enabled, users from outside an organization can transfer calls to UM-enabled users.

If this setting has been disabled for a UM-enabled user, the user's mailbox can still be located using a directory search. However, if an external caller tries to transfer to the user, the system says, "I'm sorry, I am unable to transfer the call to this user." The caller is then transferred to the operator, if an operator has been configured on the auto attendant. If no operator has been configured on the auto attendant, the call is transferred to a dial plan operator, if one has been configured. If no operator extension has been configured on the speech-enabled auto attendant, the dual tone multi-frequency (DTMF) fallback auto attendant, or the dial plan, the system responds by saying, "Sorry. Neither the operator nor the touchtone service are available."

For additional management tasks related to users who are enabled for voice mail, see [Voice mail-enabled user procedures](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailboxes" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform this procedure, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform this procedure, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Before you perform this procedure, confirm that the user's mailbox has been UM-enabled. For detailed steps, see [Enable a user for voice mail](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Use the Shell to disable calls from users who aren't UM-enabled

This example prevents Tony Smith from receiving voice calls from callers who aren't UM-enabled.

    Set UMMailbox -Identity tony@contoso.com -AllowUMCallsFromNonUsers None

