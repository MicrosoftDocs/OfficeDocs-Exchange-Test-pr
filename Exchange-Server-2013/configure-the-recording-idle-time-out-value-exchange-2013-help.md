---
title: 'Configure the recording idle time-out value: Exchange 2013 Help'
TOCTitle: Configure the recording idle time-out value
ms:assetid: a7fb9a09-fde9-447d-ad2c-95598405e99b
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee423550(v=EXCHG.150)
ms:contentKeyID: 49315481
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure the recording idle time-out value

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can specify the number of seconds of silence that the system allows when a voice message is being recorded before the call is ended. For most organizations, this value should be set to the default of 5 seconds.

This value can be set from 2 through 10. Setting this value too low can cause the system to disconnect callers before they've finished leaving their voice messages. Setting this value too high allows lengthy silences in voice messages.

For additional management tasks related to UM dial plans, see [UM dial plan procedures](um-dial-plan-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM dial plans" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to configure the recording idle time-out value

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**.

2.  In the list view, select the UM dial plan you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM dial plan** page, click **Configure**.

4.  In **Settings**, under **Recording idle time out (seconds)**, enter the number in seconds.

5.  Click **Save**.

## Use the Shell to configure the recording idle time-out value

This example sets the recording idle time-out value to 10 for a UM dial plan named `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -RecordingIdleTimeout 10

