---
title: 'Create a public folder: Exchange 2013 Help'
TOCTitle: Create a public folder
ms:assetid: 6d252e60-c8d0-4efd-b9d7-ba5284a6f8ab
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb691104(v=EXCHG.150)
ms:contentKeyID: 48679376
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.PublicFolders.NewPublicFolderWizardForm.NewPublicFolderWizardPage
---

# Create a public folder

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Public folders are designed for shared access and provide an easy and effective way to collect, organize, and share information with other people in your workgroup or organization.

By default, a public folder inherits the settings of its parent folder, including the permissions settings.


> [!NOTE]
> For more information about the storage quotas and limits for public folders, see the following topics: 
> <UL>
> <LI>
> <P>For public folders in Office 365, see <A href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online Limits</A>.</P>
> <LI>
> <P>For public folders in on-premises Exchange Server 2013, see <A href="limits-for-public-folders-exchange-2013-help.md">Limits for public folders</A>.</P></LI></UL>



For additional management tasks related to managing public folders, see [Public folder procedures](public-folder-procedures-exchange-2013-help.md).

For additional management tasks related to public folders, see [Public folder procedures in Office 365 and Exchange Online](https://technet.microsoft.com/en-us/library/jj966272\(v=exchg.150\)).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Sharing and collaboration permissions](sharing-and-collaboration-permissions-exchange-2013-help.md) topic.

  - You can’t create a public folder unless you’ve first created a public folder mailbox. For more information about how to create a public folder mailbox, see [Create a public folder mailbox](create-a-public-folder-mailbox-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## What do you want to do?

## Use the EAC to create a public folder

When using the EAC to create a public folder, you’ll only be able to set the name and the path of the public folder. To configure additional settings, you’ll need to edit the public folder after it’s created.

1.  Navigate to **Public folders** \> **Public folders**.

2.  If you want to create this public folder as a child of an existing public folder, click the existing public folder in the list view. If you want to create a top-level public folder, skip this step.

3.  Click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

4.  In **Public Folder**, type the name of the public folder.
    

    > [!IMPORTANT]
    > Don't use a backslash (\) in the name when creating a public folder.



5.  In the **Path** box, verify the path to the public folder. If this isn’t the desired path, click **Cancel** and follow Step 2 of this procedure.

6.  Click **Save**.

## Use the Shell to create a public folder

This example creates a public folder named Reports in the path Marketing\\2013.

    New-PublicFolder -Name Reports -Path \Marketing\2013


> [!IMPORTANT]
> Don't use a backslash (\) in the name when creating a public folder.



For detailed syntax and parameter information, see [New-PublicFolder](https://technet.microsoft.com/en-us/library/aa996405\(v=exchg.150\)).

## How do you know this worked?

To verify that you’ve successfully created a public folder, do the following:

  - In the EAC, click **Refresh** to refresh the list of public folders. Your new public folder should be displayed in the list.

  - In the Shell, run any of the following commands:
    
        Get-PublicFolder -Identity \Marketing\2013\Reports | Format-List
    
        Get-PublicFolder -Identity \Marketing\2013 -GetChildren
    
        Get-PublicFolder -Recurse


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


