---
title: 'Understanding exclusive scopes: Exchange 2013 Help'
TOCTitle: Understanding exclusive scopes
ms:assetid: 32492622-3b01-4e3b-8288-ed39525eea75
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd638110(v=EXCHG.150)
ms:contentKeyID: 49289222
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Understanding exclusive scopes

 

_**Applies to:** Exchange Server 2013_


*Exclusive scopes* are a special type of explicit management scope that can be associated with management role assignments. Exclusive scopes are designed to enable situations where you have a group of highly valuable objects, such as a CEO mailbox, and you want to tightly control who has access to manage those objects.

A role assignment that has an exclusive scope is called an *exclusive role assignment*.

When you create an exclusive scope, only those who are assigned that exclusive scope, or an equivalent exclusive scope, can modify the objects that match the scope. Role assignees who aren't assigned that exclusive scope, or an equivalent, can't modify the objects that match the scope, even if their own roles have scopes that would otherwise include the objects. Exclusive scopes override any other regular scope that isn't exclusive. This behavior is similar to how a deny access control entry (ACE) on an Active Directory access control list (ACL) functions.

An *equivalent exclusive scope* refers to another exclusive scope that matches some of the same objects as another exclusive scope. The scopes don't have to match the same complete set of objects. Both scopes may be able to modify some, or all, of the objects that match them.

## Creating exclusive scopes

Exclusive scopes can be created like any other explicit scope. You can specify a prebuilt relative scope; a recipient, database, or server filter; or a database or server list. Unlike regular scopes, which don't take effect until you associate a scope to a management role assignment, the deny aspect of an exclusive scope takes effect immediately. This means that as soon as an exclusive scope is created, the objects contained within that scope are immediately no longer accessible by any user until the role assignment has been created.

After the assignment has been created, the exclusive scope provides access to those assigned the management role and scope. If another equivalent exclusive scope matches the same objects, the role assignment associated with that exclusive scope is still able to access the objects.

For more information about management scope filters, see [Understanding management role scope filters](understanding-management-role-scope-filters-exchange-2013-help.md).


> [!IMPORTANT]
> Active Directory replication times should be taken into account when making changes to any management role components, including exclusive scopes.



If you have objects contained within more than one exclusive scope, being assigned to any one of the exclusive scopes provides access to the objects. For more information, see Exclusive and regular scope interaction later in this topic.

Exclusive scopes control only the explicit recipient or configuration write scope of a role assignment. The implicit recipient or configuration read scope of the role assigned to a user or group still applies. This means that the following applies:

  - Those assigned a role continue to see objects that match the role's implicit read scope.

  - Those assigned other roles may be able to see objects contained within an exclusive scope, if the read scopes of the other roles include the objects. However, the objects can only be modified by those who are assigned a role associated with the exclusive scope.

Exclusive scopes can only be used with administrative or specialist roles and can't be used with end-user roles. For more information about roles, see [Understanding management roles](understanding-management-roles-exchange-2013-help.md).

## Exclusive and regular scope interaction

The figure at the end of this section illustrates how exclusive scopes interact with each other, and with regular scopes. The users in the figure all have the following attributes associated with them.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>User</th>
<th>City</th>
<th>Title</th>
<th>Department</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Terry</p></td>
<td><p>Vancouver</p></td>
<td><p>Accountant</p></td>
<td><p>Accounting</p></td>
</tr>
<tr class="even">
<td><p>David</p></td>
<td><p>Vancouver</p></td>
<td><p>Writer</p></td>
<td><p>Marketing</p></td>
</tr>
<tr class="odd">
<td><p>Walter</p></td>
<td><p>Vancouver</p></td>
<td><p>Manager</p></td>
<td><p>Marketing</p></td>
</tr>
<tr class="even">
<td><p>Bob</p></td>
<td><p>Vancouver</p></td>
<td><p>CEO</p></td>
<td><p>Board</p></td>
</tr>
<tr class="odd">
<td><p>Christine</p></td>
<td><p>Vancouver</p></td>
<td><p>President</p></td>
<td><p>Board</p></td>
</tr>
<tr class="even">
<td><p>Fred</p></td>
<td><p>Vancouver</p></td>
<td><p>CFO</p></td>
<td><p>Executives</p></td>
</tr>
<tr class="odd">
<td><p>Martin</p></td>
<td><p>Vancouver</p></td>
<td><p>CIO</p></td>
<td><p>Executives</p></td>
</tr>
<tr class="even">
<td><p>Kim</p></td>
<td><p>Vancouver</p></td>
<td><p>Vice President, Operations</p></td>
<td><p>Executives</p></td>
</tr>
<tr class="odd">
<td><p>Jennifer</p></td>
<td><p>Vancouver</p></td>
<td><p>Vice President, Technology</p></td>
<td><p>Executives</p></td>
</tr>
</tbody>
</table>


The following three management role assignments in the figure manage the users in the preceding table. Each has an associated scope, some of which are exclusive scopes.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Role assignment</th>
<th>Scope filter</th>
<th>Exclusive or regular</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Recipient Administrators</p></td>
<td><p>City = Vancouver</p></td>
<td><p>Regular</p></td>
</tr>
<tr class="even">
<td><p>VIP Administrators</p></td>
<td><p>Title = CEO or CFO or CIO or President</p></td>
<td><p>Exclusive</p></td>
</tr>
<tr class="odd">
<td><p>Executive Administrators</p></td>
<td><p>Department = Executives</p></td>
<td><p>Exclusive</p></td>
</tr>
</tbody>
</table>


The Recipient Administrators role assignment has a scope that matches all of the users because every user is located in Vancouver. Without any exclusive scopes, this would mean that the Recipient Administrators role assignment could manage any of the users. However, this organization has created two exclusive scopes: VIP Administrators and Executive Administrators. These exclusive scopes restrict who can manage the users that match their respective scope filters. The VIP Administrators role assignment has a scope filter that matches any user who has a title of CEO, CFO, CIO, or President. The Executive Administrators role assignment has a scope filter that matches any user who is in the Executives department.

When the regular and exclusive scopes are evaluated, the following is the result:

  - The Recipient Administrators role assignment can manage the users Terry, David, and Walter. This role assignment can't manage any of the other users because they match the exclusive scope filters of the VIP Administrators and Executive Administrators role assignments.

  - The VIP Administrators role assignment can manage the users Bob, Christine, Fred, and Martin. This is because the exclusive scope filter associated with this role assignment matches the attributes on these objects. This role assignment can't manage the users Kim and Jennifer because their attributes don't match this exclusive scope.

  - The Executive Administrators role assignment can manage the users Kim, Jennifer, Fred, and Martin. This is because the exclusive scope filter associated with this role assignment matches the attributes on these objects. This role assignment can't manage the users Bob and Christine because their attributes don't match this exclusive scope.

Notice that Fred and Martin are accessible by both exclusive scopes. This is because the attributes on these users match the filters of both exclusive scopes.

**Interaction between exclusive scopes and regular scopes**

![Exclusive and regular scope interaction](images/Dd638110.0aa26d1d-1fa6-44d8-802d-83d75cd2624c(EXCHG.150).jpg "Exclusive and regular scope interaction")

For more information about management scopes, see [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md).

