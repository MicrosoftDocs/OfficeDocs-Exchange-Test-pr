---
title: 'Organization Management: Exchange 2013 Help'
TOCTitle: Organization Management
ms:assetid: 0bfd21c1-86ac-4369-86b7-aeba386741c8
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd335087(v=EXCHG.150)
ms:contentKeyID: 49289160
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Organization Management

 

_**Applies to:** Exchange Server 2013_


The Organization Management management role group is one of several built-in role groups that make up the Role Based Access Control (RBAC) permissions model in Microsoft Exchange Server 2013. Role groups are assigned one or more management roles that contain the permissions required to perform a given set of tasks. The members of a role group are granted access to the management roles assigned to the role group. For more information about role groups, see [Understanding management role groups](understanding-management-role-groups-exchange-2013-help.md).

Administrators that are members of the Organization Management role group have administrative access to the entire Exchange 2013 organization and can perform almost any task against any Exchange 2013 object, with some exceptions. By default, members of this role group can't perform mailbox searches and management of unscoped top-level management roles. For more information, see the "Delegating Only Role Assignments" section later in this topic.


> [!IMPORTANT]
> The Organization Management role group is a very powerful role and as such, only users or universal security groups (USGs) that perform organizational-level administrative tasks that can potentially impact the entire Exchange organization should be members of this role group.



This role group is equivalent to the Exchange Organization Administrators role in Exchange Server 2007.

For more information about RBAC, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

## Role group membership

By default, the account that's used to install Exchange 2013 in the organization is added as a member of the Organization Management role group. This account can then add other members to the role group as needed.

If you want to add or remove members to or from this role group, see [Manage role group members](manage-role-group-members-exchange-2013-help.md).

By default, only members of the Organization Management role group can add or remove members from this role group. For more information about how to add additional role group delegates, see the "Add or remove a role group delegate" section in [Manage role groups](manage-role-groups-exchange-2013-help.md).

You can use the following command to view a list of users or USGs that are members of this role group.

    Get-RoleGroupMember "Organization Management"

For more information about the members of a role group, see [Manage role groups](manage-role-groups-exchange-2013-help.md).

## Role group customization

This role group is assigned management roles by default. The roles that are included are listed in the "Management Roles Assigned to this Role Group" section. You can add or remove role assignments to or from this role group to match the needs of your organization.

The role groups provided with Exchange 2013 are designed to match more granular tasks. By assigning roles to a role group, you enable the members of that role group to perform the tasks associated with the role. For example, the Journaling role enables the management of the Journaling agent and journaling rules. For more information about how roles are assigned to role groups, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

The roles assigned to this role group are given default management scopes. Management scopes determine what Exchange objects can be viewed or modified by the members of a role group. You can change the scopes associated with assignments between roles and role groups. For example, you might want to do this if you only want members of a role group to be able to change recipients that are under a specific organizational unit or in a specific location. For more information about management scopes, see [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md).

For more information about how to customize this role group, see the following topics:

  - [Manage role groups](manage-role-groups-exchange-2013-help.md)

  - [Manage role group members](manage-role-group-members-exchange-2013-help.md)

If you want to create a role group and assign some of the roles that are assigned to this role group to the new role group, see the “Create a role group” section in [Manage role groups](manage-role-groups-exchange-2013-help.md).

The following are some ways you might want to customize this role:

  - **Permissions owner**   If the permissions in your organization are controlled by a specific group other than the Exchange administrators, you can create a role group and move the regular and delegating role assignments for the Role Management role to the new role group. Doing so prevents members of the Organization Management role group from managing any RBAC permissions.

  - **Active Directory split permissions**   If the creation of security principals in your organization, such as user accounts, is controlled by a specific group other than the Exchange administrators, you can create a role group and move the regular and delegating role assignments for the Mail Recipient Creation role and the Security Group Creation and Membership role to the new role group. Doing so prevents members of the Organization Management role group from creating Active Directory objects. They can, however, continue to mail-enable the new Active Directory objects. For more information about split permissions, see [Understanding split permissions](understanding-split-permissions-exchange-2013-help.md).

