---
title: 'Transport logs: Exchange 2013 Help'
TOCTitle: Transport logs
ms:assetid: f8cf635d-60c2-4aa3-9c06-244c29942cba
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd302434(v=EXCHG.150)
ms:contentKeyID: 49287006
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Transport logs

 

_**Applies to:** Exchange Server 2013_


Transport logs provide information about what's happening in the transport pipeline. The following transport logs are available in Microsoft Exchange Server 2013:

**Agent logs**   Agent logging records the actions performed on a message by specific anti-spam agents. Agent logging is available in the Transport service on a Mailbox server. For more information, see [Anti-spam agent logging](anti-spam-agent-logging-exchange-2013-help.md).

**Connectivity logs**   Connectivity logging records the outbound connection activity transport services. Connectivity logging is available in the Front End Transport service on Client Access servers, the Transport service on Mailbox servers, and the Mailbox Transport service on Mailbox servers. For more information, see [Connectivity logging](connectivity-logging-exchange-2013-help.md).

**Message tracking and delivery reports**   Message tracking logs the details of all message activity as messages are transferred to and from an Exchange 2013 Mailbox server. Message tracking is available in the Transport service on Mailbox servers, and in the Mailbox Transport service on Mailbox servers. For more information, see [Message tracking](message-tracking-exchange-2013-help.md).

Delivery reports uses the information stored in the message tracking log to search for information about messages sent to or sent from a specific mailbox. For more information, see [Delivery reports for administrators](delivery-reports-for-administrators-exchange-2013-help.md).

**Pipeline tracing**   Pipeline tracing records snapshots of messages before and after the message is affected by transport agents in the Transport service on Mailbox servers, and in the Mailbox Transport Delivery service on Mailbox servers. For more information, see [Pipeline tracing](pipeline-tracing-exchange-2013-help.md).

**Protocol logs**   Protocol logging records the SMTP conversations that occur on Send connectors and Receive connectors as part of message delivery. Protocol logging is available in the Front End Transport service on Client Access servers, the Transport service on Mailbox servers, and the Mailbox Transport service on Mailbox servers. For more information, see [Protocol logging](protocol-logging-exchange-2013-help.md).

**Routing table logs**   Routing table logging periodically records a snapshot of the routing table that's used by Exchange 2013 to route messages to their destinations. Routing table logging is available in the Transport service on Mailbox servers.

