---
title: 'Create a public folder mailbox: Exchange 2013 Help'
TOCTitle: Create a public folder mailbox
ms:assetid: 64437ffd-231b-4c10-84df-232ccbe9538f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ552410(v=EXCHG.150)
ms:contentKeyID: 48679375
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Create a public folder mailbox

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


Before you can create a public folder, you must first create a public folder mailbox. Public folder mailboxes contain the hierarchy information plus the content for public folders. The first public folder mailbox you create will be the primary hierarchy mailbox, which contains the only writable copy of the hierarchy. Any additional public folder mailboxes you create will be secondary mailboxes, which contain a read-only copy of the hierarchy.


> [!NOTE]
> For more information about the storage quotas and limits for public folders, see the following topics: 
> <UL>
> <LI>
> <P>For public folders in Office 365, see <A href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online Limits</A>.</P>
> <LI>
> <P>For public folders in on-premises Exchange Server 2013, see <A href="limits-for-public-folders-exchange-2013-help.md">Limits for public folders</A>.</P></LI></UL>



For additional management tasks related to public folders in Exchange 2013, see [Public folder procedures](public-folder-procedures-exchange-2013-help.md).

For additional management tasks related to public folders in Exchange Online, see [Public folder procedures in Office 365 and Exchange Online](https://technet.microsoft.com/en-us/library/jj966272\(v=exchg.150\)).

## What do you need to know before you begin?

  - Estimated time to complete: less than 5 minutes.

  - Exchange 2013 public folders and public folders on legacy Exchange servers can't exist in the same organization. If you try to create a public folder mailbox when you still have legacy public folders, you'll receive the error **An existing Public Folder deployment has been detected. To migrate existing Public Folder data, create new Public Folder mailbox using -HoldForMigration switch.**
    
    Before you can create public folders in Exchange 2013, you need to migrate your legacy public folders to Exchange 2013. To do this, follow the steps in [Use serial migration to migrate public folders to Exchange 2013 from previous versions](https://technet.microsoft.com/en-us/library/jj150486\(v=exchg.150\)). These steps will show you how to create a public folder mailbox that can be used to store your migrated public folders.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Sharing and collaboration permissions](sharing-and-collaboration-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## What do you want to do?

## Use the EAC to create a public folder mailbox

1.  Navigate to **Public folders** \> **Public folder mailboxes**, and then click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

2.  In **Public Folder Mailbox**, provide a name for the public folder mailbox.

3.  Click **Save**.

## Use the Shell to create a public folder mailbox

This example creates the primary public folder mailbox.

    New-Mailbox -PublicFolder -Name MasterHierarchy

This example creates a secondary public folder mailbox. The only difference between creating the primary hierarchy mailbox and a secondary hierarchy mailbox is that the primary mailbox is the first one created in the organization. You can create additional public folder mailboxes for load balancing purposes.

    New-Mailbox -PublicFolder -Name Istanbul 

For detailed syntax and parameter information, see [New-Mailbox](https://technet.microsoft.com/en-us/library/aa997663\(v=exchg.150\)).

## How do you know this worked?

To verify that you have successfully created the primary public folder mailbox, run the following Shell command:

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

For detailed syntax and parameter information, see [Get-OrganizationConfig](https://technet.microsoft.com/en-us/library/aa997571\(v=exchg.150\)).

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

