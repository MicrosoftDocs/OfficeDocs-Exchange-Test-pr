---
title: 'Understanding split permissions: Exchange 2013 Help'
TOCTitle: Understanding split permissions
ms:assetid: 2b709e15-63a2-4841-94bc-b289b71166d0
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd638106(v=EXCHG.150)
ms:contentKeyID: 49289207
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Understanding split permissions

 

_**Applies to:** Exchange Server 2013_


Organizations that separate the management of Microsoft Exchange Server 2013 objects and Active Directory objects use what's called a *split permissions* model. Split permissions enable organizations to assign specific permissions and related tasks to specific groups within the organization. This separation of work helps to maintain standards and workflows, and helps to control change in the organization.

The highest level of split permissions is the separation of Exchange management and Active Directory management. Many organizations have two groups: administrators that manage the organization's Exchange infrastructure, including servers and recipients, and administrators that manage the Active Directory infrastructure. This is an important separation for many organizations because the Active Directory infrastructure often spans many locations, domains, services, applications, and even Active Directory forests. Active Directory administrators must ensure that changes made to Active Directory don't negatively impact any other services. As a result, typically only a small group of administrators is allowed to manage that infrastructure.

At the same time, the infrastructure for Exchange, including servers and recipients, can also be complex and require specialized knowledge. Additionally, Exchange stores extremely confidential information about the business of the organization. Exchange administrators can potentially access this information. By limiting the number of Exchange administrators, the organization limits who can make changes to Exchange configuration and who can access sensitive information.

Split permissions typically make a distinction between the creation of security principals in Active Directory, such as users and security groups, and the subsequent configuration of those objects. This helps to reduce the chance of unauthorized access to the network by controlling who can create objects that grant access to it. Most often only Active Directory administrators can create security principals while other administrators, such as Exchange administrators, can manage specific attributes on existing Active Directory objects.

To support the varying needs to separate the management of Exchange and Active Directory, Exchange 2013 lets you choose whether you want a shared permissions model or a split permissions model. Exchange 2013 offers two types of split permissions models: RBAC and Active Directory. Exchange 2013 defaults to a shared permissions model.

**Contents**

Explanation of Role Based Access Control and Active Directory

Shared permissions

Split permissions

RBAC split permissions

Active Directory split permissions

## Explanation of Role Based Access Control and Active Directory


To understand split permissions, you need to understand how the Role Based Access Control (RBAC) permissions model in Exchange 2013 works with Active Directory. The RBAC model controls who can perform what actions, and on which objects those actions can be performed. For more information about the various components of RBAC that are discussed in this topic, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

In Exchange 2013, all tasks that are performed on Exchange objects must be done through the Exchange Management Shell or the Exchange Administration Center (EAC) interface. Both of these management tools use RBAC to authorize all tasks that are performed.

RBAC is a component that exists on every server running Exchange 2013. RBAC checks whether the user performing an action is authorized to do so:

  - If the user isn't authorized to perform the action, RBAC doesn't allow the action to proceed.

  - If the user is authorized to perform the action, RBAC checks whether the user is authorized to perform the action against the specific object being requested:
    
      - If the user is authorized, RBAC allows the action to proceed.
    
      - If the user isn't authorized, RBAC doesn't allow the action to proceed.

If RBAC allows an action to proceed, the action is performed in the context of the Exchange Trusted Subsystem and not the user's context. The Exchange Trusted Subsystem is a highly privileged universal security group (USG) that has read/write access to every Exchange-related object in the Exchange organization. It's also a member of the Administrators local security group and the Exchange Windows Permissions USG, which enables Exchange to create and manage Active Directory objects.


> [!WARNING]
> Don't make any manual changes to the membership of the Exchange Trusted Subsystem security group. Also, don't add it to or remove it from object access control lists (ACLs). By making changes to the Exchange Trusted Subsystem USG yourself, you could cause irreparable damage to your Exchange organization.



It's important to understand that it doesn't matter what Active Directory permissions a user has when using the Exchange management tools. If the user is authorized, via RBAC, to perform an action in the Exchange management tools, the user can perform the action regardless of his or her Active Directory permissions. Conversely, if a user is an Enterprise Admin in Active Directory but isn't authorized to perform an action, such as creating a mailbox, in the Exchange management tools, the action won't succeed because the user doesn't have the required permissions according to RBAC.


