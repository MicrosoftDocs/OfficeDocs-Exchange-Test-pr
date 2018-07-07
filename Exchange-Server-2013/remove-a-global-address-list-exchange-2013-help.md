---
title: 'Remove a global address list: Exchange 2013 Help'
TOCTitle: Remove a global address list
ms:assetid: 65d75b69-641b-4a37-a63c-47cf018f5f22
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb232077(v=EXCHG.150)
ms:contentKeyID: 49289271
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Remove a global address list

 

_**Applies to:** Exchange Online, Exchange Server 2013_


The global address list (GAL) is a directory that contains entries for every group, user, and contact within an Exchange organization.

For additional management tasks related to address lists, see [Address list procedures](address-list-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Address lists" entry in the [Email address and address book permissions](email-address-and-address-book-permissions-exchange-2013-help.md) topic.

  - By default in Exchange Online, the Address List role isn’t assigned to any role groups. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see the "Add a role to a role group" section in the topic, [Manage role groups](manage-role-groups-exchange-2013-help.md).

  - You can't remove the default GAL.

  - You can’t use the Exchange Administration Center (EAC) to perform this procedure. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to remove a GAL

This example removes the GAL Fourth Coffee from the domain controller ad-server.fourthcoffee.com.

    Remove-GlobalAddressList -Identity "Fourth Coffee" -DomainController ad-server.fourthcoffee.com

To confirm that you want to remove the GAL, type **Y**, and then press ENTER.

For detailed syntax and parameter information, see [Remove-GlobalAddressList](https://technet.microsoft.com/en-us/library/bb124368\(v=exchg.150\)).

