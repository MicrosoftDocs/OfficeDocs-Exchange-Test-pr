---
title: 'Connect to a server in Queue Viewer: Exchange 2013 Help'
TOCTitle: Connect to a server in Queue Viewer
ms:assetid: 6c1ad574-9ab5-4dcc-9398-ec10eca4fd11
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998669(v=EXCHG.150)
ms:contentKeyID: 49286846
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Connect to a server in Queue Viewer

 

_**Applies to:** Exchange Server 2013_


When you use Queue Viewer in the Exchange Toolbox on a Microsoft Exchange Server 2013 server that's located inside the Exchange organization, you can connect to other Mailbox servers. By default, when you open Queue View on a Mailbox server, Queue Viewer connects to the queue database on the local server. However, you can start more than one instance of Queue Viewer so that each instance focuses on a different server. You can also tile Queue Viewer windows so you can easily monitor more than one Mailbox server at a time.

You can also specify the server that Remote PowerShell uses to perform the specified tasks in Queue Viewer. This server doesn’t need to match the remote server you're managing in Queue Viewer.

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Queues" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - The procedures in this topic don't apply to Edge Transport servers. When you use Queue Viewer on an Edge Transport server, you can't change the focus of the tool.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Exchange Toolbox to specify the server you want to manage in Queue Viewer

1.  Click **Start** \> **All Programs** \> **Microsoft Exchange Server 2013** \> **Exchange Toolbox**.

2.  In the **Mail flow tools** section, double-click **Queue Viewer**.

3.  In the action pane, click **Connect to server**.

4.  In the **Connect to Server** window, click **Browse** to view a list of the available Mailbox servers.

5.  In the **Select Exchange Server** window, select a Mailbox server. To search for a Mailbox server, use one of the following procedures:
    
      - Enter the exact server name or the first few letters of the server name in the **Search** field, and then click **Find Now**. Select a server from the result pane.
    
      - Select the **View** menu, and then click **Show Filter**. In the **Name** column or **Version** column, click the filter icon, and then select the filter operator. Type the filter criteria in the **Enter text here** field. Press ENTER. Select a server from the result pane.

6.  Click **OK** to close the **Select Exchange Server** window.

7.  After you select a server, in the **Connect to server** window, select the **Set as default server** check box if you want Queue Viewer to focus on this server first whenever Queue Viewer is opened.

8.  In the **Connect to server** window, click **Connect**.

## Use the Exchange Toolbox to specify the server that Queue Viewer uses to run Remote PowerShell

1.  Click **Start** \> **All Programs** \> **Microsoft Exchange Server 2013** \> **Exchange Toolbox**.

2.  In the **Mail flow tools section**, double-click **Queue Viewer**.

3.  In the action pane, click **Properties**.

4.  In the **Queue Viewer - \<server name\> Properties** dialog box, select one of the following options:
    
      - **Connect to the automatically selected server**   Select this option to automatically connect to the server where you're managing queues to run Remote PowerShell.
    
      - **Specify a server to connect to**   Select this option to specify a server to run Remote PowerShell. If you select this option, click **Browse** to open the **Select Exchange Server** dialog box. Select the server where you want to run Remote PowerShell, and then click **OK**.

## How do you know this worked?

You should be able to manage the queues on the Mailbox server you specified.

