---
title: 'Understanding multiple-forest permissions: Exchange 2013 Help'
TOCTitle: Understanding multiple-forest permissions
ms:assetid: 8241033f-e201-4799-b17c-4f120c6e6445
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd298099(v=EXCHG.150)
ms:contentKeyID: 49289329
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Understanding multiple-forest permissions

 

_**Applies to:** Exchange Server 2013_


Many organizations deploy multiple forests to create security boundaries within their organizations. Using multiple forests helps administrators to define these security boundaries to better match their requirements, whether that's ensuring the fewest number of people have access to resources, or segmenting divisions within an organization.

Microsoft Exchange Server 2013 supports two types of multiple forest topologies:

  - **Cross-forest**   Cross-forest topologies can have multiple forests, each with their own installation of Exchange.

  - **Resource forest**   Resource forest topologies have an Exchange forest and one or more accounts forests.

For the purposes of this topic, the forest that contains the universal security groups (USGs) and users outside of the forest where Exchange 2013 is installed, whether it's an accounts forest or other resource forest, is called a foreign forest.

Configuration of permissions in a multiple forest topology relies on the correct configuration of forest trusts and global address list (GAL) synchronization for the creation of linked mailboxes. The Exchange 2013 forest must trust the foreign forest that contains the USGs associated with linked role groups and users associated with linked mailboxes.

Exchange 2013 uses a Role Based Access Control (RBAC) permissions model. The management role groups that administrators are members of, and the management role assignment policies that end users are assigned, determine what each administrator and end user can do. To understand multiple-forest permissions, you need to be familiar with RBAC. For more information about RBAC, role groups, and role assignment policies, see the following topics:

  - [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md)

  - [Understanding management role groups](understanding-management-role-groups-exchange-2013-help.md)

  - [Understanding management role assignment policies](understanding-management-role-assignment-policies-exchange-2013-help.md)

Looking for management tasks related to managing permissions? See [Permissions](permissions-exchange-2013-help.md).

**Contents**

Permissions in a Multiple Forest Topology

Cross-Boundary Permissions

Configure Cross-Boundary Permissions

## Permissions in a multiple forest topology

RBAC applies permissions to all Exchange objects within a single forest and the RBAC configuration in each forest is configured independently of all other forests. When you create a role group in one forest, that role group doesn't exist in any other forest and the permissions granted by that role group apply only to the forest in which it was created. For example, a member of a role group that grants permissions to create a mailbox can create a mailbox only in the forest that contains that role group.

If you have multiple Exchange forests and want to configure permissions identically within each forest, you must apply the same configuration explicitly in each forest. For example, if you have two Exchange 2013 forests and want to create a Compliance Management role group to manage permissions for your legal department, you must do the following:

  - In each forest, create a role group named Compliance Management. If your administrators are in a separate foreign forest from either Exchange forest, create both role groups as linked role groups. For more information about role groups, see the Cross-Boundary Permissions section.

  - In each forest, create role assignments between the new role groups and the roles that you want to use.

  - As part of the new role assignments, optionally add management scopes that encompass the server and recipient objects within each forest.

  - If you created the role groups as linked role groups, add members to the associated USG in the foreign forest.

The following figure shows how the role groups configured within Exchange 2013 forests are bound to their respective forests. The Organization Management role group in Exchange 2013 forest A grants permissions only to manage the mailboxes and servers that are within that forest. Likewise, the role groups in Exchange 2013 forest B grant permissions only to the mailboxes and servers within that forest.

The figure also shows that the Custom role group A is created in each forest. Even though they were created with the same name, each is its own separate entity. In fact, as the figure shows, each can be assigned different management roles in their respective forests. Custom role group A in Exchange 2013 forest A is assigned the Mailbox Search and Message Tracking roles while Custom role group A in Exchange 2013 forest B is assigned the Mailbox Search and Retention Management roles.

