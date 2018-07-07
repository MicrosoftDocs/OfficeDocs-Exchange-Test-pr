---
title: 'Configure legacy on-premises public folders for a hybrid deployment: Exchange 2013 Help'
TOCTitle: Configure legacy on-premises public folders for a hybrid deployment
ms:assetid: bcb0ac98-2949-486b-a8ab-8549c021651b
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn249373(v=EXCHG.150)
ms:contentKeyID: 54751128
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
---

# Configure legacy on-premises public folders for a hybrid deployment

 

_**Applies to:** Exchange Online, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_


**Summary:** Use the steps in this article to synchronize public folders between Office 365 and your Exchange 2007 or Exchange 2010 on-premises deployment.

In a hybrid deployment, your users can be in Exchange Online , on-premises, or both, and your public folders are either in Exchange Online or on-premises. Public folders can only reside in one place, so you must decide whether your public folders will be in Exchange Online or on-premises. They can’t be in both locations. Public folder mailboxes are synchronized to Exchange Online by the Directory Synchronization service. However, mail-enabled public folders aren’t synchronized across premises.

This topic describes how to synchronize mail-enabled public folders when your users are in Office 365 and your Exchange 2010 SP3 or Exchange 2007 SP3 RU10 public folders are on-premises. However, an Office 365 user who is not represented by a MailUser object on-premises (local to the target public folder hierarchy) won't be able to access legacy or Exchange 2013 on-premises public folders.


> [!NOTE]
> This topic refers to the Exchange 2010 SP3 and Exchange 2007 SP3 RU10 servers as the <EM>legacy Exchange server</EM>.



You will sync your mail-enabled public folders using the following scripts, which are initiated by a Windows task that runs in the on-premises environment:

1.  `Sync-MailPublicFolders.ps1`   This script synchronizes mail-enabled public folder objects from your local Exchange on-premises deployment with Office 365. It uses the local Exchange on-premises deployment as master to determine what changes need to be applied to O365. The script will create, update, or delete mail-enabled public folder objects on O365 Active Directory based on what exists in the local on-premises Exchange deployment.

2.  `SyncMailPublicFolders.strings.psd1`   This is a support file used by the preceding synchronization script and should be copied to the same location as the preceding script.

When you complete this procedure your on-premises and Office 365 users will be able to access the same on-premises public folder infrastructure.

## What hybrid versions of Exchange will work with public folders?

The following table describes the version and location combinations of user mailboxes and public folders that are supported. “Hybrid not applicable” is still a supported scenario, but is not considered a hybrid scenario since both the public folders and the users are residing in the same location.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>   </th>
<th>On-Premises Exchange 2007 or Exchange 2010 User Mailbox</th>
<th>On-Premises Exchange 2013 User Mailbox</th>
<th>Exchange Online User Mailbox</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>On-Premises Exchange 2007 or Exchange 2010 Public Folders</p></td>
<td><p>Hybrid not applicable</p></td>
<td><p>Hybrid not applicable</p></td>
<td><p>Supported</p></td>
</tr>
<tr class="even">
<td><p>On-Premises Exchange 2013 Public Folders</p></td>
<td><p>Hybrid not applicable</p></td>
<td><p>Hybrid not applicable</p></td>
<td><p>Supported</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Online Public Folders</p></td>
<td><p>Not supported</p></td>
<td><p>Supported</p></td>
<td><p>Hybrid not applicable</p></td>
</tr>
</tbody>
</table>


A hybrid configuration with Exchange 2003 public folders is not supported. If you’re running Exchange 2003 in your organization, you must move all public folder databases and replicas to Exchange 2007 SP3 RU10 or later. No public folder replicas can remain on Exchange 2003.


> [!NOTE]
> Outlook 2016 does not support accessing Exchange 2007 legacy public folders. If you have users with Outlook 2016, you will need to move your public folders to a more recent version of Exchange. More information about Outlook 2016 and Office 2016 compatibility with Exchange 2007 and earlier versions can be found in <A href="https://go.microsoft.com/fwlink/p/?linkid=849053">this article</A>.



## Step 1: What do you need to know before you begin?

1.  These instructions assume that you have used the Hybrid Configuration Wizard to configure and synchronize your on-premises and Exchange Online environments and that the DNS records used for most users’ AutoDiscover references an on-premises end-point. For more information, see [Hybrid Configuration wizard](hybrid-configuration-wizard-exchange-2013-help.md).

