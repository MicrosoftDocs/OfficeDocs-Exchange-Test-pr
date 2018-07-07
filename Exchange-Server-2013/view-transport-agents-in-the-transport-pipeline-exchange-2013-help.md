---
title: 'View transport agents in the transport pipeline: Exchange 2013 Help'
TOCTitle: View transport agents in the transport pipeline
ms:assetid: bd715d8e-7b21-48de-8f68-d425d8506e4c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124395(v=EXCHG.150)
ms:contentKeyID: 50873810
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# View transport agents in the transport pipeline

 

_**Applies to:** Exchange Server 2013_


You can use the Exchange Management Shell to view a list of transport agents in the transport pipeline on Microsoft Exchange Server 2013 Mailbox servers and Client Access servers. Specifically, the **Get-TransportPipeline** cmdlet shows information about the following types of transport agents in the transport pipeline:

  - Agents based on the **SmtpReceiveAgent**, **RoutingAgent**, **DeliveryAgent**, and **StorageAgent** classes in the Transport service on Mailbox servers.

  - Agents based on the **SmtpReceiveAgentClass** in the Mailbox Transport Delivery service on Mailbox servers.

  - Agents based on the **SmtpReceiveAgentClass** in the Front End Transport service on Client Access servers.

You can view a list of all the enabled transport agents that have encountered messages in the transport pipeline and the SMTP events they are registered on. For more information about transport agents, see [Transport agents](transport-agents-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Transport agents" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - You can only use the Shell to perform this procedure.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to view a list of transport agents in the transport pipeline

To use the Shell to view a list of transport agents in the transport pipeline on an Exchange server, run the following command:

    Get-TransportPipeline | Format-List

To export the results to a text file named C:\\My Documents\\Transport Agents.txt, run the following command:

    Get-TransportPipeline | Format-List > "C:\My Documents\Transport Agents.txt"

## How do you know this worked?

Only transport agents that have encountered messages in the transport pipeline between the time when the transport service was started and the time when the **Get-TransportPipeline** cmdlet was run are displayed by the cmdlet. A transport agent that hasn't encountered a message in the transport pipeline won't appear in the results displayed by the **Get-TransportPipeline** cmdlet, even if that transport agent is enabled.

