---
title: 'Configure offline address book distribution properties: Exchange 2013 Help'
TOCTitle: Configure offline address book distribution properties
ms:assetid: 8df985e9-75ba-47ea-9cc3-aa98a5d8acf4
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb123710(v=EXCHG.150)
ms:contentKeyID: 49289344
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.ClientAccess.OabDistributionGeneralPage
---

# Configure offline address book distribution properties

 

_**Applies to:** Exchange Online, Exchange Server 2013_


For each offline address book (OAB) distribution point in Exchange, you can configure two URLs—an internal URL that can be accessed only from your internal corporate network and an external URL that can be accessed from the Internet.

For additional management tasks related to OABs, see [Offline address book procedures](offline-address-book-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Offline address books" entry in the [Email address and address book permissions](email-address-and-address-book-permissions-exchange-2013-help.md) topic.

  - You can’t use the Exchange Administration Center (EAC) to perform this procedure. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to configure OAB distribution properties

This example sets the polling interval for OAB distribution on the OAB virtual directory OAB (Default Web Site) to six hours.

    Set-OABVirtualDirectory "OAB (Default Web Site)" -PollInterval 360

This example sets the external distribution point to https://contoso.com/OAB for the default OAB virtual directory OAB (Default Web Site).

    Set-OABVirtualDirectory "OAB (Default Web Site)" -ExternalUrl https://contoso.com/OAB

For detailed syntax and parameter information, see [Set-OabVirtualDirectory](https://technet.microsoft.com/en-us/library/bb124707\(v=exchg.150\)).

## For More Information

[Offline address books](offline-address-books-exchange-2013-help.md)

