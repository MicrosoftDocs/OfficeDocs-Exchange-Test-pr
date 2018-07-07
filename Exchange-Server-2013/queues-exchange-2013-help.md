---
title: 'Queues: Exchange 2013 Help'
TOCTitle: Queues
ms:assetid: e7ad0ba5-3789-4a2b-9825-6bb1b321609c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb125022(v=EXCHG.150)
ms:contentKeyID: 50646240
ms.date: 07/14/2016
mtps_version: v=EXCHG.150
---

# Queues

 

_**Applies to:** Exchange Server 2013_


A *queue* is a temporary holding location for messages that are waiting to enter the next stage of processing or delivery to a destination. Each queue represents a logical set of messages that the Exchange server processes in a specific order. In Microsoft Exchange Server 2013, queues hold messages before, during and after delivery. Queues exist on Mailbox servers and Edge Transport servers. Mailbox servers and Edge Transport servers are called *transport servers* throughout this topic.

Like the previous versions of Exchange, Exchange 2013 uses a single Extensible Storage Engine (ESE) database for queue storage.

You can manage queues and the messages in queues using the Exchange Management Shell and Queue Viewer in the Exchange Toolbox. You can use these interfaces to view the status and contents of queues and detailed message properties. You can also use these interfaces to perform actions that modify queues or the messages in the queues.

**Contents**

  - Types of queues

  - Queue database files

  - Queue properties
    
      - NextHopSolutionKey
    
      - IncomingRate, OutgoingRate, and Velocity
    
      - Queue status
    
      - Other queue properties

  - Message properties
    
      - Message status
    
      - Other message properties

  - Manage queues and messages in queues

## Types of queues

The following types of queues are used in Exchange 2013:

  - **Persistent queues**   *Perisistent queues* are queues that exist on every transport server in every Exchange organization. Like previous versions of Exchange, there are three persistent queues in Exchange 2013:
    
      - **Submission queue**   The Submission queue is used by the categorizer to gather all messages that have to be resolved, routed, and processed by transport agents on the transport server. All messages that are received by a transport server enter processing in the Submission queue. On Mailbox servers, messages are submitted through a Receive connector, the Pickup or Replay directories, or the Mailbox Transport Submission service. On Edge Transport servers, messages are typically submitted through a Receive connector, but the Pickup and Replay directories are also available.
        
        The categorizer retrieves messages from this queue and, among other things, determines the location of the recipient and the route to that location. After categorization, the message is moved to a delivery queue or to the Unreachable queue. Each transport server has only one Submission queue. Messages that are in the Submission queue can't be in other queues at the same time. For more information about the categorizer and the transport pipeline, see [Mail flow](mail-flow-exchange-2013-help.md).
    
      - **Unreachable queue**   The Unreachable queue contains messages that can't be routed to their destinations. Typically, an unreachable destination is caused by configuration changes that have modified the routing path for delivery. Regardless of destination, all messages that have unreachable recipients reside in this queue. Each transport server has only one Unreachable queue.
        
        Messages in the Unreachable queue are automatically resubmitted when a routing change is detected. So, after the condition or configuration error caused the messages to enter the Unreachable queue is repaired, you don't need to take additional action to move the messages out of the Unreachable queue for delivery.
        
        The Unreachable queue is typically empty. If the Unreachable queue contains no messages it doesn't appear in Queue Viewer or **Get-Queue** results.
    
      - **Poison message queue**   The poison message queue is a special queue that's used to isolate messages that are determined to be harmful to the Exchange 2013 system after a transport server or service failure. The messages may be genuinely harmful in their content and format. Alternatively, they may be the results of a poorly written agent that has caused the Exchange server to fail when it processed the supposedly bad messages.
        
        The poison message queue is typically empty. If the poison message queue contains no messages it doesn't appear in Queue Viewer or **Get-Queue** results. The messages in the poison message queue are never automatically resumed or expired. Messages remain in the poison message queue until they're manually resumed or removed by an administrator.

  - **Delivery queues**   Delivery queues hold messages that are being delivered to any local or remote destinations by using SMTP. All messages are transmitted between Exchange servers by using SMTP. Non-SMTP destinations also use delivery queues if the destination is serviced by a Delivery Agent connector. . Each delivery queue contains messages that are being routed to the same destination. It's practically inevitable that multiple delivery queues will exist on a transport server. Delivery queues are dynamically created when they're required and are automatically deleted when the queue is empty and the expiration time has passed. The queue expiration time is controlled by the *QueueMaxIdleTime* parameter on the **Set-TransportService** cmdlet. The default value is three minutes.

  - **Shadow queues**   Shadow queues hold redundant copies of a message while the message is in transit. For more information, see [Shadow redundancy](shadow-redundancy-exchange-2013-help.md).

  - **Safety Net**   Safety Net retains copies of messages that were successfully delivered by the transport server. Although it's not accessible by queue management tools, Safety Net is just another queue in the queue database. For more information, see [Safety Net](safety-net-exchange-2013-help.md).

