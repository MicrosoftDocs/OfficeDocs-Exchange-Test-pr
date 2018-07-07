---
title: 'Export mailbox audit logs: Exchange 2013 Help'
TOCTitle: Export mailbox audit logs
ms:assetid: b458a95a-3321-4647-8884-cf97f8e7186a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150552(v=EXCHG.150)
ms:contentKeyID: 47560079
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Export mailbox audit logs

 

_**Applies to:** Exchange Online, Exchange Server 2013_


When mailbox auditing is enabled for a mailbox, Microsoft Exchange logs information in the *mailbox audit log* whenever a user other than the owner accesses the mailbox. Each log entry includes information about who accessed the mailbox and when, the actions performed by the non-owner, and whether the action was successful. Entries in the mailbox audit log are retained for 90 days by default. You can use the mailbox audit log to determine if a user other than the owner has accessed a mailbox.

When you export entries from mailbox audit logs, Microsoft Exchange saves the entries in an XML file and attaches it to an email message sent to the specified recipients.

**Contents**

Before you begin

Configure mailbox audit logging

Export the mailbox audit log

View the mailbox audit log

More information

## Before you begin

  - Estimated time to complete each procedure: Times are variable. In Exchange Online, the mailbox audit log is sent within a few days after you export it.

  - In Exchange Online, you have to use Remote Windows PowerShell to perform many of the procedures in this topic. For details, see [Connect to Exchange Online using remote PowerShell](https://technet.microsoft.com/en-us/library/jj984289\(v=exchg.150\)).

  - Procedures in this topic require specific permissions. See each procedure for its permissions information.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Configure mailbox audit logging

You have to enable mailbox audit logging on each mailbox that you want to audit before you can export and view mailbox audit logs. You also have to configure Microsoft Outlook Web App to allow XML attachments to use Outlook Web App to access the audit log.

## Step 1: Enable mailbox audit logging

You have to enable mailbox audit logging for each mailbox that you want to run a non-owner mailbox access report for. If mailbox audit logging isn't enabled for a mailbox, you won't get any results for that mailbox when you export the mailbox audit log.

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox audit logging" entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

To enable mailbox audit logging for a single mailbox, run the command in the Shell.

    Set-Mailbox <Identity> -AuditEnabled $true

To enable mailbox audit logging for all user mailboxes in your organization, run the following commands.

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}

    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

## Step 2: Configure Outlook Web App to allow XML attachments

When you export the mailbox audit log, Microsoft Exchange attaches the audit log, which is an XML file, to an email message. However, Outlook Web App blocks XML attachments by default. To access the exported audit log, you have to use Microsoft Outlook or configure Outlook Web App to allow XML attachments.

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Outlook Web App mailbox policies" entry in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

Perform the following procedures to allow XML attachments in Outlook Web App. In Exchange Server 2013, use the value `Default` for the *Identity* parameter.

1.  Run the following command to add XML to the list of allowed file types in Outlook Web App.
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -AllowedFileTypes @{add='.xml'}

2.  Run the following command to remove XML from the list of blocked file types in Outlook Web App.
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -BlockedFileTypes @{remove='.xml'}

## How do you know this worked?

To verify that you’ve successfully configured mailbox audit logging, do the following:

1.  Run the following command to verify that audit logging is configured for mailboxes.
    
        Get-Mailbox | FL Name,AuditEnabled
    
    A value of `True` for the *AuditEnabled* property verifies that audit logging is enabled.

2.  Run the following command to verify that XML attachments are allowed in Outlook Web App.
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty AllowedFileTypes
    
    Verify that `.xml` is included in the list of allowed file types.

3.  Run the following command to verify that XML attachments are removed from the blocked file list in Outlook Web App.
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty BlockedFileTypes
    
    Verify that `.xml` isn’t included in the list of blocked file types.

Return to top

## Export the mailbox audit log

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "View-only administrator audit logging" entry in the [Exchange and Shell infrastructure permissions](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) topic.

1.  In the Exchange admin center (EAC), go to **Compliance Management** \> **Auditing**.

2.  Click **Export mailbox audit logs**.

3.  Configure the following search criteria for exporting the entries from the mailbox audit log:
    
      - **Start and end dates**   Select the date range for the entries to include in the exported file.
    
      - **Mailboxes to search audit log for**   Select the mailboxes to retrieve audit log entries for.
    
      - **Type of non-owner access**   Select one of the following options to define the type of non-owner access to retrieve entries for:
        
          - **All non-owners**   Search for access by administrators and delegated users inside your organization, and by Microsoft datacenter administrators in Exchange Online.
        
          - **External users**   Search for access by Microsoft datacenter administrators.
        
          - **Administrators and delegated users**   Search for access by administrators and delegated users inside your organization.
        
          - **Administrators**   Search for access by administrators in your organization.
    
      - **Recipients**   Select the users to send the mailbox audit log to.

