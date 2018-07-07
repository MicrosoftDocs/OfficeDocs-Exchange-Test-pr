---
title: 'Permissions: Exchange 2013 Help'
TOCTitle: Permissions
ms:assetid: d8dd605e-0af1-4e18-9ce6-e51d04e161ba
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd351175(v=EXCHG.150)
ms:contentKeyID: 48385617
ms.date: 07/14/2016
mtps_version: v=EXCHG.150
---

# Permissions

 

_**Applies to:** Exchange Server, Exchange Server 2013_


Microsoft Exchange Server 2013 includes a large set of predefined permissions, based on the Role Based Access Control (RBAC) permissions model, which you can use right away to easily grant permissions to your administrators and users. You can use the permissions features in Exchange 2013 so that you can get your new organization up and running quickly.


> [!NOTE]
> Several RBAC features and concepts aren't discussed in this topic because they're advanced features. If the functionality discussed in this topic doesn't meet your needs, and you want to further customize your permissions model, see <A href="understanding-role-based-access-control-exchange-2013-help.md">Understanding Role Based Access Control</A>.



Looking for a list of all permissions topics? See Permissions documentation.

**Contents**

Role-based permissions

Role groups and role assignment policies

Work with role groups

Work with role assignment policies

## Role-based permissions

In Exchange 2013, the permissions that you grant to administrators and users are based on management roles. A role defines the set of tasks that an administrator or user can perform. For example, a management role called `Mail Recipients` defines the tasks that someone can perform on a set of mailboxes, contacts, and distribution groups. When a role is assigned to an administrator or user, that person is granted the permissions provided by the role.

There are two types of roles, administrative roles and end-user roles:

  - **Administrative roles**   These roles contain permissions that can be assigned to administrators or specialist users using role groups that manage a part of the Exchange organization, such as recipients, servers, or databases.

  - **End-user roles**   These roles, assigned using role assignment policies, enable users to manage aspects of their own mailbox and distribution groups that they own. End-user roles begin with the prefix `My`.

Roles give permissions to perform tasks to administrators and users by making cmdlets available to those who are assigned the roles. Because the Exchange Administration Center (EAC) and Exchange Management Shell use cmdlets to manage Exchange, granting access to a cmdlet gives the administrator or user permission to perform the task in each of the Exchange management interfaces.

Exchange 2013 includes approximately 86 roles that you can use to grant permissions. For a list of roles included with Exchange 2013, see [Built-in management roles](built-in-management-roles-exchange-2013-help.md).

Return to top

## Role groups and role assignment policies

Roles grant permissions to perform tasks in Exchange 2013, but you need an easy way to assign them to administrators and users. Exchange 2013 provides you with the following to help you do that:

  - **Role groups**   Role groups enable you to grant permissions to administrators and specialist users.

  - **Role assignment policies**   Role assignment policies enable you to grant permissions to end users to change settings on their own mailbox or distribution groups that they own.

For more information about role groups and role assignment policies, see the following sections.

## Role groups

Every administrator that manages Exchange 2013 must be assigned at least one or more roles. Administrators might have more than one role because they may perform job functions that span multiple areas in Exchange. For example, one administrator might manage both recipients and Exchange servers. In this case, that administrator might be assigned both the `Mail Recipients` and `Exchange Servers` roles.

To make it easier to assign multiple roles to an administrator, Exchange 2013 includes role groups. Role groups are special universal security groups (USGs) used by Exchange 2013 that can contain Active Directory users, USGs, and other role groups. When a role is assigned to a role group, the permissions granted by the role are granted to all the members of the role group. This enables you to assign many roles to many role group members at once. Role groups typically encompass broader management areas, such as recipient management. They're used only with administrative roles, and not end-user roles.


> [!NOTE]
> It's possible to assign a role directly to a user or USG without using a role group. However, that method of role assignment is an advanced procedure and isn't covered in this topic. We recommend that you use role groups to manage permissions.



The following figure shows the relationship between users, role groups, and roles.

**Roles, role groups, and role group members**

![Role, role group and member relationship](images/Dd351175.3fb0b47d-333a-4953-ae38-d710d327bde0(EXCHG.150).gif "Role, role group and member relationship")

