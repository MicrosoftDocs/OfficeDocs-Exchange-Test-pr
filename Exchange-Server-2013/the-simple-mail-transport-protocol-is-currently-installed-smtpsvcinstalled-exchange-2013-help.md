---
title: 'The Simple Mail Transport Protocol is currently installed_SMTPSvcInstalled: Exchange 2013 Help'
TOCTitle: The Simple Mail Transport Protocol is currently installed_SMTPSvcInstalled
ms:assetid: f786a93c-876d-4f4e-adb6-4dfea3d820d1
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.smtpsvcinstalled(v=EXCHG.150)
ms:contentKeyID: 46629208
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# The Simple Mail Transport Protocol is currently installed\_SMTPSvcInstalled

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 setup cannot continue because the Microsoft Windows Server™ 2003 Simple Mail Transfer Protocol (SMTP) service is installed on this computer.

Microsoft Exchange setup requires that the SMTP service not be installed on servers that are used for Exchange 2007.

To resolve this issue, uninstall the SMTP service and rerun Microsoft Exchange setup.

**To uninstall the SMTP service by using Add or Remove a Windows Component in Control Panel**

1.  On the **Start** menu, click **Control Panel**.

2.  Double-click **Add or Remove Programs**.

3.  Click **Add/Remove Windows Components**.

4.  In the **Components** list, select the **Application Server** check box and then click **Details**.

5.  Select **Internet Information Services Manager** and then click **Details**.

6.  Select **SMTP Service** and then click to clear the check box.

7.  Click **OK** two times to return to the **Components** list and then click **Next**.

8.  Click **Finish** when the SMTP service is uninstalled.

