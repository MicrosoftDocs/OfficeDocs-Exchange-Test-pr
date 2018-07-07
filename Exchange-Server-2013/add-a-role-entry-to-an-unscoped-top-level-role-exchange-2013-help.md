---
title: 'Add a role entry to an unscoped top-level role: Exchange 2013 Help'
TOCTitle: Add a role entry to an unscoped top-level role
ms:assetid: 52fd3f20-c348-49d5-9bdb-f2cbf780cf2d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd979789(v=EXCHG.150)
ms:contentKeyID: 49289252
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Add a role entry to an unscoped top-level role

 

_**Applies to:** Exchange Server 2013_


You can add scripts and non-Exchange cmdlets to unscoped top-level management roles if you want to make new scripts or non-Exchange cmdlets available to existing unscoped roles. These scripts and non-Exchange cmdlets are added as management role entries to unscoped top-level management roles. They can then be used by those unscoped top-level role entries or any unscoped roles derived from the top-level roles. For more information about unscoped role entries, see [Understanding management roles](understanding-management-roles-exchange-2013-help.md).


> [!NOTE]
> If you want to change a role entry on a management role that contains Exchange cmdlets, see <A href="change-a-role-entry-exchange-2013-help.md">Change a role entry</A>.



Looking for other management tasks related to roles? Check out [Advanced permissions](advanced-permissions-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Management roles" entry in the [Role management permissions](role-management-permissions-exchange-2013-help.md) topic.

  - You must use the Shell to perform these procedures.

  - The ability to add a role entry on an unscoped top-level role isn't included in any management role group by default. You must first assign the Unscoped Role Management role to a user, or to a universal security group (USG) or role group of which the user is a member, before the user is able to add an unscoped top-level role entry. For more information about adding a role to a role group, user, or USG, see the following topics:
    
      - [Manage role groups](manage-role-groups-exchange-2013-help.md)
    
      - [Add a role to a user or USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Add a script role entry to an unscoped top-level role

If you want to add a script to an existing unscoped role, use this procedure. If you want to add a non-Exchange cmdlet to an existing unscoped role, see "Add a non-Exchange cmdlet role entry to an unscoped top-level role" later in this topic.

To add a Windows PowerShell script to an unscoped top-level role, you must add a management role entry to the role. The role entry contains the script's name and the parameters on the script that you want to make available to the role.

The script must reside in the Scripts directory in the Microsoft Exchange Server 2013 installation path on every server running Exchange 2013 where users might connect to run the script. If a user has access to run a script, but the script isn't located on the Exchange 2013 server the user is connected to, an error occurs. By default, the path to the Scripts directory is C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts.

After you copy the script to the appropriate Exchange 2013 servers and you decide what script parameters should be used, create the role entry using the following syntax.

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

This example adds the BulkProvisionUsers.ps1 script to the IT Scripts role with the *Name* and *Location* parameters.

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel


> [!NOTE]
> The <STRONG>Add-ManagementRoleEntry</STRONG> cmdlet performs basic validation to make sure that you add only the parameters that exist in the script. However, no further validation is done after the role entry is added. If parameters are later added or removed, you must manually update the role entries that contain the script.



## Add a non-Exchange cmdlet role entry to an unscoped top-level role

If you want to add a non-Exchange cmdlet to an existing unscoped role, use this procedure. If you want to add a script to an existing unscoped role, see "Add a script role entry to an unscoped top-level role" earlier in this topic.

To add a non-Exchange cmdlet to an unscoped top-level role, you must add a management role entry to the role. The role entry contains the cmdlet snap-in, cmdlet name, and the parameters on the cmdlet that you want to make available to the role.

If you add non-Exchange cmdlets to the new role, the cmdlets must be installed on every Exchange 2013 server where users might connect to run the cmdlets. To learn how to properly install and register the Windows PowerShell snap-ins that contain the cmdlets you want to use, refer to the documentation for your product.

After you install the Windows PowerShell snap-in that contains the cmdlets on the appropriate the Exchange 2013 servers and you decide what cmdlet parameters should be used, create the role entry using the following syntax.

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

This example adds the **Set-WidgetConfiguration** cmdlet in the Contoso.Admin.Cmdlets snap-in to the Widget Cmdlets role with the *Database* and *Size* parameters.

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel


> [!NOTE]
> The <STRONG>Add-ManagementRoleEntry</STRONG> cmdlet performs basic validation to make sure that you add only the parameters that exist in the cmdlet. However, no further validation is done after the role entry is added. If the cmdlet is later changed, and parameters are added or removed, you must manually update the role entries that contain the cmdlet.



## Other tasks

After you add a role entry or an unscoped top-level role, you may also want to:

[Add a role entry to a role](add-a-role-entry-to-a-role-exchange-2013-help.md)

[Manage role groups](manage-role-groups-exchange-2013-help.md)

[Manage role group members](manage-role-group-members-exchange-2013-help.md)

[Add a role to a user or USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[Remove a role from a user or USG](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

