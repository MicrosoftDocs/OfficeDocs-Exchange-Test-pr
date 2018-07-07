---
title: 'Exchange and Shell infrastructure permissions: Exchange 2013 Help'
TOCTitle: Exchange and Shell infrastructure permissions
ms:assetid: 3646a4e8-36b2-41fb-89a4-79b0963fcb11
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd638114(v=EXCHG.150)
ms:contentKeyID: 48384969
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Exchange and Shell infrastructure permissions

 

_**Applies to:** Exchange Server 2013_


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



## Exchange infrastructure permissions

The following table lists the permissions required to perform tasks that configure general Exchange 2013 settings.

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
<td><p>Administrator audit logging</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange Administration Center configuration settings</p></td>
<td><p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Administration Center connectivity</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange server configuration settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Help settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Message categories</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
</tr>
<tr class="odd">
<td><p>Product key</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Test system health</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>View-only administrator audit logging</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p>

> [!NOTE]
> You can also manually assign the View-Only Audit Logs management role to a management role group. For more information, see <A href="view-only-audit-logs-role-exchange-2013-help.md">View-Only Audit Logs role</A>.


</td>
</tr>
<tr class="even">
<td><p>Write to audit log</p></td>
<td><p>Users that are members of any role group or assigned any management role can write to the administrator audit log.</p></td>
</tr>
</tbody>
</table>


## Shell infrastructure permissions

The following table lists the permissions required to perform tasks that configure features that control how the Exchange Management Shell runs.

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
<td><p>Active Directory Domain Services server settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="even">
<td><p>Cmdlet extension agents</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="odd">
<td><p>PowerShell virtual directories</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>PowerShell and WinRM installation</p></td>
<td><p>Local Server Administrator</p></td>
</tr>
<tr class="odd">
<td><p>Remote Shell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
</tbody>
</table>


## Federation and certificates permissions

The following table lists permissions required for performing tasks related to federation trusts, OAuth configuration, certificate management, and hybrid deployment configuration.

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
<td><p>Certificate management</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Federation trusts, OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Test federation trusts, OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Hybrid deployment configuration</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Intra-Organization connectors</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
</tbody>
</table>

