---
title: 'Manage DSN messages: Exchange 2013 Help'
TOCTitle: Manage DSN messages
ms:assetid: 23c9d844-6fc7-44c9-a308-587338281611
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa996803(v=EXCHG.150)
ms:contentKeyID: 49315373
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
f1_keywords:
- change system message
- change rejection message
- change quota message
- change ndr message
---

# Manage DSN messages

 

_**Applies to:** Exchange Server 2013_


Microsoft Exchange Server 2013 uses delivery status notifications (DSN) to provide non-delivery reports (NDRs) and other status messages to message senders. You can use the built-in DSNs, or you can create custom DSN messages to meet the needs of your organization.

## What do you need to know before you begin?

  - Estimated time to complete: 15 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "DSNs" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - You can't remove a built-in DSN message that's included with Exchange. To change a built-in DSN message, you need to create a custom DSN message for the DSN code that you want to customize. When you remove a custom DSN message, the DSN code associated with that message reverts to the built-in DSN message that's included with Exchange.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to view built-in and custom DSN messages

To view a summary list of all built-in DSN messages included with Exchange 2013, run the following command:

    Get-SystemMessage -Original

To view a summary list of all custom DSN messages in your organization, run the following command:

    Get-SystemMessage

To view detailed information for the custom DSN message for DSN code 5.1.2 that's sent to internal senders in English, run the following command:

    Get-SystemMessage En\Internal\5.1.2 | Format-List

## Use the Shell to create a custom DSN message

Run the following command:

    New-SystemMessage -Internal <$true | $false> -Language <Locale> -DSNCode <x.y.z> -Text "<DSN text>"

This example creates a custom plain text DSN message for the DSN code 5.1.2 that's sent to internal senders in English.

    New-SystemMessage -Internal $true -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

This example creates a custom plain text DSN message for the DSN code 5.1.2 that's sent to external senders in English.

    New-SystemMessage -Internal $false -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact your System Administrator for more information."

This example creates a custom HTML DSN message for the DSN code 5.1.2 that's sent to internal senders in English.

    New-SystemMessage -DSNCode 5.1.2 -Internal $true -Language En -Text 'You tried to send a message to a <B>disabled</B> mailbox. Please visit <A HREF="http://it.contoso.com">Internal Support</A> or contact &quot;InfoSec&quot; for more information.'

## How do you know this worked?

To verify that you have successfully created a custom DNS message, do the following:

1.  Run the following command:
    
        Get-SystemMessge -DSNCode <x.y.z> | Format-List Name,Internal,Text,Language

2.  Verify the values you see are the values you configured.

3.  Send a test message that will generate the custom DSN you configured.

## Use the Shell to change the text of a custom DSN message

To change the text of a custom DSN message the following command:

    Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> -Text "<DSN text>"

This example changes the text assigned to the custom DSN message for DSN code 5.1.2 that's sent to internal senders in English.

    Set-SystemMessage En\Internal\5.1.2 -Text "The mailbox you tried to send an e-mail message to is disabled and is no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

## How do you know this worked?

To verify that you have successfully changed the text of a custom DNS message, do the following:

1.  Run the following command: `Get-SystemMessage`.
    
        Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> | Format-List -Text

2.  Verify the value displayed is the value you configured.

## Use the Shell to remove a custom DSN message

Run the following command:

    Remove-SystemMessage <Local>\<Internal | External>\<DSNcode>

This example removes the custom DSN message for the DSN code 5.1.2 that's sent to internal senders in English.

    Remove-SystemMessage En\Internal\5.1.2

## How do you know this worked?

To verify that you have successfully removed a custom DNS message, do the following:

1.  Run the command: `Get-SystemMessage`.

2.  Verify a DSN for the locale, internal or external recipients, and DSN code you deleted isn't listed.

## Forward copies of DSN messages to the Exchange recipient mailbox

You can specify a list of DSN codes that you want to monitor by having the DSN messages copied to the mailbox of the Exchange recipient. However, by default, no mailbox is assigned to the Exchange recipient, so any messages sent to the Exchange recipient are discarded. To send copies of DSN messages to the Exchange recipient mailbox, you need to assign a mailbox to the Exchange recipient, and then specific the DSN codes you want to monitor. By default, the following DSN codes are monitored: `5.4.8`, `5.4.6`, `5.4.4`, `5.2.4`, `5.2.0`, and `5.1.4`.

## Step 1: Use the Shell to assign a mailbox to the Exchange recipient

To assign a mailbox to the Exchange recipient, perform the following steps:

1.  Due to the potentially high volume of email, consider creating a dedicated mailbox and Active Directory user account for the Exchange recipient. For more information, see [Create user mailboxes](create-user-mailboxes-exchange-2013-help.md). Otherwise, identify the existing mailbox you want to associate with the Exchange recipient.

2.  Run the following command:
    
        Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient <MailboxIdentity>
    
    For example, to assign the existing mailbox named "Contoso System Mailbox" to the Exchange recipient, run the following command:
    
        Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient "Contoso System Mailbox"

## Step 2: Specify the DSN codes you want to monitor

## Use the EAC to specify the DSN codes

1.  In the EAC, navigate to **Mail flow** \> **Receive connectors** \> **More options** ![More Options Icon](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "More Options Icon") \> **Organization transport settings** \> **Delivery**.

2.  In the **DNS codes** section, type the DSN codes you want to monitor using the format *\<x.y.z\>*, and click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"). Select an existing entry and click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon") to modify it, or click **Remove** ![Remove icon](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Remove icon") to remove it. When you are finished, click **Save**.

## Use the Shell to specify the DSN codes

To replace the existing values, run the following command:

    Set-TransportConfig -GenerateCopyOfDSNFor <x.y.z>,<x.y.z>...

This example configures the Exchange organization to forward all DSN messages that have the DSN codes 5.7.1, 5.7.2, and 5.7.3 to the Exchange recipient.

    Set-TransportConfig -GenerateCopyOfDSNFor 5.7.1,5.7.2,5.7.3

To add or remove entries without modifying any existing values, run the following command:

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="<x.y.z>","<x.y.z>"...; Remove="<x.y.z>","<x.y.z>"...}

This example adds the DSN code 5.7.5 and removes the DSN code 5.7.1 from the existing list of DSN messages that are forwarded to the Exchange recipient.

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="5.7.5"; Remove="5.7.1"}

## How do you know this worked?

To verify that you successfully configured copies of DNS messages to be sent to the mailbox of the Exchange recipient, monitor the mailbox that's associated with the Exchange recipient, and verify the DSN messages contain the DSN codes you specified.

