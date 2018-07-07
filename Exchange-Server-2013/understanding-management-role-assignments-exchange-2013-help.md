---
title: 'Understanding management role assignments: Exchange 2013 Help'
TOCTitle: Understanding management role assignments
ms:assetid: 1dc33dd6-52fb-4852-a5ce-027bc73e1d8f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd335131(v=EXCHG.150)
ms:contentKeyID: 49289190
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Understanding management role assignments

 

_**Applies to:** Exchange Online, Exchange Server 2013_


A *management role assignment*, which is part of the Role Based Access Control (RBAC) permissions model in Microsoft Exchange Server 2013, is the link between a management role and a role assignee. A *role assignee* is a role group, role assignment policy, user, or universal security group (USG). A role must be assigned to a role assignee for it to take effect. For more information about RBAC, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).


> [!NOTE]
> This topic focuses on advanced RBAC functionality. If you want to manage basic Exchange 2013 permissions, such as using the Exchange admin center (EAC) to add and remove members to and from role groups, create and modify role groups, or create and modify role assignment policies, see <A href="permissions-exchange-2013-help.md">Permissions</A>.



This topic discusses the assignment of roles to role groups and role assignment policies and direct role assignment to users and USGs. It doesn't talk about assignment of role groups or role assignment policies to users. For more information about role groups and role assignment policies, which are the recommended way to assign permissions to users, see the following topics:

  - [Understanding management role groups](understanding-management-role-groups-exchange-2013-help.md)

  - [Understanding management role assignment policies](understanding-management-role-assignment-policies-exchange-2013-help.md)

You can create the following types of role assignments, which are explained in detail later in this topic:

  - Regular and delegating role assignments

  - Exclusive role assignments

## Managing role assignments

When you change role assignments, the changes you make will probably be between role groups and role assignment policies. By adding, removing, or modifying role assignments to or from these role assignees, you can control what permissions are given to your administrators and users, in effect turning on and off management of related features.

You might also want to assign roles directly to users or USGs. This is a more advanced task that enables you to define at a granular level what permissions your users are given. Although this provides you with flexibility, it also increases the complexity of your permissions model. For example, if the user changes jobs, you might need to manually reassign the roles assigned to that user to another user. This is why we recommend that you use role groups and role assignment policies to give permissions to your users. You can assign the roles to a role group or role assignment policy, and then just add or remove members of the role group, or change role assignment policies as needed.

You can add, remove, and enable role assignments, modify the management scope on an existing role assignment, and move role assignments to other role assignees. The process of assigning roles to role groups, role assignment policies, users, and USGs is largely the same for each role assignee. The following are the only exceptions:

  - Role assignment policies can only be assigned end-user management roles.

  - Role assignment policies can't be assigned delegating role assignments.

  - You can't specify a management scope when creating a role assignment to role assignment policies.

For more information about managing role assignments, see the following topics:

  - Role groups:
    
      - [Manage role groups](manage-role-groups-exchange-2013-help.md)

  - Role assignment policies:
    
      - [Manage role assignment policies](manage-role-assignment-policies-exchange-2013-help.md)
    
      - [Change a role assignment](change-a-role-assignment-exchange-2013-help.md)

  - Users and USGs:
    
      - [Add a role to a user or USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)
    
      - [Remove a role from a user or USG](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)
    
      - [Change a role assignment](change-a-role-assignment-exchange-2013-help.md)
    
      - [Change a role scope](change-a-role-scope-exchange-2013-help.md)
    
      - [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md)

## Regular and delegating role assignments

Regular role assignments enable the role assignee to access the management role entries made available by the associated management role. If multiple management roles are assigned to a role assignee, the management role entries from each management role are aggregated and applied. This means that if a role assignee is assigned the Transport Rules and Journaling roles, the roles are combined, and all the associated management role entries are given to the role assignee. If the role assignee is a role group or role assignment policy, the permissions provided by the roles are then given to the users assigned to the role group or role assignment policy. For more information about management roles and role entries, see [Understanding management roles](understanding-management-roles-exchange-2013-help.md).

Delegating role assignments doesn't give access to manage features. Delegating role assignments gives a role assignee the ability to assign the specified role to other role assignees. If the role assignee is a role group, any member of the role group can assign the role to another role assignee. By default, only the Organization Management role group has the ability to assign roles to other role assignees. Only the user that installed Exchange 2013 is a member of the Organization Management role group by default. You can, however, add other users to this role group as needed, or create other role groups and assign delegating role assignments to those groups.


