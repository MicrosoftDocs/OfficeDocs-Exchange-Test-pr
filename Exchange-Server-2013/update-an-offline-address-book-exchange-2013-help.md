﻿---
title: 'Update an offline address book: Exchange 2013 Help'
TOCTitle: Update an offline address book
ms:assetid: 448a207e-41b4-4cef-9fe9-a68b81e2ec4e
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997684(v=EXCHG.150)
ms:contentKeyID: 49289240
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Update an offline address book

 

_**Applies to:** Exchange Server 2013_


After you create an OAB or modify OAB settings, the changes aren't available to users until the OAB generation (OABGen) process has completed.

For additional management tasks related to OABs, see [Offline address book procedures](offline-address-book-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Offline address books" entry in the [Email address and address book permissions](email-address-and-address-book-permissions-exchange-2013-help.md) topic.

  - You can’t use the Exchange Administration Center (EAC) to perform this procedure. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to update an OAB

This example updates the OAB named My OAB.

    Update-OfflineAddressBook -Identity "My OAB"

For detailed syntax and parameter information, see [Update-OfflineAddressBook](https://technet.microsoft.com/en-us/library/aa995979\(v=exchg.150\)).

