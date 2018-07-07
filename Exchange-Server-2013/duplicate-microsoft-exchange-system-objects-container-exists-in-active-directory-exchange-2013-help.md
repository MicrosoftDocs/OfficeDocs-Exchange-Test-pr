---
title: 'Duplicate Microsoft Exchange System Objects container exists in Active Directory: Exchange 2013 Help'
TOCTitle: Duplicate Microsoft Exchange System Objects container exists in Active Directory
ms:assetid: cd0f45ab-89de-4653-b50d-c1157c2329d5
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.adiniterrorrule(v=EXCHG.150)
ms:contentKeyID: 46629118
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Duplicate Microsoft Exchange System Objects container exists in Active Directory

 

_**Applies to:** Exchange Server_


Microsoft Exchange Server 2013 Setup can’t continue because it found a duplicate Microsoft Exchange System Objects container in Active Directory Domain Naming context. When Setup finds a duplicate Microsoft Exchange System Objects container, you must delete the duplicate container before Setup can continue. When a duplicate Microsoft Exchange System Objects container exists, you can’t solve the problem by running **DomainPrep** again. You must identify and delete the duplicate Microsoft Exchange System Objects container.

To resolve this issue, do the following:

1.  Log on to the domain controller with administrative credentials.

2.  In **Administrative Tools**, click **Active Directory Users and Computers**.

3.  In the **Active Directory Users and Computers** management console pane, click **View** from the toolbar menu and then select **Advanced Features**.

4.  Locate the duplicate Microsoft Exchange System Objects container.

5.  Verify the duplicate Microsoft Exchange System Objects container doesn’t contain valid Active Directory objects.

6.  Right-click the duplicate Microsoft Exchange System Objects container, and then click **Delete**.

7.  Confirm the deletion by clicking **Yes** in the Active Directory dialog box.


> [!NOTE]
> If you want the change to be replicated immediately, you must manually initiate replication between domain controllers.



Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Did you find what you’re looking for? Please take a minute to [send us feedback](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) about the information you were hoping to find.

