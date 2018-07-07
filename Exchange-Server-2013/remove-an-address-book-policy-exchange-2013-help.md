---
title: 'Remove an address book policy: Exchange 2013 Help'
TOCTitle: Remove an address book policy
ms:assetid: c20c6f82-2f75-4116-9be1-c5af10113f71
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Hh529946(v=EXCHG.150)
ms:contentKeyID: 49289401
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Remove an address book policy

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Use this procedure to remove an address book policy (ABP).

For additional management tasks related to ABPs, see [Address book policy procedures](address-book-policy-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Address book policies" entry in the [Email address and address book permissions](email-address-and-address-book-permissions-exchange-2013-help.md) topic.

  - You can’t remove an ABP if it’s assigned to a user’s mailbox or to a soft-deleted mailbox. To determine if an ABP is assigned to a user, run the following Shell command:
    
    `Get-Mailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`
    
    To determine if an ABP is assigned to a soft-deleted mailbox, run the following command:
    
    `Get-Mailbox -SoftDeletedMailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`

  - To remove an ABP from a user’s mailbox, you can use the **Mailbox features** page of the mailbox’s properties or the **Set-Mailbox** cmdlet.

  - You can’t use the Exchange Administration Center (EAC) to remove an ABP. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to remove an ABP

This example removes the ABP ABP\_TailspinToys.

    Remove-AddressBookPolicy -Identity "ABP_TailspinToys"

For detailed syntax and parameter information, see [Remove-AddressBookPolicy](https://technet.microsoft.com/en-us/library/hh529929\(v=exchg.150\)).

