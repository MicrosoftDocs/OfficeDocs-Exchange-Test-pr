---
title: 'Enable or disable automatic speech recognition: Exchange 2013 Help'
TOCTitle: Enable or disable automatic speech recognition
ms:assetid: 92b3b679-b503-4068-8e88-25ec0f4537ab
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb232128(v=EXCHG.150)
ms:contentKeyID: 49315463
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Enable or disable automatic speech recognition

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can enable your Unified Messaging (UM) auto attendant for Automatic Speech Recognition (ASR). After you speech-enable a UM auto attendant, callers can respond verbally to auto attendant prompts and move through the menu system of the auto attendant. By default, an auto attendant isn't speech-enabled when you create it. After you speech-enable the auto attendant, callers can use only voice commands to navigate the auto attendant menu system, and touchtone inputs can't be used.

Although it isn't required, we recommend that you configure a dual tone multi-frequency (DTMF) fallback auto attendant for each speech-enabled auto attendant so callers can use touchtone inputs if the speech-enabled auto attendant doesn't recognize or understand the words they say. If a DTMF fallback auto attendant is configured, callers can use DTMF inputs, also known as touchtone inputs, to navigate the auto attendant menu system, spell a user's name, or use a custom menu prompt. We don't recommend that you speech-enable a DTMF fallback auto attendant.

For additional management tasks related to UM auto attendants, see [UM auto attendant procedures](um-auto-attendant-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM auto attendants" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM auto attendant has been created. For detailed steps, see [Create a UM auto attendant](create-a-um-auto-attendant-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to speech-enable a UM auto attendant

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Auto Attendants**, select the UM auto attendant you want to speech enable, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Auto Attendant** page \> **General**, select the check box next to **Set the auto attendant to respond to voice commands** to enable speech recognition. To disable automatic speech recognition, clear this check box.

4.  Click **Save**.

## Use the Shell to speech-enable a UM auto attendant

This example enables ASR on a UM auto attendant named `MySpeechEnabled AA`.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -SpeechEnabled $true

