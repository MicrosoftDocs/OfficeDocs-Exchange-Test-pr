---
title: 'Configure Voice Mail Preview partner services for users: Exchange 2013 Help'
TOCTitle: Configure Voice Mail Preview partner services for users
ms:assetid: 7bb914ca-5502-4e64-bae5-555034138d8a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ff630920(v=EXCHG.150)
ms:contentKeyID: 50873800
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure Voice Mail Preview partner services for users

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can configure a Voice Mail Preview partner on a Unified Messaging (UM) mailbox policy. After you've configured Voice Mail Preview partner settings, such as the Voice Mail Preview partner ID and Voice Mail Preview partner address, on a UM mailbox policy, the settings you configure will apply to all UM-enabled users who are linked with that mailbox policy.


> [!NOTE]
> You must use the Shell to configure a Voice Mail Preview partner.



For additional management tasks related to UM mailbox policies, see [UM mailbox policy procedures](um-mailbox-policy-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailbox policies" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## How do you do this?

## Step 1: Sign up with a partner service

To find the list of certified partners and detailed instructions for how to sign up, see [Voice Mail Preview advisor](voice-mail-preview-advisor-exchange-2013-help.md) or see the [Microsoft PinPoint](https://go.microsoft.com/fwlink/p/?linkid=281966) website. After you've signed up, the Voice Mail Preview partner will provide you a partner ID and the SMTP address to use to forward the voice messages.

In Step 2, you'll apply the Partner ID and SMTP address you acquired in Step 1 to the required UM mailbox policies.

## Step 2: Set the Voice Mail Preview partner address and ID

This example sets the Voice Mail Preview partner address to exumvmp@fabrikam.com and the Voice Mail Preview partner ID to CON123-2010 on a UM mailbox policy named *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com
    -VoiceMailPreviewPartnerAssignedID CON123-2010

## Step 3: Configure advanced Voice Mail Preview partner settings

If the partner requires custom settings, you may want to set two additional parameters for a Voice Mail Preview partner as follows:

  - *VoiceMailPreviewPartnerMaxMessageDuration*

  - *VoiceMailPreviewPartnerMaxDeliveryDelay*

This example sets the maximum message duration to 300 seconds (5 minutes) and the maximum delivery delay to 600 seconds (10 minutes) on a UM mailbox policy named *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerMaxMessageDuration 300 -VoiceMailPreviewPartnerMaxDeliveryDelay 600

## Step 4: Assign a UM-enabled user to the UM mailbox policy for a Voice Mail Preview partner

If you want to configure the Voice Mail Preview partner service for some, but not all, UM-enabled users in a UM dial plan, you must create a new UM mailbox policy and configure the partner settings. When you've finished, you can apply the new policy to selected UM-enabled users. For more information about how to assign a UM-enabled user to a UM mailbox policy, see the following topics:

  - [Assign a UM mailbox policy](assign-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/en-us/library/bb124893\(v=exchg.150\))

For more information about the Voice Mail Preview partner program, see [Voice Mail Preview advisor](voice-mail-preview-advisor-exchange-2013-help.md).