4.  Click **Export**.
    
    Microsoft Exchange retrieves entries in the mailbox audit log that meet your search criteria, saves them to a file named SearchResult.xml, and then attaches the XML file to an email message sent to the recipients that you specified.

## How do you know this worked?

Sign in to the mailbox where the mailbox audit log was sent. If you’ve successfully exported the audit log, you’ll receive a message sent from Exchange. In Exchange Online, it may take a few days to receive this message. The mailbox audit log (named SearchResult.xml) will be attached to this message. If you’ve correctly configured Outlook Web App to allow XML attachments, you can download the attached XML file.

Return to top

## View the mailbox audit log

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "View-only administrator audit logging" entry in the [Exchange and Shell infrastructure permissions](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) topic.

To save and view the SearchResult.xml file:

1.  Sign in to the mailbox where the mailbox audit log was sent.

2.  In the Inbox, open the message with the XML file attachment sent by Microsoft Exchange. Notice that the body of the email message contains the search criteria.

3.  Click the attachment and select to download the XML file.

4.  Open the SearchResult.xml in Microsoft Excel.

Return to top

## More information

  - **Entries in the mailbox audit log**   The following example shows an entry from the mailbox audit log contained in the SearchResult.xml file. Each entry is preceded by the **\<Event\>** XML tag and ends with the **\</Event\>** XML tag. This entry shows that the administrator purged the message with the subject, "**Notification of litigation hold**" from the Recoverable Items folder in David's mailbox on April 30, 2010.
    
        <Event MailboxGuid="6d4fbdae-e3ae-4530-8d0b-f62a14687939" 
          Owner="PPLNSL-dom\david50001-1363917750" 
          LastAccessed="2010-04-30T11:01:55.140625-07:00" 
          Operation="HardDelete" 
          OperationResult="Succeeded" 
          LogonType="Admin"
         FolderId="0000000073098C3277988F4CB882F5B82EBF64610100A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000"
          FolderPathName="\Recoverable Items\Deletions"
          ClientInfoString="Client=OWA;Action=ViaProxy" 
          ClientIPAddress="10.196.241.168" 
          InternalLogonType="Owner"
          MailboxOwnerUPN="david@contoso.com"
          MailboxOwnerSid="S-1-5-21-290112810-296651436-1966561949-1151" 
          CrossMailboxOperation="false" 
          LogonUserDN="Administrator"
          LogonUserSid="S-1-5-21-290112810-296651436-1966561949-1149">
          <SourceItems>
           <ItemId="0000000073098C3277988F4CB882F5B82EBF64610700A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000A7C317F68C24304BBD18ABE1F185E79B00000026BD540"
            Subject="Notification of litigation hold"
            FolderPathName="\Recoverable Items\Deletions" /> 
          </SourceItems>
        </Event>

  - **Useful fields in the mailbox audit log**   Here’s a description of useful fields in the mailbox audit log. They can help you identify specific information about each instance of non-owner access of a mailbox.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Field</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Owner</strong></p></td>
    <td><p>The owner of the mailbox that was accessed by a non-owner.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>LastAccessed</strong></p></td>
    <td><p>The date and time when the mailbox was accessed.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Operation</strong></p></td>
    <td><p>The action that was performed by the non-owner. For more information, see the &quot;What gets logged in the mailbox audit log?&quot; section in <a href="https://technet.microsoft.com/en-us/library/jj156300(v=exchg.150)">Learn more about running a non-owner mailbox access report</a>.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OperationResult</strong></p></td>
    <td><p>Whether the action performed by the non-owner succeeded or failed.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonType</strong></p></td>
    <td><p>The type of non-owner access. These include administrator, delegate, and external.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>FolderPathName</strong></p></td>
    <td><p>The name of the folder that contained the message that was affected by the non-owner.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>ClientInfoString</strong></p></td>
    <td><p>Information about the mail client used by the non-owner to access the mailbox.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ClientIPAddress</strong></p></td>
    <td><p>The IP address of the computer used by the non-owner to access the mailbox.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>InternalLogonType</strong></p></td>
    <td><p>The logon type of the account used by the non-owner to access this mailbox.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>MailboxOwnerUPN</strong></p></td>
    <td><p>The email address of the mailbox owner.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonUserDN</strong></p></td>
    <td><p>The display name of the non-owner.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Subject</strong></p></td>
    <td><p>The subject line of the email message that was affected by the non-owner.</p></td>
    </tr>
    </tbody>
    </table>
    
    Return to top

