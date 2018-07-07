---
title: 'Server health and performance: Exchange 2013 Help'
TOCTitle: Server health and performance
ms:assetid: 9d1fdec8-8273-4c71-88f1-b4edfd542c4f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150551(v=EXCHG.150)
ms:contentKeyID: 47560078
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Server health and performance

 

_**Applies to:** Exchange Server 2013_


Understanding server health and performance is critical to designing and maintaining a high-performance messaging infrastructure. Microsoft Exchange Server 2013 introduces improvements in server health and performance.

Looking for a list of all server health and performance topics? See Server health and performance documentation.

## Managed availability

Exchange 2013 introduces the concept of *managed availability*. Managed availability runs on every Exchange 2013 server. It’s made up of two processes, the Exchange Health Manager Service (MSExchangeHMHost.exe) and the Exchange Health Manager Worker process (MSExchangeHMWorker.exe), and the following asynchronous components:

  - **Probe engine**   The *probe engine* takes measurements on the server.

  - **Monitoring probe engine**   The *monitoring probe engine* stores the business logic about what constitutes a healthy state. It functions like a pattern recognition engine, looking for patterns and measurements that differ from a healthy state, and then evaluating whether a component or feature is unhealthy.

  - **Responder engine**   When the *responder engine* is alerted about an unhealthy component, its first action is to try to recover that component. Managed availability enables multi-stage recovery actions. The first attempt may be to restart the application pool, the second attempt may be to restart the corresponding service, and the third attempt may be to restart the server. And, the final attempt may be to put the server offline, so that it no longer accepts traffic. If all of these actions fail, an alert is sent to the help desk.

For more information about managed availability, see [Managed Availability](managed-availability-exchange-2013-help.md).

## Workload management

Exchange 2013 workload management includes the following components:

  - *User workload management* is the new name for the user throttling features of Exchange Server 2010. You can customize these setting based on the needs of your environment.

  - *System workload management* is new for Exchange 2013 and is used to automatically throttle specific Exchange workloads by monitoring the health of key server resources. These settings should be customized only under the direction of Microsoft Customer Service and Support.

For more information, see [Exchange workload management](exchange-workload-management-exchange-2013-help.md).

## Server health and performance documentation

The following table contains links to topics that will help you learn about and manage server health and performance in Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Topic</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="exchange-workload-management-exchange-2013-help.md">Exchange workload management</a></p></td>
<td><p>Learn about managing Exchange workloads by controlling how resources are consumed by individual users.</p></td>
</tr>
<tr class="even">
<td><p><a href="managed-availability-exchange-2013-help.md">Managed Availability</a></p></td>
<td><p>Learn about the built-in resource monitoring and recovery actions that are available in Exchange 2013.</p></td>
</tr>
</tbody>
</table>

