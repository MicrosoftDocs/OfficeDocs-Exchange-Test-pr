---
title: 'Create a discovery mailbox: Exchange 2013 Help'
TOCTitle: Create a discovery mailbox
ms:assetid: bc20285d-35e2-4e49-9bd3-38abf96114ba
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd638177(v=EXCHG.150)
ms:contentKeyID: 49289394
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Create a discovery mailbox

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Microsoft Exchange Server 2013 Setup creates a discovery mailbox by default. In Exchange Online, a discovery mailbox is also created by default. Discovery mailboxes are used as target mailboxes for [In-Place eDiscovery](in-place-ediscovery-exchange-2013-help.md) searches in the Exchange admin center (EAC). You can create additional discovery mailboxes as required. After you create a new discovery mailbox, you will have to assign Full Access permissions to the appropriate users so they can access eDiscovery search results that are copied to the discovery mailbox.


> [!WARNING]
> After a discovery manager copies the results of an eDiscovery search to a discovery mailbox, the mailbox can potentially contain sensitive information. You should control access to discovery mailboxes and make sure only authorized users can access them.



For more information, see [Discovery mailboxes](in-place-ediscovery-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 3 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Creating discovery mailboxes" entry in [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

  - Discovery mailboxes have a mailbox storage quota of 50 gigabytes (GB). This storage quota can’t be increased.

  - You can’t use the EAC to create a discovery mailbox or assign permissions to access it. You have to use the Shell. In Office 365, use Remote PowerShell connected to your Exchange Online organization.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## (Optional) Step 1: Connect to Exchange Online using remote PowerShell

You only need to perform this step if you have an Exchange Online or Office 365 organization. If you have an Exchange Server 2013 organization, go to the next step and run the command in the Exchange Management Shell.

1.  On your local computer, open Windows PowerShell and run the following command.
    
        $UserCredential = Get-Credential
    
    In the **Windows PowerShell Credential Request** dialog box, type user name and password for an Office 365 global admin account, and then click **OK**.

2.  Run the following command.
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  Run the following command.
    
        Import-PSSession $Session

4.  To verify that you’re connected to your Exchange Online organization, run the following command to get a list of all the mailboxes in your organization.
    
        Get-Mailbox

For more information or if you have problems connecting to your Exchange Online organization, see [Connect to Exchange Online using remote PowerShell](https://go.microsoft.com/fwlink/p/?linkid=517283).

## Step 2: Create a discovery mailbox

This example creates a discovery mailbox named SearchResults.

    New-Mailbox -Name SearchResults -Discovery 

For detailed syntax and parameter information, see [New-Mailbox](https://technet.microsoft.com/en-us/library/aa997663\(v=exchg.150\)).

To display a list of all discovery mailboxes in an Exchange organization, run the following command:

    Get-Mailbox -Resultsize unlimited -Filter {RecipientTypeDetails -eq "DiscoveryMailbox"}

For detailed syntax and parameter information, see [Get-Mailbox](https://technet.microsoft.com/en-us/library/bb123685\(v=exchg.150\)).

## Step 3: Assign permissions to a discovery mailbox

You have to explicitly assign users or groups the necessary permissions to open a discovery mailbox that you've created. Use the following syntax to assign a user or group permissions to open a discovery mailbox and view search results:

    Add-MailboxPermission <Name of the discovery mailbox> -User <Name of user or group> -AccessRights FullAccess -InheritanceType all

For example, the following command assigns the Full Access permission to the Litigation Managers group, so members of the group can open the Fabrikam Litigation discovery mailbox.

    Add-MailboxPermission "Fabrikam Litigation" -User "Litigation Managers" -AccessRights FullAccess -InheritanceType all

For detailed syntax and parameter information, see [Add-MailboxPermission](https://technet.microsoft.com/en-us/library/bb124097\(v=exchg.150\)).

## More information

  - By default, members of the Discovery Management role group only have Full Access permission to the default Discovery Search Mailbox. You will have to explicitly assign the Full Access permission to the Discovery Management role group if you want members to open a discovery mailbox that you've created.

  - Although visible in Exchange address lists, users can't send email to a discovery mailbox. Email delivery to discovery mailboxes is prohibited with delivery restrictions. This preserves the integrity of search results copied to a discovery mailbox.

  - A discovery mailbox can't be repurposed or converted to another type of mailbox.

  - You can remove a discovery mailbox as you would any other type of mailbox.

