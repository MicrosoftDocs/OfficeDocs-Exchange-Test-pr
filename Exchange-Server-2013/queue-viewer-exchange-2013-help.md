---
title: 'Queue Viewer: Exchange 2013 Help'
TOCTitle: Queue Viewer
ms:assetid: db892f88-5c13-4607-a38c-8845b35ab8b2
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124789(v=EXCHG.150)
ms:contentKeyID: 49286852
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Queue Viewer

 

_**Applies to:** Exchange Server 2013_


Queue Viewer is a Microsoft Management Console snap-in that's installed on a Mailbox server or the Edge Transport server. Queue Viewer is located in the **Mail flow tools** section of the Exchange Toolbox console. You can use this tool to view information about queues on a transport server and the messages that are present in those queues and to perform management actions on queues and mail items. Queue Viewer is useful for troubleshooting mail flow and identifying spam.

When you're using Queue Viewer to manage queues, consider the following:

  - You must connect to a transport server. By default, Queue Viewer opens the queue database on the server where you opened Queue Viewer. However, you can also connect to different servers. For more information, see [Connect to a server in Queue Viewer](connect-to-a-server-in-queue-viewer-exchange-2013-help.md).

  - The list of queues and messages can be large, depending on current mail flow, and the list of queues and messages changes when messages enter and leave the server. You can configure the options for Queue Viewer to control the interval at which the list of queues and messages is refreshed and the number of items displayed on each page. For more information, see [Set Queue Viewer options](set-queue-viewer-options-exchange-2013-help.md).

  - You can create a filter to display the specific set of queues or messages that you want to monitor. After you locate the queues and messages that you want to monitor, you can view the property information for these queues and messages. This information is helpful when you troubleshoot the cause of mail flow problems. For more information, see [Queue filters](queue-filters-exchange-2013-help.md) and [Message filters](message-filters-exchange-2013-help.md).

  - You can use the **Export List** link in the action pane to export the list of queues or a list of messages. For more information, see [Export lists from Queue Viewer](export-lists-from-queue-viewer-exchange-2013-help.md).

