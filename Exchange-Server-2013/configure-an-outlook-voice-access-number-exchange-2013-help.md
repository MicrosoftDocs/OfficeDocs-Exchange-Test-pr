---
title: 'Configure an Outlook Voice Access number: Exchange 2013 Help'
TOCTitle: Configure an Outlook Voice Access number
ms:assetid: 443c838e-f266-4893-b6b2-e5fc96579b55
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997680(v=EXCHG.150)
ms:contentKeyID: 49315403
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure an Outlook Voice Access number

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


An Outlook Voice Access number lets a user who is enabled for Unified Messaging (UM) and voice mail access their mailbox using Outlook Voice Access. When you configure an Outlook Voice Access or subscriber access number on a dial plan, UM-enabled users can call in to the number, sign in to their mailbox, and access their email, voice mail, calendar, and personal contact information.

By default, when you create a UM dial plan, an Outlook Voice Access number isn't configured. To configure an Outlook Voice Access number, you first need to create the dial plan, and then configure an Outlook Voice Access number under the dial plan's **Outlook Voice Access** option. Although an Outlook Voice Access number isn't required, you need to configure at least one Outlook Voice Access number to enable a UM-enabled user to use Outlook Voice Access to access their mailbox. You can configure multiple Outlook Voice Access numbers for a single dial plan.

Outlook Voice Access numbers can contain alphabetical, numeric, and special characters, separators, and spaces. For example:

  - \+14255551010

  - \+1-425-555-1010

  - 4255551010

  - \+1 425 555 1010

  - 1-800-555-CALL

For more information about the menu options available for Outlook Voice Access users, see the Quick Reference Guide for Outlook Voice Access, which is available from the [Microsoft Download Center](https://go.microsoft.com/fwlink/p/?linkid=64645).

For additional management tasks related to UM dial plans, see [UM dial plan procedures](um-dial-plan-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM dial plans" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to configure an Outlook Voice Access number

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**.

2.  In the list view, select the UM dial plan you want to modify and on the toolbar, click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM dial plan** page, click **Configure**.

4.  In **Outlook Voice Access**, under **Outlook Voice Access numbers**, use the box to enter the number you want to use, and then click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

5.  Click **Save**.

## Use the Shell to configure an Outlook Voice Access number

This example sets the Outlook Voice Access number to 4255550100 for a UM dial plan named `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AccessTelephoneNumbers 4255550100