> [!IMPORTANT]
> Although the RBAC permissions model doesn't apply to the Active Directory Users and Computers management tool, Active Directory Users and Computers can't manage the Exchange configuration. So although a user may have access to modify some attributes on Active Directory objects, such as the display name of a user, the user must use the Exchange management tools, and therefore must be authorized by RBAC, to manage Exchange attributes.



Return to top

## Shared permissions

The shared permissions model is the default model for Exchange 2013. You don't need to change anything if this is the permissions model you want to use. This model doesn't separate the management of Exchange and Active Directory objects from within the Exchange management tools. It allows administrators using the Exchange management tools to create security principals in Active Directory.

The following table shows the roles that enable the creation of security principals in Exchange and the management role groups they're assigned to by default.

### Security principal management roles

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Management role</th>
<th>Role group</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Mail Recipient Creation role</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">Security Group Creation and Membership role</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
</tbody>
</table>


Only role groups, users, or USGs that are assigned the Mail Recipient Creation role can create security principals such as Active Directory users. By default, the Organization Management and Recipient Management role groups are assigned this role. Therefore members of these role groups can create security principals.

Only role groups, users, or USGs that are assigned the Security Group Creation and Membership role can create security groups or manage their memberships. By default, only the Organization Management role group is assigned this role. Therefore only members of the Organization Management role group can create or manage the membership of security groups.

You can assign the Mail Recipient Creation role and the Security Group Creation and Membership role to other role groups, users, or USGs if you want other users to be able to create security principals.

To enable the management of existing security principals in Exchange 2013, the Mail Recipients role is assigned to the Organization Management and Recipient Management role groups by default. Only role groups, users, or USGs that are assigned the Mail Recipients role can manage existing security principals. If you want other role groups, users, or USGs to be able to manage existing security principals, you must assign the Mail Recipients role to them.

