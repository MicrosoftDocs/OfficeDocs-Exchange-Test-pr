---
title: 'Use batch migration to migrate legacy public folders to Office 365 and Exchange Online: Exchange Online Help'
TOCTitle: Use batch migration to migrate legacy public folders to Office 365 and Exchange Online
ms:assetid: e8ab9309-7d12-4f02-bfc4-14e61a373958
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn874017(v=EXCHG.150)
ms:contentKeyID: 63355346
ms.date: 03/26/2018
mtps_version: v=EXCHG.150
---

# Use batch migration to migrate legacy public folders to Office 365 and Exchange Online

 

_**Applies to:** Exchange Online, Exchange Server, Exchange Server 2013_


**Summary:** Use these procedures to move your Exchange 2007 and Exchange 2010 public folders to Office 365.

This topic describes how to migrate your public folders in a cutover or staged migration from Update Rollup 8 for Exchange Server 2010 Service Pack 3 (SP3) or Update Rollup 15 for Exchange 2007 SP3 to Office 365 or Exchange Online.

This topic refers to the Exchange 2010 SP3 RU8 and Exchange 2007 SP3 RU15 servers as the *legacy Exchange server*. Also, the steps in this topic apply to both Exchange Online and Office 365. The terms may be used interchangeably in this topic.


> [!NOTE]
> The batch migration method described in this article is the only supported method for migrating legacy public folders to Office 365 and Exchange Online. The old serial migration method for migrating public folders is being deprecated and is no longer supported by Microsoft.



We recommend that you don’t use Outlook’s PST export feature to migrate public folders to Office 365 or Exchange Online. Office 365 and Exchange online public folder mailbox growth is managed using an auto-split feature that splits the public folder mailbox when it exceeds size quotas. Auto-split can’t handle the sudden growth of public folder mailboxes when you use PST export to migrate your public folders and you may have to wait for up to two weeks for auto-split to move the data from the primary mailbox. We recommend that you use the cmdlet-based instructions in this document to migrate public folders to Office 365 and Exchange Online. However, if you elect to migrate public folders using PST export, see the section Migrate Public Folders to Office 365 by using Outlook PST export later in this topic.

