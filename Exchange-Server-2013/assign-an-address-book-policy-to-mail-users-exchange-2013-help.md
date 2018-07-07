---
title: 'Assign an address book policy to mail users: Exchange 2013 Help'
TOCTitle: Assign an address book policy to mail users
ms:assetid: bdfe6575-24c0-47d0-9cfb-ece910db248b
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Hh529942(v=EXCHG.150)
ms:contentKeyID: 49289398
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Assign an address book policy to mail users

 

_**Applies to:** Exchange Online, Exchange Server 2013_


After you create an address book policy (ABP), you must assign it to mailbox users. Users aren’t assigned a default ABP when their user account is created. If you don’t assign an ABP to a user, the global address list (GAL) for your entire organization will be accessible to the user through Outlook and Outlook Web App. To learn more, see [Address book policies](address-book-policies-exchange-2013-help.md).

For additional management tasks related to ABPs, see [Address book policy procedures](address-book-policy-procedures-exchange-2013-help.md).

Interested in scenarios that use this procedure? See [Scenario: Deploying address book policies](scenario-deploying-address-book-policies-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estmated time to complete: Less than 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Address book policies" entry in the [Email address and address book permissions](email-address-and-address-book-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the EAC to assign an ABP to a mailbox user

1.  Navigate to **Recipients** \> **Mailboxes**.

2.  In the list view, select the user that you want to assign the policy to, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  Click **Mailbox features**.

4.  In the **Address book policy** list, select the ABP that you want to apply to this user.

5.  Click **Save**.

## Use the EAC to assign an ABP to multiple mailbox users

1.  Navigate to **Recipients** \> **Mailboxes**.

2.  In the list view use the Ctrl key to select multiple users.

3.  In the details pane, click **More options**.

4.  Under **Address Book Policy**, click **Update**.

5.  In the **Select Address Book Policy** list, select the ABP that you want to apply to these users.

6.  Click **Save**.

## Use the Shell to assign an ABP to mailbox users

This example assigns the ABP All Fabrikam to the existing mailbox user joe@fabrikam.com.

    Set-Mailbox -Identity joe@fabrikam.com -AddressBookPolicy "All Fabrikam"

This example assigns the ABP ABP\_EngineeringDepartment to all mailbox users whose `CustomAttribute11` value contains “Engineering Department”.

    Get-Mailbox -Filter {(CustomAttribute11 -like "Engineering Department")} | Set-Mailbox -AddressBookPolicy ABP_EngineeringDepartment

For detailed syntax and parameter information, see [Set-Mailbox](https://technet.microsoft.com/en-us/library/bb123981\(v=exchg.150\)) and [Get-Mailbox](https://technet.microsoft.com/en-us/library/bb123685\(v=exchg.150\)).

