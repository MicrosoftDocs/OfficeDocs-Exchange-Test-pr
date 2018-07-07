---
title: 'Configure global address list properties: Exchange 2013 Help'
TOCTitle: Configure global address list properties
ms:assetid: 5fd2c96f-fe93-4b5a-8495-70c450511a37
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb232068(v=EXCHG.150)
ms:contentKeyID: 49289268
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure global address list properties

 

_**Applies to:** Exchange Online, Exchange Server 2013_


This topic explains how to modify the settings of a global address list (GAL).

For additional management tasks related to address lists, see [Address list procedures](address-list-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Address lists" entry in the [Email address and address book permissions](email-address-and-address-book-permissions-exchange-2013-help.md) topic.

  - By default in Exchange Online, the Address List role isn’t assigned to any role groups. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see the "Add a role to a role group" section in the topic, [Manage role groups](manage-role-groups-exchange-2013-help.md).

  - You can't edit the settings of the default GAL.

  - You can’t use the Exchange Administration Center (EAC) to perform this procedure. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to configure GAL properties

This example assigns a new name, FourthCoffee, to the GAL that has the GUID 96d0c505-eba8-4103-ad4f-577a1bf4ad7b.

    Set-GlobalAddressList -Identity 96d0c505-eba8-4103-ad4f-577a1bf4ad7b -Name FourthCoffee


> [!NOTE]
> If you're using precanned conditional filter properties, the value for the <EM>IncludedRecipients</EM> parameter can't be blank.



This example changes the recipients who will be included in the Fourth Coffee global GAL to those whose company is set to Fourth Coffee.

    Set-GlobalAddressList -Identity Fourth Coffee -RecipientFilter {Company -eq "Fourth Coffee"}

For detailed syntax and parameter information, see [Set-GlobalAddressList](https://technet.microsoft.com/en-us/library/bb123877\(v=exchg.150\)).

