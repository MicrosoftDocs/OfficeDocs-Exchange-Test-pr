---
title: 'IIS 6 Compatibility components not installed_LonghornIIS6MetabaseNotInstalled: Exchange 2013 Help'
TOCTitle: IIS 6 Compatibility components not installed_LonghornIIS6MetabaseNotInstalled
ms:assetid: 0bd52987-d3cc-496c-ac8c-d35591405195
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.longhorniis6metabasenotinstalled(v=EXCHG.150)
ms:contentKeyID: 46628802
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# IIS 6 Compatibility components not installed\_LonghornIIS6MetabaseNotInstalled

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 Setup cannot continue its attempt to install the Client Access Server server role, the Mailbox server role, or the Exchange 2007 Administrative Tools on the following Windows operating systems:

  - Windows Server 2008 R2

  - Windows Server 2008

  - Windows 7 (Administrative Tools only)

  - Windows Vista (Administrative Tools only)

This problem occurs because the Internet Information Server (IIS) 6 Metabase Compatibility component and the IIS 6 Management Console component are not installed.

Exchange 2007 setup requires that the computer on which you are installing the Exchange 2007 Client Access server role, the Mailbox server role, or the Exchange 2007 Administrative Tools has the IIS 6 Metabase Compatibility component and the IIS 6 Management Console component installed.

To resolve this problem, install the IIS 6 Metabase Compatibility component on the destination computer, and then rerun Microsoft Exchange Setup.

**Install the IIS 6.0 Management Compatibility Components in Windows Server 2008 R2 or in Windows Server by using the Server Manager tool**

1.  Click **Start**, click **Administrative Tools**, and then click **Server Manager**.

2.  In the navigation pane, expand **Roles**, right-click **Web Server (IIS)**, and then click **Add Role Services**.

3.  In the **Select Role Services** pane, scroll down to **IIS 6 Management Compatibility**.

4.  Click to select the **IIS 6 Metabase Compatibility**, **IIS 6 WMI Compatibility**, and **IIS 6 Management Console** check boxes.

5.  In the **Select Role Services** pane, click **Next**.

6.  In the **Confirm Installations Selections** pane, click **Install**.

7.  Click **Close** to exit the Add Role Services wizard.

**Install the IIS 6.0 Management Compatibility Components in Windows 7 or in Windows Vista from Control Panel**

1.  Click **Start**, click **Control Panel**, click **Programs and Features**, and then click **Turn Windows features on or off**.

2.  Open **Internet Information Services**.

3.  Open **Web Management Tools**.

4.  Open **IIS 6.0 Management Compatibility**.

5.  Click to select the **IIS 6 Metabase and IIS 6 configuration compatibility**, **IIS 6 WMI Compatibility**, and **IIS 6 Management Console** check boxes.

6.  Click **OK**.