> [!NOTE]
> Delegating role assignments enables role assignees to delegate management roles to other role assignees. This doesn't enable users to delegate role groups. For more information about role group delegation, see <A href="understanding-management-role-groups-exchange-2013-help.md">Understanding management role groups</A>.



If you want a user to be able to manage a feature and assign the role that gives permissions to use the feature to other users, assign the following:

1.  A regular role assignment for each management role that grants access to the features that need to be managed.

2.  A delegating role assignment for each management role that you allow to be assigned to other role assignees.

The regular and delegating role assignments for a role assignee don't need to be identical. For example, a user is a member of a role group assigned the Transport Rules role using a regular role assignment. This enables the user to manage the Transport Rules feature. However the user isn't assigned a delegating role assignment for the Transport Rules role so the user can't assign this role to other users. However, the user is a member of a role group assigned the Journaling management role using a delegating role assignment. The role group the user is a member of doesn't have a regular role assignment for the Journaling role but because it has a delegating role assignment, the user can assign the role to other role assignees.

## Management scopes

When you create either a regular or delegating management role assignment, you have the option of creating the assignment with a management scope to limit the objects that the user can manipulate. You can create recipient scopes or configuration scopes. Recipient scopes enable you to control who can manipulate mailboxes, mail users, distribution groups, and so on. Configuration scopes enable you to control who can manipulate servers and databases.

Recipient and configuration scopes enable you to segment the management of server, database or recipient objects in your organization. For example, a recipient scope can be added to a role assignment so that administrators in Vancouver can only manage recipients in the same office. A server configuration scope could be added to a different role assignment so that administrators in Sydney can only manage servers in their Active Directory site.

Scopes enable permissions to be assigned to groups of users and enable you to direct where those administrators can perform their administration. This enables you to create a permissions model that maps to your geographic or organizational boundaries.

You can create an assignment with a predefined scope, or you can add a custom scope to the assignment. Predefined scopes, such as limiting a user to only his or her mailbox or distribution groups, can be applied using options available on the assignment itself. Alternatively, you can create a custom recipient or configuration scope, and then add that scope to the role assignment. Custom scopes give you more granularity over which objects are included in the scope.

You can't specify predefined and custom scopes on the same assignment. You also can't mix exclusive and regular scopes on the same assignment.

Each role assignment can only have one recipient scope and one configuration scope. If you want to apply more than one recipient scope, or one configuration scope, to a role assignee for the same management role, you must create multiple role assignments.

With neither a custom or predefined scope, role assignments are limited to the recipient and configuration scopes that are defined on the role itself. These scopes are called implicit scopes. Any role assignment that doesn't have a predefined or custom scope inherits the implicit scopes from the role it's associated with.

For more information about scopes, see [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md).

## Exclusive role assignments

Exclusive role assignments are created when you associate an exclusive scope with a role assignment. Exclusive scopes work like regular scopes and enable role assignees to manage recipients that match the exclusive scope. However, unlike regular scopes, all other role assignees are denied the ability to manage the recipient, even if the recipient matches scopes applied to their role assignments. This can be useful when you want to limit who can manage a recipient to a few administrators. Only those specific administrators can manage the recipient, and all other administrators are denied access.

For example, consider the following:

  - John is an executive at Contoso. His mailbox matches an exclusive scope called VIP Users, which is associated with the VIP Restricted exclusive assignment.

  - John's mailbox is also included in a regular scope called Redmond Users, which is associated with the Redmond Administration regular assignment.

  - Bill is an administrator who is associated with the VIP Restricted exclusive assignment.

  - Chris is an administrator who is associated with the Redmond Administration regular assignment.

Because John's mailbox matches the VIP Users exclusive scope, only Bill can manage his mailbox. Even though John's mailbox also matches the Redmond Users regular scope, Chris isn't associated with the VIP Restricted exclusive assignment. Therefore, Exchange denies Chris the ability to manage John's mailbox. For Chris to manage John's mailbox, Chris needs to be assigned an exclusive assignment that has an exclusive scope that matches John's mailbox.

For more information, see [Understanding exclusive scopes](understanding-exclusive-scopes-exchange-2013-help.md).

