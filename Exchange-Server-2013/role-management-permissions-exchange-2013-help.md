---
title: 'Role management permissions: Exchange 2013 Help'
TOCTitle: Role management permissions
ms:assetid: cb9591c4-fbb3-4199-8007-6bbfdfd5a2e9
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd638186(v=EXCHG.150)
ms:contentKeyID: 48385542
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Role management permissions

 

_**Applies to:** Exchange Online, Exchange Server 2013_


The permissions required to perform tasks to configure management roles vary depending on the procedure being performed or the cmdlet you want to run. For more information about management roles, see [Understanding management roles](understanding-management-roles-exchange-2013-help.md).

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1.  In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2.  Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3.  Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.
    

    > [!NOTE]
    > You must be assigned the Role Management management role to run the <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet. If you don't have permissions to run the <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.



If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).

## Role management permissions

You can use the features in the following table to manage the management role groups, roles, assignment policies, assignments, scopes that define the permissions you can apply to administrators, and end users. Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).


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
<td><p>Management roles</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Unscoped management roles</p></td>
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">Unscoped Role Management role</a> management role</p></td>
</tr>
<tr class="odd">
<td><p>Role groups</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Assignment policies</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Role assignments</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Management scopes</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Management role entries</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Legacy permissions</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Active Directory split permissions</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>

> [!IMPORTANT]
> To run the <CODE>setup.exe</CODE> command with the <EM>PrepareAD</EM> and <EM>ActiveDirectorySplitPermissions</EM> parameters, the account you use must be a member of the Schema Admins and Enterprise Administrators groups.


</td>
</tr>
</tbody>
</table>

