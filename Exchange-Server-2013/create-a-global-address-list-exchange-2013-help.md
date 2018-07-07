---
title: 'Create a global address list: Exchange 2013 Help'
TOCTitle: Create a global address list
ms:assetid: 59e4955a-8999-4d17-be9f-23a41a23b929
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb232063(v=EXCHG.150)
ms:contentKeyID: 49289257
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Create a global address list

 

_**Applies to:** Exchange Online, Exchange Server 2013_


The global address list (GAL) is a directory that contains entries for every group, user, and contact within an organization's implementation of Microsoft Exchange. If your organization uses address book policies, you may want to create additional GALs. To learn more, see [Address book policies](address-book-policies-exchange-2013-help.md).

For additional management tasks related to address lists, see [Address list procedures](address-list-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Address lists" entry in the [Email address and address book permissions](email-address-and-address-book-permissions-exchange-2013-help.md) topic.

  - By default in Exchange Online, the Address List role isn’t assigned to any role groups. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see the "Add a role to a role group" section in the topic, [Manage role groups](manage-role-groups-exchange-2013-help.md).

  - You can’t use the Exchange Administration Center (EAC) to perform this procedure. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to create a GAL using conditional filter properties

This example creates a GAL named GAL\_Contoso that includes recipients who are mailbox users and have their company listed as Contoso.

    New-GlobalAddressList -Name "GAL_Contoso" -IncludedRecipients MailboxUsers -ConditionalCompany Contoso


> [!NOTE]
> If you’re using precanned conditional filter properties, the <EM>IncludedRecipients</EM> parameter can't be blank.



For detailed syntax and parameter information, see [New-GlobalAddressList](https://technet.microsoft.com/en-us/library/bb123785\(v=exchg.150\)).

## Use the Shell create a GAL using a recipient filter

This example creates a GAL named GAL\_AgencyA that includes recipients for which the *CustomAttribute15* parameter has a value of `AgencyA`.

    New-GlobalAddressList -Name "GAL_AgencyA" -RecipientFilter {CustomAttribute15 -like "AgencyA"}

For detailed syntax and parameter information, see [New-GlobalAddressList](https://technet.microsoft.com/en-us/library/bb123785\(v=exchg.150\)).

