---
title: 'Convert a Mailbox: Exchange 2013 Help'
TOCTitle: Convert a Mailbox
ms:assetid: dfed045e-a740-4a90-aff9-c58d53592f79
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ710164(v=EXCHG.150)
ms:contentKeyID: 49369579
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Convert a Mailbox

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Converting a mailbox to a different type of mailbox is very similar to the experience in Exchange 2010. You must still use the Set-Mailbox cmdlet in the Shell to do the conversion.

You can convert the following mailboxes from one type to another:

  - User mailbox to resource (room or equipment) mailbox

  - Shared mailbox to user mailbox

  - Shared mailbox to resource mailbox

  - Resource mailbox to user mailbox

  - Resource mailbox to shared mailbox

Note that if your organization uses a hybrid Exchange environment, you need to manage your mailboxes by using the on-premises Exchange management tools. To convert a mailbox in a hybrid environment, you might need to move the mailbox back to on-premises Exchange, convert the mailbox type, and then move it back to Office 365.


> [!IMPORTANT]
> If you are converting a user mailbox to a shared mailbox, you should either remove any mobile devices from the mailbox before the conversion, or you should block mobile access to the mailbox after the conversion. This is because once the mailbox is converted to a shared mailbox, mobile functionality will not work properly. For more information on blocking access, see <A href="https://go.microsoft.com/fwlink/p/?linkid=847873">Remove a former employee from Office 365</A>.



## Use the Shell to convert a mailbox

Estimated time to complete: 5 minutes.

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipient Provisioning Permissions" section in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

This example converts the shared mailbox, MarketingDept1 to a user mailbox.

    Set-Mailbox MarketingDept1 -Type Regular

You can use the following values for the *Type* parameter:

  - Regular

  - Room

  - Equipment

  - Shared

For detailed syntax and parameter information, see [Set-Mailbox](https://technet.microsoft.com/en-us/library/bb123981\(v=exchg.150\)).

## How do you know this worked?

To verify that you have successfully converted the mailbox, run the following Shell command:

    Get-Mailbox -Identity MarketingDept1 | Format-List RecipientTypeDetails

The value for *RecipientTypeDetails* should be *UserMailbox*.

For detailed syntax and parameter information, see [Get-Mailbox](https://technet.microsoft.com/en-us/library/bb123685\(v=exchg.150\)).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


