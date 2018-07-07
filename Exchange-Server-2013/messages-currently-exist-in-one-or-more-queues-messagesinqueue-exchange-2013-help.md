---
title: 'Messages currently exist in one or more queues_MessagesInQueue: Exchange 2013 Help'
TOCTitle: Messages currently exist in one or more queues_MessagesInQueue
ms:assetid: 3ffcdc7e-c1b7-49a7-8e5f-b30c0397908d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.messagesinqueue(v=EXCHG.150)
ms:contentKeyID: 46628874
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Messages currently exist in one or more queues\_MessagesInQueue

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 setup displays this warning because its attempt to uninstall a transport role could cause data loss from a transport queue.

Exchange 2007 setup checks to make sure that the transport queues are empty before it removes the roles associated with managing those queues.

If you remove the transport roles before delivery of messages still in the transport queues, those messages may be held indefinitely.

To resolve this issue, inspect the referenced queues to make sure that they are empty of messages before you continue with setup.

**To view the contents of a queue**

1.  Open the Exchange Management Console.

2.  In the console tree, click **Toolbox**.

3.  In the result pane, click **Exchange Queue Viewer**.

4.  In the action pane, click **Open Tool**.

5.  In the Queue Viewer, click the **Queues** tab. A list of all queues on the server to which you are connected is displayed.

6.  Right-click the queue you want and select **Properties** to view the properties of the queue.

**To view messages in a queue**

1.  Follow steps 1 through 4.

2.  In the Queue Viewer, click the **Messages** tab. A list of all messages on the server to which you are connected is displayed. To adjust the view to a single queue, click the **Queues** tab, double-click the queue name, and then click the Server\\Queue tab that appears.

3.  To view detailed information about a message, select a message, and then click **Properties** in the action pane.

