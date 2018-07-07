---
title: 'View role entries: Exchange 2013 Help'
TOCTitle: View role entries
ms:assetid: d9bb0d14-db59-456c-8f50-a8d7f7323df9
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd351179(v=EXCHG.150)
ms:contentKeyID: 49289429
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# View role entries

 

_**Applies to:** Exchange Server 2013_


Each management role entry represents a single cmdlet or script. The parameters included on a role entry determine what parameters on the cmdlet or script a user can access.

The identity of role entries consists of the management role name that the role entry is associated with, and the cmdlet or script that the role entry refers to. For more information about role entries in Microsoft Exchange Server 2013, see [Understanding management roles](understanding-management-roles-exchange-2013-help.md).

Looking for other management tasks related to role entries? Check out [Advanced permissions](advanced-permissions-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Management roles" entry in the [Role management permissions](role-management-permissions-exchange-2013-help.md) topic.

  - You must use the Shell to perform these procedures.

  - This topic makes use of pipelining, the **Format-List** cmdlet, objects, and properties. For more information about these concepts, see the following topics:
    
      - [Pipelining](https://technet.microsoft.com/en-us/library/aa998260\(v=exchg.150\))
    
      - [Working with command output](working-with-command-output-exchange-2013-help.md)
    
      - [Structured data](https://technet.microsoft.com/en-us/library/aa996386\(v=exchg.150\))

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## View a list of role entries

You can use the **Get-ManagementRoleEntry** cmdlet to retrieve a list of role entries. When you use the **Get-ManagementRoleEntry** cmdlet, you must specify a value that contains both the role name that contains the role entries you want to list and also the cmdlet name of the role entry you want to list. By combining the role name and cmdlet name with the wildcard character (\*), you can return specific or broad lists of role entries.

For detailed syntax and parameter information, see [Get-ManagementRoleEntry](https://technet.microsoft.com/en-us/library/dd335210\(v=exchg.150\)).

## View a list of all role entries on a role

To view a list of role entries on a specific role, use the following syntax.

    Get-ManagementRoleEntry <role name>\*

This examples retrieves all the role entries on the `Recipient Administrators` role.

    Get-ManagementRole "Recipient Administrators\*"

For detailed syntax and parameter information, see [Get-ManagementRoleEntry](https://technet.microsoft.com/en-us/library/dd335210\(v=exchg.150\)).

## View a list of roles that contain a specific role entry

To view a list of all the roles that contain a specific role entry, use the following syntax.

    Get-ManagementRoleEntry *\<cmdlet name>

This example retrieves all the roles that contain the **Set-Mailbox** role entry.

    Get-ManagementRoleEntry *\Set-Mailbox

For detailed syntax and parameter information, see [Get-ManagementRoleEntry](https://technet.microsoft.com/en-us/library/dd335210\(v=exchg.150\)).

## View a targeted list of roles that contain similar role entries

To view a list of targeted roles that contain cmdlets with similar names, use the following syntax.

    Get-ManagementRoleEntry *<partial role name>*\*<partial cmdlet name>*

This example returns a list of role entries that contain the string `Mailbox` that are on roles that contain the string `Tier 1` in their names.

    Get-ManagementRoleEntry "*Tier 1*\*Mailbox*"

For detailed syntax and parameter information, see [Get-ManagementRoleEntry](https://technet.microsoft.com/en-us/library/dd335210\(v=exchg.150\)).

## View a single role entry

To view the details of a single role entry, use the following syntax.

    Get-ManagementRoleEntry <role name>\<cmdlet name> | Format-List

This example retrieves the details of the **Set-Mailbox** role entry on the `Recipient Administrators` role.

    Get-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" | Format-List

If the role entry you view has too many parameters to list using the **Format-List** cmdlet, see "View the parameters on a single role entry" later in this topic.

For detailed syntax and parameter information, see [Get-ManagementRoleEntry](https://technet.microsoft.com/en-us/library/dd335210\(v=exchg.150\)).

## View the parameters on a single role entry

Some role entries have more parameters than can be viewed by piping the results of the **Get-ManagementRoleEntry** cmdlet to the **Format-List** cmdlet. If you need to view all the parameters on a role entry, you need to directly access the **Parameters** property of the role entry object.

To view parameters stored in the **Parameters** property of a role entry object, use the following syntax.

    (Get-ManagementRoleEntry <role name>\<cmdlet name>).Parameters

This example retrieves the parameters on the **Set-Mailbox** role entry on the Mail Recipients role.

    (Get-ManagementRoleEntry "Mail Recipients\Set-Mailbox").Parameters

For detailed syntax and parameter information, see [Get-ManagementRoleEntry](https://technet.microsoft.com/en-us/library/dd335210\(v=exchg.150\)).

