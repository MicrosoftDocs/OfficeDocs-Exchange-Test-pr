---
title: 'View performance counters for messaging records management: Exchange 2013 Help'
TOCTitle: View performance counters for messaging records management
ms:assetid: ec374d31-2797-4f8b-8c96-3839d01a662c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb397227(v=EXCHG.150)
ms:contentKeyID: 50873815
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# View performance counters for messaging records management

 

_**Applies to:** Exchange Server 2013_


You can use Windows Reliability and Performance Monitor (Perfmon.exe) to select and view performance counters for messaging records management (MRM). By using performance counters, you can monitor the Managed Folder Assistant while it runs resource-intensive MRM processes.

For a list of performance counters for MRM, see [Performance counters for messaging records management](performance-counters-for-messaging-records-management-exchange-2013-help.md).

Looking for other tasks related to monitoring MRM? Check out [Monitoring messaging records management](monitoring-messaging-records-management-exchange-2013-help.md).

## Use Windows Reliability and Performance Monitor to view performance counters for MRM

To perform this procedure, the account you use must be delegated membership in the local Administrators group.

1.  To start Windows Reliability and Performance Monitor, click **Start**, click **Run**, and then type **perfmon**.

2.  In the console tree, navigate to **Monitoring Tools** \> **Performance Monitor**.

3.  Click the plus sign (+) button on the toolbar. The **Add Counters** dialog box appears.

4.  From the **Select counter from computer** list, select one of the following options:
    
      - If you are performing this procedure on a local computer, select **\<Local computer\>**. This is the default selection.
    
      - If you are performing this procedure remotely, select the server you want to monitor.

5.  In the list of performance counters, expand **MSExchange Assistants - Per Database** or the **MSExchange Managed Folder Assistant**.

6.  Select the performance counters you want to monitor.

7.  For performance counters under **MSExchange Assistants - Per Database**, to view the counters for all mailbox databases, in **Instances of selected object**, click **All instances**. Or, to specify one or more mailbox databases, select instances from the list.

8.  To add the selected counters so that the counters appear in Windows Reliability and Performance Monitor, and to begin collecting performance data, click **Add**.

