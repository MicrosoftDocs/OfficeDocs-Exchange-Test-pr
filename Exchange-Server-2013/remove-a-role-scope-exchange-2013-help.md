---
title: 'Remove a role scope: Exchange 2013 Help'
TOCTitle: Remove a role scope
ms:assetid: ad17cba0-a8d3-4f40-b3c9-c37e6e5c3f36
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd351051(v=EXCHG.150)
ms:contentKeyID: 49289375
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Remove a role scope

 

_**Applies to:** Exchange Server 2013_


Management role scopes determine what objects are made available to a user who can then change the objects using the cmdlets and parameters assigned to the user. If you're no longer using a scope, it can be removed. For more information about management role scopes in Microsoft Exchange Server 2013, see [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Management scopes" entry in the [Role management permissions](role-management-permissions-exchange-2013-help.md) topic.

  - You must use the Shell to perform these procedures.

  - Before you can remove a scope, you must remove the scope from any management role assignments that might be using it. For more information about how to remove a scope from a role assignment, see [Change a role assignment](change-a-role-assignment-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to remove a scope

To remove a scope, use the following syntax.

    Remove-ManagementScope <scope name>

For example, to remove the "Dublin Servers" scope, use the following command.

    Remove-ManagementScope "Dublin Servers"

