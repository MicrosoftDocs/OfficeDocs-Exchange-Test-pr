---
title: 'Re-create the Discovery system mailbox: Exchange 2013 Help'
TOCTitle: Re-create the Discovery system mailbox
ms:assetid: 5ae8426b-5661-4ecb-99c4-cdd342107fb1
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Gg588318(v=EXCHG.150)
ms:contentKeyID: 49289261
ms.date: 01/17/2018
mtps_version: v=EXCHG.150
---

# Re-create the Discovery system mailbox

 

_**Applies to:** Exchange Server 2013_


In-Place eDiscovery uses a system mailbox to store In-Place eDiscovery search metadata. This Discovery system mailbox has the display name **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}**. Because system mailboxes aren't visible in the Exchange Administration Center (EAC) or in Exchange address lists, they are rarely deleted inadvertently.

However, if the Discovery system mailbox is deleted accidentally, discovery managers will be unable to perform In-Place eDiscovery searches or manage existing searches. In this case, to enable eDiscovery functionality, you must re-create the Discovery system mailbox.

## What you should know before you begin

  - Estimated time to complete: 10 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipient Provisioning Permissions" section in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Use the Shell to re-create the Discovery system mailbox

1.  Delete the SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9} user account from Active Directory, if it exists. By default, Exchange Server 2013 Setup creates the mailbox in the Users container in Active Directory. For details about how to delete a user account from Active Directory, see [Delete a User Account](https://go.microsoft.com/fwlink/p/?linkid=215850).

2.  Use the Shell to enable the Discovery system mailbox.
    

    > [!NOTE]
    > You can't use the EAC to enable the Discovery system mailbox.<BR>The following command must be run from the same directory where you extracted the Exchange installation media.

    
    To re-create the Discovery system mailbox, run the following command:
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

## How do I know this worked?

To verify that you have successfully re-created the Discovery system mailbox, use the **Get-Mailbox** cmdlet with the *Arbitration* switch to retrieve system mailboxes. View the results of the command to verify that the system mailbox `SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}` has been re-created.


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


