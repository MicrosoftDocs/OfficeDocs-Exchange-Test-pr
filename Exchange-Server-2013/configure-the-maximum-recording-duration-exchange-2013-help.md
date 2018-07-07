---
title: 'Configure the maximum recording duration: Exchange 2013 Help'
TOCTitle: Configure the maximum recording duration
ms:assetid: 18eeb567-1048-4c82-93cf-612cb12ec5e3
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee423539(v=EXCHG.150)
ms:contentKeyID: 49315365
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure the maximum recording duration

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can specify the maximum number of minutes allowed for each voice recording when a caller leaves a voice mail message. This value can be set to a number from 1 through 100. For most organizations, this value should be set to the default of 20 minutes. Setting this value too low can cause long voice messages to be disconnected before they're completed. Setting this value too high lets users save lengthy voice messages in their Inboxes.

This setting is important if you've implemented strict disk quotas for users. It must be set to a lower value than the one set for **Maximum call duration (minutes)**.

For additional tasks related to UM dial plans, see [UM dial plan procedures](um-dial-plan-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM dial plans" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to configure the maximum recording duration

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**.

2.  In the list view, select the UM dial plan you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM dial plan** page, click **Configure**.

4.  In **Settings**, under **Maximum recording duration (minutes)**, enter the number in minutes.

5.  Click **Save**.

## Use the Shell to configure the maximum recording duration

This example sets the maximum recording duration to 10 minutes for a UM dial plan named `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -MaxRecordingDuration 10

