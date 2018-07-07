---
title: 'Manage transport agents: Exchange 2013 Help'
TOCTitle: Manage transport agents
ms:assetid: f15ab7e4-015d-45b1-9c10-f733d7cd2a36
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb125175(v=EXCHG.150)
ms:contentKeyID: 49300743
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Manage transport agents

 

_**Applies to:** Exchange Server 2013_


Transport agents use SMTP events to operate on messages as the messages move through the transport pipeline. Most of the built-in transport agents that are included with Microsoft Exchange Server 2013 are invisible and unmanageable. However, you can install and configure third-party transport agents on Exchange servers in your organization. For more information about transport agents, see [Transport agents](transport-agents-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 10 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Transport agents" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - You can only use the Shell to perform this procedure.

  - Support for legacy transport agents isn't enabled by default, but you can enable it. For instructions, see [Enable support for legacy transport agents](enable-support-for-legacy-transport-agents-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## About transport agent procedures in the Front End Transport service on Client Access servers

You can't use the Exchange Management Shell to manage transport agent in the Front End Transport service on a Client Access server. Instead, you need to open Windows PowerShell on the Client Access server, and then import the Exchange cmdlets into the Windows PowerShell session.


> [!WARNING]
> Running Exchange cmdlets in Windows PowerShell for tasks other than managing transport agents in the Front End Transport service is not supported. There are serious consequences that can result if you bypass the Exchange Management Shell and role-based access control (RBAC) by running Exchange cmdlets in Windows PowerShell. You should always run Exchange cmdlets in the Exchange Management Shell. For more information, see <A href="release-notes-for-exchange-2013-exchange-2013-help.md">Release notes for Exchange 2013</A>.



To perform any of the Transport Agent procedures described in this topic in the Front End Transport service, you need to perform the following additional steps:

1.  On the Client Access server, open Windows PowerShell and run the following command:
    
        Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn

2.  Run the command as described, but add the following value to the command: `-TransportService FrontEnd`.
    
    For example, to view the transport agents in the Front End Transport service on a Client Access server, run the following command:
    
        Get-TransportAgent -TransportService FrontEnd

## Use the Shell to install a transport agent

When you install a transport agent, Exchange only registers the DLLs associated with the transport agent. You need to make sure all files, registry keys, and other objects that the transport agent depends on are installed correctly and configured. After Exchange loads the DLLs, it continues to reference the DLLs after the command has completed.

Transport agents have full access to all e-mail messages that they encounter. Exchange puts no restrictions on a transport agent's behavior. Transport agents that are unstable or contain security flaws may affect the stability and security of Exchange. Therefore, you should only install transport agents that you fully trust and that have been fully tested in a test environment.

Transport agents are installed in a disabled state to make sure mail flow isn't affected by transport agents that haven't been configured. Therefore, after a transport agent has been configured correctly, you need to enable the transport agent.

Use the following syntax to install a transport agent.

    Install-TransportAgent -Name <TransportAgentIdentity> -TransportAgentFactory <"TransportAgentFactory"> -AssemblyPath <"FilePath">

This example installs a fictitious transport agent named Contoso Transport Agent in the Transport service on a Mailbox server.

    Install-TransportAgent -Name "Contoso Transport Agent" -TransportAgentFactory "vendor.exchange.ContosoTransportAgentfactory" -AssemblyPath "C:\Program Files\Vendor\TransportAgent\ContosoTransportAgentFactory.dll"

## How do you know this worked?

To verify that you have successfully installed the transport agent, run the command `Get-TransportAgent` and verify the transport agent is listed.

## Use the Shell to enable a transport agent

Use the following syntax to enable a transport agent.

    Enable-TransportAgent <TransportAgentIdentity>

This example enables the transport agent named Contoso Transport Agent in the Transport service on a Mailbox server.

    Enable-TransportAgent "Contoso Transport Agent"

## How do you know this worked?

To verify that you have successfully enabled a transport agent, run the command `Get-TransportAgent | Format-List Name,Enabled` and verify the transport agent is enabled.

## Use the Shell to disable a transport agent

Use the following syntax to disable a transport agent:

    Disable-TransportAgent <TransportAgentIdentity>

This example disables the transport agent named Fabirkam Transport Agent in the Transport service on a Mailbox server.

    Disable-TransportAgent "Fabrikam Transport Agent"

## How do you know this worked?

To verify that you have successfully disabled a transport agent, run the command `Get-TransportAgent | Format-List Name,Enabled` and verify the transport agent is disabled.

## Use the Shell to view transport agents

To view a summary list of transport agents, run the following command:

    Get-TransportAgent

To view the detailed configuration of a specific transport agent, run the following command:

    Get-TransportAgent <TransportAgentIdentity> | Format-List

This example provides detailed configuration of the transport agent named Transport Rule Agent.

    Get-TransportAgent "Transport Rule Agent" | Format-List

## Use the Shell to configure the priority of a transport agent

Transport agents with a priority closest to 0 process email messages first. However, the SMTP event in the transport pipeline where the transport agent is registered may cause a lower priority agent to act on the message before a higher priority agent.

To modify the priority of an existing transport agent, run the following command:

    Set-TransportAgent <TransportAgentIdentity> -Priority <Integer>

This example sets the priority agent value of 3 for the existing transport agent named Contoso Transport Agent in the Transport service on a Mailbox server.

    Set-TransportAgent "Contoso Transport Agent" -Priority 3

## How do you know this worked?

To verify that you have successfully configured the priority of a transport agent, run the command `Get-TransportAgent | Format-List Name,Priority` and verify the priority value of the transport agent.

## Use the Shell to uninstall a transport agent

When the transport agent is uninstalled, Exchange unregisters the DLL files used with the agent. Exchange doesn't remove any files, registry keys, or other objects added by the installation of the transport agent.

To uninstall a transport agent, run the following command:

    Uninstall-TransportAgent <TransportAgentIdentity>

This example uninstalls the transport agent named Fabrikam Transport Agent from the Transport service on a Mailbox server.

    Uninstall-TransportAgent "Fabrikam Transport Agent"

## How do you know this worked?

To verify that you have successfully uninstalled the transport agent, run the command `Get-TransportAgent` and verify the transport agent isn't listed.

