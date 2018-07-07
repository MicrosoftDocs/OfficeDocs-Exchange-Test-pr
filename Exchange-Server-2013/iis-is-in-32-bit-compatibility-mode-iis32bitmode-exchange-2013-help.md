---
title: 'IIS is in 32-bit compatibility mode_IIS32BitMode: Exchange 2013 Help'
TOCTitle: IIS is in 32-bit compatibility mode_IIS32BitMode
ms:assetid: 742dfc32-353c-46a2-830e-68aed6a68ce0
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.iis32bitmode(v=EXCHG.150)
ms:contentKeyID: 46628968
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# IIS is in 32-bit compatibility mode\_IIS32BitMode

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 setup cannot continue because the Microsoft Internet Information Service (IIS) is running in 32-bit mode on this 64-bit computer.

Exchange 2007 requires that IIS be in full 64-bit mode when it runs on a 64-bit computer.

To resolve this issue, switch IIS to 64-bit mode, and then rerun Microsoft Exchange setup.

**To switch IIS to 64-bit mode**

1.  Open a command prompt.

2.  Type the following:
    
    **cscript c:\\inetpub\\adminscripts\\adsutil.vbs SET /w3svc/AppPools/Enable32BitAppOnWin64 False**

3.  Press enter

