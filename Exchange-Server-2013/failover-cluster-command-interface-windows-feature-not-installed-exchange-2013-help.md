---
title: 'Failover Cluster Command Interface Windows feature not installed: Exchange 2013 Help'
TOCTitle: Failover Cluster Command Interface Windows feature not installed
ms:assetid: 0d839514-5ab7-497d-8945-41392b4c3980
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.rsatclusteringcmdinterfaceinstalled(v=EXCHG.150)
ms:contentKeyID: 50619802
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Failover Cluster Command Interface Windows feature not installed

 

_**Applies to:** Exchange Server_


Microsoft Exchange Server 2013 Setup can't continue because the local computer is missing a required Windows feature. You'll need to install this Windows feature before Exchange 2013 can continue.

Exchange 2013 Setup requires that the **Failover Cluster Command Interface** Windows feature be installed on the computer before installation can continue.

Do the following to install the Windows feature on this computer. If the feature requires a reboot to complete installation, you'll need to exit Exchange 2013 Setup, reboot, and then start Setup again.


> [!NOTE]
> Additional Windows features or updates might need to be installed before Exchange 2013 Setup can continue. For a complete list of required Windows features and updates, check out <A href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 prerequisites</A>.



1.  Open Windows PowerShell on the local computer.

2.  Run the following command to install the required Windows feature.
    
        Install-WindowsFeature RSAT-Clustering-CmdInterface

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Did you find what you’re looking for? Please take a minute to [send us feedback](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) about the information you were hoping to find.

