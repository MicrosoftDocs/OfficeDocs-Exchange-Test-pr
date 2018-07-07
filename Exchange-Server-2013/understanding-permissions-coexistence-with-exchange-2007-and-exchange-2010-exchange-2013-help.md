---
title: 'Understanding permissions coexistence with Exchange 2007 and Exchange 2010: Exchange 2013 Help'
TOCTitle: Understanding permissions coexistence with Exchange 2007 and Exchange 2010
ms:assetid: 28ab1433-23ee-4914-8f21-9a32578792e5
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd335157(v=EXCHG.150)
ms:contentKeyID: 56278647
ms.date: 07/14/2016
mtps_version: v=EXCHG.150
---

# Understanding permissions coexistence with Exchange 2007 and Exchange 2010

 

_**Applies to:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_


When you install Microsoft Exchange Server 2013 into an existing Microsoft Exchange Server 2010 or Microsoft Exchange Server 2007 organization, you need to understand how permissions will work in the new organization. Read the section below that applies to your organization.

  - Installing Exchange 2013 into an existing Exchange 2010 organization

  - Installing Exchange 2013 into an existing Exchange 2007 organization

## Installing Exchange 2013 into an existing Exchange 2010 organization

Exchange 2013 uses the same Role Based Access Control (RBAC) permissions model that’s used in Exchange 2010. When you install Exchange 2013 into an existing Exchange 2010 organization, the same management role groups, management roles, and management scopes apply to both Exchange 2013 and Exchange 2010 servers and recipients. Members of role groups, or users assigned to roles, can administer any Exchange 2013 or Exchange 2013 server or recipient that’s included in the scope of the role group or role. If you don't use scopes in your organization and you want the members of your existing role groups to manage Exchange 2010 and Exchange 2013 servers and recipients, you don't have to do anything else. Those administrators will be able to manage Exchange 2013 servers and recipients that are added to the organization. If you need a reminder on how permissions work in Exchange 2010 and Exchange 2013, see [Permissions](permissions-exchange-2013-help.md).

In the new organization, you might want to separate the administration of Exchange 2010 and Exchange 2013 servers and recipients. The group of administrators responsible for administering Exchange 2010 servers and recipients may not be allowed to administer Exchange 2013 servers and recipients, and vice versa. In this case, you can use management scopes to define the servers and recipients each group of administrators should be allowed to manage. After you create the scopes you want, you can then copy existing role groups, add the administrators who should be a member of each, and then add the scopes to those role groups. When you're done, the members of each role group will only be able to administer the servers and recipients that match their respective scopes.

For more information about role groups, scopes, copying role groups, and adding scopes to role groups, see the following topics:

  - [Manage role groups](manage-role-groups-exchange-2013-help.md)

  - [Create a regular or exclusive scope](create-a-regular-or-exclusive-scope-exchange-2013-help.md)

  - [Understanding management role groups](understanding-management-role-groups-exchange-2013-help.md)

  - [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md)

## Installing Exchange 2013 into an existing Exchange 2007 organization

Exchange 2013 includes Role Based Access Control (RBAC) permissions that replace the Active Directory access control entry (ACE)-based authorization model used in Microsoft Exchange Server 2007. RBAC is the authorization mechanism used for most of the management of Exchange 2013. This mechanism includes the following management areas:

  - Exchange Management Shell

  - Exchange admin center (EAC)

  - Exchange Web Services

For more information about how to plan coexistence between Exchange 2013 and Exchange 2007, see [Upgrade from Exchange 2007 to Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md).

Looking for management tasks related to permissions? Check out [Permissions](permissions-exchange-2013-help.md).

## Exchange 2013 permissions

The Exchange 2013 RBAC permissions model consists of management role groups assigned one of several management roles. Management roles contain permissions that enable administrators to perform tasks in the Exchange organization. Administrators are added as members of the role groups and are granted all the permissions that the roles provide. The following table provides an example of the role groups, some of the roles assigned to role groups, and a description of the kind of user who might be a member of the role group.

