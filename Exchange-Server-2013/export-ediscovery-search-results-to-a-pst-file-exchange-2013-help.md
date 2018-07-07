---
title: 'Export eDiscovery search results to a PST file: Exchange 2013 Help'
TOCTitle: Export eDiscovery search results to a PST file
ms:assetid: bc47f5f9-d056-4b69-b669-ae65fad541c8
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn440164(v=EXCHG.150)
ms:contentKeyID: 57793072
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Export eDiscovery search results to a PST file

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can use the eDiscovery Export tool in the Exchange admin center (EAC) to export the results of an In-Place eDiscovery search to an Outlook Data File, which is also called a PST file. Administrators can distribute the results of the search to other people within your organization, such as a human resources manager or records manager, or to opposing counsel in a legal case. After search results are exported to a PST file, you or other users can open them in Outlook to review or print messages returned in the search results. PST files can also be opened in third-party eDiscovery and reporting applications. This topic shows you how to do this, as well as troubleshoot any issues you might have.

## What do you need to know before you begin?

  - Estimated time to complete: Time will vary based on the amount and size of the search results that will be exported.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "In-Place eDiscovery" entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

  - The computer you use to export search results to a PST file must meet the following system requirements:
    
      - 32- or 64-bit versions of Windows 7 and later versions
    
      - Microsoft .NET Framework 4.7
    
      - A supported browser:
        
          - Internet Explorer 10 and later versions
            
            OR
        
          - Mozilla Firefox or Google Chrome. If you use either of these browsers, be sure you install the *ClickOnce* extension. To install the ClickOnce add-in, see [Mozilla ClickOnce add-ons](https://addons.mozilla.org/en-us/firefox/search/?q=clickonce%26cat=1%2c0%26appver=%26platform=) or [ClickOnce for Google Chrome](https://chrome.google.com/webstore/search/clickonce?_category=extensions).

  - You need an active mailbox attached to the account you wish to export.

  - Ensure that the local Intranet settings are setup correctly in Internet Explorer. Make sure that **https://\*.outlook.com** is added to the Local intranet zone.

  - Make sure the following URLS are not listed in the Trusted sites zone:
    
      - https://\*.outlook.com
    
      - https://r4.res.outlook.com
    
      - https://\*.res.outlook.com

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Exchange admin center to export In-Place eDiscovery search results to a PST

1.  Go to **Compliance management** \> **In-place eDiscovery & hold**.

2.  In the list view, select the In-Place eDiscovery search you want to export the results of, and then click **Export to a PST file**.
    
    ![Export to a PST File](images/Dn440164.1ebee2ac-89b3-49fa-b70c-a07c9a65f958(EXCHG.150).gif "Export to a PST File")  

3.  In the **eDiscovery PST Export Tool** window, do the following:
    
      - Click **Browse** to specify the location where you want to download the PST file.
    
      - Click the **Enable deduplication** checkbox to exclude duplicate messages. Only a single instance of a message will be included in the PST file.
    
      - Click the **Include unsearchable items** checkbox to include mailbox items that couldn’t be searched (for example, messages with attachments of file types that couldn’t be indexed by Exchange Search). Unsearchable items are exported to a separate PST file.
        

        > [!IMPORTANT]
        > Including unsearchable items when you export eDiscovery search results takes longer when mailboxes contain a lot of unsearchable items. To reduce the time it takes to export search results and prevent large PST export files, consider the following recommendations: 
        > <UL>
        > <LI>
        > <P>Create multiple eDiscovery searches that each search a fewer number of source mailboxes.</P>
        > <LI>
        > <P>If you’re exporting all mailbox content within a specific date range (by not specifying any keywords in the search criteria), then all unsearchable items within that date range will be automatically included in the search results. Therefore, don’t select the <STRONG>Include unsearchable items</STRONG> checkbox.</P></LI></UL>



4.  Click **Start** to export the search results to a PST file.
    
    A window is displayed that contains status information about the export process.

## More information

  - You can reduce the size of the PST export fileby exporting only the unsearchable items. To do this, create or edit a search, specify a start date in the future, and then remove any keywords from the **Keywords** box. This will result in no search results being returned. When you copy or export the search results and select the **Include unsearchable items** checkbox, only the unsearchable items will be copied to the discovery mailbox or exported to a PST file.

  - If you enable de-duplication, all search results are exported in a single PST file. If you don’t enable de-duplication, a separate PST file is exported for each mailbox included in the search. And as previously stated, unsearchable items are exported to a separate PST file.

  - In addition to the PST files that contain the search results, two other files are also exported:
    
      - A configuration file (.txt file format) that contains information about the PST export request, such as the name of the eDiscovery search that was exported, the date and time of the export, whether de-duplication and unsearchable items were enabled, the search query, and the source mailboxes that were searched.
    
      - A search results log (.csv file format) that contains an entry for each message returned in the search results. Each entry identifies the source mailbox where the message is located. If you’ve enabled de-duplication, this helps you identify all mailboxes that contain a duplicate message.

  - The name of the search is the first part of the filename for each file that is exported. Also, the date and time of the export request is appended to the filename of each PST file and the results log.

  - For more information about de-duplication and unsearchable items, see:
    
      - [Estimate, preview, and copy search results](in-place-ediscovery-exchange-2013-help.md)
    
      - [Unsearchable items in Exchange eDiscovery](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

  - To export eDiscovery search results from the eDiscovery Center in SharePoint or SharePoint Online, see [Export eDiscovery content and create reports](https://go.microsoft.com/fwlink/p/?linkid=324757).

## Troubleshooting


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Symptom</th>
<th>Possible cause</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cannot export to a PST file.</p></td>
<td><ul>
<li><p>There is no active mailbox attached to the account. To export the PST, you must have an active account.</p></li>
<li><p>Your version of Internet Explorer is out of date. Try updating IE to version 10 or later. Or try a different browser.</p></li>
<li><p>Search criteria entered in the <strong>Filter based on criteria</strong> query is incorrect. For example, a username is entered instead of an email address. For more information about how to filter based on criteria, see <a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">Modify an In-Place eDiscovery search</a>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Unable to export search results on a specific machine. Export works as expected on a different machine.</p></td>
<td><p>The wrong Windows credentials were saved in the <strong>Credential Manager</strong>. Clear your credentials and log in again.</p></td>
</tr>
<tr class="odd">
<td><p>eDiscovery PST Export Tool won't start.</p></td>
<td><p>Local intranet zone settings aren't set up correctly in Internet Explorer. Make sure that *.outlook.com, *.office365.com, *.sharepoint.com and *.onmicrosoft.com are added to the Local intranet zone trusted sites.</p>
<p>To add these sites to the Trusted zone in IE, see <a href="https://windows.microsoft.com/en-us/windows/security-zones-adding-removing-websites#1tc=windows-7">Security zones: adding or removing websites</a>.</p></td>
</tr>
</tbody>
</table>

