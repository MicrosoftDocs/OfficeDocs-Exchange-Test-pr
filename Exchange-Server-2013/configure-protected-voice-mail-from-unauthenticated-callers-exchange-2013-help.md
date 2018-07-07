---
title: 'Configure Protected Voice Mail from unauthenticated callers: Exchange 2013 Help'
TOCTitle: Configure Protected Voice Mail from unauthenticated callers
ms:assetid: 106bfa0a-a0fa-4a1b-bd59-4b6df1d0d61d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd335098(v=EXCHG.150)
ms:contentKeyID: 49315355
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure Protected Voice Mail from unauthenticated callers

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can configure Unified Messaging to answer an incoming call, and then determine whether it will apply protection to voice mail messages by using encryption. When a voice mail message is protected:

  - The message is marked as Private in Microsoft Outlook and Outlook Web App.

  - The voice message can be opened only by the intended recipient of the voice message.

  - The recipient can reply to the voice message, but can't forward it to someone who wasn't included on the original voice message.

This setting applies to voice messages sent to UM-enabled users when they don't answer their phone. This setting also applies to voice messages sent directly to UM-enabled users when the caller uses a UM auto attendant.

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

## Use the EAC to configure Protected Voice Mail from unauthenticated callers

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Mailbox Policies**, select the UM mailbox policy you want to manage, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Mailbox Policy** page \> **Protected voice mail**, under **Protect voice message from unauthenticated callers**, select one of the following options:
    
      - **None**   Use this setting when you don't want protection applied to any voice messages sent to UM-enabled users.
    
      - **Private**   Use this setting when you want Unified Messaging to apply protection only to voice messages that have been marked as private by the caller.
    
      - **All**   Use this setting when you want Unified Messaging to apply protection to all voice messages, including those not marked as private.

4.  Click **Save**.

## Use the Shell to configure Protected Voice Mail from unauthenticated callers

This example protects all voice messages from all unauthenticated callers on the UM mailbox policy `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectUnauthenticatedVoiceMail -All

