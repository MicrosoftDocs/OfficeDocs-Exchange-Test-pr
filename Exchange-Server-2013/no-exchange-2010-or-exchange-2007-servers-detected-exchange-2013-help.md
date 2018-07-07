---
title: 'No Exchange 2010 or Exchange 2007 servers detected: Exchange 2013 Help'
TOCTitle: No Exchange 2010 or Exchange 2007 servers detected
ms:assetid: 789cabab-c769-4a16-a6c8-3db82cff8861
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.noe14serverwarning(v=EXCHG.150)
ms:contentKeyID: 46628970
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# No Exchange 2010 or Exchange 2007 servers detected

 

_**Applies to:** Exchange Server_


Microsoft Exchange Server 2013 Setup displayed this warning because no Exchange Server 2010 or Exchange Server 2007 server roles exist in the organization.


> [!WARNING]
> If you continue with Exchange Server 2013 installation, you won’t be able to add Exchange 2010 or Exchange 2007 servers to the organization at a future date.



Before deploying Exchange 2013, consider the following factors that may require you to deploy Exchange 2010 or Exchange 2007 servers prior to deploying Exchange 2013:

  - **Third-party or in-house developed applications**   Applications developed for earlier versions of Exchange may not be compatible with Exchange 2013. You may need to maintain Exchange 2010 or Exchange 2007 servers to support these applications.

  - **Coexistence or migration requirements**   If you plan on migrating mailboxes into your organization, some solutions may require the use of Exchange 2010 or Exchange 2007 servers.

If you decide that you need to deploy Exchange 2010 or Exchange 2007 servers, you must do so before you deploy Exchange 2013. Active Directory must be prepared for each Exchange version in the following order:

1.  Exchange 2007

2.  Exchange 2010

3.  Exchange 2013

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Did you find what you’re looking for? Please take a minute to [send us feedback](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) about the information you were hoping to find.