Return to top

## Queue database files

All the different queues are stored in a single ESE database. By default, this queue database is located on the transport server at `%ExchangeInstallPath%TransportRoles\data\Queue`.

Like any ESE database, the queue database uses log files to accept, track, and maintain data. To enhance performance, all message transactions are written first to log files and memory, and then to the database file. The checkpoint file tracks the transaction log entries that have been committed to the database. During an ordinary shutdown of the Microsoft Exchange Transport service, uncommitted database changes that are found in the transaction logs are always committed to the database.

Circular logging is used for the queue database. This means that the history of committed transactions that are found in the transaction logs isn't maintained. Any transaction logs that are older than the current checkpoint are immediately and automatically deleted. Therefore, the transaction logs can't be replayed for queue database recovery from backup.

Exchange 2013 uses *generation tables* for storage and clean-up of messages in the queue database. Instead of processing and deleting individual message records from one large table, the queue database stores messages in time-based tables, and only deletes the entire table after all the messages in the table have been successfully processed. For example, all messages queued from 1:00 PM to 2:00 PM, regardless of the queue or destination, are stored in the `1p-2p_msgs` table. At 2:00 PM, new messages are stored in the `2p-3p_msgs` table. At 4:00 PM, a new table named `4p-5p_msgs` is created, and the entire `1p-2p_msgs` table is deleted, but only if all messages in the table have been successfully processed. This approach of deleting entire messages tables instead of individual messages helps improves the I/O performance of the drive that holds the queue database.

The following table lists the files that constitute the queue database.

### Files that constitute the queue database

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>File</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.que</p></td>
<td><p>This queue database file stores all the queued messages.</p></td>
</tr>
<tr class="even">
<td><p>Tmp.edb</p></td>
<td><p>This temporary database file is used to verify the queue database schema on startup.</p></td>
</tr>
<tr class="odd">
<td><p>Trn*.log</p></td>
<td><p>This transaction log records all changes to the queue database. Changes to the database are first written to the transaction log and then committed to the database. Trn.log is the current active transaction log file. Trntmp.log is the next provisioned transaction log file that's created in advance. If the existing Trn.log transaction log file reaches its maximum size, Trn.log is renamed to Trn<em>nnnn</em>.log, where <em>nnnn</em> is a sequence number. Trntmp.log is then renamed Trn.log and becomes the current active transaction log file.</p></td>
</tr>
<tr class="even">
<td><p>Trn.chk</p></td>
<td><p>This checkpoint file tracks the transaction log entries that have been committed to the database. This file is always in the same location as the mail.que file.</p></td>
</tr>
<tr class="odd">
<td><p>Trnres00001.jrs</p>
<p>Trnres00002.jrs</p></td>
<td><p>These reserve transaction log files act as placeholders. They're only used when the hard disk that contains the transaction log runs out of space to stop the queue database cleanly.</p></td>
</tr>
</tbody>
</table>


Return to top

## Options for configuring the queue database

