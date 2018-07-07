---
title: 'Manage sender filtering: Exchange 2013 Help'
TOCTitle: Manage sender filtering
ms:assetid: a7f4b3e1-2970-45ad-911e-a9f46d880d3d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124087(v=EXCHG.150)
ms:contentKeyID: 49287406
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Manage sender filtering

 

_**Applies to:** Exchange Server 2013_


Sender filtering is provided by the Sender Filter agent. The Sender Filter agent relies on the **MAIL FROM:** SMTP header to determine what action, if any, to take on an inbound email message.

When sender filtering functionality is enabled on an Exchange server, sender filtering functionality filters all messages that come through all Receive connectors on that computer.

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Anti-spam features" entry in the [Anti-spam and anti-malware permissions](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) topic.

  - You can only use the Shell to perform this procedure.

  - By default, anti-spam features aren't enabled in the Transport service on a Mailbox server. Typically, you only enable the anti-spam features on a Mailbox server if your Exchange organization doesn't do any prior anti-spam filtering before accepting incoming messages. For more information, see [Enable anti-spam functionality on Mailbox servers](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to enable or disable sender filtering

To disable sender filtering, run the following command:

    Set-SenderFilterConfig -Enabled $false

To enable sender filtering, run the following command:

    Set-SenderFilterConfig -Enabled $true


> [!NOTE]
> When you disable sender filtering, the underlying Sender Filter agent is still enabled. To disable the Sender Filter agent, run the command: <CODE>Disable-TransportAgent "Sender Filter Agent"</CODE>.



## How do you know this worked?

To verify that you have successfully enabled or disabled sender filtering, do the following:

1.  Run the following command:
    
        Get-SenderFilterConfig | Format-List Enabled

2.  Verify the value displayed is the value you configured.

## Use the Shell to configure blocked senders and domains

To replace the existing values, run the following command:

    Set-SenderFilterConfig -BlockedSenders <sender1,sender2...> -BlockedDomains <domain1,domain2...> -BlockedDomainsAndSubdomains <domain1,domain2...>

This example configures the Sender Filter agent to block messages from kim@contoso.com and john@contoso.com, messages from the fabrikam.com domain, and messages from northwindtraders.com and all its subdomains.

    Set-SenderFilterConfig -BlockedSenders kim@contoso.com,john@contoso.com -BlockedDomains fabrikam.com -BlockedDomainsAndSubdomains northwindtraders.com

To add or remove entries without modifying any existing values, run the following command:

    Set-SenderFilterConfig -BlockedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BlockedDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...} -BlockedDomainsAndSubdomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

This example configures the Sender Filter agent with the following information:

  - Add chris@contoso.com and michelle@contoso.com to the list of existing senders who are blocked.

  - Remove tailspintoys.com from the list of existing sender domains that are blocked.

  - Add blueyonderairlines.com to the list of existing sender domains and subdomains that are blocked.

<!-- end list -->

    Set-SenderFilterConfig -BlockedSenders @{Add="chris@contoso.com","michelle@contoso.com"} -BlockedDomains @{Remove="tailspintoys.com"} -BlockedDomainsAndSubdomains @{Add="blueyonderairlines.com"}

## How do you know this worked?

To verify that you have successfully configured blocked senders, do the following:

1.  Run the following command:
    
        Get-SenderFilterConfig | Format-List BlockedSenders,BlockedDomains,BlockedDomainsAndSubdomains

2.  Verify the values displayed are the values you configured.

## Use the Shell to enable or disable blocking messages with blank senders

To enable or disable blocking message with blank senders, run the following command:

    Set-SenderFilterConfig -BlankSenderBlockingenabled <$true | $false>

This example configures the Sender Filter agent to block messages that don't specify a sender in the MAIL FROM: SMTP command:

    Set-SenderFilterConfig -BlankSenderBlockingEnabled $true

## How do you know this worked?

To verify that you have successfully enabled or disabled blocking messages with blank senders, do the following:

1.  Run the following command:
    
        Get-SenderFilterConfig | Format-List BlankSenderBlockingEnabled

2.  Verify the value displayed is the value you configured.

