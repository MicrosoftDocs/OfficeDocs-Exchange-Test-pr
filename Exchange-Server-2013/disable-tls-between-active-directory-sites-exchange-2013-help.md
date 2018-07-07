---
title: 'Disable TLS between Active Directory sites: Exchange 2013 Help'
TOCTitle: Disable TLS between Active Directory sites
ms:assetid: 1e1a0acf-24e7-4f94-9b33-603a4e0a812c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd876856(v=EXCHG.150)
ms:contentKeyID: 50934212
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Disable TLS between Active Directory sites

 

_**Applies to:** Exchange Server 2013_


Microsoft Exchange Server 2013 supports disabling TLS for SMTP communication between Mailbox servers in certain topologies where WAN Optimization Controller (WOC) devices that compress SMTP traffic are used.

This topic provides step-by-step instructions on how to configure the Transport service in your affected Mailbox servers to disable TLS, and to ensure your Active Directory routing topology is configured to correctly route messages. To learn more about this scenario, see [Scenario: Configure Exchange to support WAN Optimization Controllers](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete this task: 60 minutes.

  - Even though individual configuration steps within this scenario can be accomplished with lesser rights, to complete the entire end-to-end scenario tasks, your account needs to be a member of the Organization Management role group.

  - Make sure you disable TLS only on connections that pass through WOC devices.

  - This procedure requires that Exchange 2013 is deployed in multiple Active Directory sites, with at least one site connected to the other sites over a WAN link.

  - This procedure requires that WOC devices are deployed to compress SMTP traffic over the WAN link.

  - This procedure requires that a logical message flow path exists for Exchange going over the WAN link that has the WOC devices deployed.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Step 1: Use the Shell to configure the Transport service on the Mailbox server to use downgraded Exchange Server authentication

To configure the Transport service on a Mailbox server to use downgraded Exchange server authentication, run the following command:

    Set-TransportService <ServerIdentity> -UseDowngradedExchangeServerAuth $true

This example makes this configuration change on the server named Mailbox01.

    Set-TransportService Mailbox01 -UseDowngradedExchangeServerAuth $true

## Step 2: Create a dedicated Receive connector on the Mailbox server for the target Active Directory site

## Use the EAC to create the Receive connector

1.  In the Exchange admin center (EAC), click **Mail flow** \> **Receive connectors**, and then click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

2.  On the first page of the **New Receive connector** wizard, enter the following values
    
      - **Name**   Enter a descriptive value.
    
      - **Type**   Internal
    
    When you are finished, click **Next**.

3.  On the second page of the **New Receive connector** wizard, in the **Remote settings** section, enter the IP addresses or IP address ranges for the target Active Directory site. When you are finished, click **Finish**.

## Use the Shell to create the Receive connector

To create a Receive connector on the Mailbox server, run the following command:

    New-ReceiveConnector -Name <Name> -Server <ServerIdentity> -RemoteIPRanges <IPAddressRange> -Internal

This example creates the Receive connector named WAN on server named Mailbox01 with the following settings:

  - The *RemoteIPRanges* parameter is set to 10.0.2.0/24. This IP address range should correspond to the remote Active Directory site from where this Receive connector will receive unencrypted connections. If there's more than one IP subnet in the remote site, you can enter them all separated by commas.

  - The usage type is set to Internal.

<!-- end list -->

    New-ReceiveConnector -Name WAN -Server Hub01 -RemoteIPRanges 10.0.2.0/24 -Internal

## Step 3: Use the Shell to disable TLS on the dedicated Receive connector

To disable TLS on the Receive connector, run the following command:

    Set-ReceiveConnector <ReceiveConnectorIdentity> -SuppressXAnonymousTLS $true

This example disables TLS on the Receive connector named WAN on Mailbox server named Mailbox01.

    Set-ReceiveConnector Mailbox01\WAN -SuppressXAnonymousTLS $true

## Step 4: Use the Shell to designate the Active Directory sites as hub sites

To designate an Active Directory site as a hub site, run the following command:

    Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true

You need to perform this procedure once in each Active Directory site that has Mailbox servers that participate in non-encrypted traffic.

This example configures the Active Directory site named Central Office Site 1 as a hub site.

    Set-AdSite "Central Office Site 1" -HubSiteEnabled $true

## Step 5: Use the Shell to configure the least cost routing path through the WAN connection

Depending on how the IP site link costs are configured in Active Directory, this step may not be necessary. You need to verify that the network link with the WOC devices deployed is in the leastcost routing path. To view the Active Directory site link costs, and the Exchange-specific site link costs, run the following command:

    Get-AdSiteLink

If the network link with the WOC devices deployed isn't on the least cost routing path, you'll need to assign an Exchange-specific cost to the particular IP site link to ensure messages are routed correctly. To learn more about this particular issue, see the "Configure Exchange-specific Active Directory site link costs" section in [Scenario: Configure Exchange to support WAN Optimization Controllers](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md).

This example configures an Exchange-specific cost of 15 on the IP site link named Branch Office 2-Branch Office 1.

    Set-AdSiteLink "Branch Office 2-Branch Office 1" -ExchangeCost 15