Exchange 2013 includes several built-in role groups, each one providing permissions to manage specific areas in Exchange 2013. Some role groups may overlap with others. The following table lists each role group with a description of its use. If you want to see the roles assigned to each role group, click the name of the role group in the "Role group" column, and then open the "Management Roles Assigned to This Role Group" section.

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
<td><p>Administrators who are members of the Organization Management role group have administrative access to the entire Exchange 2013 organization and can perform almost any task against any Exchange 2013 object, with some exceptions, such as the <code>Discovery Management</code> role.</p>

> [!IMPORTANT]
> Because the Organization Management role group is a powerful role, only users or USGs that perform organizational-level administrative tasks that can potentially impact the entire Exchange organization should be members of this role group.


</td>
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
<td><p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
<td><p>The Help Desk role group, by default, enables members to view and modify the Microsoft Office Outlook Web App options of any user in the organization. These options might include modifying the user's display name, address, and phone number. They don't include options that aren't available in Outlook Web App options, such as modifying the size of a mailbox or configuring the mailbox database on which a mailbox is located.</p></td>
</tr>
<tr class="even">
<td><p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
<td><p>Administrators who are members of the Hygiene Management role group can configure the antivirus and anti-spam features of Exchange 2013. Third-party programs that integrate with Exchange 2013 can add service accounts to this role group to grant those programs access to the cmdlets required to retrieve and configure the Exchange configuration.</p></td>
</tr>
<tr class="odd">
<td><p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
<td><p>Users who are members of the Records Management role group can configure compliance features, such as retention policy tags, message classifications, and transport rules.</p></td>
</tr>
<tr class="even">
<td><p><a href="discovery-management-exchange-2013-help.md">Discovery Management</a></p></td>
<td><p>Administrators or users who are members of the Discovery Management role group can perform searches of mailboxes in the Exchange organization for data that meets specific criteria and can also configure legal holds on mailboxes.</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">Public Folder Management</a></p></td>
<td><p>Administrators who are members of the Public Folder Management role group can manage public folders on servers running Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
<td><p>Administrators who are members of the Server Management role group can configure server-specific configuration of transport, Unified Messaging, client access, and mailbox features such as database copies, certificates, transport queues and Send connectors, virtual directories, and client access protocols.</p></td>
</tr>
<tr class="odd">
<td><p><a href="delegated-setup-exchange-2013-help.md">Delegated Setup</a></p></td>
<td><p>Administrators who are members of the Delegated Setup role group can deploy servers running Exchange 2013 that have been previously provisioned by a member of the Organization Management role group.</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">Compliance Management</a></p></td>
<td><p>Users who are members of the Compliance Management role group can configure and manage Exchange compliance settings in accordance with their organization's policy.</p></td>
</tr>
</tbody>
</table>


If you work in a small organization that has only a few administrators, you might need to add those administrators to the Organization Management role group only, and you may never need to use the other role groups. If you work in a larger organization, you might have administrators who perform specific tasks administering Exchange, such as recipient or server management. In those cases, you might add one administrator to the Recipient Management role group, and another administrator to the Server Management role group. Those administrators can then manage their specific areas of Exchange 2013 but won't have permissions to manage areas they're not responsible for.

If the built-in role groups in Exchange 2013 don't match the job function of your administrators, you can create role groups and add roles to them. For more information, see Work with Role Groups later in this topic.

Return to top

## Role assignment policies

Exchange 2013 provides role assignment policies so that you can control what settings your users can configure on their own mailboxes and on distribution groups they own. These settings include their display name, contact information, voice mail settings, and distribution group membership.

Your Exchange 2013 organization can have multiple role assignment policies that provide different levels of permissions for the different types of users in your organizations. Some users can be allowed to change their address or create distribution groups, while others can't, depending on the role assignment policy associated with their mailbox. Role assignment policies are added directly to mailboxes, and each mailbox can only be associated with one role assignment policy at a time.

Of the role assignment policies in your organization, one is marked as default. The default role assignment policy is associated with new mailboxes that aren't explicitly assigned a specific role assignment policy when they're created. The default role assignment policy should contain the permissions that should be applied to the majority of your mailboxes.

Permissions are added to role assignment policies using end-user roles. End-user roles begin with `My` and grant permissions for users to manage only their mailbox or distribution groups they own. They can't be used to manage any other mailbox. Only end-user roles can be assigned to role assignment policies.

