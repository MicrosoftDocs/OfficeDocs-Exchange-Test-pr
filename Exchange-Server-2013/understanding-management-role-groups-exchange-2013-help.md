---
title: 'Understanding management role groups: Exchange 2013 Help'
TOCTitle: Understanding management role groups
ms:assetid: 2a92e06c-523e-4fd4-a937-152562b7741d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd638105(v=EXCHG.150)
ms:contentKeyID: 49289206
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Understanding management role groups

 

_**Applies to:** Exchange Online, Exchange Server 2013_


A *management role group* is a universal security group (USG) used in the Role Based Access Control (RBAC) permissions model in Microsoft Exchange Server 2013. A management role group simplifies the assignment of management roles to a group of users. All members of a role group are assigned the same set of roles. Role groups are assigned administrator and specialist roles that define major administrative tasks in Exchange 2013 such as organization management, recipient management, and other tasks. Role groups enable you to more easily assign a broader set of permissions to a group of administrators or specialist users.


> [!NOTE]
> This topic focuses on advanced RBAC functionality. If you want to manage basic Exchange 2013 permissions, such as using the Exchange admin center (EAC) to add and remove members to and from role groups, create and modify role groups, or create and modify role assignment policies, see <A href="permissions-exchange-2013-help.md">Permissions</A>.



**Contents**

Role group layers

Role group management

Built-in role groups

Linked role groups

Role group delegation

Role group membership

Role group creation workflow


> [!NOTE]
> If you want to assign permissions to users to manage their own mailbox or distribution groups, see <A href="understanding-management-role-assignment-policies-exchange-2013-help.md">Understanding management role assignment policies</A>.



## Role group layers

The following are the layers that make up the role group model:

  - **Role group member**   A *role group member* is a mailbox, universal security group (USG), or other role group that can be added as a member of a role group. When a mailbox, USG, or another role group is added as a member of a role group, the assignments that have been made between management roles and a role group are applied to the new member. This grants the new member all of the permissions provided by the management roles.

  - **Management role group**   The *management role group* is a special USG that contains mailboxes, USGs, and other role groups that are members of the role group. This is where you add and remove members, and it's also what management roles are assigned to. The combination of all the roles on a role group defines everything that members added to a role group can manage in the Exchange organization.

  - **Management role assignment**   A *management role assignment* links a management role and a role group. Assigning a management role to a role group grants members of the role group the ability to use the cmdlets and parameters defined in the management role. Role assignments can use management scopes to control where the assignment can be used. For more information, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

  - **Management role scope**   A *management role scope* is the scope of influence or impact on a role assignment. When a role is assigned with a scope to a role group, the management scope targets specifically what objects that assignment is allowed to manage. The assignment, and its scope, are then given to the members of the role group, which restricts what those members can manage. A scope can be made up of lists of servers or databases, organizational units, or filters on server, database or recipient objects. For more information, see [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md).

  - **Management role**   A *management role* is a container for a grouping of management role entries. Roles are used to define the specific tasks that can be performed by the members of a role group assigned the role. For more information, see [Understanding management roles](understanding-management-roles-exchange-2013-help.md).

  - **Management role entries**   *Management role entries* are the individual entries on a management role that provide access to cmdlets, scripts, and other special permissions that enable access to perform a specific task. Most often, role entries consist of a single cmdlet or script and the parameters that can be accessed by the management role, and therefore the role group to which the role is assigned.

The following figure shows each of the role group layers in the preceding list and how each of the layers relates to the other.

**Management role group layers**

![Management role group layers](images/Dd638105.a98c237c-7bdb-434b-8c98-22509e46cccf(EXCHG.150).gif "Management role group layers")

For more information about RBAC, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

Return to top

## Role group management

When you create a role group, you create the USG that holds the members of the role group, and you create the assignments between the role group and the management roles you specify. Optionally, you can also specify a management scope to apply to the role assignments, and you can add any mailboxes that you want to be members of the new role group.

After you create a role group, each layer becomes an independent object. The role group continues to be the central point at which all of the layers are joined together, however, each layer is managed individually. For example, to modify the management scope that you applied to the role group when it was created, you need to change the scope on each individual role assignment after the role group is created. The management of the role group model is performed using the cmdlets that manage the individual layers of the role group model.

The following table lists the role group layer and the procedural topics that you can use to manage each layer.

### Role group management topics

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role group model layer</th>
<th>Management topic</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Role group member</p></td>
<td><p><a href="manage-role-group-members-exchange-2013-help.md">Manage role group members</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Role group</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">Manage role groups</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Management roles and assignments</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">Manage role groups</a></p></td>
</tr>
<tr class="even">
<td><p>Management role entries</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">Add a role entry to a role</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">Change a role entry</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">Remove a role entry from a role</a></p>

