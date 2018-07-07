---
title: 'Recipient Management: Exchange 2013 Help'
TOCTitle: Recipient Management
ms:assetid: 669d602e-68e3-41f9-a455-b942d212d130
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd298028(v=EXCHG.150)
ms:contentKeyID: 49289275
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Recipient Management

 

_**Applies to:** Exchange Server 2013_


The Recipient Management management role group is one of several built-in role groups that make up the Role Based Access Control (RBAC) permissions model in Microsoft Exchange Server 2013. Role groups are assigned one or more management roles that contain the permissions required to perform a given set of tasks. The members of a role group are granted access to the management roles assigned to the role group. For more information about role groups, see [Understanding management role groups](understanding-management-role-groups-exchange-2013-help.md).

Administrators who are members of the Recipient Management role group have administrative access to create or modify Exchange 2013 recipients within the Exchange 2013 organization.

This role group is equivalent to the Exchange Recipient Administrators role in Exchange Server 2007.

For more information about RBAC, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

## Role group membership

If you want to add or remove members to or from this role group, see [Manage role group members](manage-role-group-members-exchange-2013-help.md).

By default, only members of the Organization Management role group can add or remove members from this role group. For more information about how to add additional role group delegates, see the "Add or remove a role group delegate" section in [Manage role groups](manage-role-groups-exchange-2013-help.md).

You can use the following command to view a list of users or universal security groups (USGs) that are members of this role group.

    Get-RoleGroupMember "Recipient Management"

For more information about the members of a role group, see [View the members of a role group](manage-role-group-members-exchange-2013-help.md) in [Manage role group members](manage-role-group-members-exchange-2013-help.md).

## Role group customization

This role group is assigned management roles by default. The roles that are included are listed in the "Management Roles Assigned to this Role Group" section. You can add or remove role assignments to or from this role group to match the needs of your organization.

The role groups provided with Exchange 2013 are designed to match more granular tasks. By assigning roles to a role group, you enable the members of that role group to perform the tasks associated with the role. For example, the Journaling role enables the management of the Journaling agent and journaling rules. For more information about how roles are assigned to role groups, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

The roles assigned to this role group are given default management scopes. Management scopes determine what Exchange objects can be viewed or modified by the members of a role group. You can change the scopes associated with assignments between roles and role groups. For example, you might want to do this if you only want members of a role group to be able to change recipients that are under a specific organizational unit or in a specific location. For more information about management scopes, see [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md).

For more information about how to customize this role group, see the following topics:

  - [Manage role groups](manage-role-groups-exchange-2013-help.md)

  - [Manage role group members](manage-role-group-members-exchange-2013-help.md)

If you want to create a role group and assign some of the roles that are assigned to this role group to the new role group, see the “Create a role group” section in [Manage role groups](manage-role-groups-exchange-2013-help.md).

If the creation of security principals in your organization, such as user accounts, is controlled by a specific group other than the Exchange administrators, you can create a role group and move the Mail Recipient Creation role and the Security Group Creation and Membership role to the new role group. Doing so prevents members of the Recipient Management role group from creating Active Directory objects. They can, however, continue to mail-enable the new Active Directory objects. For more information about split permissions, see [Understanding split permissions](understanding-split-permissions-exchange-2013-help.md).

## Management roles assigned to this role group

The following table lists all the management roles that are assigned to this role group and the following attributes of each role assignment:

  - **Regular assignment**   Enables members of the role group to access the management role entries made available by the associated management role.

  - **Delegating assignment**   Gives members of the role group the ability to assign the specified role to other role groups, role assignment policies, users, or USGs.

  - **Recipient read scope**   Determines what recipient objects members of the role group are allowed to read from Active Directory.

  - **Recipient write scope**   Determines what recipient objects members of the role group are allowed to modify in Active Directory.

  - **Configuration read scope**   Determines what configuration and server objects members of the role group are allowed to read from Active Directory.

  - **Configuration write scope**   Determines what organizational and server objects members of the role group are allowed to modify in Active Directory.

For more information about role assignments and management scopes, see the following topics:

  - [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md)

  - [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md)

### Management roles assigned to this role group

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Management role</th>
<th>Regular assignment</th>
<th>Delegating assignment</th>
<th>Recipient read scope</th>
<th>Recipient write scope</th>
<th>Configuration read scope</th>
<th>Configuration write scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="distribution-groups-role-exchange-2013-help.md">Distribution Groups role</a></p></td>
<td><p>X</p></td>
<td><p> </p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Mail Recipient Creation role</a></p></td>
<td><p>X</p></td>
<td><p> </p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mail-recipients-role-exchange-2013-help.md">Mail Recipients role</a></p></td>
<td><p>X</p></td>
<td><p> </p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="message-tracking-role-exchange-2013-help.md">Message Tracking role</a></p></td>
<td><p>X</p></td>
<td><p> </p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="migration-role-exchange-2013-help.md">Migration role</a></p></td>
<td><p>X</p></td>
<td><p> </p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">Move Mailboxes role</a></p></td>
<td><p>X</p></td>
<td><p> </p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="recipient-policies-role-exchange-2013-help.md">Recipient Policies role</a></p></td>
<td><p>X</p></td>
<td><p> </p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="team-mailboxes-role-exchange-2013-help.md">Team Mailboxes role</a></p></td>
<td><p>X</p></td>
<td><p> </p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>

