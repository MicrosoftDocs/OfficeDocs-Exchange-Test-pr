---
title: 'Back pressure: Exchange 2013 Help'
TOCTitle: Back pressure
ms:assetid: 03003544-e802-4988-9427-5fc4da64dcb8
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb201658(v=EXCHG.150)
ms:contentKeyID: 50934208
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Back pressure

 

_**Applies to:** Exchange Server 2013_


Back pressure is a system resource monitoring feature of the Microsoft Exchange Transport service that exists on Microsoft Exchange 2013 Mailbox servers and Edge Transport servers.

Exchange can detect when vital resources, such as available hard drive space and memory, are under pressure, and take action in an attempt to prevent service unavailability. Back pressure prevents the system resources from being completely overwhelmed, and the Exchange server tries to process the existing messages before accepting any new messages. When utilization of the system resource returns to a normal level, the Exchange server gradually resumes normal operation and starts accepting new messages again.

In Exchange 2013, when the Transport service on a Mailbox server or an Edge Transport server is under resource pressure, incoming connections are accepted, but incoming messages over those connections are either accepted at a slower rate or are rejected. When an SMTP host attempts to connect to an Exchange server that's under resurce pressure, the connection will succeed. However, when the host issues the **MAIL FROM** command to submit a message, depending on the resource that's under pressure, the Transport service either delays the acknowledgement of the **MAIL FROM** command or rejects the connection.

**Contents**

Resources monitored

Actions taken by Exchange Transport when under resource pressure

Back pressure configuration options in the EdgeTransport.exe.config file

Back pressure logging information

## Resources monitored

The following system resources are monitored as part of the back pressure feature:

  - Free space on the hard drive that stores the message queue database.

  - Free space on the hard drive that stores the message queue database transaction logs.

  - The number of uncommitted message queue database transactions that exist in memory.

  - The memory that's used by the EdgeTransport.exe process.

  - The memory that's used by all other processes.

  - The number of messages in the Submission queue.

For each monitored system resource on a Mailbox server or Edge Transport server, the following three levels of resource utilization are applied:

  - **Normal**   The resource isn't overused. The server accepts new connections and messages.

  - **Medium**   The resource is slightly overused. Back pressure is applied to the server in a limited manner. Mail from senders in the authoritative domain can flow. However, depending on the specific resource under pressure, the server uses tarpitting to delay server response or rejects incoming **MAIL FROM** commands from other sources.

  - **High**   The resource is severely overused. Full back pressure is applied. All message flow stops, and the server rejects all new incoming **MAIL FROM** commands.

The following sections explain how Exchange handles the situation when a specific resource is under pressure.

## Free hard drive space for the message queue database

By default, the message queue database is stored at %ExchangeInstallPath%TransportRoles\\data\\Queue. Exchange monitors the hard drive space utilization for this location. The high level of hard drive space utilization is calculated by using the following formula:

100 \* (*hard disk size* - *fixed constant*) / *hard drive size*

The value of *fixed constant* is 500 megabytes (MB).

The results of this formula are expressed as a percentage of the total hard drive space that's being used. The results of the formula are always rounded down to the nearest integer. By default, the medium level of hard drive utilization is 2 percent less than the high level. By default, the normal level of hard drive utilization is 4 percent less than the high level.

Return to top

## Free hard drive space for the message queue database transaction logs

By default, the message queue database transaction logs are stored at %ExchangeInstallPath%TransportRoles\\data\\Queue. Exchange monitors the hard drive space utilization for this location. The %ExchangeInstallPath%Bin\\EdgeTransport.exe.config application configuration file contains a *DatabaseCheckPointDepthMax* key that has a default value of 384 MB. This key controls the total allowed size of all uncommitted transaction logs that exist on the hard drive. This key is used in the formula that calculates hard drive utilization.


> [!NOTE]
> The value of the <EM>DatabaseCheckPointDepthMax</EM> key applies to all transport-related Extensible Storage Engine (ESE) databases that exist on the Mailbox server or Edge Transport server. This would include the message queue database and the IP filter database.



By default, the high level of disk utilization is calculated by using the following formula:

100 \* (*hard drive size* - Min(5 GB, 3\**DatabaseCheckPointDepthMax*)) / *hard drive size*

The results of the formula are always rounded down to the nearest integer. By default, the medium level of hard drive utilization is 2 percent less than the high level. The normal level of hard drive utilization is 4 percent less than the high level.

Return to top

## Number of uncommitted message queue database transactions in memory

A list of changes that are made to the message queue database is kept in memory until those changes can be committed to a transaction log. Then the list is committed to the message queue database itself. These outstanding message queue database transactions that are kept in memory are known as *version buckets*. The number of version buckets may increase to unacceptably high levels because of an unexpectedly high volume of incoming messages, spam attacks, problems with the message queue database integrity, or hard drive performance.

When Exchange starts receiving messages, these messages are grouped together in batches and then prepared as version buckets. If an incoming message has a large attachment, it can be separated into multiple batches. These batches that are being processed are known as *batch points*. The number of outstanding batch points can exceed the set thresholds, especially when there's an unexpectedly high volume of incoming messages with large attachments.

When version buckets or batch points are under pressure, the Exchange server will start throttling incoming connections by delaying acknowledgement to incoming messages. Exchange will reduce the rate of inbound message flow by tarpitting, which introduces a delay to the **MAIL FROM** commands. If the resource pressure condition continues, Exchange will gradually increase the tarpitting delay. After the resource utilization returns to normal, Exchange will gradually start reducing the acknowledgement delay and ease into normal operation. By default, Exchange will start delaying message acknowledgements 10 seconds when under resource pressure. If the resources continue to be under pressure, the delay is increased in 5-second increments up to 55 seconds.

Exchange keeps a history of version bucket and batch point resource utilization. If the resource utilization doesn't go down to normal level for a specific number of polling intervals, known as the history depth, Exchange will stop the tarpitting delay and start rejecting incoming messages until the resource utilization goes back to normal. By default, the history depths for version buckets and batch points are in 10 and 300 polling intervals respectively.

Return to top

## Memory used by the EdgeTransport.exe process

By default, the high level of memory utilization by the EdgeTransport.exe process is calculated by using the following formula:

75 percent of the total physical memory or 1 terabyte, whichever is less

This calculation doesn't include virtual memory that's available on the hard drive in the paging file, or the memory that's used by other processes. The results of this formula are expressed as a percentage of the total memory that's used by the EdgeTransport.exe process. The results of the formula are always rounded down to the nearest integer.

By default, the medium level of memory utilization by the EdgeTransport.exe file is calculated as 73 percent of the total physical memory or 2 percent less than the value of the high level, whichever is less. By default, the normal level of memory utilization by the EdgeTransport.exe file is calculated as 71 percent of the total physical memory or 4 percent less than the value of the high level, whichever is less.

If the memory utilization of the EdgeTransport.exe process is higher than the specified normal level, *garbage collection* is forced. Garbage collection is a process that checks for unused objects that exist in memory, and reclaims the memory that's used by those unused objects.

Exchange keeps a history of the memory utilization of the EdgeTransport.exe process. If the utilization doesn't go down to normal level for a specific number of polling intervals, known as the history depth, Exchange will start rejecting incoming messages until the resource utilization goes back to normal. By default, the history depth for EdgeTransport.exe memory utilization is 30 polling intervals.

Return to top

## Memory used by all processes

By default, the high level of memory utilization by all processes is 94 percent of total physical memory. This value doesn't include virtual memory that's available on the hard drive in the paging file.

When the specified memory utilization level is reached, *message dehydration* occurs. Message dehydration is the act of removing unnecessary elements of queued messages that are cached in memory. Complete messages are cached in memory for enhanced performance. Removal of the MIME content of queued messages from memory reduces the memory that's used at the expense of higher latency because the messages are read directly from the message queue database. By default, message dehydration is enabled.

Return to top

## Number of messages in the Submission queue

The Submission queue is associated with the Transport service on Exchange 2013 Mailbox servers and on Edge Transport servers. The categorizer processes each message in the Submission queue. This categorization results in the message being put in a delivery queue. For more information, see [Mail flow](mail-flow-exchange-2013-help.md) and [Queues](queues-exchange-2013-help.md). A large number of messages in the Submission queue indicates the categorizer is having difficulty processing messages.

When the Submission queue is under pressure, the Exchange server will start throttling incoming connections by delaying acknowledgement to incoming messages. Exchange will reduce the rate of inbound message flow by tarpitting, which introduces a delay to the **MAIL FROM** commands. If the Submission queue pressure condition continues, Exchange will gradually increase the tarpitting delay. After the Submission queue utilization returns to normal, Exchange will gradually start reducing the acknowledgement delay and ease into normal operation. By default, Exchange will start delaying message acknowledgements 10 seconds when under Submission queue pressure. If the Submission queue continues to be under pressure, the delay is increased in 5-second increments up to 55 seconds.

Exchange keeps a history of Submission queue utilization. If the Submission queue utilization doesn't go down to normal level for a specific number of polling intervals, known as the history depth, Exchange will stop the tarpitting delay and start rejecting incoming messages until the Submission utilization goes back to normal. By default, the history depth for the Submission queue is in 300 polling intervals.

## Actions taken by Exchange Transport when under resource pressure

The following table summarizes the actions taken by Exchange transport when a specific resource is under pressure.

### Back pressure actions taken by Mailbox and Edge Transport servers when responding to resource pressure

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Resource under pressure</th>
<th>Utilization level</th>
<th>Actions taken</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Hard drive space for message queue database</p></td>
<td><p>Medium</p></td>
<td><ul>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Hard drive space for message queue database</p></td>
<td><p>High</p></td>
<td><ul>
<li><p>Reject incoming messages from other Exchange servers</p></li>
<li><p>Reject message submissions from mailbox databases by the Mailbox Transport Submission service on Mailbox servers</p></li>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Hard drive space for message queue database transaction logs</p></td>
<td><p>Medium</p></td>
<td><ul>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Hard drive space for message queue database transaction logs</p></td>
<td><p>High</p></td>
<td><ul>
<li><p>Reject incoming messages from other Exchange servers</p></li>
<li><p>Reject message submissions from mailbox databases by the Mailbox Transport Submission service on Mailbox servers</p></li>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Version buckets</p></td>
<td><p>Medium</p></td>
<td><p>Introduce or increment the tarpitting delay to incoming messages. If normal level isn't reached for the entire version bucket history depth, take the following actions:</p>
<ul>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Version buckets</p></td>
<td><p>High</p></td>
<td><p>Introduce or increment the tarpitting delay to incoming messages. If normal level isn't reached for the entire version bucket history depth, take the following actions:</p>
<ul>
<li><p>Reject incoming messages from other Exchange servers</p></li>
<li><p>Reject message submissions from mailbox databases by the Mailbox Transport Submission service on Mailbox servers</p></li>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Batch point</p></td>
<td><p>Medium</p></td>
<td><p>Introduce or increment the tarpitting delay to incoming messages. If normal level isn't reached for the entire batch point history depth, take the following actions:</p>
<ul>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Batch point</p></td>
<td><p>High</p></td>
<td><p>Introduce or increment the tarpitting delay to incoming messages. If normal level isn't reached for the entire batch point history depth, take the following actions:</p>
<ul>
<li><p>Reject incoming messages from other Exchange servers</p></li>
<li><p>Reject message submissions from mailbox databases by the Mailbox Transport Submission service on Mailbox servers</p></li>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Memory used by EdgeTransport.exe process</p></td>
<td><p>Medium</p></td>
<td><ul>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
<li><p>Force garbage collection</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Memory used by EdgeTransport.exe process</p></td>
<td><p>High</p></td>
<td><ul>
<li><p>Reject incoming messages from other Exchange servers</p></li>
<li><p>Reject message submissions from mailbox databases by the Mailbox Transport Submission service on Mailbox servers</p></li>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Memory used by all processes</p></td>
<td><p>Medium</p></td>
<td><ul>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
<li><p>Force garbage collection</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Memory used by all processes</p></td>
<td><p>High</p></td>
<td><ul>
<li><p>Reject incoming messages from other Exchange servers</p></li>
<li><p>Reject message submissions from mailbox databases by the Mailbox Transport Submission service on Mailbox servers</p></li>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
<li><p>Flush enhanced DNS cache from memory</p></li>
<li><p>Start message dehydration</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Number of messages in the Submission queue</p></td>
<td><p>Medium</p></td>
<td><p>Introduce or increment the tarpitting delay to incoming messages. If normal level isn't reached for the entire Submission queue history depth, take the following actions:</p>
<ul>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
<li><p>Force garbage collection</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Number of messages in the Submission queue</p></td>
<td><p>High</p></td>
<td><p>Introduce or increment the tarpitting delay to incoming messages. If normal level isn't reached for the entire Submission queue history depth, take the following actions:</p>
<ul>
<li><p>Reject incoming messages from other Exchange servers</p></li>
<li><p>Reject message submissions from mailbox databases by the Mailbox Transport Submissions service on Mailbox servers</p></li>
<li><p>Reject incoming messages from non-Exchange servers</p></li>
<li><p>Reject message submissions from Pickup and Replay directories</p></li>
<li><p>Flush enhanced DNS cache from memory</p></li>
<li><p>Start message dehydration</p></li>
</ul></td>
</tr>
</tbody>
</table>


