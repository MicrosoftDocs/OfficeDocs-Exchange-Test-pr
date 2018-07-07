---
title: 'Configure the number of incoming calls on a Mailbox server: Exchange 2013 Help'
TOCTitle: Configure the number of incoming calls on a Mailbox server
ms:assetid: 419e1de9-2bf8-48a8-824d-2a536b0a6d90
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997637(v=EXCHG.150)
ms:contentKeyID: 49315399
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Configure the number of incoming calls on a Mailbox server

 

_**Applies to:** Exchange Server, Exchange Server 2013_


You can configure the number of incoming concurrent connections that a Mailbox server that’s running the Microsoft Exchange Unified Messaging service will accept. This includes all incoming calls including Outlook Voice Access, call answering, auto attendants, and fax calls. When you increase the number of concurrent connections on a Mailbox server, more system resources are required than if you decrease the number of concurrent calls. Decreasing the number of concurrent calls is especially important on slower computers on which Unified Messaging services are installed. The range for the number of concurrent voice calls is 0 to 200. The default setting is 100.

For additional tasks related to Unified Messaging and Mailbox servers, see [UM services procedures](um-services-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox server (UM service)" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Verify that you’ve correctly installed the Client Access and Mailbox servers.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to configure the number of incoming calls on a Mailbox server

1.  In the EAC, navigate to **Servers** \> **Servers**.

2.  In the list view, select the Exchange server you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **Exchange Server** page, click **Unified Messaging**.

4.  Under **UM Service settings**, under **Maximum number of calls allowed**, enter a number from 0 to 200, and click **Save**.

## Use the Shell to configure the number of incoming calls on a Mailbox server

This example sets the number of incoming voice, Outlook Voice Access, and fax calls that can be accepted by a Mailbox server named `MyMailboxServer1` to 50.

    Set-UMService -Identity MyMailboxServer1 -MaxCallsAllowed 50