For more information about how to add roles to role groups, users, or USGs, see the following topics:

  - [Manage role groups](manage-role-groups-exchange-2013-help.md)

  - [Add a role to a user or USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

If you switched to a split permissions model and want to change back to a shared permissions model, see [Configure Exchange 2013 for shared permissions](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md).

Return to top

## Split permissions

If your organization separates Exchange management and Active Directory management, you need to configure Exchange to support the split permissions model. When configured correctly, only the administrators who you want to create security principals, such as Active Directory administrators, will be able to do so and only Exchange administrators will be able to modify the Exchange attributes on existing security principals. This splitting of permissions also falls roughly along the lines of the domain and configuration partitions in Active Directory. Partitions are also called naming contexts. The domain partition stores the users, groups, and other objects for a specific domain. The configuration partition stores the forest-wide configuration information for the services that used Active Directory, such as Exchange. Data that's stored in the domain partition is typically managed by Active Directory administrators, although objects may contain Exchange-specific attributes that can be managed by Exchange administrators. Data that's stored in the configuration partition is managed by the administrators for each respective service that stores data in this partition. For Exchange, this is typically Exchange administrators.

Exchange 2013 supports the two following types of split permissions:

  - **RBAC split permissions**   Permissions to create security principals in the Active Directory domain partition are controlled by RBAC. Only Exchange servers, services, and those who are members of the appropriate role groups can create security principals.

  - **Active Directory split permissions**   Permissions to create security principals in the Active Directory domain partition are completely removed from any Exchange user, service, or server. No option is provided in RBAC to create security principals. Creation of security principals in Active Directory must be performed using Active Directory management tools.
    

    > [!IMPORTANT]
    > Although Active Directory split permissions can be enabled or disabled by running Setup on a computer that has Exchange 2013 installed, Active Directory split permissions configuration applies to both Exchange 2013 and Exchange 2010 servers. It doesn't, however, have any impact on Microsoft Exchange Server 2007 servers.



If your organization chooses to use a split permissions model instead of shared permissions, we recommend that you use the RBAC split permissions model. The RBAC split permissions model provides significantly more flexibility while providing the nearly same administration separation as Active Directory split permissions, with the exception that Exchange servers and services can create security principals in the RBAC split permissions model.

You're asked whether you want to enable Active Directory split permissions during Setup. If you choose to enable Active Directory split permissions, you can only change to shared permissions or RBAC split permissions by rerunning Setup and disabling Active Directory split permissions. This choice applies to all Exchange 2010 and Exchange 2013 servers in the organization.

The following sections describe RBAC and Active Directory split permissions in more detail.

Return to top

## RBAC split permissions

The RBAC security model modifies the default management role assignments to separate who can create security principals in the Active Directory domain partition from those who administer the Exchange organization data in the Active Directory configuration partition. Security principals, such as users with mailboxes and distribution groups, can be created by administrators who are members of the Mail Recipient Creation and Security Group Creation and Membership roles. These permissions remain separate from the permissions required to create security principals outside of the Exchange management tools. Exchange administrators who aren't assigned the Mail Recipient Creation or Security Group Creation and Membership roles can still modify Exchange-related attributes on security principals. Active Directory administrators also have the option of using the Exchange management tools to create Active Directory security principals.

Exchange servers and the Exchange Trusted Subsystem also have permissions to create security principals in Active Directory on behalf of users and third-party programs that integrate with RBAC.

RBAC split permissions is a good choice for your organization if the following are true:

  - Your organization doesn't require that security principal creation be performed using only Active Directory management tools and only by users who are assigned specific Active Directory permissions.

  - Your organization allows services, such as Exchange servers, to create security principals.

  - You want to simplify the process required to create mailboxes, mail-enabled users, distribution groups, and role groups by allowing their creation from within the Exchange management tools.

  - You want to manage the membership of distribution groups and role groups within the Exchange management tools.

  - You have third-party programs that require that Exchange servers be able to create security principals on their behalf.

If your organization requires a complete separation of Exchange and Active Directory administration where no Active Directory administration can be performed using Exchange management tools or by Exchange services, see the Active Directory Split Permissions section later in this topic.

Switching from shared permissions to RBAC split permissions is a manual process where you remove the permissions required to create security principals from the role groups that are granted them by default. The following table shows the roles that enable the creation of security principals in Exchange and the management role groups they're assigned to by default.

### Security principal management roles

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Management role</th>
<th>Role group</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Mail Recipient Creation role</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">Security Group Creation and Membership role</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
</tbody>
</table>


By default, members of the Organization Management and Recipient Management role groups can create security principals. You must transfer the ability to create security principals from the built-in role groups to a new role group that you create.

To configure RBAC split permissions, you must do the following:

1.  Disable Active Directory split permissions if it's enabled.

2.  Create a role group, which will contain the Active Directory administrators that will be able to create security principals.

3.  Create regular and delegating role assignments between the Mail Recipient Creation role and the new role group.

4.  Create regular and delegating role assignments between the Security Group Creation and Membership role and the new role group.

5.  Remove the regular and delegating management role assignments between the Mail Recipient Creation role and the Organization Management and Recipient Management role groups.

6.  Remove the regular and delegating role assignments between the Security Group Creation and Membership role and the Organization Management role group.

After doing this, only members of the new role group that you create will be able to create security principals, such as mailboxes. The new group will only be able to create the objects. It won't be able to configure the Exchange attributes on the new object. An Active Directory administrator, who is a member of the new group, will need to create the object, and then an Exchange administrator will need to configure the Exchange attributes on the object. Exchange administrators won't be able to use the following cmdlets:

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Exchange administrators will, however, be able to create and manage Exchange-specific objects, such as transport rules, distribution groups, and so on and manage Exchange-related attributes on any object.

Additionally, the associated features in the EAC and Outlook Web App, such as the New Mailbox Wizard, will also no longer be available or will generate an error if you try to use them.

If you want the new role group to also be able to manage the Exchange attributes on the new object, the Mail Recipients role also needs to be assigned to the new role group.

For more information about configuring a split permissions model, see [Configure Exchange 2013 for split permissions](configure-exchange-2013-for-split-permissions-exchange-2013-help.md).

Return to top

## Active Directory split permissions

With Active Directory split permissions, the creation of security principals in the Active Directory domain partition, such as mailboxes and distribution groups, must be performed using Active Directory management tools. Several changes are made to the permissions granted to the Exchange Trusted Subsystem and Exchange servers to limit what Exchange administrators and servers can do. The following changes in functionality occur when you enable Active Directory split permissions:

  - Creation of mailboxes, mail-enabled users, distribution groups, and other security principals is removed from the Exchange management tools.

  - Adding and removing distribution group members can't be done from the Exchange management tools.

  - All permissions granted to the Exchange Trusted Subsystem and Exchange servers to create security principals are removed.

  - Exchange servers and the Exchange management tools can only modify the Exchange attributes of existing security principals in Active Directory.

For example, to create a mailbox with Active Directory split permissions enabled, a user must first be created using Active Directory tools by a user with the required Active Directory permissions. Then, the user can be mailbox-enabled using the Exchange management tools. Only the Exchange-related attributes of the mailbox can be modified by Exchange administrators using the Exchange management tools.

Active Directory split permissions is a good choice for your organization if the following are true:

  - Your organization requires that security principals be created using only the Active Directory management tools or only by users who are granted specific permissions in Active Directory.

  - You want to completely separate the ability to create security principals from those who manage the Exchange organization.

  - You want to perform all distribution group management, including creation of distribution groups and adding and removing members of those groups, using Active Directory management tools.

  - You don't want Exchange servers, or third-party programs that use Exchange on their behalf, to create security principals.


> [!IMPORTANT]
> Switching to Active Directory split permissions is a choice that you can make when you install Exchange 2013 either by using the Setup wizard or by using the <EM>ActiveDirectorySplitPermissions</EM> parameter while running <CODE>setup.exe</CODE> from the command line. You can also enable or disable Active Directory split permissions after you've installed Exchange 2013 by rerunning <CODE>setup.exe</CODE> from the command line. To enable Active Directory split permissions, set the <EM>ActiveDirectorySplitPermissions</EM> parameter to <CODE>true</CODE>. To disable it, set it to <CODE>false</CODE>. You must always specify the <EM>PrepareAD</EM> switch along with the <EM>ActiveDirectorySplitPermissions</EM> parameter.<BR>If you have multiple domains within the same forest, you must also either specify the <EM>PrepareAllDomains</EM> switch when you apply Active Directory split permissions or run setup with the <EM>PrepareDomain</EM> switch in each domain. If you choose to run setup with the <EM>PrepareDomain</EM> switch in each domain rather than use the <EM>PrepareAllDomains</EM> switch, you must prepare every domain that contains Exchange servers, mail-enabled objects, or global catalog servers that could be accessed by an Exchange server.




> [!IMPORTANT]
> You can't enable Active Directory split permissions if you've installed Exchange 2010 or Exchange 2013 on a domain controller.<BR>After you enable or disable Active Directory split permissions, we recommend that you restart the Exchange 2010 and Exchange 2013 servers in your organization to force them to pick up the new Active Directory access token with the updated permissions.



Exchange 2013 achieves Active Directory split permissions by removing permissions and membership from the Exchange Windows Permissions security group. This security group, in shared permissions and RBAC split permissions, is given permissions to many non-Exchange objects and attributes throughout Active Directory. By removing the permissions and membership to this security group, Exchange administrators and services are prevented from creating or modifying those non-Exchange Active Directory objects.

For a list of changes that occur to the Exchange Windows Permissions security group and other Exchange components when you enable or disable Active Directory split permissions, see the following table.


> [!NOTE]
> Role assignments to role groups that enable Exchange administrators to create security principals are removed when Active Directory split permissions is enabled. This is done to remove access to cmdlets that would otherwise generate an error when they're run because they don't have permissions to create the associated Active Directory object.



### Active Directory split permissions changes

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Action</th>
<th>Changes made by Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Enable Active Directory split permissions during first Exchange 2013 server installation</p></td>
<td><p>The following happens when you enable Active Directory split permissions either through the Setup wizard or by running <code>setup.exe</code> with the <code>/PrepareAD</code> and <code>/ActiveDirectorySplitPermissions:true</code> parameters:</p>
<ul>
<li><p>An organizational unit (OU) called <strong>Microsoft Exchange Protected Groups</strong> is created.</p></li>
<li><p>The <strong>Exchange Windows Permissions</strong> security group is created in the <strong>Microsoft Exchange Protected Groups</strong> OU.</p></li>
<li><p>The <strong>Exchange Trusted Subsystem</strong> security group isn't added to the <strong>Exchange Windows Permissions</strong> security group.</p></li>
<li><p>Creation of non-delegating management role assignments to management roles with the following management role types is skipped:</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>Access control entries (ACEs) that would have been assigned to the <strong>Exchange Windows Permissions</strong> security group aren't added to the Active Directory domain object.</p></li>
</ul>
<p>If you run setup with the <em>PrepareAllDomains</em> or <em>PrepareDomain</em> switch, the following happens in each child domain that's prepared:</p>
<ul>
<li><p>All ACEs assigned to the <strong>Exchange Windows Permissions</strong> security group are removed from the domain object.</p></li>
<li><p>ACEs are set in each domain with the exception of any ACEs assigned to the <strong>Exchange Windows Permissions</strong> security group.</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>Switch from shared permissions or RBAC split permissions to Active Directory split permissions</p></td>
<td><p>The following happens when you run the <code>setup.exe</code> command with the <code>/PrepareAD</code> and <code>/ActiveDirectorySplitPermissions:true</code> parameters:</p>
<ul>
<li><p>An OU called <strong>Microsoft Exchange Protected Groups</strong> is created.</p></li>
<li><p>The <strong>Exchange Windows Permissions</strong> security group is moved to the <strong>Microsoft Exchange Protected</strong> Groups OU.</p></li>
<li><p>The <strong>Exchange Trusted Subsystem</strong> security group is removed from the <strong>Exchange Windows Permissions</strong> security group.</p></li>
<li><p>Any non-delegating role assignments to management roles with the following role types are removed:</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>All ACEs assigned to the <strong>Exchange Windows Permissions</strong> security group are removed from the domain object.</p></li>
</ul>
<p>If you run setup with either the <em>PrepareAllDomains</em> or <em>PrepareDomain</em> switch, the following happens in each child domain that's prepared:</p>
<ul>
<li><p>All ACEs assigned to the <strong>Exchange Windows Permissions</strong> security group are removed from the domain object.</p></li>
<li><p>ACEs are set in each domain with the exception of any ACEs assigned to the <strong>Exchange Windows Permissions</strong> security group.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Switch from Active Directory split permissions to shared permissions or RBAC split permissions</p></td>
<td><p>The following happens when you run the <code>setup.exe</code> command with the <code>/PrepareAD</code> and <code>/ActiveDirectorySplitPermissions:false</code> parameters:</p>
<ul>
<li><p>The <strong>Exchange Windows Permissions</strong> security group is moved to the <strong>Microsoft Exchange Security Groups</strong> OU.</p></li>
<li><p>The <strong>Microsoft Exchange Protected Groups</strong> OU is removed.</p></li>
<li><p>The <strong>Exchange Trusted Subsystems</strong> security group is added to the <strong>Exchange Windows Permissions</strong> security group.</p></li>
<li><p>ACEs are added to the domain object for the <strong>Exchange Windows Permissions</strong> security group.</p></li>
</ul>
<p>If you run setup with either the <em>PrepareAllDomains</em> or <em>PrepareDomain</em> switch, the following happens in each child domain that's prepared:</p>
<ul>
<li><p>ACEs are added to the domain object for the <strong>Exchange Windows Permissions</strong> security group.</p></li>
<li><p>ACEs are set in each domain including ACEs assigned to the <strong>Exchange Windows Permissions</strong> security group.</p></li>
</ul>
<p>Role assignments to the Mail Recipient Creation and Security Group Creation and Membership roles aren't automatically created when switching from Active Directory split to shared permissions. If delegating role assignments were customized prior to Active Directory split permissions being enabled, those customizations are left intact. To create role assignments between these roles and the Organization Management role group, see <a href="configure-exchange-2013-for-shared-permissions-exchange-2013-help.md">Configure Exchange 2013 for shared permissions</a>.</p></td>
</tr>
</tbody>
</table>


After you enable Active Directory split permissions, the following cmdlets are no longer available:

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

After you enable Active Directory split permissions, the following cmdlets are accessible but you cannot use them to create distribution groups or modify distribution group membership:

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Update-DistributionGroupMember**

Some cmdlets, although still available, may offer only limited functionality when used with Active Directory split permissions. This is because they may allow you to configure recipient objects that are in the domain Active Directory partition and Exchange configuration objects that are in the configuration Active Directory partition. They may also allow you to configure Exchange-related attributes on objects stored in the domain partition. Attempts to use the cmdlets to create objects, or modify non-Exchange-related attributes on objects, in the domain partition will result in an error. For example, the **Add-ADPermission** cmdlet will return an error if you attempt to add permissions to a mailbox. However, the **Add-ADPermission** cmdlet will succeed if you configure permissions on a Receive connector. This is because a mailbox is stored in the domain partition while Receive connectors are stored in the configuration partition.

Additionally, the associated features in the Exchange Administration Center and Outlook Web App, such as the New Mailbox wizard, will also no longer be available or will generate an error if you try to use them.

Exchange administrators will, however, be able to create and manage Exchange-specific objects, such as transport rules, and so on.

For more information about configuring an Active Directory split permissions model, see [Configure Exchange 2013 for split permissions](configure-exchange-2013-for-split-permissions-exchange-2013-help.md).

Return to top

