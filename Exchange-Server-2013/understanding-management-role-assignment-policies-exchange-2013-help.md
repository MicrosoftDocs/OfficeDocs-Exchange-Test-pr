---
title: 'Understanding management role assignment policies: Exchange 2013 Help'
TOCTitle: Understanding management role assignment policies
ms:assetid: 25913e43-326a-4371-90b5-021a35f100fe
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd638100(v=EXCHG.150)
ms:contentKeyID: 49289200
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Understanding management role assignment policies

 

_**Applies to:** Exchange Online, Exchange Server 2013_


A *management role assignment policy* is a collection of one or more end-user management roles that enables end users to manage their own Microsoft Exchange Server 2013 mailbox and distribution group configuration. Role assignment policies, which are part of the Role Based Access Control (RBAC) permissions model in Exchange 2013, enable you to control what specific mailbox and distribution group configuration settings your end users can modify. Different groups of users can have role assignment policies specialized to them.


> [!NOTE]
> This topic focuses on advanced RBAC functionality. If you want to manage basic Exchange 2013 permissions, such as using the Exchange admin center (EAC) to add and remove members to and from role groups, create and modify role groups, or create and modify role assignment policies, see <A href="permissions-exchange-2013-help.md">Permissions</A>.



For more information about RBAC, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

**Contents**

Role assignment policy layers

Default and explicit role assignment policies

Using role assignment policies

Role assignment policy management

## Role assignment policy layers

The following list describes the layers that make up the role assignment policy model:

  - **Mailbox**   Mailboxes are assigned a single role assignment policy. When a mailbox is assigned a role assignment policy, the assignments between management roles and a role assignment policy are applied to the mailbox. This grants the mailbox all of the permissions provided by the management roles.

  - **Management role assignment policy**   The *management role assignment policy* is a special object in Exchange 2013. Users are associated with a role assignment policy when their mailboxes are created, or if you change the role assignment policy on a mailbox. This is also what you assign end-user management roles to. The combination of all the roles on a role assignment policy defines everything that the user can manage on his or her mailbox or distribution groups.

  - **Management role assignment**   A *management role assignment* is the link between a management role and a role assignment policy. Assigning a management role to a role assignment policy grants the ability to use the cmdlets and parameters defined in the management role. When you create a role assignment between a role assignment policy and a management role, you can't specify any scope. The scope applied by the assignment is based on the management role and is either `Self` or `MyGAL`. For more information, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

  - **Management role**   A *management role* is a container for a grouping of management role entries. Roles are used to define the specific tasks that a user can do with his or her mailbox or distribution groups. A *management role entry* is a cmdlet, script, or special permission that enables each specific task in a management role to be performed. You can only use end-user management roles with role assignment policies. For more information, see [Understanding management roles](understanding-management-roles-exchange-2013-help.md).

  - **Management role entry**   Management role entries are the individual entries on a management role that determine what cmdlets and parameters are available to the management role and the role group. Each role entry consists of a single cmdlet and the parameters that can be accessed by the management role.

The following figure shows each of the role assignment policy layers in the preceding list and how each of the layers relates to the other.

**Management role assignment policy model**

![Role Assignment Model Relationships](images/Dd638100.7f7c11ca-0d61-464d-98a3-a9991ec811b5(EXCHG.150).jpg "Role Assignment Model Relationships")

For more information about management roles, role assignments, and scopes, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

## Default and explicit role assignment policies

The following sections describe the two types of role assignment policies in Exchange 2013.

## Default role assignment policy

A default role assignment policy is one assigned to a mailbox when the mailbox is created or moved to a server running Exchange 2013, and a role assignment policy wasn't provided using the *RoleAssignmentPolicy* parameter on the **New-Mailbox** or **Enable-Mailbox** cmdlets.

Exchange 2013 includes a default role assignment policy that provides end users with the permissions most commonly used. You can change the default permissions on the default role assignment policy by adding or removing management roles to or from it.

If you want to replace the built-in default role assignment policy with your own default role assignment policy, you can use the **Set-RoleAssignmentPolicy** cmdlet to select a new default. When you do this, any new mailboxes are assigned the role assignment policy you specified by default if you don't explicitly specify a role assignment policy.

When you change the default role assignment policy, mailboxes assigned the default role assignment policy aren't automatically assigned the new default role assignment policy. If you want to update previously created mailboxes to use the role assignment policy you've set as default, you must use the **Set-Mailbox** cmdlet to do so.

## Explicit Role Assignment Policy

An explicit role assignment policy is a policy that you assign to a mailbox manually using the *RoleAssignmentPolicy* parameter on the **New-Mailbox**, **Set-Mailbox**, or **Enable-Mailbox** cmdlets. When you assign an explicit role assignment policy, the new policy takes effect immediately and replaces the previously assigned explicit role assignment policy.

## Using role assignment policies

Role assignment policies enable you to tailor permissions based on what business needs your users need to be able to configure. If the default role assignment policy meets your needs, you don't need to do any customization. However, if you have many different user groups with specialized needs, you can create role assignment policies for each of them.

The default role assignment policy you use should contain the permissions that apply to your broadest set of users. Then, create role assignment policies for each of your specialized user groups and tailor those role assignment policies to grant more or less restrictive permissions to them. When you organize your role assignment policies this way, you reduce complexity by only explicitly assigning role assignment policies to your specialized users while the majority of your users receive the more common permissions provided by the default role assignment policy.

A mailbox can have only one role assignment policy. All users, including administrators and specialist users, are assigned one role assignment policy. If you want a user to have a different set of permissions, you must assign that user's mailbox another role assignment policy with the required permissions.

## Role assignment policy management

To add a new role assignment policy, you first create one and decide whether it should be the default role assignment policy. After you create a role assignment policy, you assign management roles to the role assignment policy, and then assign the role assignment policy to mailboxes. You can later choose to add or remove management roles or choose a different role assignment policy to be the default.

The following table lists the role assignment policy layer and the procedural topics that you can use to manage each layer.

### Role assignment policy management topics

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role assignment policy model layer</th>
<th>Management topics</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mailbox</p></td>
<td><p><a href="manage-user-mailboxes-exchange-2013-help.md">Manage user mailboxes</a></p>
<p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Change the assignment policy on a mailbox</a></p></td>
</tr>
<tr class="even">
<td><p>Role assignment policy</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Manage role assignment policies</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Management roles and assignments</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Manage role assignment policies</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Management role entries</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">Add a role entry to a role</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">Change a role entry</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">Remove a role entry from a role</a></p>

> [!NOTE]
> Changing the management role entries in management roles in a role assignment policy is an advanced task and is generally not required in most cases. You may, instead, be able to use a preexisting management role that suits your requirements. For more information, see <A href="built-in-role-groups-exchange-2013-help.md">Built-in role groups</A>.


</td>
</tr>
</tbody>
</table>

