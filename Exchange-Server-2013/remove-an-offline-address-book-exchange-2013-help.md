---
title: 'Remove an offline address book: Exchange 2013 Help'
TOCTitle: Remove an offline address book
ms:assetid: d69f1e8a-b3cb-4739-90cd-85ea450d06f3
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124744(v=EXCHG.150)
ms:contentKeyID: 49289424
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Remove an offline address book

 

_**Applies to:** Exchange Online, Exchange Server 2013_


This topic explains how to remove an offline address book (OAB).

For additional management tasks related to OABs, see [Offline address book procedures](offline-address-book-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Offline address books" entry in the [Email address and address book permissions](email-address-and-address-book-permissions-exchange-2013-help.md) topic.

  - By default in Exchange Online, the Address List role isn’t assigned to any role groups. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see the "Add a role to a role group" section in the topic, [Manage role groups](manage-role-groups-exchange-2013-help.md).

  - After you remove an OAB that's linked to a user or to a mailbox database, the recipient will download the default OAB until you assign a new OAB for that user. If you remove the default OAB, you must assign a different OAB as the default OAB. For instructions about how to change the default OAB, see [Change the default offline address book](change-the-default-offline-address-book-exchange-2013-help.md).

  - You can’t use the Exchange Administration Center (EAC) to perform this procedure. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to remove an OAB

This example removes an OAB named My OAB.

    Remove-OfflineAddressBook -Identity "My OAB"

Type **Y** to confirm that you want to remove the OAB, and then press ENTER.

For detailed syntax and parameter information, see [Remove-OfflineAddressBook](https://technet.microsoft.com/en-us/library/bb123594\(v=exchg.150\)).

