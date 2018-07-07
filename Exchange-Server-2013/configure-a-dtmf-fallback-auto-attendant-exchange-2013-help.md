---
title: 'Configure a DTMF fallback auto attendant: Exchange 2013 Help'
TOCTitle: Configure a DTMF fallback auto attendant
ms:assetid: a82d85f7-de30-40db-8ee6-b091ac14da9d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb232158(v=EXCHG.150)
ms:contentKeyID: 49315482
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure a DTMF fallback auto attendant

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can configure a speech-enabled Unified Messaging (UM) auto attendant that has a dual tone multi-frequency (DTMF) fallback auto attendant. A DTMF fallback auto attendant is used when the UM speech-enabled auto attendant can't understand or recognize the speech inputs provided by a caller. If a DTMF fallback auto attendant has been configured, the caller has to use DTMF inputs, also known as touchtone inputs, to navigate the auto attendant menu system, spell a user's name, or use a custom menu prompt. If no DTMF fallback auto attendant has been configured, and the maximum number of speech inputs is exceeded because the system didn't understand what the caller said, the system will respond with this prompt: "Sorry, I couldn't help. Please call back later."

By default, an auto attendant isn't speech-enabled when you create it. After you speech-enable the auto attendant, callers can use only voice commands to navigate the auto attendant menu system, and touchtone inputs can't be used. Although it isn't required, we recommend that you configure a DTMF fallback auto attendant for each speech-enabled auto attendant so callers can use touchtone inputs if the speech-enabled auto attendant doesn't recognize or understand the words they say. We also recommend that you don't speech-enable a DTMF fallback auto attendant.

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

## Use the EAC to configure a speech-enabled auto attendant with a DTMF fallback auto attendant

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change and click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Auto Attendants**, select the UM auto attendant for which you want to create a DTMF fallback auto attendant. On the toolbar, click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Auto Attendant** page \> **General**, select the check box next to **Use this auto attendant when voice commands don’t work correctly**, and then click **Browse**.

4.  On the **Select a UM Auto Attendant** page, select the auto attendant you want to use as a DTMF fallback auto attendant, and then click **Save**.


> [!IMPORTANT]
> You must first speech-enable the auto attendant before you can browse for a DTMF fallback auto attendant you have set up.



## Use the Shell to configure a speech-enabled auto attendant with a DTMF fallback auto attendant

This example configures a UM auto attendant named `MySpeechEnabledAA` to use a DTMF fallback auto attendant named `MyDTMFAA`.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA

