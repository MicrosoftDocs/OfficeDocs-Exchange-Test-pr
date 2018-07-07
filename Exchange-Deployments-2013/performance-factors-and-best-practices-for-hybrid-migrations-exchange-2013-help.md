---
title: 'Performance factors and best practices for hybrid migrations: Exchange 2013 Help'
TOCTitle: Performance factors and best practices for hybrid migrations
ms:assetid: 120a7832-d2d3-47d7-b305-918360c2ef66
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Mt483789(v=EXCHG.150)
ms:contentKeyID: 69135272
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
---

# Performance factors and best practices for hybrid migrations

 

_**Applies to:** Exchange Server 2016_


There are many paths to migrate data from an on-premises email organization to Office 365. When planning a migration to Office 365, a common question is about how to improve the performance of data migration and optimize migration velocity. This article discusses migration performance for Exchange hybrid deployments, For performance information about other migration methods, see [Office 365 migration performance and best practices](http://go.microsoft.com/fwlink/p/?linkid=623651).

## Performance factors and best practices for hybrid migrations

Hybrid deployment migration supports the smooth migration between on-premises Exchange servers and Exchange Online in Office 365.

Hybrid deployment migration is by far the fastest migration method to migrate mailbox data to Office 365. We have seen up to 100 GB/hour throughput during real customer deployments The follow table provides a list of factors that apply to native Office 365 hybrid migration scenarios.

If your on-premises environment contains multiple sites in geographically spread locations, you can improve migration performance by creating geographically close migration endpoints. This is because as in such a scenario the migration uses Microsoft's network compared to using a centralized migration endpoint that uses the your on-premises network.

## Factor 1: Data source (Exchange Server)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Checklist</th>
<th>Description</th>
<th>Best practices</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>System performance</p></td>
<td><p>Data extraction is an intensive task. The source system must have sufficient resources, such as CPU time and memory, to provide better migration performance. At the time of migration, the source system is usually close to full capacity to serve regular end-user workload—additional migration workload sometimes even brings down end users' access because of a lack of system resources.</p></td>
<td><p>Monitor system performance during a pilot migration test. If the system is busy, we recommend avoiding an aggressive migration schedule for the specific system because of potential migration slowness and service availability issues. If possible, enhance the source system performance by adding hardware resources and reducing the load on the system by moving tasks and users to other servers that aren’t involved in the migration.</p>
<p>For more information see:</p>
<ul>
<li><p><a href="http://go.microsoft.com/fwlink/?linkid=723566">Ask the Perf Guy: Sizing Exchange 2016 Deployments</a></p></li>
<li><p><a href="https://technet.microsoft.com/en-us/library/jj150551(v=exchg.150)">Server health and performance</a></p></li>
<li><p><a href="http://technet.microsoft.com/en-us/library/dd351192.aspx">Understanding Exchange 2010 Performance</a></p></li>
</ul>
<p>When migrating from an on-premises Exchange organization where there are multiple mailbox servers and multiple databases, we recommend that you create a migration user list that is evenly distributed across multiple mailbox servers and databases. Based on individual server performance, the list can be further fine-tuned to maximize throughput.</p>
<p>For example, if server A has 50 percent more resource availability than server B, it’s reasonable to have 50 percent more users from server A in the same migration batch. Similar practices can be applied to other source systems.</p>
<p>Perform migrations when servers have maximum resource availability, such as after hours or on weekends and holidays.</p></td>
</tr>
<tr class="even">
<td><p>Back-end tasks</p></td>
<td><p>Other back-end tasks that are running during migration time. Because it’s a best practice to perform migration after business hours, it’s common that migrations conflict with other maintenance tasks running on your on-premises servers, such as data backup.</p></td>
<td><p>Review other system tasks that might be running during migration. We recommend that you perform data migration when no other resource-intensive tasks are running.</p>
<p><strong>Note</strong>   For customers using on-premises Microsoft Exchange, the common back-end tasks are backup solutions and <a href="http://technet.microsoft.com/en-us/library/aa996226(exchg.65).aspx">Exchange store maintenance</a>.</p></td>
</tr>
</tbody>
</table>


## Factor 2: Migration server

Hybrid deployment migration is a cloud-initiated pull/push data migration, and an Exchange hybrid server acts as the migration server. This is often overlooked, and customers use a low-scale virtual machine to act as the hybrid server. This results in poor migration performance

**Best practice**

In addition to the applying the best practices previously described, we’ve tested the following best practices which resulted in improved migration performance in real customer migrations:

  - Use powerful server-class physical machines instead of virtual machines for the Exchange hybrid servers.

  - Use multiple hybrid servers that are behind the customer’s network load balancer.

For example, in real customer migrations, we have achieved consistent 30 GB/hour throughput by using the following configuration:

  - **Network **  500-MB outbound pipe to the Internet; internal network on 1 GB with a 10-GB fiber backbone.

  - **Hardware**   The specifications for the two client access/HUB (physical) servers are:
    
      - CPU: Intel® Xeon® CPU E5520 @ 2.27 GHz 2.26 GHz (two processors).
    
      - RAM: 24 GB.
    
      - Disks: Eight at 146 GB per disk. RAID 5 configuration = 960 GB total raw space.

  - **MRSProxy**   Configured with a concurrency of 100.

## Factor 3: Migration engine

Hybrid deployment migration uses native Office 365 tools. It’s subject to Office 365 migration service throttling.

**Exchange 2003 vs. later versions of Exchange**

There is a key difference for the end-user experience when the migration is from Exchange 2003. Unlike later versions of Exchange, Exchange 2003 end users cannot access their mailboxes when their data is being migrated. Therefore, Exchange 2003 customers are usually more concerned about when to schedule migrations and the time required to migrate, especially when migration performance is low because of large mailbox sizes or a slow network.

Exchange 2003 migration is also very sensitive to interruptions. For example, in a real customer migration, during the migration of a 10-GB mailbox, a service incident occurred when the migration of the mailbox was 50 percent complete. The Office 365 client access server, which was processing the data migration, had to be restarted to resolve the issue. In this case, the migration of that mailbox had to be restarted, which meant that the customer had to migrate all 10 GB of data again. The migration couldn’t resume from the point when it stopped. However, Exchange 2010, and later versions of Exchange, are able to resume migrations after interruptions.

**Best practice**

Some customers choose to do two-hop migrations for large and sensitive Exchange 2003 mailboxes:

  - **First hop**   Migrate mailboxes from Exchange 2003 to an Exchange 2010 or later server, which is usually the hybrid server. The first hop is an offline move, but it’s usually a very fast migration over a local network.

  - **Second hop**   Migrate mailboxes from Exchange 2010 or later to Office 365.

The second hop is an online move, which provides a better user experience and fault tolerance. This two-hop approach requires an Exchange license for the temporary on-premises user mailbox.

**Mailbox Replication Service Proxy (MRSProxy)**

MRS Proxy is the on-premises migration feature that works with the Mailbox Replication Service running on the Office 365 side. For more information, see [Understanding Move Requests](http://technet.microsoft.com/en-us/library/dd298174.aspx).

**Best practice**

It’s possible to configure the maximum number of MRSProxy connections for the on-premises Exchange hybrid server. Run the following Windows PowerShell command.

    Set-WebServicesVirtualDirectory -Identity "EWS (Default Web Site)" -MRSMaxConnections <number between 0 and unlimited; default is 100>


> [!NOTE]
> For most customer migrations, it’s unnecessary to change the default MRSMaxConnections value. If you need to protect the source server from being overwhelmed by the migration load, customers can reduce the number of connections. This setting is per MRSProxy server. If a customer has two MRSProxy servers, each set to 10 connections, they'll get 20 (2 x 10) as the total number of MRSProxy connections. For more information about configuring the MRSProxy service in your on-premises Exchange 2010 organization, see <A href="http://technet.microsoft.com/en-us/library/ee732395.aspx">Start the MRSProxy Service on a Remote Client Access Server</A>.



## Factor 4: Network

**Verification tests**

For customers running Exchange 2010 or later, testing the network performance for hybrid migrations can be done by performing multiple test mailbox migrations. Alternatively, you can migrate actual user mailboxes with the -SuspendWhenReadyToComplete option to get an indication of migration performance. When testing is complete, remove the move request to avoid affecting end users.

For more information about move requests, see [New-MoveRequest](https://technet.microsoft.com/en-us/library/dd351123\(v=exchg.150\)).

## Factor 5: Office 365 service

Office 365 resource health-based throttling affects migrations using the Office 365 hybrid deployment migrations. See the Office 365 resource health-based throttling section above for more details.

