---
title: 'Manage recipient filtering on Edge Transport servers: Exchange 2013 Help'
TOCTitle: Manage recipient filtering on Edge Transport servers
ms:assetid: f2d0041f-2872-4669-95ec-443233f4956d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb125187(v=EXCHG.150)
ms:contentKeyID: 49287411
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Manage recipient filtering on Edge Transport servers

 

_**Applies to:** Exchange Server 2013_


Recipient filtering is provided by the Recipient Filter agent. When recipient filtering is enabled on an Exchange server, it filters inbound messages that come from the Internet but aren't authenticated. These messages are handled as external messages.


> [!NOTE]
> Although the Recipient Filter agent is available on Mailbox servers, you shouldn't configure it. When recipient filtering on a Mailbox server detects one invalid or blocked recipient in a message that contains other valid recipients, the message is rejected. If you install the anti-spam agents on a Mailbox server, the Recipient Filter agent is enabled by default. However, it isn't configured to block any recipients. For more information, see <A href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Enable anti-spam functionality on Mailbox servers</A>.



## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Anti-spam features" entry in the [Anti-spam and anti-malware permissions](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) topic.

  - You can only use the Shell to perform this procedure.

  - By default, anti-spam features aren't enabled in the Transport service on a Mailbox server. Typically, you only enable the anti-spam features on a Mailbox server if your Exchange organization doesn't do any prior anti-spam filtering before accepting incoming messages. For more information, see [Enable anti-spam functionality on Mailbox servers](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - The *AddressBookEnabled* parameter on the **Set-AcceptedDomain** cmdlet enables or disables recipient filtering for recipients in an accepted domain. By default, recipient filtering is enabled for authoritative domains, and disabled for internal relay domains and external relay domains. To view the status of the *AddressBookEnabled* parameter for the accepted domains in your organization, run the following command:
    
        Get-AcceptedDomain | Format-List Name,AddressBookEnabled

  - If you disable recipient filtering using the procedure in this topic, recipient filtering functionality will be disabled, but the underlying Recipient Filter agent will remain enabled.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to enable or disable recipient filtering

To disable recipient filtering, run the following command:

    Set-RecipientFilterConfig -Enabled $false

To enable recipient filtering, run the following command:

    Set-RecipientFilterConfig -Enabled $true


> [!NOTE]
> When you disable recipient filtering, the underlying Recipient Filter agent is still enabled. To disable the Recipient Filter agent, run the command: <CODE>Disable-TransportAgent "Recipient Filter Agent"</CODE>.



## How do you know this worked?

To verify that you have successfully enabled or disabled recipient filtering, do the following:

1.  Run the following command:
    
        Get-RecipientFilterConfig | Format-List Enabled

2.  Verify the value displayed is the value you configured.

## Use the Shell to enable or disable the Recipient Block list

Run the following command:

    Set-RecipientFilterConfig -BlockListEnabled <$true | $false>

This example enables the Recipient Block list:

    Set-RecipientFilterConfig -BlockListEnabled $true

## How do you know this worked?

To verify that you have successfully enabled or disabled the Recipient Block list, do the following:

1.  Run the following command:
    
        Get-RecipientFilterConfig | Format-List BlockListEnabled

2.  Verify the value displayed is the value you configured.

## Use the Shell to configure the Recipient Block list

To replace the existing values, run the following command:

    Set-RecipientFilterConfig -BlockedRecipients <recipient1,recipient2...>

This example configures the Recipient Block list with the valuesmark@contoso.com and kim@contoso.com:

    Set-RecipientFilterConfig -BlockedRecipients mark@contoso.com,kim@contoso.com

To add or remove entries without modifying any existing values, run the following command:

    Set-RecipientFilterConfig -BlockedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...}

This example adds chris@contoso.com to the list of recipients, and removes michelle@contoso.com from the list of recipients in the Recipient Block list:

    Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"; Remove="michelle@contoso.com"}

## How do you know this worked?

To verify that you have successfully configured the Recipient Block list, do the following:

1.  Run the following command:
    
        Get-RecipientFilterConfig | Format-List BlockedRecipients

2.  Verify the values displayed are the values you configured.

## Use the Shell to enable or disable Recipient Lookup

Run the following command:

    Set-RecipientFilterConfig -RecipientValidationEnabled <$true | $false>

To block messages to recipients that don't exist in your organization, run the following command:

    Set-RecipientFilterConfig -RecipientValidationEnabled $true

## How do you know this worked?

To verify that you have successfully enabled or disabled Recipient Lookup, do the following:

1.  Run the following command:
    
        Get-RecipientFilterConfig | Format-List RecipientValidationEnabled

2.  Verify the value displayed is the value you configured.

