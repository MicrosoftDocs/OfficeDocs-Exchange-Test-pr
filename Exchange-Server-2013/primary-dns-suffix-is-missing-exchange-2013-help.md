---
title: 'Primary DNS Suffix is missing: Exchange 2013 Help'
TOCTitle: Primary DNS Suffix is missing
ms:assetid: 310765bf-a650-4a3d-a5e4-6173b559d4f6
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.fqdnmissing(v=EXCHG.150)
ms:contentKeyID: 61200284
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Primary DNS Suffix is missing

 

_**Applies to:** Exchange Server_


Microsoft Exchange Server 2013 Setup can't continue because the primary domain name system (DNS) suffix for the computer you're installing Exchange on hasn't been configured.

To resolve this issue, add a primary DNS suffix on the computer using the steps below and then run Setup again.


> [!IMPORTANT]
> Changing the computer name or primary DNS suffix after you install Exchange 2013 isn't supported.



1.  Log on to the computer where you want to install the Edge Transport role as a user that's a member of the local Administrators group.

2.  Open the **Control Panel** and then double-click **System**.

3.  In the **Computer name, domain, and workgroup settings** section, click **Change settings**.

4.  In the **System Properties** window, make sure the **Computer Name** tab is selected and then click **Change…**.

5.  In **Computer Name/Domain Changes**, click **More…**.

6.  In **Primary DNS suffix of this computer**, enter the DNS domain name for the Edge Transport server. For example, contoso.com.

7.  Click **OK** to close each window.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Did you find what you’re looking for? Please take a minute to [send us feedback](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) about the information you were hoping to find.

