---
title: 'ExecutionPolicy GPO is defined: Exchange 2013 Help'
TOCTitle: ExecutionPolicy GPO is defined
ms:assetid: 63de83e2-9a6b-4f57-85b9-df445bea18dd
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.powershellexecutionpolicycheckset(v=EXCHG.150)
ms:contentKeyID: 61200286
ms.date: 12/15/2016
mtps_version: v=EXCHG.150
---

# ExecutionPolicy GPO is defined

 

_**Applies to:** Exchange Server_


Microsoft Exchange Server 2013 Setup can’t continue because it detected that the **ExecutionPolicy** Group Policy Object (GPO) defines one or both of the following policies:

  - **MachinePolicy**

  - **UserPolicy**

It doesn't matter how the policies have been defined. It only matters that they have been defined.

When you run Exchange 2013 Setup, Exchange stops and disables the Windows Management Instrumentation (WMI) service. When either of these policies are defined, the WMI service needs to be enabled to run a Windows PowerShell script. If the policies are defined and the WMI service is stopped, Setup will fail and the server will be left in an inconsistent state.

To allow Setup to continue, you need to temporarily remove any definition of **MachinePolicy** or **UserPolicy** in the **ExecutionPolicy** GPO.

For information on how to remove any definitions of **MachinePolicy** or **UserPolicy** in the **ExecutionPolicy** GPO, see [Knowledge Base article KB981474](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=981474).


> [!NOTE]
> Even though this Knowledge Base article was written for Exchange 2010, it also applies to Exchange 2013 cumulative updates and service packs.



Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Did you find what you’re looking for? Please take a minute to [send us feedback](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) about the information you were hoping to find.

