---
title: 'Suspend or resume a mailbox database copy: Exchange 2013 Help'
TOCTitle: Suspend or resume a mailbox database copy
ms:assetid: 96aa1b82-3e15-4215-843e-3d583af9504b
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd298159(v=EXCHG.150)
ms:contentKeyID: 48385374
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Suspend or resume a mailbox database copy

 

_**Applies to:** Exchange Server 2013_


You may need to suspend or resume a database copy for a variety of reasons, such as maintenance on the disk that contains a database copy, or suspend an individual database copy from activation for disaster recovery purposes.

Looking for other management tasks related to mailbox database copies? Check out [Managing mailbox database copies](managing-mailbox-database-copies-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete this task: 1 minute

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox database copies" entry in the [High availability and site resilience permissions](high-availability-and-site-resilience-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to suspend a mailbox database copy

1.  In the EAC, go to **Servers** \> **Databases**.

2.  Select the database whose copy you want to suspend.

3.  In the Details pane, under **Database Copies**, click **Suspend** under the database copy you want to suspend.

4.  In the **Comments** field, add an optional comment of up to 512 characters specifying the reason for the suspension.

5.  To suspend the database copy from automatic activation, select the **This copy can only be activated by manual intervention** check box.

6.  Click **save** to suspend the database copy.

## Use the EAC to resume a mailbox database copy

1.  In the EAC, go to **Servers** \> **Databases**.

2.  Select the database whose copy you want to resume.

3.  In the Details pane, under **Database Copies**, click **Resume** under the database copy you want to resume.

4.  Click **yes** to resume the database copy.

## Use the Shell to suspend a mailbox database copy

This example suspends continuous replication for a copy of the database DB1 hosted on the server MBX1. An optional comment has also been specified.

    Suspend-MailboxDatabaseCopy -Identity DB1\MBX1 -SuspendComment "Maintenance on MBX1" -Confirm:$False

This example suspends activation for a copy of the database DB2 hosted on the server MBX2.

    Suspend-MailboxDatabaseCopy -Identity DB2\MBX2 -ActivationOnly -Confirm:$False

## Use the Shell to resume a mailbox database copy

This example resumes a copy of the database DB1 on the server MBX1.

    Resume-MailboxDatabaseCopy -Identity DB1\MBX1

This example resumes a copy of the database DB2 on the server MBX2 for replication only.

    Resume-MailboxDatabaseCopy -Identity DB2\MBX2 -ReplicationOnly

## How do you know this worked?

To verify that you have successfully suspended or resumed a mailbox database copy, do one of the following:

  - In the EAC, navigate to **Servers** \> **Databases**. Select the appropriate database, and in the Details pane, click **View details** to view the database copy properties.

  - In the Shell, run the following command to display status information for a database copy.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