You configure the queue database by adding or modifying keys in the `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML application configuration file. This file is associated with the Microsoft Exchange Transport service. Changes you make to the EdgeTransport.exe.config file take effect after you restart the Microsoft Exchange Transport service.

The `<appSettings>` section of the EdgeTransport.exe.config file is where you can add new keys or modify existing keys. If a specific key doesn't exist, you can add it manually to change its value.

The keys for the queue database that are available in the EdgeTransport.exe.config file are described in the following table.

### Message queue database keys that are available in the EdgeTransport.exe.config file

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Key</th>
<th>Default value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabaseBatchSize</em></p></td>
<td><p>40</p></td>
<td><p>This key specifies the number of database I/O operations that can be grouped together before they're executed. By default, this key doesn't exist in the EdgeTransport.exe.config file.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseBatchTimeout</em></p></td>
<td><p>100</p></td>
<td><p>This key specifies the maximum time in milliseconds that the database will wait for multiple database I/O operations to group before it executes them. The database I/O operations are executed without waiting for any more if the following conditions are true:</p>
<ul>
<li><p>The number of database I/O operations that's specified by the <em>QueueDatabaseBatchSize</em> key hasn't been reached.</p></li>
<li><p>The time specified by the <em>QueueDatabaseBatchTimeout</em> key has passed.</p></li>
</ul>
<p>By default, this key doesn't exist in the EdgeTransport.exe.config file.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxConnections</em></p></td>
<td><p>4</p></td>
<td><p>This key specifies the number of ESE database connections that can be open.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingBufferSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>This key specifies the memory that's used to cache the transaction records before they're written to the transaction log file.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseLoggingFileSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>This key specifies the maximum size of a transaction log file. When the maximum log file size is reached, a new log file is opened.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>This key specifies the default directory for the queue database log files. For instructions on how to change the location of the queue database, see <a href="change-the-location-of-the-queue-database-exchange-2013-help.md">Change the location of the queue database</a>.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxBackgroundCleanupTasks</em></p></td>
<td><p>32</p></td>
<td><p>This key specifies the maximum number of background cleanup work items that can be queued to the database engine thread pool at any time.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragEnabled</em></p></td>
<td><p>True</p></td>
<td><p>The key enables or disables scheduled online defragmentation of the mail queue database. By default, this key doesn't exist in the EdgeTransport.exe.config file.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseOnlineDefragSchedule</em></p></td>
<td><p><code>1:00:00</code> or 1:00 A.M.</p></td>
<td><p>This key specifies the time of day in 24 hour format to start the online defragmentation of the mail queue database. To specify a value, enter the value as a time: <em>hh:mm:ss</em>, where <em>h</em> = hours, <em>m</em> = minutes, and <em>s</em> = seconds.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragTimeToRun</em></p></td>
<td><p><code>3:00:00</code> or 3 hours</p></td>
<td><p>This key specifies the length of time the online defragmentation task is allowed to run. Even if the defragmentation task doesn't finish in the time specified, the queue database is left in a consistent state. To specify a value, enter the value as a time span: <em>hh:mm:ss</em>, where <em>h</em> = hours, <em>m</em> = minutes, and <em>s</em> = seconds.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>This key specifies the default directory for the queue database files. For instructions on how to change the location of the queue database, see <a href="change-the-location-of-the-queue-database-exchange-2013-help.md">Change the location of the queue database</a>.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Any customized per-server settings you make in Exchange XML application configuration files, for example, web.config files on Client Access servers or the EdgeTransport.exe.config file on Mailbox servers, will be overwritten when you install an Exchange Cumulative Update (CU). Make sure that you save this information so you can easily re-configure your server after the install. You must re-configure these settings after you install an Exchange CU.



Return to top

## Queue properties

A queue has many properties that describe the purpose and status of the queue. Some queue properties are applied to the queue when the queue is created, and don't change. Other properties contain status size, time, or other indicators that are updated frequently.

Return to top

## NextHopSolutionKey

The routing component of the categorizer in the Microsoft Exchange Transport service selects the destination for a message, and this destination is used to create the delivery queue. The destination is stamped on every recipient as the **NextHopSolutionKey** attribute. Every unique value of the **NextHopSolutionKey** attribute corresponds to a separate delivery queue.

The **NextHopSolutionKey** attribute contains the following fields:

  - **DeliveryType**   The value of this field represents the results of the categorization of the message, and how the Transport service intends to transmit the message to the next hop, which could be the ultimate destination of the message, or an intermediate hop along the way. The Transport service uses a predefined list of values for **DeliveryType** based on the target routing destination or delivery group.

  - **NextHopDomain**   This field uses specific values based on the value of the **DeliveryType** field. For delivery queues, the value of this field is effectively the name of the queue. The value of **NextHopDomain** isn't always a domain name. For example, the value could be the name of the target Active Directory site or database availability group (DAG). Think of this field as the next hop name, where the value is the name of the routing destination or the target delivery group.

  - **NextHopConnector**   This field uses specific values based on the value of the **DeliveryType** field. The value is always expressed as a GUID. If this field isn't used, the value is a GUID with all zeroes. The value of **NextHopConnector** isn't always the GUID of a connector. For example, the value could be the GUID of the target Active Directory site or DAG. Think of this field as the next hop GUID, where the value is the GUID of the routing destination or the target delivery group.

Exchange 2013 also adds the **NextHopCategory** property to the queue based on the value of **DeliveryType**. The value of **NextHopCategory** is `External` or `Internal`. The value `External` indicates the next hop of the queue is outside the Exchange organization. The value `Internal` indicates the next hop of the queue is inside the Exchange organization. Note that a message for an external recipient may require one or more internal hops before the message is delivered externally.

The values of **DeliveryType**, **NextHopCategory**, **NextHopDomain** and **NextHopConnector** are described in the following table.


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Delivery Type in Queue Viewer</th>
<th>DeliveryType in the Shell</th>
<th>Description</th>
<th>NextHopCategory</th>
<th>NextHopDomain</th>
<th>NextHopConnector</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Delivery Agent</strong></p></td>
<td><p><strong>DeliveryAgent</strong></p></td>
<td><p>The queue holds messages for delivery to recipients in a non-SMTP address space. The messages are delivered by using a Delivery Agent connector that's configured on the local server.</p></td>
<td><p>External</p></td>
<td><p>This value is the destination address space that's configured on the Delivery Agent connector.</p></td>
<td><p>This value is he GUID of the Delivery Agent connector. For example, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p>The queue holds messages for delivery to recipients in an SMTP address space. The messages are delivered by using a Send connector that's configured on the local server. The Send connector is configured to use DNS routing.</p></td>
<td><p>External</p></td>
<td><p>This value is the destination address space that's configured on the Send connector. For example, <code>contoso.com</code>.</p></td>
<td><p>This value is the GUID of the Send connector. For example, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p>The queue holds messages for delivery to recipients in a non-SMTP address space. The messages are delivered by using a Foreign connector that's configured on the local server.</p></td>
<td><p>External</p></td>
<td><p>This value is the destination address space that's configured on the Foreign connector.</p></td>
<td><p>This value is the GUID of the Foreign connector. For example, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p>The queue holds messages for delivery to recipients in an SMTP address space. The messages are delivered by using a Send connector that's configured on the local server. The Send connector is configured to use smart host routing.</p></td>
<td><p>External</p></td>
<td><p>This value is the list of smart hosts that are configured on the Send connector. Smart hosts can be configured as FQDNs, IP addresses or both. The values can be one of the following:</p>
<ul>
<li><p><strong>FQDN</strong>   The syntax is <code>&lt;FQDN1,FQDN2,...&gt;</code>. For example, <code>smarthost01.contoso.com</code> or <code>smarthost01.contoso.com,smarthost02.fabrikam.com</code>.</p></li>
<li><p><strong>IP address</strong>   The syntax is <code>&lt;[IPAddress1],[IPAddress2],...&gt;</code>. For example, <code>[10.10.10.100]</code> or <code>[10.10.10.100],[10.10.10.101]</code>.</p></li>
<li><p><strong>FQDN and IP address</strong>   The syntax is <code>&lt;[IPAddress1],FQDN1,...&gt;</code>, and depends on how the smart hosts are listed on the Send connector. For example, <code>[172.17.17.7],relay.tailspintoys.com</code> or <code>mail.contoso.com,[192.168.1.50]</code>.</p></li>
</ul></td>
<td><p>This value is the GUID of the Send connector. For example, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SMTP Delivery to Mailbox</strong></p></td>
<td><p><strong>SmtpDeliveryToMailbox</strong></p></td>
<td><p>The queue holds messages for delivery to Exchange 2013 mailbox recipients. The destination mailbox database is in one of the following locations:</p>
<ul>
<li><p>The local Exchange 2013 Mailbox server.</p></li>
<li><p>An Exchange 2013 Mailbox server in the same DAG.</p></li>
<li><p>An Exchange 2013 Mailbox server in the same Active Directory site in non-DAG environments.</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>This value is the name of the destination mailbox database. For example, <code>Mailbox Database 0471695037</code>.</p></td>
<td><p>This value is the GUID of the target mailbox database. For example, <code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP Relay to Send Connector Source Servers</strong></p></td>
<td><p><strong>SmtpRelayToConnectorSourceServers</strong></p></td>
<td><p>The queue holds messages for delivery to SMTP or non-SMTP recipients. The messages are delivered by using a Send connector, Delivery Agent connector, or Foreign connector that's configured on a remote transport server. The remote transport server could be an Exchange 2013 Mailbox server, or an Exchange 2007 or Exchange 2010 Hub Transport server from a previous version of Exchange. The remote server could be located in the local Active Directory site, or in a remote Active Directory site.</p></td>
<td><p>Internal</p></td>
<td><p>This value is the name of the destination Send connector, Delivery Agent connector, or Foreign connector. For example, <code>Contoso.com Send Connector</code>.</p></td>
<td><p>This value is the GUID of the destination Send connector, Delivery Agent connector, or Foreign connector. For example, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SMTP Relay to Database Availability Group</strong></p></td>
<td><p><strong>SmtpRelayToDag</strong></p></td>
<td><p>The queue holds messages for delivery to Exchange 2013 mailbox recipients, where the destination mailbox database is located in a remote DAG. The remote DAG could be in the local Active Directory site, or a remote Active Directory site.</p></td>
<td><p>Internal</p></td>
<td><p>This value is the name of the destination DAG. For example, <code>DAG1</code>.</p></td>
<td><p>This value is the GUID of the destination DAG. For example, <code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code></p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP Relay to Mailbox Delivery Group</strong></p></td>
<td><p><strong>SmtpRelayToMailboxDeliveryGroup</strong></p></td>
<td><p>The queue holds messages for delivery to legacy mailbox recipients, where the destination mailbox is on an Exchange 2007 or Exchange 2010 Mailbox server. The message is related to a Hub Transport server that's running the same version of Exchange as the destination mailbox. The destination Hub Transport server could be in the local Active Directory site, or a remote Active Directory site.</p></td>
<td><p>Internal</p></td>
<td><p>The queue name uses the syntax: <code>Site:&lt;ADSiteName&gt;;Version:&lt;ExchangeVersion&gt;</code>, where <em>&lt;ADSiteName&gt;</em> is the name of the destination Active Directory site, and <em>&lt;ExchangeVersion&gt;</em> is the version of Exchange on the Mailbox server.</p></td>
<td><p>This value is blank.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SMTP Relay to Remote Active Directory Site</strong></p></td>
<td><p><strong>SmtpRelayToRemoteActiveDirectorySite</strong></p></td>
<td><p>The queue holds messages for delivery to a remote destination, and the routing topology requires the message to be routed through a specific Active Directory site. The site is an intermediate hop on the way to the final destination. This situation occurs under the following circumstances:</p>
<ul>
<li><p>The message needs to be routed through a hub site.</p></li>
<li><p>The message requires delivery through a Send connector that's configured on an Edge Transport server that's subscribed to a remote Active Directory site.</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>This value is the target Active Directory site name. For example, <code>NorthAmericanSite</code>.</p></td>
<td><p>This value is the GUID of the target Active Directory site. For example, <code>bfd6c3df-5b65-8bfb-53f1f2c0d55c</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP Relay to Specified Exchange Servers</strong></p></td>
<td><p><strong>SmtpRelayToServers</strong></p></td>
<td><p>The queue holds messages for delivery to a distribution group that's configured for a specific expansion server. The expansion could be an Exchange 2013 Mailbox server, or an Exchange 2007 or Exchange 2010 Hub Transport server. The server could be in the local Active Directory site, or in a remote Active Directory site.</p></td>
<td><p>Internal</p></td>
<td><p>This value is the FQDN of the target expansion server. For example, <code>mailbox01.contoso.com</code>.</p></td>
<td><p>This value is <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SMTP Relay in Active Directory Site to Edge Transport Server</strong></p></td>
<td><p><strong>SmtpRelayWithinAdSiteToEdge</strong></p></td>
<td><p>The queue holds messages for delivery to an SMTP address space. The messages are delivered by using a Send connector that's configured on an Edge Transport server that's subscribed to the local Active Directory site.</p></td>
<td><p>Internal</p></td>
<td><p>This value is the name of the Send connector that sends outbound Internet mail from the organization to the Internet. This Send connector is automatically created by the Edge subscription, and is named <code>EdgeSync - &lt;ADSiteName&gt; to Internet</code>. <em>&lt;ADSiteName&gt;</em> is the name of the local Active Directory site to which the Edge Transport server is subscribed.</p></td>
<td><p>This value is the GUID of the Send connector. For example, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Heartbeat</strong></p></td>
<td><p><strong>Heartbeat</strong></p></td>
<td><p>This value is reserved for internal Microsoft use. For more information about heartbeat, see <a href="shadow-redundancy-exchange-2013-help.md">Shadow redundancy</a>.</p></td>
<td><p>n/a</p></td>
<td><p>n/a</p></td>
<td><p>n/a</p></td>
</tr>
<tr class="odd">
<td><p><strong>Shadow Redundancy</strong></p></td>
<td><p><strong>ShadowRedundancy</strong></p></td>
<td><p>The queue holds messages in a shadow queue. A shadow queue holds redundant copies messages in transit in case the primary messages aren't successfully delivered. For more information, see <a href="shadow-redundancy-exchange-2013-help.md">Shadow redundancy</a>.</p></td>
<td><p>Internal</p></td>
<td><p>This value is the FQDN of the primary server for which the shadow queue is holding redundant copies of the primary messages. For example, <code>mailbox01.contoso.com</code>.</p></td>
<td><p>This value is <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Undefined</strong></p></td>
<td><p><strong>Undefined</strong></p></td>
<td><p>This value is used only on the Submission queue and the poison message queue.</p></td>
<td><p>Internal</p></td>
<td><p>For the Submission queue, this value is <code>Submisssion</code>. For the poison message queue, this value is <code>Poison Message</code>.</p></td>
<td><p>This value is <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Undreachable</strong></p></td>
<td><p><strong>Unreachable</strong></p></td>
<td><p>This value is used only on the Unreachable queue.</p></td>
<td><p>Internal</p></td>
<td><p>This value is <code>Unreachable Domain</code>.</p></td>
<td><p>This value is <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
</tbody>
</table>


Note that Exchange 2013 supports legacy values of **DeliveryType** for backwards compatibility with previous versions of Exchange. These values are available in Queue Viewer and the Shell, but they aren't used by Exchange 2013. These legacy **DeliveryType** values are:

  - **MapiDelivery**   The queue holds messages for delivery by an Exchange 2007 or Exchange 2010 Hub Transport server to a mailbox on an Exchange 2007 or Exchange 2010 Mailbox server in the local Active Directory site.

  - **SmtpRelayWithinAdSite**   The queue holds messages for delivery by an Exchange 2007 or Exchange 2010 Hub Transport server to another Hub Transport server in the same Active Directory site. The destination Hub Transport server can be the source server for a connector, or a distribution group expansion server.

  - **SmtpRelaytoTiRg**   The queue holds messages for delivery by an Exchange 2007 or Exchange 2010 Hub Transport server to an Exchange Server 2003 routing group. The destination server can be the source server for a connector, a distribution group expansion server, or an Exchange 2003 bridgehead server.

Return to top

## IncomingRate, OutgoingRate, and Velocity

Exchange 2013 measures the rate of messages entering and leaving a queue and stores these values in queue properties. You can use these rates as an indicator of queue and transport server health. The properties are:

  - **IncomingRate**   This property is the rate that messages are entering the queue.
    
    This value is calculated from the number of messages entering the queue every 5 seconds averaged over the last 60 seconds. The formula can be expressed as `(i1+i2+i3+i4+i5+i6)/6`, where i*n* = the number of incoming messages in 5 seconds.

  - **OutgoingRate**   This property is the rate that messages are leaving the queue.
    
    This value is calculated from the number of messages leaving the queue every 5 seconds averaged over the last 60 seconds. The formula can be expressed as `(o1+o2+o3+o4+o5+o6)/6`, where o*n* = the number of outgoing messages in 5 seconds.

  - **Velocity**   This property is the drain rate of the queue, and is calculated by subtracting the value of **IncomingRate** from the value of **OutgoingRate**.
    
    If the value of **Velocity** is greater than 0, messages are leaving the queue faster than they are entering the queue.
    
    If the value of **Velocity** is equals 0, messages are leaving the queue as fast as they are entering the queue. This is also the value you'll see when the queue is inactive.
    
    If the value of **Velocity** is less than 0, messages are entering the queue faster than they are leaving the queue.

At a basic level, a positive value of **Velocity** indicates a healthy queue that's efficiently draining, and a negative value of **Velocity** indicates a queue that isn't efficiently draining. However, you also need to consider the values of the **IncomingRate**, **OutgoingRate**, and **MessageCount** properties, as well as the magnitude of the **Velocity** value for the queue. For example, a queue that has a large negative value of **Velocity**, a large **MessageCount** value, a small **OutgoingRate** value, and a large **IncominRate** value are accurate indicators that the queue isn't draining properly. However, a queue with a negative **Velocity** value that's very close to zero that also has very small values for **IncomingRate**, **OutgoingRate**, and **MessageCount** doesn't indicate a problem with the queue.

Return to top

## Queue status

The current status of a queue is stored in the **Status** property of the queue. A queue can have one of the following status values:

  - **Active**   The queue is actively transmitting messages.

  - **Connecting**   The queue is in the process of connecting to the next hop.

  - **Ready**   The queue recently transmitted messages, but the queue is now empty.

  - **Retry**   The last automatic or manual connection attempt failed, and the queue is waiting to retry the connection.

  - **Suspended**   The queue has been manually suspended by an administrator to prevent message delivery. New messages can enter the queue, and messages that are in the act of being transmitted to the next hop will finish delivery and leave the queue. Otherwise, messages won't leave the queue until the queue is manually resumed by an administrator. Note that suspending a queue doesn’t change the status of the individual messages in the queue.
    
    You can suspend a queue that has a status of Active or Retry. You can also suspend the Unreachable queue and the Submission queue.
    
    If you suspend the Unreachable queue, messages won't be automatically resubmitted to the categorizer when configuration updates are detected. To automatically resubmit these messages, you need to manually resume the Unreachable queue. If you suspend the Submission queue, messages won't be picked up by the categorizer until the queue is resumed.

Return to top

## Other queue properties

There are other queue properties that are self-explanatory. You use most of the queue properties as filter options. By specifying filter criteria, you can quickly locate queues and take action on them. For a complete description of the filterable queue properties, see [Queue filters](queue-filters-exchange-2013-help.md).

An important queue property that's also worth mentioning here is the **MessageCount** property that shows how many messages are in a queue. This property is an important indicator of queue health. For example, a delivery queue that contains a large number of messages that continues to grow and never decreases could indicate a routing or transport pipeline issue that requires your attention.

Return to top

## Message properties

A message in a queue has many properties. Many of the properties reflect the information that was used to create the message. Some of the messages status and information properties are heavily influenced by corresponding properties on the queue. However, an individual message may have a different value than the corresponding property of the queue. Other properties contains status, time, or other indicators that are updated frequently.

Return to top

## Message status

The current status of a message is stored in the **Status** property of the message. A message can have one of the following status values:

  - **Active**   If the message is in a delivery queue, the message is being delivered to its destination. If the message is in the Submission queue, the message is being processed by the categorizer.

  - **Locked**   This value is reserved for internal Microsoft use, and isn't used in on-premises Exchange organizations.

  - **PendingRemove**   The message was deleted by the administrator, but the message was already in the act of being transmitted to the next hop. The message will be deleted if the delivery ends in an error that causes the message to reenter the queue. Otherwise, delivery will continue.

  - **PendingSuspend**   The message was suspended by the administrator, but the message was already in the act of being transmitted to the next hop.. The message will be suspended if the delivery ends in an error that causes the message to reenter the queue. Otherwise, delivery will continue.

  - **Ready**   The message is waiting in the queue and is ready to be processed.

  - **Retry**   The last automatic or manual connection attempt for the queue in which this message is located failed. The message is waiting for the next automatic queue connection retry.

  - **Suspended**   The message was manually suspended by the administrator. All messages in the poison message queue are in a permanently suspended state.

Return to top

## Other message properties

There are other message properties that are self-explanatory. You can use most of the message properties as filter options. By specifying filter criteria, you can quickly locate messages and take action on them. For a complete description of the filterable message properties, see [Message filters](message-filters-exchange-2013-help.md).

Return to top

## Manage queues and messages in queues

Queue Viewer and virtually all of the queue and message management cmdlets are restricted to a single Exchange server. You can view or operate on individual queues or messages, or multiple queues or messages, but only on a specific server.

Exchange 2013 introduces the **Get-QueueDigest** cmdlet that provides a high-level, aggregate view of the state of queues on all servers within a specific scope, for example, a DAG, an Active Directory site, a list of servers, or the entire Active Directory forest. Note that queues on a subscribed Edge Transport server in the perimeter network aren't included in the results. Also, **Get-QueueDigest** is available on an Edge Transport server, but the results are restricted to queues on the Edge Transport server.


> [!NOTE]
> By default, the <STRONG>Get-QueueDigest</STRONG> cmdlet displays delivery queues that contain ten or more messages, and the results are between one and two minutes old. For instructions on how to change these default values, see <A href="configure-get-queuedigest-exchange-2013-help.md">Configure Get-QueueDigest</A>.



The following table describes the management tasks you can perform on queues or messages in queues.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Task</th>
<th>Description</th>
<th>Tool to use</th>
<th>Instructions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>View and filter queues on a server</p></td>
<td><p>This action displays one or more queues on a transport server. You can use the results to take action on the queues.</p></td>
<td><p>Queue Viewer or the <strong>Get-Queue</strong> cmdlet.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Manage queues</a></p></td>
</tr>
<tr class="even">
<td><p>View and filter queues on specific servers in specific DAGs, specific Active Directory sites, or in the whole Active Directory forest.</p></td>
<td><p>This action displays a summary view of queues across a defined scope (servers, DAGs, Active Directory sites, or the entire Active Directory forest).</p></td>
<td><p><strong>Get-QueueDigest</strong> cmdlet only</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Manage queues</a></p></td>
</tr>
<tr class="odd">
<td><p>Suspend queues</p></td>
<td><p>This action temporarily prevents delivery of messages that are currently in the queue. The queue continues to accept new messages, but no messages leave the queue.</p></td>
<td><p>Queue Viewer or the <strong>Suspend-Queue</strong> cmdlet.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Manage queues</a></p></td>
</tr>
<tr class="even">
<td><p>Resume queues</p></td>
<td><p>This action reverses the effect of the suspend queue action and enables delivery of queued messages to resume.</p></td>
<td><p>Queue Viewer or the <strong>Resume-Queue</strong> cmdlet.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Manage queues</a></p></td>
</tr>
<tr class="odd">
<td><p>Retry queues</p></td>
<td><p>This action immediately tries to connect to the next hop. Without manual intervention, when the connection to the next hop fails, the connection is attempted a specific number of times after a specific time interval between each attempt.</p>
<p>Whether the connection attempt is manual or automatic, any connection attempt resets the next retry time. For more information, see <a href="message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md">Message retry, resubmit, and expiration intervals</a>.</p></td>
<td><p>Queue Viewer or the <strong>Retry-Queue</strong> cmdlet.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Manage queues</a></p></td>
</tr>
<tr class="even">
<td><p>Resubmit messages in queues</p></td>
<td><p>This action causes the messages in the queue to be resubmitted to the Submission queue and to go back through the categorization process.</p></td>
<td><p><strong>Retry-Queue</strong> with the <em>Resubmit</em> parameter</p>
<p>Note that you can use Queue Viewer to resubmit messages, but only from the poison message queue. To resubmit a message in poison message, you resume the message in Queue Viewer, or by using the <strong>Resume-Message</strong> cmdlet.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Manage queues</a></p></td>
</tr>
<tr class="odd">
<td><p>Suspend messages in queues</p></td>
<td><p>This action temporarily prevents delivery of a message. You can use the suspend message action to prevent delivery of a message to all the recipients in a specific queue or to all recipients in all queues.</p></td>
<td><p>Queue Viewer or the <strong>Suspend-Message</strong> cmdlet.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Manage messages in queues</a></p></td>
</tr>
<tr class="even">
<td><p>Resume messages in queues</p></td>
<td><p>This action reverses the effect of the suspend message action and enables delivery of queued messages to resume. You can use the resume message action to resume delivery of a message to all the recipients in a specific queue or to all recipients in all queues.</p></td>
<td><p>Queue Viewer or the <strong>Resume-Message</strong> cmdlet.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Manage messages in queues</a></p></td>
</tr>
<tr class="odd">
<td><p>Remove messages from queues</p></td>
<td><p>This action permanently prevents delivery of a message. You can use the remove message action to prevent delivery of a message to any recipients in a specified queue or to all recipients in all queues. You can also configure the remove message action to send a non-delivery report (NDR) to the sender when the message is removed.</p></td>
<td><p>Queue Viewer or the <strong>Remove-Message</strong> cmdlet.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Manage messages in queues</a></p></td>
</tr>
<tr class="even">
<td><p>Export messages from queues</p></td>
<td><p>This action copies a message to the file path that you specify. The messages aren't deleted from the queue, but a copy of the message is saved to a file location. This enables administrators or officials in an organization to later examine the messages. Before you export a message, you need to suspend the message in the queue so that typical delivery doesn't continue during the export process.</p></td>
<td><p><strong>Export-Message</strong> cmdlet only.</p></td>
<td><p><a href="export-messages-from-queues-exchange-2013-help.md">Export messages from queues</a></p></td>
</tr>
</tbody>
</table>


Return to top

