---
title: 'Automatic mailbox distribution: Exchange 2013 Help'
TOCTitle: Automatic mailbox distribution
ms:assetid: f4db4636-948c-466b-839c-300c1a3a9544
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ff477621(v=EXCHG.150)
ms:contentKeyID: 56474986
ms.date: 07/14/2016
mtps_version: v=EXCHG.150
---

# Automatic mailbox distribution

 

_**Applies to:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_


When you create or move a mailbox, or mail-enable an existing user, that mailbox needs to be stored in a mailbox database. In Microsoft Exchange Server 2013, you have the option of letting Exchange choose the database for you using automatic mailbox distribution.

With automatic mailbox distribution, Exchange looks at the mailbox databases in your organization, excludes databases that aren't suitable using criteria discussed later in this topic, and then randomly chooses a database where the mailbox should be located. This process randomly distributes mailboxes across all of the suitable mailbox databases in your organization.

Automatic distribution is used when you don't specify the *Database* parameter on the **New-Mailbox** and **Enable-Mailbox** cmdlets or the *TargetDatabase* parameter on the **New-MoveRequest** cmdlet.


> [!NOTE]
> Automatic mailbox distribution is performed only when a mailbox is created on an Exchange 2013 server, moved to an Exchange 2013 server, or when a user is mail-enabled. The <STRONG>New-Mailbox</STRONG>, <STRONG>New-MoveRequest</STRONG>, and <STRONG>Enable-Mailbox</STRONG> cmdlets must be run from a server running Exchange 2013. Exchange doesn't redistribute mailboxes to distribute load across databases automatically based on server load.



The following process is used to find a suitable mailbox database where a new or moved mailbox should be located:

1.  Exchange retrieves a list of all mailbox databases in the Exchange 2013 organization.

2.  Any mailbox database that's marked for exclusion from the distribution process is removed from the available list of databases. You can control which databases are excluded. For more information, see Exclude Databases from Automatic Distribution later in this topic.

3.  Any mailbox database that's outside of the database management scopes applied to the administrator performing the operation is removed from the list of available databases. For more information, see Database Scopes later in this topic.

4.  Any mailbox database that's outside of the local Active Directory site where the operation is being performed is removed from the list of available databases.

5.  From the remaining list of mailbox databases, Exchange chooses a database randomly. If the database is online and healthy, the database is used by Exchange. If it's offline or not healthy, another database is chosen at random. If no online or healthy databases are found, the operation fails with an error.

The process of selecting a mailbox database is performed by the Mailbox Resources Management Agent cmdlet extension agent. The `Mailbox Resources Management Agent` is one of several cmdlet extension agents that extend the functionality of running cmdlets. For more information about cmdlet extension agents, see [Cmdlet extension agents](cmdlet-extension-agents-exchange-2013-help.md).

If you never want mailboxes to be distributed automatically, you can disable the `Mailbox Resources Management Agent`. When you disable the agent, the change is applied to the entire Exchange organization. For more information about how to disable cmdlet extension agents, see [Manage cmdlet extension agents](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Exclude Databases from Automatic Distribution

By default, all online and healthy mailbox databases on Exchange 2013 servers in the local Active Directory site can be chosen by automatic mailbox distribution to store a new or moved mailbox. However, you might want to exclude some databases from the distribution process for various reasons. For example, you may designate a mailbox database as a journaling database in which only mailboxes you manually specify should be located. Or you might want to temporarily remove a database from rotation to perform scheduled maintenance. Exchange 2013 gives you the option to either permanently or temporarily exclude databases from the exclusion process using the *IsExcludedFromProvisioning* parameter that can be set using the **Set-MailboxDatabase** cmdlet.


> [!NOTE]
> Two other parameters, <EM>IsSuspendedFromProvisioning</EM> and <EM>IsExcludedFromInitialProvisioning</EM>, are also available on the <STRONG>Set-MailboxDatabase</STRONG> cmdlet. These parameters will be removed in a future release of Exchange and their use isn't supported.



The *IsExcludedFromProvisioning* parameter has have two valid values, `$True` and `$False`. When you set this property to `$True`, the mailbox database is excluded from the automatic distribution process. When you set it to `$False`, the mailbox database is included in the automatic distribution process. The default value is `$False`.

To exclude a mailbox database from automatic distribution, use the following command:

    Set-MailboxDatabase <database name> -IsExcludedFromProvisioning $True

When a mailbox database is excluded from automatic distribution, the only way to create a mailbox in, or move a mailbox to, the database is to use the *Database* parameter on the **New-Mailbox** and **Enable-Mailbox** cmdlets or the *TargetDatabase* parameter on the **New-MoveRequest** cmdlet.

## Database Scopes

Database management scopes are an additional level of control over the automatic mailbox distribution process that are available in Exchange 2013. If a mailbox database is online and healthy, it's in the local Active Directory site, and it isn't excluded from the automatic distribution process, Exchange 2013 checks to see if the mailbox database is included in the database scope applied to the administrator running the cmdlet. If it's included in the database scope, it's included in the list of databases available to that administrator.

Database scopes are part of the Role Based Access Control (RBAC) permissions model. For more information about RBAC and database scopes, see the following topics:

  - [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md)

  - [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md)

Database scopes can be useful if you have many mailbox databases in your local Active Directory site that are available to automatic distribution, but you want to limit which databases can be used by certain sets of administrators. For example, your Exchange 2013 servers may serve several agencies but you only want to allow each agency to create or move mailboxes to mailbox databases that are allocated to them.

By default, all administrators in an Exchange 2013 organization can see all of the mailbox databases in the organization. To limit the databases that they can see, and therefore limit the databases they can potentially create mailboxes in or move mailboxes to, you must do the following:

1.  Create a custom database management scope using the **New-ManagementScope** cmdlet that includes only the mailbox databases you want the administrator to use.

2.  Associate the new database scope with a management role assignment in one of the following ways:
    
      - Add the new database scope to an existing management role assignment using the *CustomConfigWriteScope* parameter on the **Set-ManagementRoleAssignment** cmdlet. The database scope is now applied to the management role group, universal security group (USG), or user assigned the role assignment.
    
      - Create a management role assignment using the **New-ManagementRoleAssignment** cmdlet and use the *CustomConfigWriteScope* parameter to specify the new database scope. You can create a role assignment between a management role and a role group, USG, or user.

3.  If you created a role assignment to a role group or USG, add users to the role group or USG so that the role assignment and database scope are applied to the users.

4.  If applicable, remove the user (or users who are members of role groups or USGs you created in the preceding steps) you assigned the new role assignment to from any other role groups or USGs that might be assigned a database scope that contains databases you don't want them to access.

5.  Verify that the administrators have access only to the databases they should have access to.

After you complete these steps, the administrators that are assigned role assignments with the database scopes you created will only be able to create mailboxes in or move mailboxes to the databases you specified.

For more information about how to use database scopes to limit which mailbox databases are available to administrators, see [Control automatic mailbox distribution using database scopes](control-automatic-mailbox-distribution-using-database-scopes-exchange-2013-help.md).