## Customization limitations

Any role can be added to or removed from this role group, with the following limitations:

  - Every role must have at least one delegating role assignment to a role group or USG before the delegating role assignment can be removed from this role group.

  - The Role Management role must have at least one regular role assignment to a role group or USG before the regular role assignment can be removed from this role group.

These limitations are intended to help prevent you from inadvertently locking yourself out of the system. By requiring that at least one delegating role assignment exists between every role and one or more role groups or USGs, you will always be able to assign roles to role assignees. By requiring that at least one regular role assignment exists between the Role Management role and one or more role groups or USGs, you will always be able to configure role groups and role assignments.


> [!IMPORTANT]
> These limitations require that role groups or USGs be the targets of the delegating and regular role assignments. You can't remove a delegating role assignment or the regular assignment for the Role Management role if the last assignment is to a user.



## Delegating only role assignments

Some role assignments between the Organization Management role group and management roles, such as Mailbox Search and Unscoped Role Management, are delegating only role assignments. These roles allow access to sensitive or personal information, such as the contents of mailboxes, or enable the creation of powerful unscoped management roles.

Delegating only role assignments enable members of the Organization Management role group only to assign the associated roles to other role groups, management role assignment policies, users, or USGs. Members of the Organization Management role group aren't given, by default, any permissions that the roles provide. This helps avoid accidental exposure to personal information or accidental elevation of privileges.

Members of the Organization Management role group can, however, assign themselves any role, in effect enabling them to perform any task. For example, a member of the Organization Management role group can assign the Mailbox Search role to the Organization Management role group. After this role assignment is made, members of the Organization Management role group can perform tasks enabled by the Mailbox Search role.

For more information about delegating role assignments, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

## Additional permissions

The permissions granted to members of the Organization Management role group are primarily determined by the management roles assigned to the role group. However, not all tasks that you need to perform are covered by management roles. Some tasks occur outside of the Exchange management tools, and therefore the RBAC permissions model doesn't apply. For these tasks, permissions are provided by adding the Organization Management role group to the access control lists (ACLs) of certain Active Directory objects.