### Examples of role groups and roles in Exchange 2013

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Management role group</th>
<th>Management roles</th>
<th>Members of this role group</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>The following roles are some of the roles assigned to this role group:</p>
<ul>
<li><p>Address Lists</p></li>
<li><p>Exchange Servers</p></li>
<li><p>Journaling</p></li>
<li><p>Mail Recipients</p></li>
<li><p>Public Folders</p></li>
</ul></td>
<td><p>Users who manage the entire Exchange 2013 organization should be members of this role group. With some exceptions, members of this role group can manage nearly any aspect of the Exchange 2013 organization.</p>
<p>By default, the user account used to prepare Active Directory for Exchange 2013 is a member of this role group.</p>
<p>For more information about this role group and for a complete list of roles assigned to this role group, see <a href="organization-management-exchange-2013-help.md">Organization Management</a>.</p></td>
</tr>
<tr class="even">
<td><p>View Only Organization Management</p></td>
<td><p>The following roles are assigned to this role group:</p>
<ul>
<li><p>Monitoring</p></li>
<li><p>View-Only Configuration</p></li>
<li><p>View-Only Recipients</p></li>
</ul></td>
<td><p>Users who view the configuration of the entire Exchange 2013 organization should be members of this role group. These users must be able to view server configuration and recipient information, and perform monitoring functions without the ability to change organization or recipient configuration.</p>
<p>For more information about this role group, see <a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Recipient Management</p></td>
<td><p>The following roles are assigned to this role group:</p>
<ul>
<li><p>Distribution Groups</p></li>
<li><p>Mail Enabled Public Folders</p></li>
<li><p>Mail Recipient Creation</p></li>
<li><p>Mail Recipients</p></li>
<li><p>Message Tracking</p></li>
<li><p>Migration</p></li>
<li><p>Move Mailboxes</p></li>
<li><p>Recipient Policies</p></li>
</ul></td>
<td><p>Users who manage recipients such as mailboxes, contacts, and distribution groups in the Exchange 2013 organization should be members of this role group. These users can create recipients, modify or delete existing recipients, or move mailboxes.</p>
<p>For more information about this role group and for a complete list of roles assigned to this role group, see <a href="recipient-management-exchange-2013-help.md">Recipient Management</a>.</p></td>
</tr>
<tr class="even">
<td><p>Server Management</p></td>
<td><p>The following roles are some of the roles assigned to this role group:</p>
<ul>
<li><p>Databases</p></li>
<li><p>Exchange Connectors</p></li>
<li><p>Exchange Servers</p></li>
<li><p>Receive Connectors</p></li>
<li><p>Transport Queues</p></li>
</ul></td>
<td><p>Users who manage Exchange server configuration such as Receive connectors, certificates, databases, and virtual directories should be members of this role group. These users can modify Exchange server configuration, create databases, and restart and manipulate transport queues.</p>
<p>For more information about this role group and for a complete list of roles assigned to this role group, see <a href="server-management-exchange-2013-help.md">Server Management</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Discovery Management</p></td>
<td><p>The following roles are assigned to this role group:</p>
<ul>
<li><p>Legal Hold</p></li>
<li><p>Mailbox Search</p></li>
</ul></td>
<td><p>Users who perform searches of mailboxes to support legal proceedings or to configure legal holds should be members of this role group.</p>
<p>This is an example of a role group that might contain non-Exchange administrators, such as personnel in the legal department. Legal personnel can perform their tasks without intervention from Exchange administrators.</p>
<p>For more information about this role group and for a complete list of roles assigned to this role group, see <a href="discovery-management-exchange-2013-help.md">Discovery Management</a>.</p></td>
</tr>
</tbody>
</table>


This table shows that Exchange 2013 provides a granular level of control over the permissions that you grant to your administrators. You can choose among 12 role groups in Exchange 2013. For a complete list of role groups and the permissions that they provide, see [Built-in role groups](built-in-role-groups-exchange-2013-help.md).

Because Exchange 2013 provides many role groups and because further customization is possible by creating role groups that have different role combinations, the manipulation of access control lists (ACLs) on Active Directory objects is no longer necessary and has no effect. ACLs are no longer used to apply permissions to individual administrators or groups in Exchange 2013. All tasks, such as an administrator creating a mailbox or a user accessing a mailbox, are managed by RBAC. RBAC authorizes the task, and then Exchange performs the task on behalf of the user if allowed. Exchange performs the task in the Exchange Trusted Subsystem universal security group (USG). With some exceptions, all the ACLs on objects in Active Directory that Exchange 2010 has to access are granted to the Exchange Trusted Subsystem USG. This is a fundamental change from how permissions are handled in Exchange 2007.

