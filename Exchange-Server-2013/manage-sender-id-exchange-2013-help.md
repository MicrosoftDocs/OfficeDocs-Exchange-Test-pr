---
title: 'Manage Sender ID: Exchange 2013 Help'
TOCTitle: Manage Sender ID
ms:assetid: 2e7b646a-8a66-4be7-a7c1-0bd43bb79a5b
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997136(v=EXCHG.150)
ms:contentKeyID: 49287404
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Manage Sender ID

 

_**Applies to:** Exchange Server 2013_


Sender ID functionality is provided by the Sender ID agent. Sender ID validates the origin of email messages by verifying the IP address of the sender against the purported owner of the sender domain. Sender ID filtering is performed on inbound messages that come from the Internet but aren't authenticated. These messages are handled as external messages.

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Anti-spam features" entry in the [Anti-spam and anti-malware permissions](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) topic.

  - You can only use the Shell to perform this procedure.

  - By default, anti-spam features aren't enabled in the Transport service on a Mailbox server. Typically, you only enable the anti-spam features on a Mailbox server if your Exchange organization doesn't do any prior anti-spam filtering before accepting incoming messages. For more information, see [Enable anti-spam functionality on Mailbox servers](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to enable or disable Sender ID

To disable Sender ID, run the following command:

    Set-SenderIDConfig -Enabled $false

To enable Sender ID, run the following command:

    Set-SenderIDConfig -Enabled $true


> [!NOTE]
> When you disable Sender ID, the underlying Sender ID agent is still enabled. To disable the Sender ID agent, run the command: <CODE>Disable-TransportAgent "Sender ID Agent"</CODE>.



## How do you know this worked?

To verify that you have successfully enabled or disabled Sender ID, do the following:

1.  Run the following command:
    
        Get-SenderIDConfig | Format-List Enabled

2.  Verify the value displayed is the value you configured.

## Use the Shell to configure the Sender ID action for spoofed messages

To configure the Sender ID action for spoofed messages, run the following command:

    Set-SenderIDConfig -SpoofedDomainAction <StampStatus | Reject | Delete>

This example configures the Sender ID agent to reject any messages where the IP address of the sending server isn't listed as an authoritative SMTP sending server in the DNS Sender Policy Framework (SPF) record for the sending domain.

    Set-SenderIDConfig -SpoofedDomainAction Reject

## How do you know this worked?

To verify that you have successfully configured the Sender ID action for spoofed messages, do the following:

1.  Run the following command:
    
        Get-SenderIDConfig | Format-List SpoofedDomainAction

2.  Verify the value displayed is the value you configured.

## Use the Shell to configure the Sender ID action for transient errors

To configure the Sender ID action for transient errors, run the following command:

    Set-SenderIDConfig -TempErrorAction <StampStatus | Reject | Delete>

This example configures the Sender ID agent to stamp the messages when the Sender ID status can't be determined due to a temporary DNS server error. The message will be processed by other anti-spam agents and the Content Filter agent will use the mark when determining the SCL value for the message.

    Set-SenderIDConfig -TempErrorAction StampStatus

Note that `StampStatus` is the default value for the *TempErrorAction* parameter.

## How do you know this worked?

To verify that you have successfully configured the Sender ID action for transient errors, do the following:

1.  Run the following command:
    
        Get-SenderIDConfig | Format-List TempErrorAction

2.  Verify the value displayed is the value you configured.

## Use the Shell to configure recipient and sender domain exceptions

To replace the existing values, run the following command:

    Set-SenderIDConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenderDomains <domain1,domain2...>

This example configures the Sender ID agent to bypass the Sender ID check for messages sent to kim@contoso.com and john@contoso.com, and to bypass the Sender ID check for messages sent from the fabrikam.com domain.

    Set-SenderIDConfig -BypassedRecipients kim@contoso.com,john@contoso.com -BypassedSenderDomains fabrikam.com

To add or remove entries without modifying any existing values, run the following command:

    Set-SenderIDConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

This example configures the Sender ID agent with the following information:

  - Add chris@contoso.com and michelle@contoso.com to the list of existing recipients who bypass the Sender ID check.

  - Remove tailspintoys.com from the list of existing domains that bypass the Sender ID check.

<!-- end list -->

    Set-SenderIDConfig -BypassedRecipients @{Add="chris@contoso.com","michelle@contoso.com"} -BypassedSenderDomains @{Remove="tailspintoys.com"}

## How do you know this worked?

To verify that you have successfully configured recipient and sender domain exceptions, do the following:

1.  Run the following command:
    
        Get-SenderIDConfig | Format-List BypassedRecipients,BypassedSenderDomains

2.  Verify the values displayed are the values you configured.