The following tasks are granted permissions by way of ACLs on Active Directory objects and not by management roles assigned to the Organization Management role group:

  - Running DomainPrep and ForestPrep using Setup.exe

  - Deploying additional servers in the organization

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
<td><p><a href="active-directory-permissions-role-exchange-2013-help.md">Active Directory Permissions role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="address-lists-role-exchange-2013-help.md">Address Lists role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="applicationimpersonation-role-exchange-2013-help.md">ApplicationImpersonation role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="archiveapplication-role-exchange-2013-help.md">ArchiveApplication role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="audit-logs-role-exchange-2013-help.md">Audit Logs role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="cmdlet-extension-agents-role-exchange-2013-help.md">Cmdlet Extension Agents role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="data-loss-prevention-role-exchange-2013-help.md">Data Loss Prevention role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="database-availability-groups-role-exchange-2013-help.md">Database Availability Groups role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="database-copies-role-exchange-2013-help.md">Database Copies role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="databases-role-exchange-2013-help.md">Databases role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="disaster-recovery-role-exchange-2013-help.md">Disaster Recovery role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="distribution-groups-role-exchange-2013-help.md">Distribution Groups role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="edge-subscriptions-role-exchange-2013-help.md">Edge Subscriptions role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="e-mail-address-policies-role-exchange-2013-help.md">E-Mail Address Policies role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">Exchange Connectors role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">Exchange Server Certificates role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Exchange Servers role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">Exchange Virtual Directories role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="federated-sharing-role-exchange-2013-help.md">Federated Sharing role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="information-rights-management-role-exchange-2013-help.md">Information Rights Management role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="journaling-role-exchange-2013-help.md">Journaling role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="legal-hold-role-exchange-2013-help.md">Legal Hold role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="legalholdapplication-role-exchange-2013-help.md">LegalHoldApplication role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">Mail Enabled Public Folders role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Mail Recipient Creation role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mail-recipients-role-exchange-2013-help.md">Mail Recipients role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mail-tips-role-exchange-2013-help.md">Mail Tips role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mailbox-import-export-role-exchange-2013-help.md">Mailbox Import Export role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mailbox-search-role-exchange-2013-help.md">Mailbox Search role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mailboxsearchapplication-role-exchange-2013-help.md">MailboxSearchApplication role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="message-tracking-role-exchange-2013-help.md">Message Tracking role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="migration-role-exchange-2013-help.md">Migration role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="monitoring-role-exchange-2013-help.md">Monitoring role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">Move Mailboxes role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="officeextensionapplication-role-exchange-2013-help.md">OfficeExtensionApplication role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="organization-client-access-role-exchange-2013-help.md">Organization Client Access role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="organization-configuration-role-exchange-2013-help.md">Organization Configuration role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="organization-transport-settings-role-exchange-2013-help.md">Organization Transport Settings role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">POP3 and IMAP4 Protocols role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="public-folders-role-exchange-2013-help.md">Public Folders role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="receive-connectors-role-exchange-2013-help.md">Receive Connectors role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="recipient-policies-role-exchange-2013-help.md">Recipient Policies role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="remote-and-accepted-domains-role-exchange-2013-help.md">Remote and Accepted Domains role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="reset-password-role-exchange-2013-help.md">Reset Password role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="retention-management-role-exchange-2013-help.md">Retention Management role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="role-management-role-exchange-2013-help.md">Role Management role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">Security Group Creation and Membership role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="send-connectors-role-exchange-2013-help.md">Send Connectors role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="support-diagnostics-role-exchange-2013-help.md">Support Diagnostics role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="teammailboxlifecycleapplication-role-exchange-2013-help.md">TeamMailboxLifecycleApplication role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-agents-role-exchange-2013-help.md">Transport Agents role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="transport-hygiene-role-exchange-2013-help.md">Transport Hygiene role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-queues-role-exchange-2013-help.md">Transport Queues role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="transport-rules-role-exchange-2013-help.md">Transport Rules role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="um-mailboxes-role-exchange-2013-help.md">UM Mailboxes role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="um-prompts-role-exchange-2013-help.md">UM Prompts role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">Unscoped Role Management role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="unified-messaging-role-exchange-2013-help.md">Unified Messaging role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="userapplication-role-exchange-2013-help.md">UserApplication role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="user-options-role-exchange-2013-help.md">User Options role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="view-only-audit-logs-role-exchange-2013-help.md">View-Only Audit Logs role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">View-Only Configuration role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">View-Only Recipients role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="workloadmanagement-role-exchange-2013-help.md">WorkloadManagement role</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="my-custom-apps-role-exchange-2013-help.md">My Custom Apps role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="my-marketplace-apps-role-exchange-2013-help.md">My Marketplace Apps role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mybaseoptions-role-exchange-2013-help.md">MyBaseOptions role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mycontactinformation-role-exchange-2013-help.md">MyContactInformation role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mydiagnostics-role-exchange-2013-help.md">MyDiagnostics role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mydistributiongroupmembership-role-exchange-2013-help.md">MyDistributionGroupMembership role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mydistributiongroups-role-exchange-2013-help.md">MyDistributionGroups role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myprofileinformation-role-exchange-2013-help.md">MyProfileInformation role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="myretentionpolicies-role-exchange-2013-help.md">MyRetentionPolicies role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myteammailboxes-role-exchange-2013-help.md">MyTeamMailboxes role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">MyTextMessaging role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myvoicemail-role-exchange-2013-help.md">MyVoiceMail role</a></p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>

