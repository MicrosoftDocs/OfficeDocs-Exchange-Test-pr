---
title: 'Install and configure the Address Book Policy Routing agent: Exchange 2013 Help'
TOCTitle: Install and configure the Address Book Policy Routing agent
ms:assetid: 20e8a43d-4508-4388-a2c9-aa3073593cc2
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ907308(v=EXCHG.150)
ms:contentKeyID: 50639771
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Install and configure the Address Book Policy Routing agent

 

_**Applies to:** Exchange Online, Exchange Server 2013_


The Address Book Policy Routing agent is a Transport agent that runs on the Mailbox server that controls how recipients are resolved in your organization. When the ABP Routing agent is installed and configured, users that are assigned to different GALs appear as external recipients in that they can’t view external recipients’ contact cards.

For additional management tasks related to ABPs, see [Address book policy procedures](address-book-policy-procedures-exchange-2013-help.md).

Looking for the Exchange Online version of this topic? See [Turn on address book policy routing](https://technet.microsoft.com/en-us/library/jj891095\(v=exchg.150\)).

## What do you need to know before you begin?

  - Estimated time to complete this task: 15 minutes.

  - After the ABP Routing agent is installed and configured, it may take up to 30 minutes for email in the organization to be evaluated by agent.

  - You can’t use the EAC to perform this procedure. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## How do you do this?

## Step 1: Install the ABP Routing agent

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Transport Agents" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

Install the ABP Routing agent by running the following command. This is the exact command and syntax you’ll need to use.

    Install-TransportAgent -Name "ABP Routing Agent" -TransportAgentFactory "Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.AddressBookPolicyRoutingAgentFactory" -AssemblyPath $env:ExchangeInstallPath\TransportRoles\agents\AddressBookPolicyRoutingAgent\Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.dll

You’ll get a warning that the Transport service needs to be restarted for your changes to take effect, but perform Step 2 first so you only have to restart the Transport service once.

For detailed syntax and parameter information, see [Install-TransportAgent](https://technet.microsoft.com/en-us/library/aa997998\(v=exchg.150\)).

## Step 2: Enable the Transport Routing agent

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Transport Agents" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

After the ABP Routing agent is installed, you need to enable it by running the following command:

    Enable-TransportAgent "ABP Routing Agent"

For detailed syntax and parameter information, see [Enable-TransportAgent](https://technet.microsoft.com/en-us/library/bb124921\(v=exchg.150\)).

## Step 3: Restart the Transport service and verify the ABP Routing agent is installed and enabled

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Transport Agents" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

1.  Restart the Transport service by running the following command.
    
        Restart-Service MSExchangeTransport

2.  After the service has restarted, verify that the ABP Routing agent is installed and enabled by running the following cmdlet.
    
        Get-TransportAgent
    
    If the ABP Routing agent is listed, the agent has been correctly installed.

For detailed syntax and parameter information, see [Get-TransportAgent](https://technet.microsoft.com/en-us/library/bb123536\(v=exchg.150\)).

## Step 4: Enable the ABP Routing agent

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Transport configuration" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

The final step in this process is to enable ABP routing for the organization. Run the following command.

    Set-TransportConfig -AddressBookPolicyRoutingEnabled $true

For detailed syntax and parameter information, see [Set-TransportConfig](https://technet.microsoft.com/en-us/library/bb124151\(v=exchg.150\)).

