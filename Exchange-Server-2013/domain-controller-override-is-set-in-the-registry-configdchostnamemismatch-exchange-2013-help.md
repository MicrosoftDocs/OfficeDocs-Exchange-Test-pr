---
title: 'Domain Controller Override is set in the Registry_ConfigDCHostNameMismatch: Exchange 2013 Help'
TOCTitle: Domain Controller Override is set in the Registry_ConfigDCHostNameMismatch
ms:assetid: 3aef5470-d510-4b59-a4b6-36d274a984ae
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.configdchostnamemismatch(v=EXCHG.150)
ms:contentKeyID: 46628888
ms.date: 12/15/2016
mtps_version: v=EXCHG.150
---

# Domain Controller Override is set in the Registry\_ConfigDCHostNameMismatch

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft Exchange Server 2007 setup cannot continue because its attempt to use the specified domain controller failed. A domain controller has been statically mapped in the registry.

Exchange 2007 setup requires that the domain controller specified in the setup command match the domain controller that has been statically mapped using a registry override.

To resolve this issue, run setup again, specifying the statically mapped domain controller for the **/DomainController: \<***FQDN of the* *statically mapped domain controller***\>** parameter.

For more information about DSAccess and directory services detection, see Microsoft Knowledge Base article 250570, "Directory Service Server Detection and DSAccess Usage" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=250570](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=250570)).