You’ll perform the migration using the **\*-MigrationBatch** cmdlets, in addition to the following PowerShell scripts:

  - `Export-PublicFolderStatistics.ps1`   This script creates the folder name-to-folder size mapping file. You’ll run this script on the legacy Exchange server.

  - `Export-PublicFolderStatistics.psd1`   This support file is used by the `Export-PublicFolderStatistics.ps1` script and should be downloaded to the same location.

  - `PublicFolderToMailboxMapGenerator.ps1`   This script creates the public folder-to-mailbox mapping file by using the output from the `Export-PublicFolderStatistics.ps1` script. You’ll run this script on the legacy Exchange server.

  - `PublicFolderToMailboxMapGenerator.strings.psd1`   This support file is used by the `PublicFolderToMailboxMapGenerator.ps1` script and should be downloaded to the same location.

  - `Create-PublicFolderMailboxesForMigration.ps1` This script creates the target public folder mailboxes for the migration. In addition, this script calculates the number of mailboxes necessary to handle the estimated user load, based on the guidelines for the number of user logons per public folder mailbox recommended in [Limits for public folders](limits-for-public-folders-exchange-2013-help.md).

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` This support file is used by the Create-PublicFolderMailboxesForMigration.ps1 script and should be downloaded to the same location.

  - `Sync-MailPublicFolders.ps1`   This script synchronizes mail-enabled public folder objects between your local Exchange deployment and Office 365. You'll run this script on the legacy Exchange server.

  - `SyncMailPublicFolders.strings.psd1`   This is a support file used by the `Sync-MailPublicFolders.ps1` script and should be copied to the same location as the preceding scripts.

Step 1: Download the migration scripts provides details about where to download these scripts. Make sure all scripts are downloaded to the same location.

For additional management tasks related to public folders, see [Public folder procedures](public-folder-procedures-exchange-2013-help.md).

## What versions of Exchange are supported for migrating public folders to Office 365 and Exchange Online?

Exchange supports moving your public folders to Office 365 and Exchange Online from the following legacy versions of Exchange Server:

  - Exchange 2010 SP3 RU8 or later

  - Exchange 2007 SP3 RU15 or later

If you need to move your public folders to Exchange Online but your on-premises servers aren't running the minimum support versions of Exchange 2010 or Exchange 2007, we strongly recommend that you upgrade your on-premises servers and use batch migration, which is the only supported public folder migration method.

You can’t migrate public folders directly from Exchange 2003. If you’re running Exchange 2003 in your organization, you need to move all public folder databases and replicas to Exchange 2010 SP3 RU8 or later, or Exchange 2007 SP3 RU10 or later. No public folder replicas can remain on Exchange 2003. Additionally, mail destined for an Exchange 2013 public folder can't be routed through an Exchange 2003 server.

## What do you need to know before you begin?

  - The Exchange 2010 server needs to be running Exchange 2010 SP3 RU8 or later.

  - The Exchange 2007 server needs to be running Exchange 2007 SP3 RU15 or later.

  - In Office 365 and Exchange Online, you need to be a member of the Organization Management role group. This role group is different from the permissions assigned to you when you subscribe to Office 365 or Exchange Online. For details about how to enable the Organization Management role group, see [Manage role groups](manage-role-groups-exchange-2013-help.md).

  - In Exchange 2010, you need to be a member of the Organization Management or Server Management RBAC role groups. For details, see [Add Members to a Role Group](https://go.microsoft.com/fwlink/?linkid=299212).

  - In Exchange 2007, you need to be assigned the Exchange Organization Administrator role or the Exchange Server Administrator role. In addition, you need to be assigned the Public Folder Administrator role and local Administrators group for the target server. For details, see [How to Add a User or Group to an Administrator Role](https://go.microsoft.com/fwlink/p/?linkid=81779).

  - On the Exchange 2007 server, upgrade to [Windows PowerShell 2.0 and WinRM 2.0 for Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930).

  - Before migration, if any public folder in your organization is greater than 2 GB, we recommend either deleting content from that folder or splitting it up into multiple public folders. If either of these options isn’t feasible, we recommend that you do not move your public folders to Office 365 and Exchange Online.

  - In Office 365 and Exchange Online, you can create a maximum of 1,000 public folder mailboxes.

  - Before you migrate your public folders, we recommend that you first move all user mailboxes to Office 365 and Exchange Online. For details, see [Ways to migrate multiple email accounts to Office 365](https://go.microsoft.com/fwlink/p/?linkid=524030).

  - Outlook Anywhere needs to be enabled on the legacy Exchange server. For details about enabling Outlook Anywhere on Exchange 2010 servers, see [Enable Outlook Anywhere](https://go.microsoft.com/fwlink/p/?linkid=187249). For details about enabling Outlook Anywhere on Exchange 2007 servers, see [How to Enable Outlook Anywhere](https://go.microsoft.com/fwlink/p/?linkid=167210).

  - You can’t use the Exchange admin center (EAC) or the Exchange Management Console (EMC) to perform this procedure. On the legacy Exchange servers, you need to use the Exchange Management Shell. For Exchange Online, you need to use Exchange Online PowerShell. For more information, see [Connect to Exchange Online using remote PowerShell](https://technet.microsoft.com/en-us/library/jj984289\(v=exchg.150\)).

  - You must use a single migration batch to migrate all of your public folder data. Exchange allows creating only one migration batch at a time. If you attempt to create more than one migration batch simultaneously, the result will be an error.

  - Before you begin, we recommend that you read this topic in its entirety as downtime is required for some steps.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## How do you do this?

## Step 1: Download the migration scripts

1.  Download all scripts and supporting files from [Public Folders Migration Scripts](https://go.microsoft.com/fwlink/?linkid=299838).

2.  Save the scripts to the local computer on which you’ll be running PowerShell. For example, C:\\PFScripts. Make sure all scripts are saved in the same location.

3.  Download the following files from [Mail-enabled Public Folders - directory sync script](https://go.microsoft.com/fwlink/p/?linkid=532376):
    
    1.  `Sync-MailPublicFolders.ps1`
    
    2.  `SyncMailPublicFolders.strings.psd1`

4.  Save the scripts to the same location you did for step 2. For example, C:\\PFScripts.

## Step 2: Prepare for the migration

Perform the following prerequisite steps before you begin the migration.

**General prerequisite steps**

  - Make sure that there are no orphaned public folder mail objects in Active Directory, meaning objects in Active Directory without a corresponding Exchange object.

  - Confirm that SMTP email address configured for public folders in Active Directory match the SMTP email addresses on the Exchange objects.

  - Make sure that there are no duplicate public folder objects in Active Directory, to avoid a situation where two or more Active Directory objects are pointing to the same mail-enabled public folder.

**Prerequisite steps on the legacy Exchange server**

1.  On the legacy Exchange server, make sure that routing to the mail-enabled public folders that will exist in Office 365 or Exchange Online continues to work until all DNS caches over the Internet are updated to point to the Office 365 or Exchange Online DNS where your organization now resides. To do this, run the following command to configure an accepted domain with a well-known name that will properly route email messages to the Office 365 or Exchange Online domain.
    
        New-AcceptedDomain -Name "PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99" -DomainName contoso.onmicrosoft.com -DomainType InternalRelay 

2.  If the name of a public folder contains a backslash **\\**, the public folders will be created in the parent public folder when migration occurs. Before you migrate, we recommend that you rename any public folders that have a backslash in the name.
    
    1.  In Exchange 2010, to locate public folders that have a backslash in the name, run the following command:
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  In Exchange 2007, to locate public folders that have a backslash in the name, run the following command:
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  If any public folders are returned, you can rename them by running the following command:
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  Make sure there isn’t a previous record of a successful migration. If there is, you’ll need to set that value to `$false`. If the value is set to `$true`, the migration request will fail.
    
    1.  The following example checks the public folder migration status.
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
    
    2.  If the status of the *PublicFoldersLockedforMigration* or *PublicFolderMigrationComplete* properties is `$true`, run the following command to set the value to `$false`.
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    

    > [!WARNING]
    > After resetting these properties, you need to wait for Exchange to detect the new settings. This may take up to two hours to complete.



4.  For verification purposes at the end of migration, we recommend that you first run the following Exchange Management Shell commands on the legacy Exchange server to take snapshots of your current public folder deployment.
    
    1.  Run the following command to take a snapshot of the original source folder structure.
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
    2.  Run the following command to take a snapshot of public folder statistics such as item count, size, and owner.
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
    3.  Run the following command to take a snapshot of the permissions.
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    Save the information from the preceding commands for comparison at the end of the migration.

5.  If you are using Microsoft Azure Active Directory Connect (Azure AD Connect) to synchronize your on-premises directories with Azure Active Directory, you need to do the following (if you are not using Azure AD Connect, you can skip this step):
    
    1.  On an on-premises computer, open Microsoft Azure Active Directory Connect, and then select **Configure**.
    
    2.  On the **Additional tasks** screen, select **Customize synchronization options**, and then click **Next**.
    
    3.  On the **Connect to Azure AD** screen, enter the appropriate credentials, and then click **Next**. Once connected, keep clicking **Next** until you are on the **Optional Features** screen.
    
    4.  Make sure that **Exchange Mail Public Folders** is not selected. If it isn't selected, you can continue to the next section, *Prerequisite steps in Office 365 or Exchange Online*. If it is selected, click to clear the check box, and then click **Next**.
        

        > [!NOTE]
        > If you don't see <STRONG>Exchange Mail Public Folders</STRONG> as an option on the <STRONG>Optional Features</STRONG> screen, you can exit Microsoft Azure Active Directory Connect and proceed to the next section, <EM>Prerequisite steps in Office 365 or Exchange Online</EM>.

    
    5.  After you have cleared the **Exchange Mail Public Folders** selection, keep clicking **Next** until you are on the **Ready to configure** screen, and then click **Configure**.

For detailed syntax and parameter information, see the following topics:

  - [New-AcceptedDomain](https://technet.microsoft.com/en-us/library/aa995975\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/en-us/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/en-us/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/en-us/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/en-us/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/en-us/library/bb124365\(v=exchg.150\))

  - [Get-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Prerequisite steps in Office 365 or Exchange Online**

1.  Make sure there are no existing public folder migration requests. If there are, clear them or your own migration request will fail. This step isn’t required in all cases; it’s only required if you think there may be an existing migration request in the pipeline.
    
    An existing migration request can be one of two types: batch migration or serial migration. The commands for detecting requests for each type and for removing requests of each type are as follows.
    

    > [!IMPORTANT]
    > Before removing a migration request, it is important to understand why there was an existing one. Running the following commands will determine when a previous request was made and help you diagnose any problems that may have occurred. You may need to communicate with other administrators in your organization to determine why the change was made.

    
    The following example will discover any existing serial migration requests.
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics -IncludeReport | Format-List
    
    The following example removes any existing public folder serial migration requests.
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    The following example will discover any existing batch migration requests.
    
        $batch = Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    The following example removes any existing public folder batch migration requests.
    
        $batch | Remove-MigrationBatch -Confirm:$false

2.  Make sure no public folders or public folder mailboxes exist in Office 365.
    

    > [!IMPORTANT]
    > If you do see public folders in Office 365 or Exchange Online, it is important to determine why they are there and who in your organization started a public folder hierarchy before removing the public folders and public folder mailboxes.

    
    1.  In Office 365 or Exchange Online PowerShell, run the following command to see if any public folders mailboxes exist.
        
            Get-Mailbox -PublicFolder 
    
    2.  If the command didn’t return any public folder mailboxes, continue to Step 3: Generate the .csv files. If the command returned any public folders mailboxes, run the following command to see if any public folders exist:
        
            Get-PublicFolder
    
    3.  If you have any public folders in Office 365 or Exchange Online, run the following PowerShell command to remove them. Make sure you've saved any information that was in the public folders in Office 365. All information contained in the public folders will be permanently deleted when you remove the public folders.
        
            Get-MailPublicFolder | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            
            
            Get-PublicFolder -GetChildren \ | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  After the public folders are removed, run the following commands to remove all public folder mailboxes.
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false

For detailed syntax and parameter information, see the following topics:

  - [Get-MigrationBatch](https://technet.microsoft.com/en-us/library/jj219164\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/en-us/library/jj218718\(v=exchg.150\))

  - [Remove-PublicFolderMigrationRequest](https://technet.microsoft.com/en-us/library/jj218625\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/en-us/library/bb123685\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/en-us/library/aa997615\(v=exchg.150\))

  - [Get-MailPublicFolder](https://technet.microsoft.com/en-us/library/bb124772\(v=exchg.150\))

  - [Disable-MailPublicFolder](https://technet.microsoft.com/en-us/library/bb123781\(v=exchg.150\))

  - [Remove-PublicFolder](https://technet.microsoft.com/en-us/library/bb124894\(v=exchg.150\))

  - [Remove-Mailbox](https://technet.microsoft.com/en-us/library/aa995948\(v=exchg.150\))

## Step 3: Generate the .csv files

1.  On the legacy Exchange server, run the `Export-PublicFolderStatistics.ps1` script to create the folder name-to-folder size mapping file. This script needs to always be run by a local administrator. The file will contain two columns: **FolderName** and **FolderSize**. The values for the **FolderSize** column will be displayed in bytes. For example, **\\PublicFolder01,10000**.
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server* equals the fully qualified domain name of the Mailbox server where the public folder hierarchy is hosted.
    
      - *Folder to size map path* equals the file name and path on a network shared folder where you want the .csv file saved. Later in this topic, you’ll need to use the Exchange Online PowerShell to access this file. If you specify only the file name, the file will be generated in the current PowerShell directory on the local computer.
    
      - If necessary, remove any mail-enabled system folders from the script output before proceeding.

2.  Run the `PublicFolderToMailboxMapGenerator.ps1` script to create the public folder-to-mailbox mapping file. This file is used to calculate the correct number of public folder mailboxes in Exchange Online.
    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    

    > [!IMPORTANT]
    > The public folder-to-mailbox mapping file should not exceed 1,000 rows. If this file exceeds 1,000 rows, your public folder structure needs to be simplified. Proceeding with a file of greater than 1,000 rows is not recommended and could cause migration errors.

    
      - Before you run the script, use the following cmdlet to check the current public folder limits in your Exchange Online tenant. Then, note the current quota values for public folders. `Get-OrganizationConfig | fl *quota*`
        
        In Exchange Online, the default value is 1.7 GB for **DefaultPublicFolderIssueWarningQuota** and 2 GB for **DefaultPublicFolderProhibitPostQuota**.
    
      - *Maximum mailbox size in bytes* equals the maximum size that you want to set for the new public folder mailboxes. In Exchange Online, the maximum size of public folder mailboxes is 100 GB. We recommend that you use a setting of 15 GB so that each public folder mailbox has room to grow. Exchange Online has a default public folder "prohibit post" quota of 2 GB. If you have individual public folders that are larger than 2 GB, you can use any of the following options to fix this issue:
        
          - Before you start the migration batch, increase the default public folder "prohibit post" quota by running the following cmdlet:
            
            `Set-OrganizationConfig -DefaultPublicFolderProhibitPostQuota <size value> -DefaultPublicFolderIssueWarningQuota <size value>`
        
          - Before you start the migration batch, delete public folder content to reduce the size of the content to 2 GB or less.
        
          - Before you start the migration batch, split the public folder into multiple public folders that are each 2 GB or less.
        

        > [!NOTE]
        > If the public folder is larger than 30 GB, and if it isn't feasible to delete content or split it into multiple public folders, we recommend that you don’t move your public folders to Exchange Online.

    
      - *Folder to size map path* equals the file path of the .csv file that you created when you ran the `Export-PublicFolderStatistics.ps1` script.
    
      - *Folder to mailbox map path* equals the file name and path of the folder-to-mailbox .csv file that you create in this step. If you specify only the file name, the file is generated in the current PowerShell directory on the local computer.


> [!NOTE]
> After the scripts are run and the .csv files are generated, any new public folders or updates to existing public folders will not be collected.



## Step 4: Create the public folder mailboxes in Exchange Online

1.  Run the following command to create the target public folder mailboxes. The script will create a target mailbox for each mailbox in the .csv file that you generated previously in Step 3, by running the PublicFoldertoMailboxMapGenerator.ps1 script.
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv* is the file generated by the PublicFoldertoMailboxMapGenerator.ps1 script in Step 3. The estimated number of simultaneous user connections browsing a public folder hierarchy is usually less than the total number of users in an organization.

## Step 5: Start the migration request

1.  On the legacy Exchange server, run the following command to synchronize mail-enabled public folders from your local Active Directory to Exchange Online.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    `Credential` is your Office 365 user name and password. `CsvSummaryFile` is the file path to where you would like to log, in .CSV format, synchronization operations and errors.
    

    > [!NOTE]
    > We recommend that you first simulate the actions that the script would take before actually executing it, which you can do by running the script with a <CODE>-WhatIf</CODE> parameter.



2.  On the legacy Exchange server, get the following information that’s needed to run the migration request:
    
    1.  Find the `LegacyExchangeDN` of the user’s account who is a member of the Public Folder Administrator role. This will be the same user whose credentials you need in step 3 of this procedure.
        
            Get-Mailbox <PublicFolder_Administrator_Account> | Select-Object LegacyExchangeDN
    
    2.  Find the `LegacyExchangeDN` of any Mailbox server that has a public folder database.
        
            Get-ExchangeServer <public folder server> | Select-Object -Expand ExchangeLegacyDN
    
    3.  Find the FQDN of the Outlook Anywhere host name. If you have multiple instances of Outlook Anywhere, we recommend that you select the instance that is either closest to the migration endpoint or the one that is closest to the public folder replicas in the legacy Exchange organization. The following command will find all instances of Outlook Anywhere:
        
            Get-OutlookAnywhere | Format-Table Identity,ExternalHostName

3.  In Office 365 PowerShell, run the following commands to pass the information that was returned in the previous step to variables that will then be used in the migration request.
    
    1.  Pass the credential of a user who has administrative permissions on the legacy Exchange server into the variable `$Source_Credential`. The migration request that’s run in Exchange Online will use this credential to gain access to your legacy Exchange servers to copy the content over.
        
            $Source_Credential = Get-Credential <source_domain\PublicFolder_Administrator_Account>
    
    2.  Use the `ExchangeLegacyDN` of the migration user on the legacy Exchange server that you found in step 2a and pass it into the variable `$Source_RemoteMailboxLegacyDN`.
        
            $Source_RemoteMailboxLegacyDN = "<paste the value here>"
    
    3.  Use the `ExchangeLegacyDN` of the public folder server that you found in step 2b above and pass it into the variable `$Source_RemotePublicFolderServerLegacyDN`.
        
            $Source_RemotePublicFolderServerLegacyDN = "<paste the value here>"
    
    4.  Use the External Host Name of Outlook Anywhere that you found in step 2c above and pass it into the variable `$Source_OutlookAnywhereExternalHostName`.
        
            $Source_OutlookAnywhereExternalHostName = "<paste the value here>"

4.  Finally, in Exchange Online PowerShell, run the following commands to create the migration request.
    

    > [!NOTE]
    > The authentication method in the following Exchange Management Shell example needs to match your Outlook Anywhere settings, otherwise the command will fail.

    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RPCProxyServer $Source_OutlookAnywhereExternalHostName -Credentials $Source_Credential -SourceMailboxLegacyDN $Source_RemoteMailboxLegacyDN -PublicFolderDatabaseServerLegacyDN $Source_RemotePublicFolderServerLegacyDN -Authentication Basic
        
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    
    Where the \<*folder\_mapping.csv*\> file is the file that was generated in Step 3: Generate the .csv files.

5.  Start the migration using the following command:
    
        Start-MigrationBatch PublicFolderMigration

While batch migrations need to be created using the **New-MigrationBatch** cmdlet in the Exchange Management Shell, the progress and completion of the migration can be viewed and managed in the EAC. Because the **New-MigrationBatch** cmdlet initiates a mailbox migration request for each public folder mailbox, you can view the status of these requests using the mailbox migration page. You can get to the mailbox migration page, and create migration reports that can be emailed to you, by doing the following:

1.  Log into Exchange Online and open the EAC.

2.  Navigate to **Mailbox** \> **Migration**.

3.  Select the migration request that was just created and then click **View Details** in the **Details** pane.

For detailed syntax and parameter information, see the following topics:

  - [Get-Mailbox](https://technet.microsoft.com/en-us/library/bb123685\(v=exchg.150\))

  - [Get-ExchangeServer](https://technet.microsoft.com/en-us/library/bb123873\(v=exchg.150\))

  - [Get-OutlookAnywhere](https://technet.microsoft.com/en-us/library/bb124263\(v=exchg.150\))

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/en-us/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/en-us/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/en-us/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/en-us/library/jj218697\(v=exchg.150\))

## Step 6: Lock down the public folders on the legacy Exchange server for final migration (downtime required)

Until this point in the migration process, users have been able to access public folders. The next steps will log users off from the legacy public folders and lock the folders while the migration completes its final synchronization. Users won’t be able to access public folders during this process. Also, any mail sent to mail-enabled public folders will be queued and won’t be delivered until the public folder migration is complete.

Before you run the `PublicFoldersLockedForMigration` command as described below, make sure that all jobs are in the **Synced** state. You can do this by running the `Get-PublicFolderMailboxMigrationRequest` command. Continue with this step only after you've verified that all jobs are in the **Synced** state.

On the legacy Exchange server, run the following command to lock the legacy public folders for finalization.

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true

For detailed syntax and parameter information, see [Set-OrganizationConfig](https://technet.microsoft.com/en-us/library/aa997443\(v=exchg.150\)).

If your organization has multiple public folder databases, you’ll need to wait until public folder replication is complete to confirm that all public folder databases have picked up the `PublicFoldersLockedForMigration` flag and any pending changes users recently made to folders have converged across the organization. This may take several hours.

## Step 7: Finalize the public folder migration (downtime required)

To complete the public folder migration, run the following command:

    Complete-MigrationBatch PublicFolderMigration

When you complete the migration, Exchange will perform a final synchronization between the legacy Exchange server and Exchange Online. If the final synchronization is successful, the public folders in Exchange Online will be unlocked and the status of the migration batch will changed to **Completed**. It is common for the migration batch to take a few hours before its status changes from **Synced** to **Completing**, at which point the final synchronization will begin.

If you've configured a hybrid deployment between your on-premises Exchange servers and Office 365, you need to run the following command in Exchange Online PowerShell after migration is complete:

    Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## Step 8: Test and unlock the public folder migration

After you finalize the public folder migration, you should run the following test to make sure that the migration was successful. This allows you to test the migrated public folder hierarchy before you switch to using Office 365 or Exchange Online public folders.

1.  In Office 365 or Exchange Online PowerShell, assign some test mailboxes to use any newly migrated public folder mailbox as the default public folder mailbox.
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  Log on to Outlook 2007 or later with the test user identified in the previous step, and then perform the following public folder tests:
    
      - View the hierarchy.
    
      - Check permissions.
    
      - Create and delete public folders.
    
      - Post content to and delete content from a public folder.

3.  If you run into any issues, see Roll back the migration later in this topic. If the public folder content and hierarchy is acceptable and functions as expected, continue to the next step.

4.  On the legacy Exchange server, run the following command to indicate that the public folder migration is complete:
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  After you've verified that migration is complete, run the following command in Exchange Online PowerShell to make sure that the *PublicFoldersEnabled* parameter on **Set-OrganizationConfig** is set to `Local`:
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

For detailed syntax and parameter information, see the following topics:

[Set-Mailbox](https://technet.microsoft.com/en-us/library/bb123981\(v=exchg.150\))

[Get-Mailbox](https://technet.microsoft.com/en-us/library/bb123685\(v=exchg.150\))

[Set-OrganizationConfig](https://technet.microsoft.com/en-us/library/aa997443\(v=exchg.150\))

## How do I know this worked?

In Step 2: Prepare for the migration, you were instructed to take snapshots of the public folder structure, statistics, and permissions before the migration began. The following steps will help verify that your public folder migration was successful by taking the same snapshots after the migration is complete. You can then compare the data in both files to verify success.

1.  In Exchange Online PowerShell, run the following command to take a snapshot of the new folder structure.
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  In Exchange Online PowerShell, run the following command to take a snapshot of the public folder statistics such as item count, size, and owner.
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  In Exchange Online PowerShell, run the following command to take a snapshot of the permissions.
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## Remove public folder databases from the legacy Exchange servers

After the migration is complete, and you have verified that your Exchange Online public folders are working as expected, you should remove the public folder databases on the legacy Exchange servers.


> [!IMPORTANT]
> Since all of your mailboxes have been migrated to Office 365 prior to the public folder migration, we strongly recommend that you route the traffic through Office 365 (decentralized mail flow) instead of centralized mail flow through your on-premises environment. If you choose to keep mail flow centralized, it could cause delivery issues to your public folders, since you've removed the public folder mailbox databases from your on-premises organization.



  - For details about how to remove public folder databases from Exchange 2007 servers, see [Removing Public Folder Databases](https://go.microsoft.com/fwlink/?linkid=123678).

  - For details about how to remove public folder databases from Exchange 2010 servers, see [Remove Public Folder Databases](https://go.microsoft.com/fwlink/?linkid=81409).

## Roll back the migration

If you run into issues with the migration and need to reactivate your legacy Exchange public folders, perform the following steps.


> [!WARNING]
> If you roll your migration back to the legacy Exchange servers, you will lose any email that was sent to mail-enabled public folders or content that was posted to public folders after the migration. To save this content, you need to export the public folder content to a .pst file and then import it to the legacy public folders when the rollback is complete.



1.  On the legacy Exchange server, run the following command to unlock the legacy Exchange public folders. This process may take several hours.
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  In Exchange Online PowerShell, run the following commands to remove all Exchange Online public folders.
    
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force

3.  On the legacy Exchange server, run the following command to set the `PublicFolderMigrationComplete` flag to `$false`.
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

## Migrate Public Folders to Office 365 by using Outlook PST export

We recommend that you don’t use Outlook’s PST export feature to migrate public folders to Office 365 or Exchange Online if your on-premises public folder hierarchy is greater than 30 GB. Office 365 online public folder mailbox growth is managed using an auto-split feature that splits the public folder mailbox when it exceeds size quotas. Auto-split can’t handle the sudden growth of public folder mailboxes when you use PST export to migrate your public folders and you may have to wait for up to two weeks for auto-split to move the data from the primary mailbox. In addition, consider the following before using Outlook PST to export public folders to Office 365 or Exchange Online:

  - Public folder permissions will be lost during this process. Capture the current permissions before migration and manually add them back once the migration is completed.

  - If you use complex permissions or have many folders to migrate, we recommend that you use the cmdlet method for migration.

  - Any item and folder changes made to the source public folders during the PST export migration will be lost. Therefore, we recommend that you use the cmdlet method if this export and import process will take a long time to complete.

If you still want to migrate your public folders by using PST files, follow these steps to ensure a successful migration.

1.  Use the instructions in Step 1: Download the migration scripts to download the migration scripts. You only need to download the `PublicFolderToMailboxMapGenerator.ps1` file.

2.  Follow step 2 of Step 3: Generate the .csv files to create the public folder-to-mailbox mapping file. This file is used to calculate the correct number of public folder mailboxes in Exchange Online.

3.  Create the public folder mailboxes that you’ll need based on the mapping file. For more information, see [Create a public folder mailbox](create-a-public-folder-mailbox-exchange-2013-help.md).

4.  Use the New-PublicFolder cmdlet to create the top-most public folder in each of the public folder mailboxes by using the *Mailbox* parameter.

5.  Export and import the PST files using Outlook.

6.  Set the permissions on the public folders using the EAC. For more information, follow [Step 3: Assign permissions to the public folder](set-up-public-folders-in-a-new-organization-exchange-2013-help.md) in the [Set up public folders in a new organization](set-up-public-folders-in-a-new-organization-exchange-2013-help.md) topic.


> [!WARNING]
> If you’ve already started a PST migration and have run into an issue where the primary mailbox is full, you have two options for recovering the PST migration: 
> <OL>
> <LI>
> <P>Wait for the auto-split to move the data from the primary mailbox. This may take up to two weeks. However, all the public folders in a completely filled public folder mailbox won’t be able to receive new content until the auto-split completes.</P>
> <LI>
> <P><A href="create-a-public-folder-mailbox-exchange-2013-help.md">Create a public folder mailbox</A> and then use the <STRONG>New-PublicFolder</STRONG> cmdlet with the <EM>Mailbox</EM> parameter to create the remaining public folders in the secondary public folder mailbox. This example creates a new public folder named PF201 in the secondary public folder mailbox.</P><PRE><CODE>New-PublicFolder -Name PF201 -Mailbox SecondaryPFMbx</CODE></PRE></LI></OL>



## New to Office 365?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="The short icon for LinkedIn Learning" alt="The short icon for LinkedIn Learning" /> <strong>New to Office 365?</strong><br />
Discover free video courses for <a href="https://support.office.com/en-us/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>, brought to you by LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

