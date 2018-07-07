---
title: 'Manage health sets and server health: Exchange 2013 Help'
TOCTitle: Manage health sets and server health
ms:assetid: a4f84312-6cfa-4f17-9707-676aadab1143
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn482054(v=EXCHG.150)
ms:contentKeyID: 59888995
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Manage health sets and server health

 

_**Applies to:** Exchange Online, Exchange Server 2013 SP1_


You can use the built-in health reporting cmdlets to perform a variety of tasks related to managed availability, such as:

  - Viewing the health of a server or group of servers

  - Viewing a list of health sets

  - Viewing a list of probes, monitors, and responders associated with a particular health set

  - View a list of monitors and their current health

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 2 minutes

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## View Server Health

You can use the Shell to get a summary of the health of a server running Exchange 2013.

## Use the Shell to View Server Health

Run either of the following commands to view the health sets and health information on a server running Exchange 2013.

    Get-HealthReport -Identity <ServerName>

    Get-ServerHealth -Identity <ServerName> | Format-Table Server,CurrentHealthSetState,Name,HealthSetName,AlertValue,HealthGroupName -Auto

Run any of the following commands to view the health sets on a server or database availability group running Exchange 2013.

    Get-ExchangeServer | Get-HealthReport -RollupGroup

    Get-ExchangeServer | Get-HealthReport -RollupGroup -HealthSetName <HealthSet>

    (Get-DatabaseAvailabiltyGroup <DAGName>).Servers | Get-HealthReport -RollupGroup

## View a List of Health Sets

A health set is a group of monitors, probes and responders for a component that determine whether the component is healthy or unhealthy. You can use the Shell to view the list of health sets on a server running Exchange 2013.

## Use the Shell to View a List of Health Sets

Run the following command to view the health sets on a server running Exchange 2013.

    Get-HealthReport -Server <ServerName>

## View the Probes, Monitors and Responders for a Health Set

A health set is a group of monitors, probes and responders for a component that determine whether the component is healthy or unhealthy. You can use the Shell to view the list of probes, monitors, and responders associated with a health set on a server running Exchange 2013.

## Use the Shell to View the Probes, Monitors and Responders for a Health Set

Run the following command to view the probes, monitors and responders associated with a health set on a server running Exchange 2013.

    Get-MonitoringItemIdentity -Server <ServerName> -Identity <HealthSetName> | Format-Table Identity,ItemType,Name -Auto

## View a List of Monitors and Their Current Health

The health of a monitor is reported by using the “worst of” monitors in the health set. You can view the details of a health set to see which monitors are healthy and which ones are unhealthy.

## Use the Shell to View a List of Monitors and Their Current Health

Run the following command to view a list of the monitors and their current health on a server running Exchange 2013.

    Get-ServerHealth -HealthSet <HealthSetName> -Server <ServerName> | Format-Table Name, AlertValue -Auto

