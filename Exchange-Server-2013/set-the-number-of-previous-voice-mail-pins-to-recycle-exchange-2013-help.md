﻿---
title: 'Set the number of previous voice mail PINs to recycle: Exchange 2013 Help'
TOCTitle: Set the number of previous voice mail PINs to recycle
ms:assetid: b094e68e-c493-4576-a6b1-4c780e635405
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124254(v=EXCHG.150)
ms:contentKeyID: 49315496
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Set the number of previous voice mail PINs to recycle

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


When Outlook Voice Access users dial in to an Outlook Voice Access number, they're prompted to enter their PIN so that the voice mail system can authenticate them. After they're authenticated, they can access the voice mail, email, calendaring, and personal contact information in their mailbox from any telephone.

Several PIN-related settings can be configured on a Unified Messaging (UM) mailbox policy. The **PIN recycle count** setting specifies the number of unique PINs users must use before they can reuse an old PIN. You can set the value of this setting between 1 and 20. For most organizations, this value should be set to 5 PINs, which is the default. Setting this value too high can frustrate users because it can be difficult for users to create and memorize many PINs. Setting it too low may introduce a security threat to your network.


> [!IMPORTANT]
> The PIN recycle count can't be disabled.



For additional tasks related to Outlook Voice Access PIN security, see [PIN security procedures](pin-security-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailbox policies" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to change the PIN recycle count

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**.

2.  In the list view, select the dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM dial plan** page, under **UM Mailbox Policies**, select the UM mailbox policy you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

4.  Click **PIN policies**, and next to **PIN recycle count**, enter a value between 1 and 20.

5.  Click **Save**.

## Use the Shell to change the PIN recycle count

This example sets the PIN recycle count on the UM mailbox policy `MyUMMailboxPolicy` to 10.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINHistoryCount 10

