﻿---
title: 'Exchange auditing reports: Exchange 2013 Help'
TOCTitle: Exchange auditing reports
ms:assetid: 2b3e1529-1677-4564-be0b-ce22757ddc0d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150497(v=EXCHG.150)
ms:contentKeyID: 47559963
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Exchange auditing reports

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Use audit logging to troubleshoot configuration issues by tracking specific changes made by administrators and to help you meet regulatory, compliance, and litigation requirements. Microsoft Exchange provides two types of audit logging:

  - *Administrator audit logging* records any action, based on an Exchange Management Shell cmdlet, performed by an administrator. This can help you troubleshoot configuration issues or identify the cause of security-related or compliance-related problems. In Exchange Online, actions performed by Microsoft administrators and delegated administrators, are also recorded.

  - *Mailbox audit logging* records when a mailbox is accessed by an administrator, a delegated user, or the person who owns the mailbox. This can help you determine who has accessed a mailbox and what they’ve done.

This topic explains the following:

  - Export audit logs

  - Run auditing reports

  - Configure audit logging
    
      - Enable mailbox audit logging
    
      - Give users access to auditing reports
    
      - Configure Outlook Web App to allow XML attachments

## Export audit logs

On the **Compliance Management** \> **Auditing** page in the Exchange admin center (EAC), you can search for and export entries from the administrator audit log and the mailbox audit log.

  - **Export the administrator audit log**   Any action performed by an administrator that’s based on a Shell cmdlet and doesn't begin with the verbs **Get**, **Search**, or **Test** is logged in the administrator audit log. Audit log entries include the cmdlet that was run, the parameter and values used with the cmdlet, and when the operation was successful. You can search for and export entries from the administrator audit log. When you export your search results, Microsoft Exchange saves them in an XML file and attaches it to an email message. For more information, see:
    
      - [Search the role group changes or administrator audit logs](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)
    
      - [View and export the external admin audit log](https://technet.microsoft.com/en-us/library/dn505728\(v=exchg.150\))
    

    > [!NOTE]
    > By default, admin audit log entries are kept for 90&nbsp;days. When an entry is older than 90&nbsp;days, it's deleted. This setting can’t be changed in a cloud-based organization. However, it can be changed in an on-premises Exchange organization by using the <STRONG>Set-AdminAuditLog</STRONG> cmdlet.



  - **Export mailbox audit logs**   When mailbox audit logging is enabled for a mailbox, Microsoft Exchange stores a record of actions performed on mailbox data by non-owners in the mailbox audit log, which is stored in a hidden folder in the mailbox being audited. Mailbox audit logging can also be configure to log owner actions. Entries in this log indicate who accessed the mailbox and when, the actions performed, and whether the action was successful. When you search for entries in the mailbox audit log and export them, Microsoft Exchange saves the search results in an XML file and attaches it to an email message. For more information, see [Export mailbox audit logs](export-mailbox-audit-logs-exchange-2013-help.md).

## Run auditing reports

When you run any of the following reports on the **Auditing** page in the EAC, the results are displayed in the details pane of the report.

  - **Run a non-owner mailbox access report**   Use this report to find mailboxes that have been accessed by someone other than the person who owns the mailbox. For more information, see [Run a non-owner mailbox access report](run-a-non-owner-mailbox-access-report-exchange-online-help.md).

  - **Run an administrator role group report**   Use this report to search for changes made to administrator role groups. For more information, see [Search the role group changes or administrator audit logs](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

  - **Run an in-place discovery and hold report**   Use this report to find mailboxes that have been put on, or removed from, In-Place Hold. For more information, see:
    
      - [In-Place Hold and Litigation Hold](in-place-hold-and-litigation-hold-exchange-2013-help.md)
    
      - [In-Place eDiscovery](in-place-ediscovery-exchange-2013-help.md)

  - **Run a per-mailbox litigation hold report**   Use this report to find mailboxes that were put on, or removed from, litigation hold. For more information, see.
    
      - [Run a per-mailbox litigation hold report](run-a-per-mailbox-litigation-hold-report-exchange-2013-help.md)
    
      - [Place a mailbox on Litigation Hold](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - **Run the admin audit log report**   Use this report to view entries from the administrator audit log. Instead of exporting the administrator audit log, which can take up to 24 hours to receive in an email message, you can run this report in the EAC. This report records configuration changes made by administrators in your organization. Up to 5000 entries will be displayed on multiple pages. To narrow the search, you can specify a date range. For more information, see:
    
      - [View the administrator audit log](view-the-administrator-audit-log-exchange-2013-help.md)
    
      - [Administrator audit logging](administrator-audit-logging-exchange-2013-help.md)

  - **Run the external admin audit log report**   This report is only available in Exchange Online and Exchange Online Protection. Actions performed by Microsoft administrators or delegated administrators are logged in the administrator audit log. Use the external admin audit log report to search for and view the actions that administrators outside your organization performed on the configuration of your Exchange Online organization. For more information, see [View and export the external admin audit log](https://technet.microsoft.com/en-us/library/dn505728\(v=exchg.150\)).

## Configure audit logging

Before you can run auditing reports and export audit logs, you have to configure audit logging for your organization.

## Enable mailbox audit logging

You have to enable mailbox audit logging for each mailbox that you want to run a non-owner mailbox access report for. If mailbox audit logging isn't enabled for a mailbox, you won't get any results when you run a report for it or export the mailbox audit log.

To enable mailbox audit logging for a single mailbox, run the following command in the Shell.

    Set-Mailbox <Identity> -AuditEnabled $true

To enable mailbox auditing for all user mailboxes in your organization, run the following commands.

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

For more information about configuring which actions are logged, see:

  - **Exchange 2013**   [Enable or disable mailbox audit logging for a mailbox](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)

  - **Exchange Online**   [Enable mailbox auditing in Office 365](https://go.microsoft.com/fwlink/p/?linkid=626109)

## Give users access to Auditing reports

By default, administrators can access and run any of the reports on the Auditing page in the EAC. However, other users, such as a records manager or legal staff, have to be assigned the necessary permissions.

The easiest way to give users access is to add them to the Records Management role group. You can also use the Shell to give a user access to the **Auditing** page in the EAC by assigning the Audit Logs role to the user.

## Add a user to the Records Management role group

1.  Go to **Permissions** \> **Admin Roles**.

2.  In the list of role groups, click **Records Management**, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  Under **Members**, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

4.  In the **Select Members** dialog box, select the user. You can search for a user by typing all or part of a display name, and then clicking **Search** ![Search icon](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Search icon"). You can also sort the list by clicking the **Name** or **Display Name** column headings.

5.  Click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") and then click **OK** to return to the role group page.

6.  Click **Save** to save the change to the role group.

In the details pane, the user is listed under **Members** and can access the Auditing page in the EAC, run auditing reports, and export audit logs.

## Assign the Audit Logs role to a user

Run the following command to assign the Audit Logs role to a user.

    New-ManagementRoleAssignment -Role "Audit Logs" -User <Identity>

This enables the user to select **Compliance Management** \> **Auditing** in the EAC to run any of the reports. The user can also export the mailbox audit log, and export and view the administrator audit log.


> [!NOTE]
> To allow a user to run auditing reports but not to export audit logs, use the preceding command to assign the View-Only Audit Logs role.



## Configure Outlook Web App to allow XML attachments

When you export the mailbox audit log or administrator audit log, Microsoft Exchange attaches the audit log, which is an XML file, to an email message. However, Outlook Web App blocks XML attachments by default. If you want to use Outlook Web App to access these audit logs, you have to configure Outlook Web App to allow XML attachments.

Run the following command to allow XML attachments in Outlook Web App.

    Set-OwaMailboxPolicy -Identity Default -AllowedFileTypes '.rpmsg','.xlsx','.xlsm','.xlsb','.tiff','.pptx','.pptm','.ppsx','.ppsm','.docx','.docm','.zip','.xls','.wmv','.wma','.wav','.vsd','.txt','.tif','.rtf','.pub','.ppt','.png','.pdf','.one','.mp3','.jpg','.gif','.doc','.bmp','.avi','.xml'

