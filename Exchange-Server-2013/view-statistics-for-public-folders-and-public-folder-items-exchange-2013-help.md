---
title: 'View statistics for public folders and public folder items: Exchange 2013 Help'
TOCTitle: View statistics for public folders and public folder items
ms:assetid: 4e412710-9a74-4649-ab01-502e969a7eda
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997949(v=EXCHG.150)
ms:contentKeyID: 49289249
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# View statistics for public folders and public folder items

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


This topic explains how to retrieve statistics about a public folder, such as the display name, creation time, last user modified time, last user access, and item size. You can use this information to make decisions about deleting or retaining public folders.


> [!NOTE]
> In the Exchange admin center (EAC), you can view some of the quota and usage information for public folders by navigating to <STRONG>Public Folders</STRONG> &gt; <STRONG>Edit</STRONG> <IMG title="Edit icon" alt="Edit icon" src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif"> &gt; <STRONG>Mailbox usage</STRONG>. However, this information is incomplete, and we recommend that you use the Shell to view public folder statistics.



For additional management tasks related to managing public folders, see [Public folder procedures](public-folder-procedures-exchange-2013-help.md).

For additional management tasks related to public folders, see [Public folder procedures in Office 365 and Exchange Online](https://technet.microsoft.com/en-us/library/jj966272\(v=exchg.150\)).

## What do you need to know before you begin?

  - Estimated time to complete: 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Sharing and collaboration permissions](sharing-and-collaboration-permissions-exchange-2013-help.md) topic.

  - You can't use the EAC to retrieve public folder statistics.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to retrieve public folder statistics

This example returns the statistics for the public folder Marketing with a piped command to format the list.

    Get-PublicFolderStatistics -Identity \Marketing | Format-List


> [!NOTE]
> The value for the <EM>Identity</EM> parameter must include the path to the public folder. For example, if the public folder Marketing existed under the parent folder Business, you would provide the following value: <CODE>\Business\Marketing</CODE>



For detailed syntax and parameter information, see [Get-PublicFolderStatistics](https://technet.microsoft.com/en-us/library/aa998663\(v=exchg.150\)).

## Use the Shell to view statistics for public folder items

You can view the following information about items within a public folder:

  - Type of item

  - Subject

  - Last user modification time

  - Last user access time

  - Creation time

  - Attachments

  - Message size

You can use this information to make decisions about what actions to take for your public folders, such as which public folders to delete. For example, you may want to delete a public folder if the items haven't been accessed for over two years, or you may want to convert a public folder that's being used as a document repository to another client access application.

This example returns default statistics for all items in the public folder Pamphlets under the path \\Marketing\\2013. Default information includes item identity, creation time, and subject.

    Get-PublicFolderItemStatistics -Identity "\Marketing\2013\Pamphlets"

This example returns additional information about the items within the public folder Pamphlets, such as subject, last modification time, creation time, attachments, message size, and the type of item. It also includes a piped command to format the list.

    Get-PublicFolderItemStatistics -Identity "\Marketing\2010\Pamphlets" | Format-List

For detailed syntax and parameter information, see [Get-PublicFolderItemStatistics](https://technet.microsoft.com/en-us/library/ee332344\(v=exchg.150\)).

## Use the Shell to export the output of the Get-PublicFolderItemStatistics cmdlet to a .csv file

This example exports the output of the cmdlet to the PFItemStats.csv file that includes the following information for all items within the public folder \\Marketing\\Reports:

  - Subject of the message (`Subject`)

  - Date and time that the item was last modified (`LastModificationTime`)

  - Whether the item has attachments (`HasAttachments`)

  - Type of item (`ItemType)`

  - Size of the item (`MessageSize`)

<!-- end list -->

    Get-PublicFolderItemStatistics -Identity "\Marketing\Reports" | Select Subject,LastModificationTime,HasAttachments,ItemType,MessageSize | Export-CSV C:\PFItemStats.csv

For detailed syntax and parameter information, see [Get-PublicFolderItemStatistics](https://technet.microsoft.com/en-us/library/ee332344\(v=exchg.150\)).

