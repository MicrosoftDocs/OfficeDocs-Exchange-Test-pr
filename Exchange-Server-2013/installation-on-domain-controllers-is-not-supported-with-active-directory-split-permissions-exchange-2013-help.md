---
title: 'Installation on domain controllers is not supported with Active Directory split permissions: Exchange 2013 Help'
TOCTitle: Installation on domain controllers is not supported with Active Directory split permissions
ms:assetid: 977e3758-5e09-40a2-80c1-fe344b1d8a2a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.installondcinadsplitpermissionmode(v=EXCHG.150)
ms:contentKeyID: 46629039
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Installation on domain controllers is not supported with Active Directory split permissions

 

_**Applies to:** Exchange Server_


Microsoft Exchange Server 2013 Setup has detected that you’re attempting to run Setup on an Active Directory domain controller and one of the following is true:

  - The Exchange organization is already configured for Active Directory split permissions.

  - You selected the Active Directory split permissions option in Exchange 2013 Setup.

The installation of Exchange 2013 on domain controllers isn’t supported when the Exchange organization is configured for Active Directory split permissions.

If you want to install Exchange 2013 on a domain controller, you must configure the Exchange organization for Role Based Access Control (RBAC) split permissions or shared permissions.


> [!IMPORTANT]
> We don’t recommend installing Exchange 2013 on Active Directory domain controllers. For more information, see <A href="installing-exchange-on-a-domain-controller-is-not-recommended-exchange-2013-help.md">Installing Exchange on a domain controller is not recommended</A>.



If you want to continue using Active Directory split permissions, you must install Exchange 2013 on a member server.

For more information about split and shared permissions in Exchange 2013, see the following topics:

[Understanding split permissions](understanding-split-permissions-exchange-2013-help.md)

[Configure Exchange 2013 for split permissions](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)

[Configure Exchange 2013 for shared permissions](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md)

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Did you find what you’re looking for? Please take a minute to [send us feedback](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) about the information you were hoping to find.

