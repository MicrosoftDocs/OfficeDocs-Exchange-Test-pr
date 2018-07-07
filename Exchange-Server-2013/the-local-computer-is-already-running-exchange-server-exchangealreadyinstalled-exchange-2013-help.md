---
title: 'The local computer is already running Exchange Server_ExchangeAlreadyInstalled: Exchange 2013 Help'
TOCTitle: The local computer is already running Exchange Server_ExchangeAlreadyInstalled
ms:assetid: 3f168b5d-9910-418f-86fb-e99d852dcb5e
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.exchangealreadyinstalled(v=EXCHG.150)
ms:contentKeyID: 46628873
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# The local computer is already running Exchange Server\_ExchangeAlreadyInstalled

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 setup cannot continue because the local computer has previous Microsoft Exchange components installed.

Exchange 2007 setup requires that the local computer not have existing Microsoft Exchange components installed.

To resolve this issue, remove any Microsoft Exchange 2000 Server or Microsoft Exchange Server 2003 components, and then rerun Microsoft Exchange setup.

**To remove Microsoft Exchange components**

1.  Click **Start**, point to **Settings**, and then click **Control Panel**.

2.  Double-click **Add or Remove Programs**.

3.  In the **Currently installed programs** list, click **Microsoft Exchange**, and then click **Change/Remove**.

4.  In Microsoft Exchange Installation Wizard, click **Next**.

5.  In the Action list on the Component Selection page, click the down arrow next to each component that has been installed, and then click **Remove**.
    

    > [!NOTE]
    > Installed components have a check mark in the Action list. When you click <STRONG>Remove</STRONG>, the check mark is replaced by the word <STRONG>Remove</STRONG>.



6.  Click **Next** two times.

7.  Click **Finish**.

