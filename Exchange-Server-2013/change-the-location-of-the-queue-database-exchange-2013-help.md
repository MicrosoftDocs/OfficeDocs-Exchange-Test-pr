---
title: 'Change the location of the queue database: Exchange 2013 Help'
TOCTitle: Change the location of the queue database
ms:assetid: f170cb0c-04a9-4fa7-b594-206e3a787e14
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb125177(v=EXCHG.150)
ms:contentKeyID: 50646241
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Change the location of the queue database

 

_**Applies to:** Exchange Server 2013_


A *queue* is a temporary holding location for messages that are waiting to enter the next stage of processing. Each queue represents a logical set of messages that a transport server processes in a specific order.

Like the previous versions of Exchange, Microsoft Exchange Server 2013 uses an Extensible Storage Engine (ESE) database for queue message storage. All the different queues are stored in a single ESE database. Queues exist only on Mailbox servers or on Edge Transport servers.

The location of the queue database and the queue database transaction logs is controlled by keys in the `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML application configuration file. This file is associated with the Microsoft Exchange Transport service. The following table explains each key in more detail.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Key</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p>This key specifies the location of the queue database files. The files are:</p>
<ul>
<li><p>Mail.que</p></li>
<li><p>Trn.chk</p></li>
</ul>
<p>The default location is <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p>This key specifies the location of the queue database transaction log files. The files are:</p>
<ul>
<li><p>Trn.log</p></li>
<li><p>Trntmp.log</p></li>
<li><p>Trn<em>nnn</em>.log</p></li>
<li><p>Trnres00001.jrs</p></li>
<li><p>Trnres00002.jrs</p></li>
<li><p>Temp.edb</p></li>
</ul>
<p>Note that Temp.edb is used to verify the queue database schema when the Microsoft Exchange Transport service starts. Although Temp.edb isn't a transaction log file, it's kept in the same location as the transaction log files.</p>
<p>The default location is <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>.</p></td>
</tr>
</tbody>
</table>


## What do you need to know before you begin?

  - Estimated time to complete: 15 minutes.

  - Exchange permissions don't apply to the procedures in this topic. These procedures are performed in the operating system of the Exchange Server.

  - When you stop or restart the Microsoft Exchange Transport service, mail flow on the server is interrupted.

  - When you change the location of the queue database or the transaction logs, the existing queue database and transaction log files aren't moved. A new queue database and new transaction logs are created at the new location. The existing files are left at the old location. However, they're no longer used. If you want to reuse the existing queue database or transaction log files at the new location, you must move the existing files to the new location after the Microsoft Exchange Transport service is stopped, but before the service is started.

  - If the target folder for the queue database or transaction logs doesn't exist, it will be created for you if the parent folder has the following permissions applied to it:
    
      - Network Service: Full Control
    
      - System: Full Control
    
      - Administrators: Full Control

  - Any customized per-server settings you make in Exchange XML application configuration files, for example, web.config files on Client Access servers or the EdgeTransport.exe.config file on Mailbox servers, will be overwritten when you install an Exchange Cumulative Update (CU). Make sure that you save this information so you can easily re-configure your server after the install. You must re-configure these settings after you install an Exchange CU.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## What do you want to do?

## Use the Command Prompt to create a new queue database and transaction logs in a new location

1.  Create the folders where you want to keep the queue database and transaction logs. Make sure that the correct permissions are applied to the folders.

2.  In a Command prompt window, open the EdgeTransport.exe.config file in Notepad by running the following command:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

3.  Modify the following keys in the `<appSettings>` section.
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    For example, to create a new queue database in D:\\Queue\\QueueDB and new transaction logs in D:\\Queue\\QueueLogs, use the following values:
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  When you are finished, save and close the EdgeTransport.exe.config file.

5.  Restart the Microsoft Exchange Transport service by running the following command:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## How do you know this worked?

To verify that you successfully created a new queue database and new transaction logs at a new location, do the following:

1.  Verify the new database files Mail.que and Trn.chk exist at the new location.

2.  Verify the new transaction log files Trn.log, Trntmp.log, Trnres00001.jrs, Trnres00002.jrs, and Temp.edb files exist at the new location.

3.  If you can delete the old queue database and transaction log files from the old location after the Microsoft Exchange Transport service has started, those files are no longer being used.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Return to top

## Use the Command Prompt to move the existing queue database and transaction logs to a new location

Only disaster recovery scenarios where the Microsoft Exchange Transport service wasn't shut down correctly or a hard disk drive failure would require that you restore and relocate an existing queue database and its existing transaction logs.

Under ordinary circumstances, you shouldn't have to reuse existing transaction logs. An ordinary shutdown of the Microsoft Exchange Transport service writes all uncommitted transaction log entries to the queue database. And, circular logging is used, so transaction logs that contain previously committed database changes aren't preserved.

Use the following procedure to move the existing queue database and transaction logs at a new location:

1.  Create the folders where you want to keep the queue database and transaction logs. Make sure that the correct permissions are applied to the folders.

2.  In a Command prompt window, open the EdgeTransport.exe.config file in Notepad by running the following command:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

3.  Modify the following keys in the `<appSettings>` section:
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    For example, to change the location of the queue database to D:\\Queue\\QueueDB and the transaction logs to D:\\Queue\\QueueLogs, use the following values:
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  When you are finished, save and close the EdgeTransport.exe.config file.

5.  Stop the Microsoft Exchange Transport service by running the following command:
    
        net stop MSExchangeTransport

6.  Move the existing database files Mail.que and Trn.chk from the original location to the new location.

7.  Move the existing transaction log files Trn.log, Trntmp.log, Trn*nnnnn*.log, Trnres00001.jrs, Trnres00002.jrs, and Temp.edb from the old location to the new location.

8.  Start the Microsoft Exchange Transport service by running the following command:
    
        net start MSExchangeTransport

## How do you know this worked?

To verify that you successfully moved the existing queue database and transaction logs to the new location, do the following:

1.  Verify the queue database files Mail.que and Trn.chk exist at the new location.

2.  Verify the transaction log files Trn.log, Trntmp.log, Trnres00001.jrs, Trnres00002.jrs, and Temp.edb files exist at the new location.

3.  Verify there are no queue database or transaction log files at the original location.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Return to top

