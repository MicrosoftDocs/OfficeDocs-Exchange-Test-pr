---
title: 'Create an address list by using recipient filters: Exchange 2013 Help'
TOCTitle: Create an address list by using recipient filters
ms:assetid: 8eabea64-97c6-40af-b61c-9b6a125cbdf1
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb123718(v=EXCHG.150)
ms:contentKeyID: 49289339
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Create an address list by using recipient filters

 

_**Applies to:** Exchange Online, Exchange Server 2013_


This topic explains how to create an address list by using recipient filters. To learn more about address lists, see [Address lists](address-lists-exchange-2013-help.md).

For additional management tasks related to address lists, see [Address list procedures](address-list-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Address lists" entry in the [Email address and address book permissions](email-address-and-address-book-permissions-exchange-2013-help.md) topic.

  - By default in Exchange Online, the Address List role isn’t assigned to any role groups. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see the "Add a role to a role group" section in the topic, [Manage role groups](manage-role-groups-exchange-2013-help.md).

  - To use the *RecipientFilter* parameter to create a custom filter, you must specify a string for the filter. The Shell uses OPATH for the filtering syntax. OPATH is a querying language designed to query object data sources.

  - You can’t use the Exchange Administration Center (EAC) to perform this procedure. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to create an address list by using recipient filters

This example creates an address list for all users with Exchange mailboxes who reside in Washington or Oregon.

    New-AddressList -Name "Pacific Northwest Mailboxes" -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

This example creates an address list for all users with Exchange mailboxes who have `AgencyB` as the value for the *CustomAttribute15* parameter.

    New-AddressList -Name "AgencyB" -RecipientFilter {(RecipientType -eq 'UserMailbox') -and (CustomAttribute15 -like *AgencyB*)}

For detailed syntax and parameter information, see [New-AddressList](https://technet.microsoft.com/en-us/library/aa996912\(v=exchg.150\)).

