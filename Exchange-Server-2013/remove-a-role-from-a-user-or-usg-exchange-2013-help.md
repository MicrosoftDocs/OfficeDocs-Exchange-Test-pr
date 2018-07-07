---
title: 'Remove a role from a user or USG: Exchange 2013 Help'
TOCTitle: Remove a role from a user or USG
ms:assetid: df3510ef-e0c2-4d3c-81b0-7dc3e70c01a0
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd351196(v=EXCHG.150)
ms:contentKeyID: 49289437
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Remove a role from a user or USG

 

_**Applies to:** Exchange Server 2013_


Management role assignments assign a management role to a user or universal security group (USG). If you remove a role assignment, the users assigned the role will no longer have access to the cmdlets available on that role. For more information about management role assignments in Microsoft Exchange Server 2013, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

Looking for other management tasks related to roles? Check out [Advanced permissions](advanced-permissions-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete this procedure: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Role assignments" entry in the [Role management permissions](role-management-permissions-exchange-2013-help.md) topic.

  - You must use the Shell to perform these procedures.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Remove a management role assignment

If you know the name of the role assignment you want to remove, use the following syntax.

    Remove-ManagementRoleAssignment <assignment name>

For example, to remove the "Tier 2 Help Desk Assignment" role assignment, use the following command.

    Remove-ManagementRoleAssignment "Tier 2 Help Desk Assignment"

If you don't know the name of the role assignment, you can use the following syntax.

    Get-ManagementRoleAssignment -RoleAssignee <user or USG> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment 

For example, if you want to remove the Mail Recipients regular role assignment from the user davids, use the following command.

    Get-ManagementRoleAssignment -RoleAssignee davids -Role "Mail Recipients" -Delegating $false | Remove-ManagementRoleAssignment

