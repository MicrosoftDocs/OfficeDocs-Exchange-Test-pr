---
title: 'Configure the maximum call duration: Exchange 2013 Help'
TOCTitle: Configure the maximum call duration
ms:assetid: 01aa40d2-f918-472b-bace-158222143484
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee423535(v=EXCHG.150)
ms:contentKeyID: 49315345
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure the maximum call duration

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can specify the maximum number of minutes that an incoming call can be connected to the system without being transferred to a valid extension number before the call is ended. For most organizations, this value should be set to the default: 30 minutes. This setting applies to all calls, including incoming Outlook Voice Access calls, voice calls internal to your organization, voice calls into Unified Messaging (UM) auto attendants, and fax calls placed from outside your organization.

This value can be set to a number from 10 through 120. Setting this value too low can cause incoming calls to be disconnected before they're completed. For example, if your organization receives many large fax messages, you may want to consider increasing this value from the default so that all the pages of fax messages are received.

For additional tasks related to UM dial plans, see [UM dial plan procedures](um-dial-plan-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM dial plans" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to configure the maximum call duration

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**.

2.  In the list view, select the UM dial plan you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM dial plan** page, click **Configure**.

4.  In **Settings**, under **Maximum call duration (minutes)**, enter the number in minutes.

5.  Click **Save**.

## Use the Shell to configure the maximum call duration

This example sets the maximum call duration to 10 minutes on a UM dial plan named `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -MaxCallDuration 10

