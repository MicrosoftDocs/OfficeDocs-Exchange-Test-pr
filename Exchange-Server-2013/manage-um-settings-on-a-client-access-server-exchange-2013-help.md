---
title: 'Manage UM settings on a Client Access server: Exchange 2013 Help'
TOCTitle: Manage UM settings on a Client Access server
ms:assetid: 08667911-fa86-404e-84b1-65cedd94d579
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673507(v=EXCHG.150)
ms:contentKeyID: 49315349
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Manage UM settings on a Client Access server

 

_**Applies to:** Exchange Server 2013_


After you install a Client Access server that is running the Microsoft Exchange Unified Messaging Call Router service, you can configure several options, including the number of concurrent calls, the TCP and Transport Layer Security (TLS) listening ports, the status, and the startup mode.


> [!NOTE]
> It’s not required that Client Access servers be added to a UM dial plan before it can process calls for Unified Messaging (UM), except when you’re integrating UM and Microsoft Office Communications Server 2007 R2 or Microsoft Lync Server. By default, all Client Access servers in an organization are available to answer incoming calls.



For additional tasks related to Unified Messaging and Client Access servers, see [UM services procedures](um-services-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Client Access server (UM call router service)" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Verify that the Client Access server is installed, either on the same computer as the Mailbox server or on a separate computer.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the Shell to configure Unified Messaging properties on a Client Access server

This example removes a Client Access server named `MyClientAccessServer` from all Session Initiation Protocol (SIP) dial plans.

    Set-UMCallRouterSettings -DialPlans $null - Server MyClientAccessServer

This example adds a Client Access server named `MyClientAccessServer` to a SIP dial plan named `MySIPDialPlan` and also sets the maximum number of incoming voice calls.

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan -MaxCalls 150 -Server MyClientAccessServer

This example sets the SIP TCP listening port to 5077 and the startup mode to Dual mode on a Client Access server named `MyClientAccessServer`.

    Set-UMCallRouterSettings  -Server MyClientAccessServer-SipTCPListeningPort 5077 -UMStartUpMode -Dual 

## Use the Shell to view Client Access server properties

This example displays a list of all the Client Access servers.

    Get-UMCallRouterSettings

This example displays a formatted list of properties for the Client Access server.

    Get-UMCallRouterSettings | Format-List