The permissions granted to a user in Active Directory are separate from the permissions granted to the user by RBAC when that user is using the Exchange 2013 management tools.

For more information about RBAC, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

## Exchange 2007 permissions

The Exchange 2007 administrative model leverages Active Directory forests to define security boundaries. There is no isolation of security permissions within a specific forest. Forest owners and enterprise administrators can always gain access to all resources in any domain. In Exchange 2007, you may have to grant enterprise administrator rights and top-level domain administrator rights on a temporary basis only.

Exchange 2007 provides the following predefined administrator roles:

  - **Exchange Organization Administrator role**   This role grants permissions to control all aspects of the Exchange 2007 organization. Additionally, an administrator who has this role can grant permissions to other Exchange administrators. This role is granted to the account that you use to install Exchange 2007.

  - **Exchange View-Only Administrator role**   This role grants permissions to view Exchange configuration. However, an administrator who has this role can't modify objects in the Exchange 2007 organization.

  - **Exchange Recipient Administrator role**   This role grants permissions to manage e-mail recipients. An administrator who has this role can modify Exchange-related items for users, groups, contacts, and distribution groups.

  - **Exchange Server Administrator role**   This role grants permissions to manage a specific server. However, this role doesn't grant permissions to perform actions that have a global impact on the Exchange 2007 organization.

  - **Exchange Public Folder Administrator role**   This role was added in Exchange 2007 Service Pack 1**.** This role grants permissions to manage public folders in the Exchange 2007 organization.

This permissions model uses USGs for all roles except for the Exchange Server Administrator role. When you run the Exchange 2007 **Setup /PrepareAD** command, the Setup program creates the USGs in the root domain and gives a forest-wide scope to the USGs. The USGs are assigned ACLs to manage Exchange objects throughout Active Directory.

In Exchange 2007, you can separate administrators by assigning them various roles. The permissions are assigned directly either to the user or to the USG of which the user is a member. Any actions performed by the user are performed in the context of that user's Active Directory account. The following table lists the Exchange 2007 administrator roles together with their Exchange-related permissions.

### Exchange 2007 administrator roles

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Administrator role</th>
<th>Members</th>
<th>Member of</th>
<th>Exchange permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Organization Administrator</p></td>
<td><p>The Administrator account or the account used to install the first Exchange 2007 server</p></td>
<td><p>Exchange Recipient Administrator</p>
<p>Administrators local group of <em>&lt;server name&gt;</em></p></td>
<td><p>Full control of the Microsoft Exchange container in Active Directory</p></td>
</tr>
<tr class="even">
<td><p>Exchange View-Only Administrator</p></td>
<td><p>Exchange Recipient Administrators</p>
<p>Exchange Server Administrators (<em>&lt;server name</em>&gt;)</p></td>
<td><p>Exchange Recipient Administrators</p>
<p>Exchange Server Administrators</p></td>
<td><p>Read access to the Microsoft Exchange container in Active Directory</p>
<p>Read access to all the Windows domains that have Exchange recipients</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Recipient Administrator</p></td>
<td><p>Exchange Organization Administrators</p></td>
<td><p>Exchange View-Only Administrators</p></td>
<td><p>Full control of Exchange properties on Active Directory user objects</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server Administrator</p></td>
<td><p>Exchange Organization Administrators</p></td>
<td><p>Exchange View-Only Administrators</p>
<p>Administrators local group of <em>&lt;server name</em>&gt;</p></td>
<td><p>Full control of Exchange <em>&lt;server name</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>Each Exchange 2007 computer account</p></td>
<td><p>Exchange View-Only Administrators</p></td>
<td><p>Special</p></td>
</tr>
<tr class="even">
<td><p>Exchange Public Folder Administrator</p></td>
<td><p>Exchange Organization Administrators</p></td>
<td><p>Exchange View-Only Administrators</p></td>
<td><p>Full control to manage all public folders (granted the Create top level public folder extended right)</p></td>
</tr>
</tbody>
</table>


If you need to make more granular permission assignments, you can modify the ACLs on individual Exchange 2007 objects, such as address lists or databases. You must add the user or security group of which the user is a member directly to the ACL. Then, the actions are performed in the context of the particular user.

