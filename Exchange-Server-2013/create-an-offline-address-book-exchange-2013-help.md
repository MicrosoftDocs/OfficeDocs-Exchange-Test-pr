---
title: 'Create an offline address book: Exchange 2013 Help'
TOCTitle: Create an offline address book
ms:assetid: b57bb4ce-5b6e-4702-a2f8-04bf3898a861
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124339(v=EXCHG.150)
ms:contentKeyID: 49289380
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewOabWizardForm.OabIntroductionWizardPage
---

# Create an offline address book

 

_**Applies to:** Exchange Online, Exchange Server 2013_


An offline address book (OAB) in Exchange Server 2013 is a downloaded copy of an address book that allows an Outlook user to access the information while disconnected from the server. Exchange administrators can decide which address books are made available to users who work offline, and they can also configure the method by which the address books are distributed (web-based distribution or public folder distribution).

For additional management tasks related to OABs, see [Offline address book procedures](offline-address-book-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Offline address books" entry in the [Email address and address book permissions](email-address-and-address-book-permissions-exchange-2013-help.md) topic.

  - By default in Exchange Online, the Address List role isn’t assigned to any role groups. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see the "Add a role to a role group" section in the topic, [Manage role groups](manage-role-groups-exchange-2013-help.md).

  - You can’t use the Exchange Administration Center (EAC) to perform this procedure. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to create an OAB with web-based distribution

This example creates an OAB named OAB\_Contoso that uses web-based distribution for Outlook 2007 or later clients by using the default virtual directory.

    New-OfflineAddressBook -Name "OAB_Contoso" -AddressLists "\Default Global Address List" -VirtualDirectories $Null -GlobalWebDistributionEnabled $True

For detailed syntax and parameter information, see [New-OfflineAddressBook](https://technet.microsoft.com/en-us/library/bb123692\(v=exchg.150\)).

