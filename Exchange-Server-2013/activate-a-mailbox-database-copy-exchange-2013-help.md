---
title: 'Activate a mailbox database copy: Exchange 2013 Help'
TOCTitle: Activate a mailbox database copy
ms:assetid: d948269b-c902-4d8d-8c2b-269473359baa
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee364750(v=EXCHG.150)
ms:contentKeyID: 48385619
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Activate a mailbox database copy

 

_**Applies to:** Exchange Server 2013_


Activating a mailbox database copy is the process of designating a specific passive copy as the new active copy of a mailbox database. This process is referred to as a *database switchover*. A database switchover involves dismounting the current active database and mounting the database copy on the specified server as the new active mailbox database copy. The database copy that will become the active mailbox database must be healthy and current.

Looking for other management tasks related to mailbox database copies? Check out [Managing mailbox database copies](managing-mailbox-database-copies-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete this task: 1 minute

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox database copies" entry in the [High availability and site resilience permissions](high-availability-and-site-resilience-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to move the active mailbox database

1.  In the EAC, go to **Servers** \> **Databases**.

2.  Select the database whose copy you want to activate.

3.  In the Details pane, under **Database Copies**, click **Activate** under the database copy you want to activate.

4.  Click **yes** to activate the database copy.

## Use the Shell to move the active mailbox database

This example activates and mounts a copy of the database DB4 hosted on MBX3 as the new active mailbox database. This command makes DB4 the new active mailbox database, and it doesn't override the database mount dial settings on MBX3.

    Move-ActiveMailboxDatabase DB4 -ActivateOnServer MBX3 -MountDialOverride:None

This example performs a switchover of the database DB2 to the Mailbox server MBX1. When the command completes, MBX1 hosts the active copy of DB2. Because the *MountDialOverride* parameter is set to `None`, MBX1 mounts the database using its own defined database auto mount dial settings.

    Move-ActiveMailboxDatabase DB2 -ActivateOnServer MBX1 -MountDialOverride:None

This example performs a switchover of the database DB1 to the Mailbox server MBX3. When the command completes, MBX3 hosts the active copy of DB1. Because the *MountDialOverride* parameter is specified with a value of `Good Availability`, MBX3 mounts the database using a database auto mount dial setting of *GoodAvailability*.

    Move-ActiveMailboxDatabase DB1 -ActivateOnServer MBX3 -MountDialOverride:GoodAvailability

This example performs a switchover of the database DB3 to the Mailbox server MBX4. When the command completes, MBX4 hosts the active copy of DB3. Because the *MountDialOverride* parameter isn't specified, MBX4 mounts the database using a database auto mount dial setting of *Lossless*.

    Move-ActiveMailboxDatabase DB3 -ActivateOnServer MBX4

This example performs a server switchover for the Mailbox server MBX1. All active mailbox database copies on MBX1 will be activated on one or more other Mailbox servers with healthy copies of the active databases on MBX1.

    Move-ActiveMailboxDatabase -Server MBX1

This example performs a switchover of the database DB4 to the Mailbox server MBX5. In this example, the database copy on MBX5 has a replay queue greater than 6. As a result, the *SkipLagChecks* parameter must be specified to activate the database copy on MBX5.

    Move-ActiveMailboxDatabase DB4 MBX5 -SkipLagChecks

This example performs a switchover of the database DB5 to the Mailbox server MBX6. In this example, the database copy on MBX6 has a *ContentIndexState* of Failed. As a result, the *SkipClientExperienceChecks* parameter must be specified to activate the database copy on MBX6.

    Move-ActiveMailboxDatabase DB5 MBX6 -SkipClientExperienceChecks

## How do you know this worked?

To verify that you've successfully activated a mailbox database copy, do one of the following:

  - In the EAC, navigate to **Servers** \> **Databases**. Select the appropriate database, and in the Details pane, click **View details** to view the database copy properties.

  - In the Shell, run the following command to display status information for a database copy.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

## For more information

[Mailbox database copies](mailbox-database-copies-exchange-2013-help.md)

[Configure mailbox database copy properties](configure-mailbox-database-copy-properties-exchange-2013-help.md)