Finally, management scopes created in each forest are also bound by the forest. Server scopes created in each forest can only contain the servers that are members of that forest. Server scope A can contain only servers within Exchange 2013 forest A while Server scope B can contain only servers that are within Exchange 2013 forest B. Similarly, the recipient scope in Exchange 2013 forest B can only contain mailboxes that are within Exchange 2013 forest B.

**RBAC and forest scope boundary relationship**

![RBAC and forest boundary scope relationships](images/Dd298099.220da7c3-cbb8-42ac-9d58-084d996bf837(EXCHG.150).gif "RBAC and forest boundary scope relationships")

## Cross-boundary permissions

The permissions granted by RBAC only allow users to view or modify Exchange objects within a specific forest. However, you can grant permissions to view and modify Exchange objects in a forest to users outside of that forest. By using cross-boundary permissions, you can centralize Exchange management accounts in a single forest rather than having to authenticate against each individual forest to perform tasks.


> [!NOTE]
> The permissions that are granted to a user outside of an Exchange forest still apply only to that specific Exchange forest. For example, if a user in a foreign forest is a member of the Organization Management linked role group that's located in ForestA, the user can manage only the Exchange objects contained within ForestA. A user must be made a member of linked role groups in each Exchange forest to be granted permissions to manage each forest.



Cross-boundary permissions also enable you to apply role assignment policies to the mailboxes of users who have mailboxes in an Exchange forest, but have user accounts that reside in an accounts forest. Exchange 2013 supports cross-boundary permission using linked role groups and linked mailboxes, which are discussed in the following sections.

## Administrative permissions

Administrative permissions are granted cross forest boundaries by the use of linked role groups and linked mailboxes.

A linked role group is created in the Exchange 2013 organization and is linked to a USG across the forest boundary in the foreign forest. The USG the linked role group is linked to can be any of the following:

  - A dedicated USG for the specific use of the linked role group

  - A USG that's linked to by linked role groups in multiple Exchange 2013 forests

  - A role group USG in another Exchange 2013 forest

  - A USG associated with an Exchange Server 2007 administrative role or Exchange 2010 role group

The USG that a linked role group is linked to must be in another forest. You can't link a linked role group to a USG in the same forest.

The following figure shows that USGs in an accounts forest can be associated with role groups in one or more Exchange 2013 resource forests. The members of the USGs in the accounts forest effectively become members of the role groups through the USGs.

**Linked role groups associated with USGs in a separate forest**

![Linked role group and USG relationships](images/Dd298099.23f245e8-b80f-4082-8628-ee6701259be6(EXCHG.150).gif "Linked role group and USG relationships")

When you create a linked role group, you assign roles to the linked role group in the Exchange 2013 forest. The assignments that associate the roles to the linked role group can include management scopes, if necessary. These scopes are confined to the forest in which the linked role group is created.

Membership of the linked role group is managed by adding and removing members to and from the USG in the foreign forest. When you add members to this USG, they are granted the permissions assigned to the linked role group in the Exchange 2013 forest. If you've linked multiple linked role groups with the same USG, the members of that USG are granted the permissions assigned to each linked role group in each Exchange 2013 forest.

You can't manage the membership of a linked role group from the Exchange 2013 forest.

A second method to assign administrative permissions across forest boundaries is through the use of linked mailboxes. For users in an accounts forest to use an Exchange 2013 deployment in a separate Exchange 2013 resource forest, you must configure linked mailboxes for each user. Linked mailboxes can be added as members to role groups within the Exchange 2013 forest. When a linked mailbox becomes a member of a role group, that linked mailbox, and in turn the user in the accounts forest associated with the linked mailbox, is granted the permissions provided by the role group.

The following figure shows the relationship between users in an accounts forest, the linked mailboxes associated with them, and the role groups in which they're members.

**Users in an accounts forest associated with linked mailboxes that are members of role groups**

![Role group and linked mailbox relationships](images/Dd298099.e59242f6-5c63-4114-90f7-6b6c2478570c(EXCHG.150).gif "Role group and linked mailbox relationships")

Linked role groups and linked mailboxes both have advantages and disadvantages when used to assign administrative permission across forest boundaries. The following table describes some of them.

