---
title: 'IIS 7 .NET Extensibility component is required_LonghornIIS7NetExt: Exchange 2013 Help'
TOCTitle: IIS 7 .NET Extensibility component is required_LonghornIIS7NetExt
ms:assetid: 8b481626-b68a-4fba-b66e-a02c03856bfd
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.longhorniis7netext(v=EXCHG.150)
ms:contentKeyID: 46629018
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# IIS 7 .NET Extensibility component is required\_LonghornIIS7NetExt

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2010 Setup cannot continue because the required Internet Information Server (IIS) 7 .NET Extensibility component is not installed on the target server.

Before Exchange 2010 can use Windows PowerShell Remoting, the IIS 7 .NET Extensibility component must be installed on the target server.

To address this error, use Server Manager to install the IIS 7 .NET Extensibility component on this server and then rerun Exchange 2010 setup.

**Install the IIS 7 .NET Extensibility component in Windows Server 2008 or in Windows Server 2008 R2 by using the Server Manager tool**

1.  Click **Start**, click **Administrative Tools** and then **Server Manager**.

2.  In the left navigation pane, expand **Roles**, and then right-click **Web Server (IIS)** and select **Add Role Services**.

3.  On the **Select Role Services** pane, scroll down to **Application Development**.

4.  Select the check box under **.NET Extensibility**.

5.  Click **Next** from the **Select Role Services** pane, and then click **Install** at the **Confirm Installations Selections** pane.

6.  Click **Close** to exit the Add Role Services wizard.

