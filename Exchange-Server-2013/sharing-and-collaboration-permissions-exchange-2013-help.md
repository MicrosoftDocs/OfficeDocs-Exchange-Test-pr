---
title: 'Sharing and collaboration permissions: Exchange 2013 Help'
TOCTitle: Sharing and collaboration permissions
ms:assetid: b7fa4b7c-1266-45bd-a14b-f66be0459cc5
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150556(v=EXCHG.150)
ms:contentKeyID: 47560082
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Sharing and collaboration permissions

 

_**Applies to:** Exchange Server 2013_


The permissions required to configure sharing and collaboration features vary depending on the procedure being performed or the cmdlet you want to run. For more information about sharing and collaboration, see [Collaboration](collaboration-exchange-2013-help.md) and [Sharing](sharing-exchange-2013-help.md).

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1.  In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2.  Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3.  Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.
    

    > [!NOTE]
    > You must be assigned the Role Management management role to run the <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet. If you don't have permissions to run the <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.



If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).

## Sharing and collaboration feature permissions

You can use the features in the following table to configure sharing and collaboration features. The role groups that are required to configure each feature are listed.

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
<td><p>Partner applications - configure</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Public folders, mail-enabled</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Public folders</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="public-folder-management-exchange-2013-help.md">Public Folder Management</a></p></td>
</tr>
<tr class="even">
<td><p>Site mailboxes</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Site mailbox provisioning policy</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
</tbody>
</table>

