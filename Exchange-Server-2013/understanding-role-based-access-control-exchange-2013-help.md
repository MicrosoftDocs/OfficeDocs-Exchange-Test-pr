---
title: 'Understanding Role Based Access Control: Exchange 2013 Help'
TOCTitle: Understanding Role Based Access Control
ms:assetid: fd268867-2ae5-441b-8103-7a7583eb2bbe
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd298183(v=EXCHG.150)
ms:contentKeyID: 49289479
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Understanding Role Based Access Control

 

_**Applies to:** Exchange Online, Exchange Server 2013_


*Role Based Access Control* (RBAC) is the permissions model used in Microsoft Exchange Server 2013. With RBAC, you don't need to modify and manage access control lists (ACLs), which was done in Exchange Server 2007. ACLs created several challenges in Exchange 2007, such as modifying ACLs without causing unintended consequences, maintaining ACL modifications through upgrades, and troubleshooting problems that occurred due to using ACLs in a nonstandard way.

RBAC enables you to control, at both broad and granular levels, what administrators and end-users can do. RBAC also enables you to more closely align the roles you assign users and administrators to the actual roles they hold within your organization. In Exchange 2007, the server permissions model applied only to the administrators who managed the Exchange 2007 infrastructure. In Exchange 2013, RBAC now controls both the administrative tasks that can be performed and the extent to which users can now administer their own mailbox and distribution groups.

RBAC has two primary ways of assigning permissions to users in your organization, depending on whether the user is an administrator or specialist user, or an end-user: management role groups and management role assignment policies. Each method associates users with the permissions they need to perform their jobs. A third, more advanced method, direct user role assignment, can also be used. The following sections in this topic explain RBAC and provide examples of its use.


> [!NOTE]
> This topic focuses on advanced RBAC functionality. If you want to manage basic Exchange 2013 permissions, such as using the Exchange admin center (EAC) to add and remove members to and from role groups, create and modify role groups, or create and modify role assignment policies, see <A href="permissions-exchange-2013-help.md">Permissions</A>.



**Contents**

Management role groups

Management role assignment policies

Direct user role assignment

Summary and examples

For more information

## Management role groups

*Management role groups* associate management roles to a group of administrators or specialist users. Administrators manage a broad Exchange organization or recipient configuration. Specialist users manage the specific features of Exchange, such as compliance. Or they may have limited management abilities, such as Help desk members, but aren't given broad administrative rights. Role groups typically associate administrative management roles that enable administrators and specialist users to manage the configuration of their organization and recipients. For example, whether administrators can manage recipients or use mailbox discovery features is controlled using role groups.

Adding or removing users to or from role groups is how you most often assign permissions to administrators or specialist users. For more information, see [Understanding management role groups](understanding-management-role-groups-exchange-2013-help.md).

Role groups consist of the following components that define what administrators and specialist users can do:

  - **Management role group**   The *management role group* is a special universal security group (USG) that contains mailboxes, users, USGs, and other role groups that are members of the role group. This is where you add and remove members, and it's also what management roles are assigned to. The combination of all the roles on a role group defines everything that users added to a role group can manage in the Exchange organization.

  - **Management role**   A *management role* is a container for a grouping of management role entries. Roles are used to define the specific tasks that can be performed by the members of a role group that's assigned the role. A *management role entry* is a cmdlet, script, or special permission that enables each specific task in a role to be performed. For more information, see [Understanding management roles](understanding-management-roles-exchange-2013-help.md).

  - **Management role assignment**   A *management role assignment* links a role and a role group. Assigning a role to a role group grants members of the role group the ability to use the cmdlets and parameters defined in the role. Role assignments can use management scopes to control where the assignment can be used. For more information, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

  - **Management role scope**   A *management role scope* is the scope of influence or impact on a role assignment. When a role is assigned with a scope to a role group, the management scope targets specifically what objects that assignment is allowed to manage. The assignment, and its scope, are then given to the members of the role group, and restrict what those members can manage. A scope can consist of a list of servers or databases, organizational units (OUs), or filters on server, database or recipient objects. For more information, see [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md).

When you add a user to a role group, the user is given all of the roles assigned to the role group. If scopes are applied to any of the role assignments between the role group and the roles, those scopes control what server configuration or recipients the user can manage.

If you want to change what roles are assigned to role groups, you need to change the role assignments that link the role groups to roles. Unless the assignments built into Exchange 2013 don't suit your needs, you won't have to change these assignments. For more information, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

For more information about role groups, see [Understanding management role groups](understanding-management-role-groups-exchange-2013-help.md).

## Management role assignment policies

