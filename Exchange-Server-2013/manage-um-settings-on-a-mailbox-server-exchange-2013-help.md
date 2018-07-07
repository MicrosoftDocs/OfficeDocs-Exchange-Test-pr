---
title: 'Manage UM settings on a Mailbox server: Exchange 2013 Help'
TOCTitle: Manage UM settings on a Mailbox server
ms:assetid: 6df4853d-21d2-473f-b0ca-ebc996d8794a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998815(v=EXCHG.150)
ms:contentKeyID: 49315441
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMServerPropertiesPropertyPage
---

# Manage UM settings on a Mailbox server

 

_**Applies to:** Exchange Server 2013_


After you install a Mailbox server that is running the Microsoft Exchange Unified Messaging service, you can configure several options, including the number of concurrent calls, the TCP and Transport Layer Security (TLS) listening ports, the status, and the UM startup mode.


> [!IMPORTANT]
> It’s not required that Mailbox servers be added to a UM dial plan before it can process calls for Unified Messaging (UM), except when you’re integrating UM and Microsoft Office Communications Server 2007 R2 or Microsoft Lync Server. By default, all Mailbox servers in an organization are available to answer incoming calls.



For additional management tasks related to Unified Messaging and Mailbox servers, see [UM services procedures](um-services-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox server (UM service)" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Verify that the Mailbox server is installed, either on the same computer as the Client Access server or on a separate computer.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the Shell to configure Unified Messaging properties on a Mailbox server

This example removes a Mailbox server named `MyMailboxServer` from all Session Initiation Protocol (SIP) dial plans.

    Set-UMService -Identity MyMailboxServer -DialPlans $null

This example adds the Mailbox server named `MyMailboxServer` to a UM SIP dial plan named `MySIPDialPlanName` and also sets the maximum number of incoming voice calls.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -MaxCalls 150 

This example sets the startup mode to Dual mode on a Mailbox server named `MyUMServer`.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -UMStartUpMode -Dual 

## Use the Shell to view Mailbox server properties

This example displays a list of all the Mailbox servers.

    Get-UMService

This example displays a formatted list of properties for the Mailbox server named `MyMailboxServer`.

    Get-UMService -Identity MyMailboxServer | Format-List

