---
title: 'Add an address list to or remove an address list from an offline address book: Exchange 2013 Help'
TOCTitle: Add an address list to or remove an address list from an offline address book
ms:assetid: 86bd5651-ad41-4516-bf23-6579f4e4da03
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb123563(v=EXCHG.150)
ms:contentKeyID: 49289338
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Add an address list to or remove an address list from an offline address book

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can use the Shell to add or remove an address list from an offline address book (OAB). By default, there is an OAB named the Default Offline Address Book that contains the global address list (GAL). OABs are generated based on the address lists that they contain. To create custom OABs that users can download, you can add or remove address lists from OABs.

For additional management tasks related to OABs, see [Offline address book procedures](offline-address-book-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Offline address books" entry in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - By default in Exchange Online, the Address List role isn’t assigned to any role groups. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see the "Add a role to a role group" section in the topic, [Manage role groups](manage-role-groups-exchange-2013-help.md).

  - Changes to the address list aren't available for client download until after the OAB in which the address list resides has been generated. For more information, see [Update an offline address book](update-an-offline-address-book-exchange-2013-help.md).

  - You can’t use the Exchange Administration Center (EAC) to perform this procedure. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to add an address list to an OAB

When using the *AddressLists* parameter, any address lists that currently exist will be overwritten. You must include existing address lists when you use the *AddressLists* parameter to continue to generate those address lists in your OAB. This example, in which you have AddressList1 and AddressList2, adds AddressList3.

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2,AddressList3

For detailed syntax and parameter information, see [Set-OfflineAddressBook](https://technet.microsoft.com/en-us/library/aa996330\(v=exchg.150\)).

## Use the Shell to remove an address list from an OAB

To remove an address list from an OAB, simply omit that address list from the list of address lists. This example, in which you have AddressList1, AddressList2, and AddressList3, removes AddressList3.

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2

For detailed syntax and parameter information, see [Set-OfflineAddressBook](https://technet.microsoft.com/en-us/library/aa996330\(v=exchg.150\)).