> [!NOTE]
> Changing the management role entries in management roles in a role group is an advanced task and is generally not required in most cases. Instead, you may be able to use a pre-existing management role that suits your requirements. For more information, see <A href="built-in-role-groups-exchange-2013-help.md">Built-in role groups</A>.


</td>
</tr>
</tbody>
</table>


Return to top

## Built-in role groups

Built-in roles groups are roles shipped with Exchange 2013. They provide you with a set of role groups that you can use to provide varying levels of administrative permissions to groups of users. You can add or remove users to or from any built-in role group. You can also add or remove role assignments to or from most role groups. The only exceptions are the following:

  - You can't remove any delegating role assignments from the Organization Management role group.

  - You can't remove the Role Management role from the Organization Management role group.

The following table lists all the built-in role groups included with Exchange 2013. For more information about built-in role groups, see [Built-in role groups](built-in-role-groups-exchange-2013-help.md).

### Built-in role groups

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role group</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
<td><p>Administrators who are members of the Organization Management role group have administrative access to the entire Exchange 2013 organization and can perform almost any task against any Exchange 2013 object, with some exceptions. By default, members of this role group can't perform mailbox searches and management of unscoped top-level management roles.</p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p></td>
<td><p>Administrators who are members of the View Only Organization Management role group can view the properties of any object in the Exchange organization.</p></td>
</tr>
<tr class="odd">
<td><p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
<td><p>Administrators who are members of the Recipient Management role group have administrative access to create or modify Exchange 2013 recipients within the Exchange 2013 organization.</p></td>
</tr>
<tr class="even">
<td><p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
<td><p>Administrators who are members of the UM Management role group can manage features in the Exchange organization such as Unified Messaging (UM) service configuration, UM properties on mailboxes, UM prompts, and UM auto attendant configuration.</p></td>
</tr>
<tr class="odd">
<td><p><a href="discovery-management-exchange-2013-help.md">Discovery Management</a></p></td>
<td><p>Administrators or users who are members of the Discovery Management role group can perform searches of mailboxes in the Exchange organization for data that meets specific criteria and can also configure litigation holds on mailboxes.</p></td>
</tr>
<tr class="even">
<td><p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
<td><p>Users who are members of the Records Management role group can configure compliance features, such as retention policy tags, message classifications, transport rules, and more.</p></td>
</tr>
<tr class="odd">
<td><p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
<td><p>Administrators who are members of this role group can configure server-specific configuration of transport , client access, and mailbox features such as database copies, certificates, transport queues and Send connectors, virtual directories, and client access protocols.</p></td>
</tr>
<tr class="even">
<td><p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
<td><p>Users who are members of the Help Desk role group can perform limited recipient management of Exchange 2013 recipients.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
<td><p>Users who are members of the Hygiene Management role group can configure the anti-spam and anti-malware features of Exchange 2013. Third-party programs that integrate with Exchange 2013 can add service accounts to this role group to grant those programs access to the cmdlets required to retrieve and configure the Exchange configuration.</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">Compliance Management</a></p></td>
<td><p>Users who are members of the Compliance Management role group can configure and manage Exchange compliance configuration in accordance with their policies.</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">Public Folder Management</a></p></td>
<td><p>Administrators who are members of the Public Folder Management role group can manage public folders on servers running Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="delegated-setup-exchange-2013-help.md">Delegated Setup</a></p></td>
<td><p>Administrators who are members of the Delegated Setup role group can deploy servers running Exchange 2013 that have been previously provisioned by a member of the Organization Management role group.</p></td>
</tr>
</tbody>
</table>


Return to top

## Linked role groups

Linked role groups are used in organizations that install Exchange 2013 in a dedicated resource forest and place users in other, trusted foreign forests. Linked role groups, as the name implies, create a link between a role group in the Exchange forest and a USG in a foreign forest. This is useful when the Active Directory Domain Services (AD DS) user accounts of the administrators you want to administer Exchange don't reside in the same resource forest as Exchange. Linked role groups can only be associated with one foreign USG. Additionally, you don't need to create a two-way trust between the Exchange forest and the foreign forest. The Exchange forest needs to trust the foreign forest but the foreign forest doesn't need to trust the Exchange forest.

For more information about permissions in multiple-forest topologies, see [Understanding multiple-forest permissions](understanding-multiple-forest-permissions-exchange-2013-help.md).

A linked role group consists of two parts:

  - **Linked role group**   The linked role group is a container object that associates the foreign USG with the management role assignments assigned to the role group.

  - **Foreign USG**   The foreign USG contains the members that should be granted the permissions provided by the linked role group.

When you create a linked role group, you provide a domain controller in the foreign forest that contains the users you want to manage the Exchange forest and the USG that contains those users as members, the foreign USG name, and the credentials required to access the foreign forest. Exchange adds the security identifier (SID) of the foreign USG to the linked role group. Because the USG SID is the only identification of the foreign USG, we strongly recommend that you specify the foreign forest in the name of the role group if you have multiple foreign forests.

