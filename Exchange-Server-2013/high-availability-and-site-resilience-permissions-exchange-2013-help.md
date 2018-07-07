---
title: 'High availability and site resilience permissions: Exchange 2013 Help'
TOCTitle: High availability and site resilience permissions
ms:assetid: 66085107-4d4d-41c3-a425-82314acd9eee
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd638136(v=EXCHG.150)
ms:contentKeyID: 48385175
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# High availability and site resilience permissions

 

_**Applies to:** Exchange Server 2013_


The permissions required to configure high availability vary depending on the procedure being performed or the cmdlet you want to run. For more information about high availability, see [High availability and site resilience](high-availability-and-site-resilience-exchange-2013-help.md).

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1.  In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2.  Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3.  Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.
    

    > [!NOTE]
    > You must be assigned the Role Management management role to run the <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet. If you don't have permissions to run the <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.



If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).

## Database availability group permissions

You can use the features in the following table to add, remove, and configure settings for database availability groups (DAGs).

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissions required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Database availability group membership</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Database Availability Groups role</a></p></td>
</tr>
<tr class="even">
<td><p>Database availability group properties</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Database Availability Groups role</a></p></td>
</tr>
<tr class="odd">
<td><p>Database availability groups</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Database Availability Groups role</a></p></td>
</tr>
<tr class="even">
<td><p>Database availability networks</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Database Availability Groups role</a></p></td>
</tr>
</tbody>
</table>


## Mailbox database copy permissions

You can use the features in the following table to add, remove, update, and activate mailbox database copies.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissions required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Database switchover</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="databases-role-exchange-2013-help.md">Databases role</a></p></td>
</tr>
<tr class="even">
<td><p>Mailbox database copies</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">Database Copies role</a></p></td>
</tr>
<tr class="odd">
<td><p>Server switchover</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="databases-role-exchange-2013-help.md">Databases role</a></p></td>
</tr>
<tr class="even">
<td><p>Update a mailbox database copy</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">Database Copies role</a></p></td>
</tr>
</tbody>
</table>