Management role assignment policies associate end-user management roles to users. Role assignment policies consist of roles that control what a user can do with his or her mailbox or distribution groups. These roles don't allow management of features that aren't directly associated with the user. When you create a role assignment policy, you define everything a user can do with his or her mailbox. For example, a role assignment policy may allow a user to set the display name, set up voice mail, and configure Inbox rules. Another role assignment policy might allow a user to change the address, use text messaging, and set up distribution groups. Every user with an Exchange 2013 mailbox, including administrators, is given a role assignment policy by default. You can decide which role assignment policy should be assigned by default, choose what the default role assignment policy should include, override the default for certain mailboxes, or not assign role assignment policies by default at all.

Assigning a user to an assignment policy is how you most often manage permissions for users to manage their own mailbox and distribution group options. For more information, see [Understanding management role assignment policies](understanding-management-role-assignment-policies-exchange-2013-help.md).

Role assignment policies consist of the following components that define what users can do with their own mailboxes. Notice that some of the same components also apply to role groups. When used with role assignment policies, these components are limited to enable users to manage only their own mailbox:

  - **Management role assignment policy**   The *management role assignment policy* is a special object in Exchange 2013. Users are associated with the role assignment policy when their mailboxes are created or if you change the role assignment policy on a mailbox. This is also what you assign end-user management roles to. The combination of all the roles on a role assignment policy defines everything that the user can manage on his or her mailbox or distribution groups.

  - **Management role**   A *management role* is a container for a grouping of management role entries. Roles are used to define the specific tasks that a user can do with his or her mailbox or distribution groups. A *management role entry* is a cmdlet, script or special permission that enables each specific task in a management role to be performed. You can only use end-user roles with role assignment policies. For more information, see [Understanding management roles](understanding-management-roles-exchange-2013-help.md).

  - **Management role assignment**   A *management role assignment* is the link between a role and a role assignment policy. Assigning a role to a role assignment policy grants the ability to use the cmdlets and parameters defined in the role. When you create a role assignment between a role assignment policy and a role, you can't specify any scope. The scope applied by the assignment is either `Self` or `MyGAL`. All role assignments are scoped to the user's mailbox or distribution groups. For more information, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

If you want to change what roles are assigned to role assignment policies, you need to change the role assignments that link the role assignment policies to roles. Unless the assignments built into Exchange 2013 don't suit your needs, you won't have to change these assignments. For more information, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

For more information, see [Understanding management role assignment policies](understanding-management-role-assignment-policies-exchange-2013-help.md).

## Direct user role assignment

*Direct role assignment* is an advanced method for assigning management roles directly to a user or USG without using a role group or role assignment policy. Direct role assignments can be useful when you need to provide a granular set of permissions to a specific user and no others. However, using direct role assignments can significantly increase the complexity of your permissions model. If a user changes jobs or leaves the company, you need to manually remove the assignments and add them to the new employee. We recommend that you use role groups to assign permissions to administrators and specialist users, and role assignment policies to assign permissions to users.

For more information about direct user assignment, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

## Summary and examples

The following figure shows the components in RBAC and how they fit together:

  - Role groups:
    
      - One or more administrators can be members of a role group. They can also be members of more than one role group.
    
      - The role group is assigned one or more role assignments. These link the role group with one or more administrative roles that define what tasks can be performed.
    
      - The role assignments can contain management scopes that define where the users of the role group can perform actions. The scopes determine where the users of the role group can modify configuration.

  - Role assignment policies:
    
      - One or more users can be associated with a role assignment policy.
    
      - The role assignment policy is assigned one or more role assignments. These link the role assignment policy with one or more end-user roles. The end-user roles define what the user can configure on his or her mailbox.
    
      - The role assignments between role assignment policies and roles have built-in scopes that restrict the scope of assignments to the user's own mailbox or distribution groups.

  - Direct role assignment (advanced):
    
      - A role assignment can be created directly between a user or USG and one or more roles. The role defines what tasks the user or USG can perform.
    
      - The role assignments can contain management scopes that define where the user or USG can perform actions. The scopes determine where the user or USG can modify configuration.

**RBAC overview**

![RBAC component relationships](images/Dd298183.1dee60cc-1d58-4d36-b34e-639f091e7a56(EXCHG.150).jpg "RBAC component relationships")

As shown in the preceding figure, many components in RBAC are related to each other. It's how each component is put together that defines the permissions applied to each administrator or user. The following examples provide some additional context about how role groups and role assignment policies are used in an organization.

## Jane the Administrator

Jane is an administrator for the medium-size company, Contoso. She's responsible for managing the company's recipients in their Vancouver office. When the permissions model for Contoso was created, Jane was made a member of the Recipient Management - Vancouver custom role group. The Recipient Management - Vancouver custom role group most closely matches her job's duties, which include creating and removing recipients, such as mailboxes and contacts, managing distribution group membership and mailbox properties, and similar tasks.

In addition to the Recipient Management - Vancouver custom role group, Jane also needs a role assignment policy to manage her own mailbox's configuration settings. The organization administrators have decided that all users, except for senior management, receive the same permissions when they manage their own mailboxes. They can configure their voice mail, set up retention policies and change their address information. The default role assignment policy provided with Exchange 2013 now reflects these requirements.


