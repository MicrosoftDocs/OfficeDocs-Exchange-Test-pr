---
title: 'Configure the number of input failures before Outlook Voice Access users are disconnected: Exchange 2013 Help'
TOCTitle: Configure the number of input failures before Outlook Voice Access users are disconnected
ms:assetid: 64c13d17-a26a-4c9b-b495-bd69c716456a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee423547(v=EXCHG.150)
ms:contentKeyID: 49315429
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure the number of input failures before Outlook Voice Access users are disconnected

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can configure the number of times that users who call in to an Outlook Voice Access number can enter incorrect data before they're disconnected. This setting applies to both Outlook Voice Access users and unauthenticated callers who use directory search.

The following are examples of types of data that are considered incorrect:

  - A caller requests an extension number that isn't found in the system.

  - The system can't locate the user's extension number to transfer the call.

  - A caller presses a menu option that isn't valid.

The value of this setting can be from 1 through 20. For most organizations, this value should be set to the default of three attempts. Setting this value too low may prematurely disconnect callers.

For additional management tasks related to UM dial plans, see [UM dial plan procedures](um-dial-plan-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM dial plans" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to configure the input failures before disconnect

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**.

2.  In the list view, select the UM dial plan you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM dial plan** page, click **Configure**.

4.  In **Settings**, under **Number of input failures before disconnecting**, enter the number of input failures.

5.  Click **Save**.

## Use the Shell to configure the input failures before disconnect

This example sets the input failures before disconnect to 5 on a UM dial plan named `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -InputFailuresBeforeDisconnect 5

