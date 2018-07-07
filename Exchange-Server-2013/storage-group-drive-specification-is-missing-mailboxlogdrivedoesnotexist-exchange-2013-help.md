---
title: 'Storage group drive specification is missing_MailboxLogDriveDoesNotExist: Exchange 2013 Help'
TOCTitle: Storage group drive specification is missing_MailboxLogDriveDoesNotExist
ms:assetid: fe210f29-60cb-4d34-877e-1356a21dc02a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.mailboxlogdrivedoesnotexist(v=EXCHG.150)
ms:contentKeyID: 46629193
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Storage group drive specification is missing\_MailboxLogDriveDoesNotExist

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 Disaster Recovery setup cannot continue because Disaster Recovery setup cannot access the storage group database drive specification that was used in the previous installation of this server.

Microsoft Exchange Disaster Recovery setup requires that the same storage group database drive specifications previously used for this server be available during the restore.

To resolve this situation, configure the drives to match the original logical drive configuration and rerun Microsoft Exchange Disaster Recovery setup.

**Assign or change a drive letter**

1.  Open **Computer Management** **(Local)**.

2.  In the console tree, click **Computer Management (Local)**, click **Storage**, and then click **Disk Management**.

3.  Right-click a partition, logical drive, or volume, and then click **Change Drive Letter and Paths**.

4.  Use one of the following procedures:
    
      - To assign a drive letter, click **Add**, click the drive letter you want to use, and then click **OK**.
    
      - To modify a drive letter, click it, click **Change**, click the drive letter you want to use, and then click **OK**.

For more information about how to assign drive letters, see "Assign, change, or remove a drive letter" ([https://go.microsoft.com/fwlink/?LinkId=66764](https://go.microsoft.com/fwlink/?linkid=66764)).