> [!NOTE]
> You may have noticed that because Jane is a member of the Recipient Management - Vancouver custom role group, that should give her permissions to manage her own mailbox. This is true; however, the role group doesn't provide her all of the permissions necessary to manage all of the features of her mailbox. The permissions needed to manage voice mail and retention policy settings aren't included in her role group. Those are provided only by the default role assignment policy assigned to her.



To allow for this, consider the role group, which provides Jane's administrative permissions over the recipients in Vancouver:

1.  A custom role group called Recipient Management - Vancouver was created. When it was created, the following occurred:
    
    1.  The role group was assigned all of the same management roles that are also assigned to the Recipient Management built-in role group. This gives users added to the Recipient Management - Vancouver custom role group the same permissions as those users added to the Recipient Management role group. However, the following steps limit where they can use those permissions.
    
    2.  The Vancouver Recipients custom management scope was created, which matches only recipients who are located in Vancouver. This was done by creating a scope that filters on a user's city or other unique information.
    
    3.  The role group was created with the Vancouver Recipients custom management scope. This means while administrators added to the Recipient Management - Vancouver custom role group have full recipient management permissions, they can only use those permissions against recipients based in Vancouver.
    
    For more information about creating a custom role group, see [Manage role groups](manage-role-groups-exchange-2013-help.md).

2.  Jane is then added as a member of the Recipient Management - Vancouver custom role group.
    
    For more information about adding members to a role group, see [Manage role group members](manage-role-group-members-exchange-2013-help.md).

To give Jane the ability to manage her own mailbox settings, a role assignment policy needs to be configured with the required permissions. The default role assignment policy is used to provide users with the permissions they need to configure their own mailbox. All end-user roles are removed from the default role assignment policy, except for: `MyBaseOptions`, `MyContactInformation`, `MyVoicemail`, and `MyRetentionPolicies`. `MyBaseOptions` is included because this management role provides the basic user functionality in Outlook Web App, such as Inbox rules, calendar configuration, and other tasks.

Nothing else needs to be done because Jane is already assigned the default role assignment policy. This means that the changes made to that role assignment policy are immediately applied to her mailbox, and any other mailboxes also assigned to the default role assignment policy.

For more information about customizing the default role assignment policy, see [Manage role assignment policies](manage-role-assignment-policies-exchange-2013-help.md).

## Joe the Specialist

Joe works for Contoso, the same company that Jane works for. He's responsible for performing legal discovery, setting the retention policies, and configuring transport rules and journaling for the whole organization. As with Jane, when the permissions model for Contoso was created, Joe was added to the role groups that match his job duties. The Records Management role group provides Joe with the permissions to configure retention policies, journaling, and transport rules. The Discovery Management role group provides him with the ability to perform mailbox searches.

As with Jane, Joe also needs permissions to manage his own mailbox. He is given the same permissions as Jane: He can set up his voice mail and retention policies, and change his address information.

To give Joe the permissions to perform his job duties, Joe is added to the Records Management and Discovery Management role groups. The role groups don't need to be changed in any way because they already provide him with the permissions he needs, and the management scopes applied to them encompass the entire organization.

For more information about adding a user to a role group, see [Manage role group members](manage-role-group-members-exchange-2013-help.md).

Joe's mailbox is also assigned the same default role assignment policy that's applied to Jane's mailbox. This gives him all the permissions he needs to manage the features of his mailbox that he's allowed to manage.

## Isabel the Vice President

Isabel is the Vice President of Marketing at Contoso. Isabel, as part of the senior leadership team of Contoso, is given more permissions than the average user. This includes the permissions she's provided to manage her mailbox, with one exception: Isabel isn't allowed to manage her own retention policies for legal compliance reasons. Isabel can configure her voice mail, change her contact information, change her profile information, create and manage her own distribution groups, and add or remove herself from existing distribution groups owned by others.

So, Isabel is given different permissions on her own mailbox. Most users at Contoso are assigned to the default role assignment policy. However, senior leadership is assigned to the Senior Leadership role assignment policy. The following is done to create the custom role assignment policy:

1.  A custom role assignment policy called Senior Leadership is created. The role assignment policy is assigned the `MyBaseOptions`, `MyContactInformation`, `MyVoicemail`, `MyProfileInformation`, `MyDistributionGroupMembership`, and` MyDistributionGroups` roles. `MyBaseOptions` is included because this role provides the basic user functionality in Outlook Web App, such as Inbox rules, calendar configuration, and other tasks.

2.  Isabel is then manually assigned the Senior Leadership role assignment policy.

Isabel's mailbox now has the permissions provided by the Senior Leadership role assignment policy. Any changes made to this role assignment policy are automatically applied to her mailbox, and any other mailboxes also assigned to the same role assignment policy.

## For more information

[Manage role assignment policies](manage-role-assignment-policies-exchange-2013-help.md)

[Change the assignment policy on a mailbox](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

