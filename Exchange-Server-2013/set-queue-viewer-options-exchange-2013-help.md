---
title: 'Set Queue Viewer options: Exchange 2013 Help'
TOCTitle: Set Queue Viewer options
ms:assetid: 03a9134c-0714-4c13-b286-92bccc7ec05e
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa995934(v=EXCHG.150)
ms:contentKeyID: 49286845
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Set Queue Viewer options

 

_**Applies to:** Exchange Server 2013_


You can set options in Queue Viewer to adjust the number of items that are displayed on the page and adjust the auto-refresh interval. The auto-refresh interval determines how frequently the results in Queue Viewer are updated.

## What do you need to know before you begin?

  - Estimated time to complete: 10 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Queues" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Exchange Toolbox to set Queue Viewer options

1.  Click **Start** \> **All Programs** \> **Microsoft Exchange Server 2013** \> **Exchange Toolbox**.

2.  In the **Mail flow tools** section, double-click **Queue Viewer**.

3.  In Queue Viewer, click **View** \> **Options** to configure the following settings in the **Queue Viewer Options** dialog box:
    
    1.  In the **Refresh interval (seconds)** field, enter the frequency at which Queue Viewer should update the display.
        

        > [!NOTE]
        > The default auto-refresh interval is 30 seconds and can't be set for a shorter time. If you disable auto-refresh functionality by clearing the <STRONG>Auto-refresh screen</STRONG> check box on the <STRONG>Queue Viewer Options</STRONG> page, you must manually update the results that are displayed in Queue Viewer by clicking <STRONG>Refresh</STRONG>.

    
    2.  In the **Number of items to display on each page** field, enter the maximum number of items to display in Queue Viewer. This number must be from 1 through 10,000. If you have more items than the limit, you will see the items in groups of the maximum number of items. For example, the following figure shows a queue with 14 messages with Queue Viewer configured to display 10 items on each page. The number of objects on the page is displayed on the upper right. At the bottom of the page, you can see the total number of items in the queue. You can use the navigation controls to see the additional items in the queue.

4.  When you are finished, click **OK**.
    
    **Queue Viewer**
    
    ![Queue Viewer with more items than item limit](images/Aa995934.e82196e6-002a-4e9e-823d-b244b0bd25e2(EXCHG.150).gif "Queue Viewer with more items than item limit")  

## How do you know this worked?

You'll know this procedure worked if Queue Viewer uses the refresh interval and number of items per page settings.