When an end-user role is assigned to a role assignment policy, all of the mailboxes associated with that role assignment policy receive the permissions granted by the role. This enables you to add or remove permissions to sets of users without having to configure individual mailboxes. The following figure shows:

  - End-user roles are assigned to role assignment policies. Role assignment policies can share the same end-user roles.

  - Role assignment policies are associated with mailboxes. Each mailbox can only be associated with one role assignment policy.

  - After a mailbox is associated with a role assignment policy, the end-user roles are applied to that mailbox. The permissions granted by the roles are granted to the user of the mailbox.

**Roles, role assignment policies, and mailboxes**

![Role, role assignment policy, mailbox relationship](images/Dd351175.82e07b3d-da59-465b-b349-e0bfde369ace(EXCHG.150).gif "Role, role assignment policy, mailbox relationship")

The Default Role Assignment Policy role assignment policy is included with Exchange 2013. As the name implies, it's the default role assignment policy. If you want to change the permissions provided by this role assignment policy, or if you want to create role assignment policies, see Work with Role Assignment Policies later in this topic.

## Work with role groups

To manage your permissions using role groups in Exchange 2013, we recommend that you use the Exchange Administration Center. When you use the EAC to manage role groups, you can add and remove roles and members, create role groups, and copy role groups with a few clicks of your mouse. The EAC provides simple dialog boxes, such as the **new role group** dialog box, shown in the following figure, to perform these tasks.

**New role group dialog box in the EAC**

![New role group dialog box in the EAC](images/Dd351175.e0577090-73e6-4671-ae98-78a8064fde87(EXCHG.150).jpg "New role group dialog box in the EAC")

Exchange 2013 includes several role groups that separate permissions into specific administrative areas. If these existing role groups provide the permissions your administrators need to manage your Exchange 2013 organization, you need only add your administrators as members of the appropriate role groups. After you add administrators to a role group, they can administer the features that relate to that role group. To add or remove members to or from a role group, open the role group in the EAC, and then add or remove members from the membership list. For a list of built-in role groups, see [Built-in role groups](built-in-role-groups-exchange-2013-help.md).


> [!IMPORTANT]
> If an administrator is a member of more than one role group, Exchange 2013 grants the administrator all of the permissions provided by the role groups he or she is a member of.



If none of the role groups included with Exchange 2013 have the permissions you need, you can use the EAC to create a role group and add the roles that have the permissions you need. For your new role group, you will:

1.  Choose a name for your role group.

2.  Select the roles you want to add to the role group.

3.  Add members to the role group.

4.  Save the role group.

After you create the role group, you manage it like any other role group.

If there's an existing role group that has some, but not all of the permissions you need, you can copy it and then make changes to create a role group. You can copy an existing role group and make changes to it, without affecting the original role group. As part of copying the role group, you can add a new name and description, add and remove roles to and from the new role group, and add new members. When you create or copy a role group, you use the same dialog box that's shown in the preceding figure.

Existing role groups can also be modified. You can add and remove roles from existing role groups, and add and remove members from it at the same time, using an EAC dialog box similar to the one in the preceding figure. By adding and removing roles to and from role groups, you turn on and off administrative features for members of that role group. For a list of roles you can add to a role group, see [Built-in management roles](built-in-management-roles-exchange-2013-help.md).


> [!NOTE]
> Although you can change which roles are assigned to built-in role groups, we recommend that you copy built-in role groups, modify the role group copy, and then add members to the role group copy.



Return to top

## Work with role assignment policies

To manage the permissions that you grant end users to manage their own mailbox in Exchange 2013, we recommend that you use the EAC. When you use the EAC to manage end-user permissions, you can add roles, remove roles, and create role assignment policies with a few clicks of your mouse. The EAC provides simple dialog boxes, such as the **role assignment policy** dialog box, shown in the following figure, to perform these tasks.

**Role assignment policy dialog box in the EAC**

![Role assignment policy dialog box in the EAC](images/Dd351175.ecdf3cd4-d50e-4014-95f8-1bd5dafacaff(EXCHG.150).jpg "Role assignment policy dialog box in the EAC")

Exchange 2013 includes a role assignment policy named Default Role Assignment Policy. This role assignment policy enables users whose mailboxes are associated with it to do the following:

  - Join or leave distribution groups that allow members to manage their own membership.

  - View and modify basic mailbox settings on their own mailbox, such as Inbox rules, spelling behavior, junk mail settings, and Microsoft ActiveSync devices.

  - Modify their contact information, such as work address and phone number, mobile phone number, and pager number.

  - Create, modify, or view text message settings.

  - View or modify voice mail settings.

  - View and modify their marketplace apps.

  - Create team mailboxes and connect them to Microsoft SharePoint lists.

