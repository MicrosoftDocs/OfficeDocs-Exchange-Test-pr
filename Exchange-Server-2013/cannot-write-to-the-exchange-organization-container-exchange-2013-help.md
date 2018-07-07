---
title: 'Cannot write to the Exchange organization container: Exchange 2013 Help'
TOCTitle: Cannot write to the Exchange organization container
ms:assetid: 17c4667b-7db1-4e0a-b824-1f6d51d980a9
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.globalserverinstall(v=EXCHG.150)
ms:contentKeyID: 46628820
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Cannot write to the Exchange organization container

 

_**Applies to:** Exchange Server_


Microsoft Exchange Server 2013 Setup can’t continue because the logged-on user doesn't have the account permissions that are required to write to the organization container in the Active Directory directory service.

Setup requires that the user who is logged on when Exchange 2013 is installed has permission to create and modify objects in Active Directory. If you’re running Exchange 2013 Setup in your organization for the first time, the account you use must be a member of the Schema Admins and Enterprise Admins groups. These permissions are required because Active Directory is prepared for Exchange 2013 the first time Setup is run. After Active Directory is prepared, the account you use to install additional Exchange 2013 servers must be a member of the Organization Management management role group.

To resolve this issue, grant the logged-on user the appropriate permissions, or log on with an account that has those permissions and run Exchange 2013 Setup again.


> [!IMPORTANT]
> Cross-forest installation of Exchange 2013 isn't supported. Use an account that is a member of the Active Directory forest where you're installing Exchange 2013.



Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Did you find what you’re looking for? Please take a minute to [send us feedback](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) about the information you were hoping to find.