Return to top

## Back pressure configuration options in the EdgeTransport.exe.config file

All configuration options for back pressure are available in the %ExchangeInstallPath%Bin\\EdgeTransport.exe.config XML application configuration file.


> [!WARNING]
> These settings are listed as a reference only. We strongly discourage any modifications to the back pressure settings in the EdgeTransport.exe.config file. Modifications to the back pressure settings may result in poor performance or data loss. We recommend that you investigate and correct the root cause of any back pressure events that you may encounter.



### Back pressure configuration options

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Key name</th>
<th>Default value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>EnableResourceMonitoring</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>ResourceMonitoringInterval</em></p></td>
<td><p><code>00:00:02</code> (2 seconds)</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. This value indicates that the default formula will be used.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. This value indicates that the actual value is 2 percent less than the value of <em>PercentageDatabaseDiskSpaceUsedHighThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. This value indicates that the actual value is 2 percent less than the value of <em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. This value indicates that the default formula will be used.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. This value indicates that the actual value is 2 percent less than the value of <em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. This value indicates that the actual value is 2 percent less than the value of <em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedHighThreshold</em></p></td>
<td><p>0. This value indicates that the default calculation will be used.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePrivateBytesUsedMediumThreshold</em></p></td>
<td><p>0. This value indicates that the actual value is 2 percent less than the value of <em>PercentagePrivateBytesUsedHighThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedNormalThreshold</em></p></td>
<td><p>0. This value indicates that the actual value is 2 percent less than the value of <em>PercentagePrivateBytesUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsHighThreshold</em></p></td>
<td><p>200</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsMediumThreshold</em></p></td>
<td><p>120</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsNormalThreshold</em></p></td>
<td><p>80</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsHistoryDepth</em></p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointHighThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointMediumThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointNormalThreshold</em></p></td>
<td><p>1000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointUseCostForPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointBatchSize</em></p></td>
<td><p>40</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointBatchTimeout</em></p></td>
<td><p><code>00:00:00.100</code> (0.1 seconds)</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointItemExpiryInterval</em></p></td>
<td><p><code>00:05:00</code> (5 minutes)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPBaseThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:00</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPMaxThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:55</code> (55 seconds)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPStepThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:05</code> (5 seconds)</p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPStartThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:10</code> (10 seconds)</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePhysicalMemoryUsedLimit</em></p></td>
<td><p>94</p></td>
</tr>
<tr class="odd">
<td><p><em>DehydrateMessagesUnderMemoryPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateBytesHistoryDepth</em></p></td>
<td><p>30</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueHighThreshold</em></p></td>
<td><p>10000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueMediumThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueNormalThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
</tbody>
</table>


Return to top

## Back pressure logging information

The following list describes the event log entries that are generated by specific back pressure events in Exchange:

  - **Event log entry for an increase in any resource utilization level**
    
    Event Type: Error
    
    Event Source: MSExchangeTransport
    
    Event Category: Resource Manager
    
    Event ID: 15004
    
    Description: Resource pressure increased from *Previous Utilization Level* to *Current Utilization Level*.

  - **Event log entry for a decrease in any resource utilization level**
    
    Event Type: Information
    
    Event Source: MSExchangeTransport
    
    Event Category: Resource Manager
    
    Event ID: 15005
    
    Description: Resource pressure decreased from *Previous Utilization Level* to *Current Utilization Level*.

  - **Event log entry for critically low available disk space**
    
    Event Type: Error
    
    Event Source: MSExchangeTransport
    
    Event Category: Resource Manager
    
    Event ID: 15006
    
    Description: The Microsoft Exchange Transport service is rejecting messages because available disk space is below the configured threshold. Administrative action may be required to free disk space for the service to continue operations.

  - **Event log entry for critically low available memory**
    
    Event Type: Error
    
    Event Source: MSExchangeTransport
    
    Event Category: Resource Manager
    
    Event ID: 15007
    
    Description: The Microsoft Exchange Transport service is rejecting message submissions because the service continues to consume more memory than the configured threshold. This may require that this service be restarted to continue normal operation.

Return to top

