---
title: 'Set up public folders in a new organization: Exchange 2013 Help'
TOCTitle: Set up public folders in a new organization
ms:assetid: 7b419906-8977-47f0-8687-a87911b5ebec
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ651147(v=EXCHG.150)
ms:contentKeyID: 49352795
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Set up public folders in a new organization

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


**Summary:** How to set up public folders, including assigning permissions to them in the EAC.

This topic shows you how to get public folders configured and running in a new organization or in an organization that has never previously had public folders.


> [!NOTE]
> For more information about the storage quotas and limits for public folders, see the following topics: 
> <UL>
> <LI>
> <P>For public folders in Office 365, see <A href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online Limits</A>.</P>
> <LI>
> <P>For public folders in on-premises Exchange Server 2013, see <A href="limits-for-public-folders-exchange-2013-help.md">Limits for public folders</A>.</P></LI></UL>



For additional management tasks related to public folders in Exchange Server 2013, see [Public folder procedures](public-folder-procedures-exchange-2013-help.md).

For additional management tasks related to public folders in Exchange Online, see [Public folder procedures in Office 365 and Exchange Online](https://technet.microsoft.com/en-us/library/jj966272\(v=exchg.150\)).

## What do you need to know before you begin?

  - Estimated time to complete this task: 30 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Sharing and collaboration permissions](sharing-and-collaboration-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## How do you do this?

## Step 1: Create the primary public folder mailbox

The primary public folder mailbox contains a writeable copy of the public folder hierarchy plus content and is the first public folder mailbox that you create for your organization. Subsequent public folder mailboxes will be secondary public folder mailboxes, which will contain a read-only copy of the hierarchy plus content.

For detailed steps, see [Create a public folder mailbox](create-a-public-folder-mailbox-exchange-2013-help.md).

## Step 2: Create your first public folder

For detailed steps, see [Create a public folder](create-a-public-folder-exchange-2013-help.md).

## Step 3: Assign permissions to the public folder

After you create the public folder, you’ll need to assign the **Owner** permissions level so that at least one user can access the public folder from the client and create subfolders. Any public folders created after this one will inherit the permissions of the parent public folder.

1.  In the Exchange admin center (EAC), navigate to **Public folders** \> **Public folders**.

2.  In the list view, select the public folder.

3.  In the details pane, under **Folder permissions**, click **Manage**.

4.  In **Public Folder Permissions**, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

5.  Click **Browse** to select a user.

6.  In the **Permission level** list, select a level. At least one user should be an **Owner**.

7.  Click **Save**.

8.  You can add multiple users by clicking **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") and assigning the appropriate permissions using the steps above. You can also customize the permission level by selecting or clearing the check boxes. When you edit a predefined permission level such as **Owner**, the permission level will change to **Custom**.

For information about how to use the Shell to assign permissions to a public folder, see [Add-PublicFolderClientPermission](https://technet.microsoft.com/en-us/library/bb124743\(v=exchg.150\)).

## Step 4 (Optional): Mail-enable the public folder

If you want users to send mail to the public folder, you can mail-enable it. This step is optional. If you don't mail-enable the public folder, users can post messages to the public folder by dragging items into it from within Outlook.

1.  In the EAC, navigate to **Public folders** \> **Public folders**.

2.  In the list view, select the public folder you want to mail-enable.

3.  In the details pane, under **Mail settings – Disabled**, click **Enable**.
    
    A warning displays asking if you are sure you want to enable mail for the public folder. Click **Yes**.

The public folder will be mail-enabled and the name of the public folder will become the alias of the public folder. If you have multiple recipients with that name, the public folder’s alias will be appended with a number. For example, if you have a distribution group named SalesTeam and you create a public folder named SalesTeam and then mail-enable it, the alias of that public folder will be SalesTeam1.

For information about how to use the Shell to mail-enable a public folder, see [Enable-MailPublicFolder](https://technet.microsoft.com/en-us/library/aa998824\(v=exchg.150\)).

