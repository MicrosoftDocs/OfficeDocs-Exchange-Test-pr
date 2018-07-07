---
title: 'Server health and performance permissions: Exchange 2013 Help'
TOCTitle: Server health and performance permissions
ms:assetid: 00b23fd3-6679-4b06-a3d4-51df3112b9cd
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150479(v=EXCHG.150)
ms:contentKeyID: 47559932
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Server health and performance permissions

 

_**Applies to:** Exchange Online, Exchange Server 2013_


The permissions required to perform tasks to configure various components of Microsoft Exchange Server 2013 depend on the procedure being performed or the cmdlet you want to run. See each of the sections in this topic for more information about their respective features.

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1.  In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2.  Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3.  Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.
    

    > [!NOTE]
    > You must be assigned the Role Management management role to run the <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet. If you don't have permissions to run the <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.



If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).


> [!NOTE]
> Some features may require that you have local administrator permissions on the server you want to manage. To manage these features, you must be a member of the Local Administrators group on that server.



## Exchange workload management permissions

The following table lists the permissions required to perform tasks that manage the health and performance of your Exchange 2013 organization. For more information, see [Exchange workload management](exchange-workload-management-exchange-2013-help.md).

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
<td><p>User throttling</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange workload throttling</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p></td>
</tr>
</tbody>
</table>


## Exchange event log permissions

The following table lists the permissions required to perform tasks that manage Exchange event log settings.

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
<td><p>Exchange event log management</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
</tbody>
</table>

