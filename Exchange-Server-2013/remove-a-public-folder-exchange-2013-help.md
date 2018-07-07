---
title: 'Remove a public folder: Exchange 2013 Help'
TOCTitle: Remove a public folder
ms:assetid: 334b831d-e372-4d85-a407-5c8a5d0e78de
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997202(v=EXCHG.150)
ms:contentKeyID: 49289225
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Remove a public folder

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You may need to remove public folders that are no longer being used in your organization. To help determine which public folders should be removed, see [View statistics for public folders and public folder items](view-statistics-for-public-folders-and-public-folder-items-exchange-2013-help.md).

For additional management tasks related to managing public folders, see [Public folder procedures](public-folder-procedures-exchange-2013-help.md).

For additional management tasks related to public folders, see [Public folder procedures in Office 365 and Exchange Online](https://technet.microsoft.com/en-us/library/jj966272\(v=exchg.150\)).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Sharing and collaboration permissions](sharing-and-collaboration-permissions-exchange-2013-help.md) topic.

  - You can’t delete a mail-enabled public folder. Before you can delete it, you must first disable email for the public folder. For more information, see [Mail-enable or mail-disable a public folder](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the EAC to remove a public folder

1.  Navigate to **Public folders** \> **Public folders**.

2.  In the list view, select the public folder you want to delete. Note that clicking on the folder name will display sub-folders within that folder, if there are any. At that point you can click to select a specific sub-folder to remove.
    
    To delete a folder or sub-folder, click anywhere on the folder's row except the underlined name of the folder, and then click **Delete** ![Delete icon](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon"). If you click the underlined name of the folder, the **Delete** option will not be available to select.
    
    ![Selecting a public folder to remove](images/Aa997202.8666290d-3f19-4c70-afe3-45569762718b(EXCHG.150).png "Selecting a public folder to remove")  

3.  A warning box displays asking if you’re sure you want to delete the public folder. Click **Yes** to continue.

## Use the Shell to delete a public folder

This example deletes the public folder Help Desk\\Resolved. This command assumes that the Resolved public folder doesn’t have any subfolders.

    Remove-PublicFolder -Identity "\Help Desk\Resolved"

This example tests the previous command without making any modifications.

    Remove-PublicFolder -Identity "\HelpDesk\Resolved" -WhatIf

This example removes the public folder Marketing and all its subfolders because the command runs recursively.

    Remove-PublicFolder -Identity "\Marketing" -Recurse:$True

For detailed syntax and parameter information, see [Remove-PublicFolder](https://technet.microsoft.com/en-us/library/bb124894\(v=exchg.150\)).