For more information about how to manage permissions in Exchange 2007, see [Configuring Permissions in Exchange Server 2007](http://go.microsoft.com/fwlink/p/?linkid=90671).

## Exchange 2013 and Exchange 2007 coexistence permissions

Because the permissions models for Exchange 2013 and for Exchange 2007 differ, Exchange 2013 permission assignments are separate from Exchange 2007 permission assignments. This is true even if both versions of Exchange are installed in the same forest. Without additional configuration, Exchange 2013 administrators don't have the required permissions to manage Exchange 2007-based servers, and Exchange 2007 administrators don't have the required permissions to manage Exchange 2013-based servers. You should consider the following questions:

  - Do you want to grant Exchange 2013 administrators access to manage Exchange 2007 servers?

  - Do you want to grant Exchange 2007 administrators access to manage Exchange 2013 servers?

  - Do you want to customize Exchange 2013 permissions so that they match any customizations that have been made to Exchange 2007 ACLs?

## Granting Exchange 2013 permissions to Exchange 2007 administrators

If you want Exchange 2007 administrators to administer Exchange 2013 servers, the Exchange 2007 administrators must be added as members of one or more Exchange 2013 role groups. You can add either users or USGs to role groups. The permissions granted to the role groups are then applied to the users or the USGs that you add as members.


> [!IMPORTANT]
> If you use domain local or global Active Directory security groups, you must change them to USGs if you want to add them as members of an Exchange 2013 role group. Exchange 2013 supports only USGs.



The following table describes the mapping between Exchange 2007 administrator roles and Exchange 2013 role groups.

### Exchange 2007 administrator roles and Exchange 2010 role groups

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007 administrator role</th>
<th>Exchange 2013 role group</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Organization Administrator</p></td>
<td><p>Organization Management</p></td>
</tr>
<tr class="even">
<td><p>Exchange Recipient Administrator</p></td>
<td><p>Recipient Management</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server Administrator</p></td>
<td><p>Server Management</p></td>
</tr>
<tr class="even">
<td><p>Exchange View-Only Administrator</p></td>
<td><p>View Only Organization Management</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>No equivalent role group in Exchange 2013</p>
<p>(For more information about how to create custom role groups, see <a href="manage-role-groups-exchange-2013-help.md">Manage role groups</a>.)</p></td>
</tr>
<tr class="even">
<td><p>Exchange Public Folder Administrator</p></td>
<td><p>Public Folder Management</p></td>
</tr>
</tbody>
</table>


If all your Exchange 2007 administrators are members of one of the Exchange 2007 administrative roles, you can add the members of each of the administrative groups to their equivalent Exchange 2013 role group. For example, if you want to give all Exchange 2007 organization administrators full access to Exchange 2013 objects, add the Exchange Organization Administrators USG to the Organization Management role group.

For more information about how to add users and USGs to role groups, see [Manage role group members](manage-role-group-members-exchange-2013-help.md).

If you modify ACLs on Exchange 2007 objects to grant more granular permissions to Exchange 2007 administrators, and if you want to assign similar permissions to Exchange 2013 servers to those administrators, follow these steps:

1.  Review the ACL customizations that have been made to the Exchange 2007 objects, and locate the administrators who have been granted permissions to each object.

2.  Categorize each Exchange 2007 object. For example, determine whether the object is a database, server, or recipient object.

3.  Map the objects to the corresponding Exchange 2013 role group. For a list of built-in role groups, see [Built-in role groups](built-in-role-groups-exchange-2013-help.md).

4.  Add the USGs or users for each kind of object to the corresponding Exchange 2013 role groups. For more information about how to add users and USGs to role groups, see [Manage role group members](manage-role-group-members-exchange-2013-help.md).

After you complete these steps, the Exchange 2007 administrators will be members of the specific role group that's mapped to the appropriate Exchange 2013 objects. The Exchange 2007 administrators can use the Exchange 2013 management tools to manage the Exchange 2013 servers and recipients.


> [!IMPORTANT]
> In general, Exchange 2007 servers and recipients must be managed by using Exchange 2007 management tools, and Exchange 2013 servers and recipients must be managed by using Exchange 2013 management tools.



If the built-in role groups don't provide the specific set of permissions that you want to grant to some administrators, you can create custom role groups. When you create a custom role group, you can select which roles to add to it. You can define the specific features you want members of the role group to manage. For example, if you want administrators to manage only distribution groups, you can create a custom role group, and then select only the Distribution Groups role. After you do this, members of that custom role group can manage only distribution groups. For more information about how to create custom role groups, see [Manage role groups](manage-role-groups-exchange-2013-help.md).

If you assign selective permissions to certain Exchange 2007 objects (for example, you allow administrators to administer only specific databases), and if you want to apply the same configuration to your Exchange 2013 servers, see "Re-Creating Exchange 2007 ACL Customization Using Management Scopes in Exchange 2013" later in this topic.

## Granting Exchange 2007 permissions to Exchange 2013 administrators

If you want Exchange 2013 administrators to administer Exchange 2007 servers, add the Exchange 2013 administrators to the USGs or the security group that corresponds to the particular Exchange 2007 administrator role. Alternatively, if you have customized ACL settings, add the administrators to the appropriate ACLs. Role groups are USGs, so role groups can be added directly to Exchange 2007 administrator role USGs.

After you finish, the Exchange 2013 administrators will be members of the appropriate Exchange 2007 administrator role or roles. The Exchange 2013 administrators can use the Exchange 2007 management tools to manage Exchange 2007 servers and recipients.

## Re-Creating Exchange 2007 ACL customization using management scopes in Exchange 2013

In Exchange 2007, when you want to restrict who can administer a specific mailbox store, administer specific users, or control which mailbox store mailboxes are created on, you must modify the ACLs on the objects you want to restrict. Exchange 2013 provides the same capabilities, but without having to modify any ACLs. It does this by using management scopes, which are a component of RBAC.

Management scopes provide built-in scopes and custom scopes to define the objects that administrators can manage. By applying management scopes, you can define which recipients can be administered, which mailbox databases mailboxes can be created on, and which recipients or servers should be administered by a small group of administrators and by no one else.

You can create the following types of management scopes:

  - **Predefined relative**   Predefined relative scopes are included in Exchange 2013. You can control what a user sees and what a user modifies. For example, predefined relative scopes can control whether users see only information about themselves or information about the entire organization.

  - **Recipient**   Recipient scopes control which recipients an administrator can create, modify, or delete. These selections can be based on an organizational unit (OU), a recipient filter, or both. Recipient filters specify the criteria that a recipient must match to be included in the scope. For example, you might create a recipient filter scope that includes all users in a certain location or in a specific department. You can even combine OUs and recipient filters to match only users who are within a specific OU and who report to a specific manager.

  - **Server**   Server scopes control which servers an administrator can manage. You can specify either server lists or server filters. For server lists, you define a static list of servers that can be managed. Server filters work in the same manner as recipient filters in that you can specify the criteria that have to be matched. For example, you might create a server scope that matches all servers within a particular Active Directory site.

  - **Database**   Database scopes control which databases an administrator can manage. They can also control which databases mailboxes can be created on or which databases mailboxes can be moved to. Like server scopes, they can be defined as lists or as filters. For example, you might create a list or filter that allows administrators to create mailboxes on or move mailboxes to specific mailbox databases managed by a specific subsidiary.

  - **Exclusive**   Recipient, server, and database scopes can also be created as exclusive scopes. Exclusive scopes work in the same manner as deny access ACEs in ACLs. If anything matches an exclusive scope, only the administrators assigned an exclusive scope can manage that object. This is true even if another scope that isn't exclusive matches the same object. This is especially useful when you might want only a few, highly trusted individuals to be able to manage an executive's mailbox. Even if another regular recipient scope is broader and includes the executive's mailbox in the scope, the administrators assigned the broader, regular recipient scope won't be able to manage that executive's mailbox unless they are also assigned the exclusive scope.

Management scopes are used with management roles, management role assignments, and management role groups to control who can manage what objects and in what manner they can manage those objects. For more information, see the following topics:

  - [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md)

  - [Understanding exclusive scopes](understanding-exclusive-scopes-exchange-2013-help.md)

  - [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md)

  - [Understanding management role groups](understanding-management-role-groups-exchange-2013-help.md)

  - [Understanding management roles](understanding-management-roles-exchange-2013-help.md)

To create the same permissions model in Exchange 2013 using management scopes that you might have defined using customized ACLs, you must inventory the ACLs that you've customized, and then create management scopes that match them. You can use the filterable properties available on recipient, server, and database objects to create management scopes that include the objects to which you want each management scope to control access. For more information about the properties that you can use with management scope filters, see [Understanding management role scope filters](understanding-management-role-scope-filters-exchange-2013-help.md).

For more information about how to create management scopes, see [Create a regular or exclusive scope](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