If you want to add or remove permissions from the Default Role Assignment Policy or any other role assignment policy, you can use the EAC. The dialog box you use is similar to the one in the preceding figure. When you open the role assignment policy in the EAC, select the check box next to the roles you want to assign to it or clear the check box next to the roles you want to remove. The change you make to the role assignment policy is applied to every mailbox associated with it.

If you want to assign different end-user permissions to the various types of users in your organization, you can create role assignment policies. When you create a role assignment policy, you see a dialog box similar to the one in the preceding figure. You can specify a new name for the role assignment policy, and then select the roles you want to assign to the role assignment policy. After you create a role assignment policy, you can associate it with mailboxes using the EAC.

If you want to change which role assignment policy is the default, you must use the Shell. When you change the default role assignment policy, any mailboxes that are created will be associated with the new default role assignment policy if one wasn't explicitly specified. The role assignment policy associated with existing mailboxes doesn't change when you select a new default role assignment policy.


> [!NOTE]
> If you select a check box for a role that has child roles, the check boxes for the child roles are also selected. If you clear the check box for a role with child roles, the check boxes for the child roles are also cleared.<BR>For detailed steps about how to create role assignment policies or make changes to existing role assignment policies, see the following topics: 
> <UL>
> <LI>
> <P><A href="manage-role-assignment-policies-exchange-2013-help.md">Manage role assignment policies</A></P>
> <LI>
> <P><A href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Change the assignment policy on a mailbox</A></P></LI></UL>



Return to top

## Permissions documentation

The following table contains links to topics that will help you learn about and manage permissions in Exchange 2013.


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
<td><p><a href="understanding-role-based-access-control-exchange-2013-help.md">Understanding Role Based Access Control</a></p></td>
<td><p>Learn about each of the components that make up RBAC and how you can create advanced permissions models if role groups and management roles aren’t enough.</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-multiple-forest-permissions-exchange-2013-help.md">Understanding multiple-forest permissions</a></p></td>
<td><p>Learn about implementing RBAC permissions in organizations with account and resource forests.</p></td>
</tr>
<tr class="odd">
<td><p><a href="understanding-split-permissions-exchange-2013-help.md">Understanding split permissions</a></p></td>
<td><p>Learn about splitting Exchange and security principal management using RBAC and Active Directory split permissions.</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-permissions-coexistence-with-exchange-2007-and-exchange-2010-exchange-2013-help.md">Understanding permissions coexistence with Exchange 2007 and Exchange 2010</a></p></td>
<td><p>Configure permissions to enable administration of Exchange 2013 in existing Exchange 2007 and Exchange 2010 organizations.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-role-groups-exchange-2013-help.md">Manage role groups</a></p></td>
<td><p>Configure permissions for Exchange administrators and specialist users using role groups.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-group-members-exchange-2013-help.md">Manage role group members</a></p></td>
<td><p>Add members to and from role groups. By adding and removing members to and from role groups, you configure who’s able to administer Exchange features.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-linked-role-groups-exchange-2013-help.md">Manage linked role groups</a></p></td>
<td><p>Configure permissions for Exchange administrators and specialist users in multi-forest Exchange deployments.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Manage role assignment policies</a></p></td>
<td><p>Configure which features end-users have access to on their mailboxes using role assignment policies.</p></td>
</tr>
<tr class="odd">
<td><p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Change the assignment policy on a mailbox</a></p></td>
<td><p>Configure which role assignment policy is applied to one or more mailboxes.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md">Create linked role groups that mirror built-in role groups</a></p></td>
<td><p>Re-create the built-in role groups as linked role groups in multi-forest Exchange deployments.</p></td>
</tr>
<tr class="odd">
<td><p><a href="view-effective-permissions-exchange-2013-help.md">View effective permissions</a></p></td>
<td><p>View who has permissions to administer Exchange features.</p></td>
</tr>
<tr class="even">
<td><p><a href="feature-permissions-exchange-2013-help.md">Feature permissions</a></p></td>
<td><p>Learn more about the permissions required to manage Exchange features and services.</p></td>
</tr>
<tr class="odd">
<td><p><a href="advanced-permissions-exchange-2013-help.md">Advanced permissions</a></p></td>
<td><p>Use advanced RBAC features to create highly customized permission models to fit the needs of any organization.</p></td>
</tr>
</tbody>
</table>

