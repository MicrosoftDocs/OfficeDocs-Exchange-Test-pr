---
title: 'Set Outlook Voice Access PIN policies: Exchange 2013 Help'
TOCTitle: Set Outlook Voice Access PIN policies
ms:assetid: 5b2800b7-bfa6-4282-975c-0706ae25ad64
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998285(v=EXCHG.150)
ms:contentKeyID: 49315427
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Set Outlook Voice Access PIN policies

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can set PIN policies on a Unified Messaging (UM) mailbox policy. UM mailbox policies can be configured to increase the level of security for UM-enabled users that use Outlook Voice Access by requiring users to comply with the predefined PIN policies for your organization.

To set PIN policies for Outlook Voice Access users, you can either create a new UM mailbox policy or modify an existing UM mailbox policy. After a new UM mailbox policy is created, you can then configure the UM mailbox policy by configuring the following PIN settings:

  - `MinPasswordLength`

  - `PINLifetime`

  - `LogonFailuresBeforePINReset`

  - `MaxLogonAttempts`

  - `AllowCommonPatterns`

  - `PINHistoryCount`

It's a security best practice to implement strong PIN requirements for UM users. This can be enforced by creating UM PIN policies that require 6 or more digits for PINs and increase the level of security for your network.

When you change the PIN policy, the new PIN setting is applied to users who are currently associated with the UM mailbox policy. For example, if you modify the UM mailbox policy and change the minimum PIN length from 7 to 10 digits, the next time users log on they'll be forced to change their PIN to comply with the changed PIN requirement.

For additional tasks related to Outlook Voice Access PIN security, see [PIN security procedures](pin-security-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailbox policies" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to set PIN policies for Outlook Voice Access users

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, click the UM dial plan you want to edit, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Mailbox Policies**, select the UM mailbox policy you want to edit, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  Click **Properties**.

4.  On the **UM mailbox policy** page, click **PIN policies**.

5.  On the **PIN Policies** page, configure the PIN settings for the Outlook Voice Access users associated with this UM mailbox policy, and then click **Save**.

## Use the Shell to set PIN policies for Outlook Voice Access users

This example sets the PIN settings for users associated with the UM mailbox policy `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

