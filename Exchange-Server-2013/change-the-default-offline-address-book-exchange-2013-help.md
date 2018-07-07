---
title: 'Change the default offline address book: Exchange 2013 Help'
TOCTitle: Change the default offline address book
ms:assetid: 61abf78e-2543-4431-acc8-839e3c7a4548
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998569(v=EXCHG.150)
ms:contentKeyID: 49289273
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Change the default offline address book

 

_**Applies to:** Exchange Online, Exchange Server 2013_


By default, when you install the Mailbox server role, a Web-based default offline address book (OAB) named Default Offline Address Book is created. You can set any OAB in your Exchange organization as the default OAB. This new default OAB is associated with all newly created mailbox databases. You can have only one default OAB in your organization. If you delete the default OAB, Microsoft Exchange doesn't automatically assign another OAB as the default. You must manually designate another OAB as the default.

For additional management tasks related to OABs, see [Offline address book procedures](offline-address-book-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Offline address books" entry in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - By default in Exchange Online, the Address List role isn’t assigned to any role groups. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see the "Add a role to a role group" section in the topic, [Manage role groups](manage-role-groups-exchange-2013-help.md).

  - You can’t use the Exchange Administration Center (EAC) to perform this procedure. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to change the default OAB

This example sets the OAB named My OAB as the default OAB.

    Set-OfflineAddressBook -Identity "My OAB" -IsDefault $true

For detailed syntax and parameter information, see [Set-OfflineAddressBook](https://technet.microsoft.com/en-us/library/aa996330\(v=exchg.150\)).