A linked role group doesn't contain any members. All of the members of that role group are managed using the foreign USG. This means you can't use the **Update-RoleGroupMember**, **Add-RoleGroupMember**, or **Remove-RoleGroupMember** cmdlets to add or remove role group members. When you add members to the foreign USG, they are given the permissions provided by the linked role group.

You can't change a standard role group, which contains its own members, to a linked role group and vice versa. If you want to change a role group from a standard role group to a linked role group, you must create a new linked role group and replicate the management role assignments that are present on the standard role group on the linked role group. This is also the case for built-in role groups because they're standard role groups. If you want to perform all of the management of your Exchange forest from a foreign forest, you need to create new linked role groups and add the management roles that exist on the built-in role groups to the new linked role groups. For more information about how to accomplish this, see [Create linked role groups that mirror built-in role groups](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md).

Return to top

## Role group delegation

By default, members of the Organization Management role group can add and remove members to and from role groups. However, you might want to enable users who aren't members of the Organization Management role group to add and remove role group members. If so, you can use role group delegation.

Role group delegation is controlled by the **ManagedBy** property on each role group. The **ManagedBy** property contains a list of users who can add and remove members to and from that role group or change the configuration of a role group. The users aren't assigned any permissions given by the role group unless they're also members of the role group.

If the **ManagedBy** property is set on a role group, only those users who are listed as role group managers on that property can modify a role group or the membership of a role group by default. However, an optional parameter on cmdlets that modify role groups or role group membership can override that restriction. The *BypassSecurityGroupManagerCheck* switch can be used by users who are members of the Organization Management role or are assigned, either directly or indirectly, the Role Management management role. When this switch is used, the **ManagedBy** property is ignored and the user can modify the role group or role group membership.

If the **ManagedBy** property isn't set on a role group, only users who are members of the Organization Management role or are assigned, either directly or indirectly, the Role Management management role can modify a role group or role group membership.


> [!NOTE]
> Roles assigned to a role group may be assigned using delegating role assignments. With delegating role assignments, members of a role group that's assigned a delegated role can assign that role to another role group, assignment policy, user, or USG. Members of the role group can assign only that role and can't delegate the role group, unless they're also added to the <STRONG>ManagedBy</STRONG> property. For more information about delegated role assignments, see <A href="understanding-management-role-assignments-exchange-2013-help.md">Understanding management role assignments</A>.



For more information about how to manage role group delegation, see [Manage role groups](manage-role-groups-exchange-2013-help.md).

Return to top

## Role group membership

When a user is made a member of a role group, the management roles assigned to the role group are assigned to the user. If a user is a member of multiple role groups, the management roles from each role group are aggregated and assigned to the user. Users, USGs, and other role groups can be members of role groups.

Only users who are members of the Organization Management or Role Management role groups and users who have been delegated the ability to add and remove users to or from role groups can manage role group membership.

For more information about how to manage role group membership, see [Manage role group members](manage-role-group-members-exchange-2013-help.md).

## Role group creation workflow

As mentioned previously, a role group is made up of several layers. To help you understand what happens when a role group is created, consider the following example, which creates a new role group.

    New-RoleGroup -Name "Seattle Recipient Management" -Roles "Mail Recipients", "Distribution Groups", "Move Mailboxes", "UM Mailboxes" -CustomRecipientWriteScope "Seattle Users", -ManagedBy "Brian", "David", "Katie" -Members "Ray", "Jenn", "Maria", "Chris", "Maija", "Carter", "Jenny", "Sam", "Lukas", "Isabel", "Katie"

When the preceding command is run, the following happens:

1.  A new role group object, which is a special USG, called Seattle Recipient Management is created.

2.  The mailboxes for Ray, Jenn, Maria, Chris, Maija, Carter, Jenny, Sam, Lukas, Isabel, and Katie are added as members of the role group. These users receive the permissions provided by this role group.

3.  The users Brian and David are added to the **ManagedBy** property of the role group. These users can add and remove members to and from the role group but won't be given any permissions provided by the role group because they're not members. Katie is also added to the **ManagedBy** property of the role group. Because she's added to the **ManagedBy** property, and she's a member of the role group, she can add or remove members to and from the role group, and she also receives the permissions provided by the role group.

4.  The following management role assignments are created. The role assignments assign each management role specified in the command to the role group. The management scope Seattle Users is added to each role assignment. The name of each role assignment is a combination of the management role being assigned and the role group name.
    
      - `Mail Recipients_Seattle Recipient Management`
    
      - `Distribution Groups_Seattle Recipient Management`
    
      - `Move Mailboxes_Seattle Recipient Management`
    
      - `UM Mailboxes_Seattle Recipient Management`

If you compare the results of this command to the Management role group layers figure earlier in this topic, you can see where each step correlates to the role group layers. You can then refer to the Management role group management topics shown in "Role group management" earlier in this topic to manage each role group layer.

Return to top