2.  These instructions assume that Outlook Anywhere is enabled and functional on the on-premises legacy Exchange server(s). For information on how to enable Outlook Anywhere, see [Outlook Anywhere](https://technet.microsoft.com/en-us/library/bb123741\(v=exchg.150\)).

3.  Implementing legacy public folder coexistence for a hybrid deployment of Exchange with Office 365 may require you to fix conflicts during the import procedure. Conflicts can happen due to non-routable email address assigned to mail enabled public folders, conflicts with other users and groups in Office 365, and other attributes.

4.  These instructions assume your Exchange Online organization has been upgraded to a version that supports public folders.

5.  In Exchange Online, you must be a member of the Organization Management role group. This role group is different from the permissions assigned to you when you subscribe to Exchange Online. For details about how to enable the Organization Management role group, see [Manage role groups](https://technet.microsoft.com/en-us/library/jj657480\(v=exchg.150\)).

6.  In Exchange 2010, you must be a member of the Organization Management or Server Management RBAC role groups. For details, see [Add Members to a Role Group](https://go.microsoft.com/fwlink/?linkid=299212)

7.  In Exchange 2007, you need to be assigned the Exchange Organization Administrator role or the Exchange Server Administrator role. In addition, you must be assigned the Public Folder Administrator role and local Administrators group for the target server. For details, see [How to Add a User or Group to an Administrator Role](https://go.microsoft.com/fwlink/p/?linkid=81779)

8.  If you have Exchange Server 2007 running on Windows Server 2008 x64, then you must upgrade to [Windows PowerShell 2.0 and WinRM 2.0 for Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930). If you have Exchange Server 2007 running on Windows Server 2003 x64, then you must upgrade to Windows PowerShell 2.0. For more information, see [Update for Windows Server 2003 x64 Edition](https://www.microsoft.com/en-us/download/details.aspx?id=10512)..

9.  In order to access public folders cross-premises, users must upgrade their Outlook clients to the November 2012 Outlook public update or later.
    
    1.  To download the November 2012 Outlook update for Outlook 2010, see [Update for Microsoft Outlook 2010 (KB2687623) 32-Bit Edition](https://www.microsoft.com/en-us/download/details.aspx?id=35702).
    
    2.  To download the November 2012 Outlook Update for Outlook 2007, see [Update for Microsoft Office Outlook 2007 (KB2687404)](https://www.microsoft.com/en-us/download/details.aspx?id=35718).

10. Outlook 2016 for Mac (and earlier versions) and Outlook for Mac for Office 365 are not supported for cross-premises legacy public folders. Users must be in the same location as the public folders to access them with Outlook for Mac or Outlook for Mac for Office 365. In addition, users whose mailboxes are in Exchange Online won’t be able to access on-premises public folders using Outlook Web App.

11. After you have followed the instructions in this article to configure your on-premises public folders for a hybrid deployment, users who are external to your organization won't be able to send messages to your on-premises public folders unless you take additional steps. You can either set the accepted domain for the public folders to Internal Relay (see [Manage accepted domains in Exchange Online](https://technet.microsoft.com/en-us/library/jj945194\(v=exchg.150\)) for more information) or you can disable Directory Based Edge Blocking (DBEB), as described in [Use Directory Based Edge Blocking to Reject Messages Sent to Invalid Recipients](https://technet.microsoft.com/en-us/library/dn600322\(v=exchg.150\)).

## Step 2: Make remote public folders discoverable

1.  If your public folders are on Exchange 2010 or later servers, then you need to install the Client Access Server role on all mailbox servers that have a public folder database. This allows the Microsoft Exchange RpcClientAccess service to be running, which allows for all clients to access public folders. The client access role isn’t required for Exchange 2007 public folder servers, and this step isn’t necessary. For more information, see [Install Exchange Server 2010](https://technet.microsoft.com/en-us/library/bb124778\(v=exchg.141\).aspx). This step isn’t necessary for Exchange 2007 public folders.
    

    > [!NOTE]
    > This server doesn’t have to be part of the Client Access load balancing. For more information, see <A href="https://technet.microsoft.com/en-us/library/ff625247(v=exchg.141).aspx">Understanding Load Balancing in Exchange 2010</A>.



2.  Create an empty mailbox database on each public folder server.
    
    For Exchange 2010, run the following command. This command excludes the mailbox database from the mailbox provisioning load balancer. This prevents new mailboxes from automatically being added to this database.
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true
    
    For Exchange 2007, run the following command:
    
        New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
    

    > [!NOTE]
    > We recommend that the only mailbox that you add to this database is the proxy mailbox that you’ll create in step&nbsp;3. No other mailboxes should be created on this mailbox database.



3.  Create a proxy mailbox within the new mailbox database and hide the mailbox from the address book. The SMTP of this mailbox will be returned by AutoDiscover as the *DefaultPublicFolderMailbox* SMTP, so that by resolving this SMTP the client can reach the legacy exchange server for public folder access.
    
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs>
    
        Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true

4.  For Exchange 2010, enable AutoDiscover to return the proxy public folder mailboxes. This step isn’t necessary for Exchange 2007.
    
        Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>

5.  Repeat the preceding steps for every public folder server in your organization.

## Step 3: Download the scripts

1.  Download the following files from [Mail-enabled Public Folders - directory sync script](https://www.microsoft.com/en-us/download/details.aspx?id=46381):
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  Save the files to the local computer on which you’ll be running PowerShell. For example, C:\\PFScripts.

## Step 4: Configure directory synchronization

The Directory Synchronization service doesn’t synchronize mail-enabled public folders. Running the following script will synchronize the mail-enabled public folders across premises. Special permissions assigned to mail-enabled public folders will need to be recreated in the cloud since cross-premise permission are not supported in Hybrid Deployment scenarios. For more information, see [Exchange Server 2013 Hybrid Deployment](exchange-server-hybrid-deployments-exchange-2013-help.md).


> [!NOTE]
> Synchronized mail-enabled public folders will appear as mail contact objects for mail flow purposes and will not be viewable in the Exchange admin center. See the Get-MailPublicFolder command. To recreate the SendAs permissions in the cloud, use the Add-RecipientPermission command.



1.  On the legacy Exchange server, run the following command to synchronize mail-enabled public folders from your local on-premises Active Directory to O365.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    Where `Credential` is your Office 365 user name and password, and `CsvSummaryFile` is the path to where you would like to log synchronization operations and errors, in .csv format.


> [!NOTE]
> Before running the script, we recommend that you first simulate the actions that the script would take in your environment by running it as described above with the <CODE>-WhatIf</CODE> parameter.<BR>We also recommend that you run this script daily to synchronize your mail-enabled public folders.



## Step 5: Configure Exchange Online users to access on-premises public folders

The final step in this procedure is to configure the Exchange Online organization and to allow access to the legacy on-premises public folders.

Enable the exchange online organization to access the on-premises public folders. You will point to all of the proxy public folder mailboxes that you created in Step 2: Make remote public folders discoverable.

Run the following command in **Windows PowerShell**:

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3

You must wait until ActiveDirectory synchronization has completed to see the changes. This process can take up to 3 hours to complete. If you don’t want to wait for the recurring synchronizations that occur every three hours, you can force directory synchronization at any time. For detailed steps to do force directory synchronization, see [Force directory synchronization](http://technet.microsoft.com/en-us/library/jj151771.aspx). Office 365 randomly selects one of the public folder mailboxes that's supplied in this command.


> [!IMPORTANT]
> An Office 365 user who is not represented by a MailUser object on-premises (local to the target public folder hierarchy) won't be able to access legacy or Exchange 2013 on-premises public folders. See the Knowledge Base article <A href="https://go.microsoft.com/fwlink/p/?linkid=699451">Exchange Online users can't access legacy on-premises public folders</A> for a solution.



## How do I know this worked?

1.  Log on to Outlook for a user who is in Exchange Online and perform the following public folder tests:
    
      - View the hierarchy.
    
      - Check permissions
    
      - Create and delete public folders.
    
      - Post content to and delete content from a public folder.

## New to Office 365?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="The short icon for LinkedIn Learning" alt="The short icon for LinkedIn Learning" /> <strong>New to Office 365?</strong><br />
Discover free video courses for <a href="https://support.office.com/en-us/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>, brought to you by LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