### Linked role group and linked mailbox advantages and disadvantages

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Linked role groups or linked mailboxes</th>
<th>Advantage</th>
<th>Disadvantage</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Linked role groups</p></td>
<td><p>You can associate multiple linked role groups from multiple Exchange 2013 forests to a single USG in an accounts forest or other Exchange resource forest. This enables you to administer complex Exchange forest topologies through a small set of USGs in a single forest.</p></td>
<td><p>A regular role group can't be converted to a linked role group. You must manually create linked role groups to replace each regular role group that has the permissions you want to grant across a forest boundary. For more information, see Configure cross-boundary permissions.</p></td>
</tr>
<tr class="even">
<td><p>Linked mailboxes</p></td>
<td><p>Linked mailboxes allow you to use the existing role groups within the Exchange forest. Linked mailboxes are added as members to the existing role groups just like regular mailboxes, USGs, and users in the same Exchange forest.</p></td>
<td><p>If you grant permissions in multiple Exchange 2013 forests using linked mailboxes linked to a single user in an accounts forest, you must modify the role group membership in each Exchange 2013 forest if you want to modify the permissions granted to the user.</p></td>
</tr>
</tbody>
</table>


We recommend that you use linked role groups to grant permission across forest boundaries if you plan on having multiple Exchange resource forests.

## End-user permissions

End-user permissions are assigned to individual mailboxes using role assignment policies. When Exchange 2013 is installed in a resource forest, linked mailboxes are created in the resource forest and are associated with user accounts in the accounts forest.

When a linked mailbox is created, it's assigned to a default role assignment policy just like a regular mailbox. The role assignment policy determines which end-user permissions are granted to the mailbox. These permissions enable users to view and modify settings related to the following, and other, features:

  - End-user profile information

  - End-user voicemail

  - End-user distribution membership and ownership

When a role assignment policy is assigned to a linked mailbox, the user in the accounts forest associated with the linked mailbox is granted permissions to manage the features available to that user. The permissions apply to only the resources in the Exchange forest where the linked mailbox is located. The following figure shows the relationship between the end user in the accounts forest, its associated linked mailbox, and the role assignment policy assigned to the linked mailbox. Additionally, a linked mailbox associated with an administrative user in the accounts forest can be associated with multiple role groups in addition to a role assignment policy.

**Users in an accounts forest associated with linked mailboxes that are each assigned a role assignment policy**

![Role group and assignment policy relationships](images/Dd298099.785b9b35-4292-43ce-917b-117d0174742e(EXCHG.150).gif "Role group and assignment policy relationships")

Return to top

## Configure cross-boundary permissions

To configure cross-boundary permissions in a multiple-forest topology, you must create linked role groups for each of the role groups you want to link to USGs in a foreign forest. This means that you must create a linked role group for each built-in role group. You need to:

1.  Create a USG in the foreign forest for each linked role group to be created. Add members to this USG that you want to grant permissions to.

2.  Create a linked role group for each built-in role group. The following happens when the linked role group is created:
    
      - The same roles that are assigned to the built-in role group are assigned to the new linked role group.
    
      - The linked role group is associated with the USG in the foreign forest.

3.  Create linked role groups for any custom role groups you created.

4.  Optionally assign custom scopes to the new linked role groups.

For detailed information about how to perform these steps, see the following topics:

  - [Create linked role groups that mirror built-in role groups](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)

  - [Manage linked role groups](manage-linked-role-groups-exchange-2013-help.md)

  - [Manage role groups](manage-role-groups-exchange-2013-help.md)

If you need to change the USG that a linked role group is associated with, see [Manage linked role groups](manage-linked-role-groups-exchange-2013-help.md).

When a linked mailbox is created, it's automatically assigned to a role assignment policy. You can change the role assignment policy that's assigned to the linked mailbox or change the role assignment policy that's assigned to mailboxes by default when they're created. For more information, see the following topics:

  - [Change the assignment policy on a mailbox](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

  - [Manage role assignment policies](manage-role-assignment-policies-exchange-2013-help.md)

