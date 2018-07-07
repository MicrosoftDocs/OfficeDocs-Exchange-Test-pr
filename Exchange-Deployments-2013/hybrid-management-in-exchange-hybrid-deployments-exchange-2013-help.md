---
title: 'Hybrid management in Exchange hybrid deployments: Exchange 2013 Help'
TOCTitle: Hybrid management in Exchange hybrid deployments
ms:assetid: 233f9f34-3ff5-47e1-a9e8-3244ee868d6e
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ659048(v=EXCHG.150)
ms:contentKeyID: 49345015
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Hybrid management in Exchange hybrid deployments

 

_**Applies to:** Exchange Server 2013, Exchange Server 2016_


When you install an Exchange server, the Exchange management tools are automatically installed on the server. You’ll use the following tools to configure and manage both the on-premises Exchange and the Exchange Online organization:

  - **Exchange admin center**   The EAC is a web-based management console that allows for ease of use and is optimized for on-premises, online, or hybrid Exchange deployments. The EAC replaces the Exchange Management Console (EMC) and the Exchange Control Panel (ECP), which were the interfaces used to manage Exchange Server 2010.

  - **Exchange Management Shell**   The Exchange Management Shell is a Windows PowerShell-based command-line interface.

## The Exchange admin center

The EAC enables you to perform many deployment tasks and most common day-to-day administrative tasks on both the on-premises Exchange servers and the Exchange Online organization. It's installed by default on every Exchange 2013 or newer server. In addition, because it’s a web-based management console, you can also access it by using a web browser on other computers in your network or via the Internet by using the ECP virtual directory URL.

You access the Exchange Online organization in the EAC by selecting the Office 365 cross-premises navigation tab. The cross-premises navigation allows you to easily switch between your Exchange Online and your on-premises Exchange organizations. If you’ve configured a hybrid deployment, selecting the Office 365 tab allows you to manage the Exchange Online organization and recipient objects. If you don’t have an Exchange Online organization, selecting the Office 365 link will direct you to the Office 365 sign-up page.

For more information about the EAC, see [Exchange admin center in Exchange 2013](https://technet.microsoft.com/en-us/library/jj150562\(v=exchg.150\)).

## The Exchange Management Shell

The Exchange Management Shell enables you to perform any task that the EAC does and some additional tasks that can only be performed in the Exchange Management Shell. The Exchange Management Shell is a collection of Windows PowerShell scripts and cmdlets that are installed on a computer when the Exchange management tools are installed. These scripts and cmdlets are only loaded when you open the Exchange Management Shell using the Exchange Management Shell icon. If you open Windows PowerShell directly, the Exchange scripts and cmdlets aren't loaded and you won't be able to manage your on-premises organization.


> [!NOTE]
> You can create a manual Windows PowerShell connection to your local on-premises organization, similar to how you manually connect to the Exchange Online organization below. However, we strongly recommend that you use the Exchange Management Shell icon to open the Exchange Management Shell to manage your on-premises Exchange servers.



When you open the Exchange Management Shell using the Exchange Management Shell icon on a computer that has the management tools installed, you can manage your on-premises organization. However, you can't manage the Exchange Online organization when you open the Exchange Management Shell using this icon. This is because opening the Exchange Management Shell using the Exchange Management Shell icon automatically connects you to a local Exchange server.

If you want to manage the Exchange Online organization using Windows PowerShell, you must open Windows PowerShell directly and not via the Exchange Management Shell icon. When you open Windows PowerShell, you can then manually specify where you want to connect. When you create a manual connection, you specify an administrator account in the Office 365 tenant organization, and then you run a command to create a connection. When the connection is established, the Exchange cmdlets you have permissions to run are made available to you. Learn more at [Use Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=209660).

If you're new to the Exchange Management Shell and want to learn the basics about how the Exchange Management Shell works, command syntax, and more, see [Using PowerShell with Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/en-us/library/bb123778\(v=exchg.150\)).

