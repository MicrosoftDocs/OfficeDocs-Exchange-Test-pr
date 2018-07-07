---
title: 'Setup cannot install Exchange to a read-only domain controller_ComputerRODC: Exchange 2013 Help'
TOCTitle: Setup cannot install Exchange to a read-only domain controller_ComputerRODC
ms:assetid: 4934d755-65be-47e2-86b0-6ea1ab148a96
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.computerrodc(v=EXCHG.150)
ms:contentKeyID: 46628890
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Setup cannot install Exchange to a read-only domain controller\_ComputerRODC

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft Exchange Server 2007 Setup cannot continue the installation because the target computer is a Read-Only Domain Controller (RODC).

Read-Only Domain Controllers are a feature of Windows Server 2008 Active Directory. The RODC is a type of domain controller install option that can be installed in remote sites that may have lower levels of physical security.

Exchange Setup requires write access to the target install computer.

To resolve this issue, select a target install computer that is not designated as an RODC, and rerun Setup.

