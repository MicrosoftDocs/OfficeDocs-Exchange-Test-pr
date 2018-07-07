---
title: 'Find the internal and external URLs for the Exchange admin center: Exchange 2013 Help'
TOCTitle: Find the internal and external URLs for the Exchange admin center
ms:assetid: 3ddb30ff-a405-4b9d-8d77-2d7a3a5ab8fa
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ680108(v=EXCHG.150)
ms:contentKeyID: 49558154
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Find the internal and external URLs for the Exchange admin center

 

_**Applies to:** Exchange Server 2013_


Because the Exchange admin center (EAC) is a web-based management console in Exchange Server 2013, you access it by using the ECP virtual directory URL in a web browser. This topic shows you how to find the ECP virtual directory URL.


> [!NOTE]
> The ECP is the web-based user interface developed for Exchange Server 2010. The EAC cmdlets for virtual directories still use “ECP” in the name, and these cmdlets can be used to manage Exchange 2010 and Exchange 2013 ECP virtual directories.



To learn more about the EAC, see [Exchange admin center in Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You can’t use the EAC to perform this procedure. You must use the Shell.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Exchange Administration Center connectivity" entry in the [Exchange and Shell infrastructure permissions](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to find the internal and external URLs for the ECP virtual directory

This example returns the ECP virtual directory name, internal URL, and external URL in a formatted list.

    Get-ECPVirtualDirectory | Format-List Name,InternalURL,ExternalURL

When the command is completed, use the *InternalURL* or *ExternalURL* values in your web browser to launch the EAC.

For detailed syntax and parameter information, see [Get-EcpVirtualDirectory](https://technet.microsoft.com/en-us/library/dd351058\(v=exchg.150\)).

