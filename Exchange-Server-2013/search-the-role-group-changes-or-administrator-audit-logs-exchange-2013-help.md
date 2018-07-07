---
title: 'Search the role group changes or administrator audit logs: Exchange 2013 Help'
TOCTitle: Search the role group changes or administrator audit logs
ms:assetid: c7188d53-e672-492b-b57d-cd711379ddb3
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ff459262(v=EXCHG.150)
ms:contentKeyID: 50117648
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Search the role group changes or administrator audit logs

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can search the administrator audit logs to discover who made changes to organization, server, and recipient configuration. This can be helpful when you're trying to track the cause of unexpected behavior, to identify a malicious administrator, or to verify that compliance requirements are being met. For more information about administrator audit logging, see [Administrator audit logging](administrator-audit-logging-exchange-2013-help.md).

If you want to search the mailbox audit log, see [Mailbox audit logging](mailbox-audit-logging-exchange-2013-help.md).


> [!TIP]
> In Exchange Online, you can use the EAC to view entries in the administrator audit log. For more information, see <A href="view-the-administrator-audit-log-exchange-2013-help.md">View the administrator audit log</A>.



## What do you need to know before you begin?

  - Estimated time to complete each procedure: less than 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "View-only administrator audit logging" entry in the [Exchange and Shell infrastructure permissions](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) topic.

  - Administrator audit logging is enabled by default. To verify that it’s enabled, run the following command:
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    A value of `True` indicates that administrator audit logging is enabled. A value of `False` indicates that it’s disabled. If you need to enable administrator audit logging for an on-premises Exchange organization, run the following command:
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $true
    

    > [!NOTE]
    > The <STRONG>Set-AdminAuditLogConfig</STRONG> cmdlet isn’t available in Exchange Online.

    
    For more information, see [Manage administrator audit logging](manage-administrator-audit-logging-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the EAC to run the management role group changes report

If you want to know what changes to management role group membership have been made to role groups in your organization, you can use the Administrator Role Group report in the Exchange Administration Center (EAC). Using the Administrator Role Group report, you can view a list of role groups that have changed during a specified date range. You can also select the specific role groups you want to view changes for.

1.  In the EAC, select **Compliance management** \> **Auditing**, and then click **Run an administrator role group report**.

2.  Select a date range using the **Start date** and **End date** fields.

3.  Click **Select role groups**, and then select the role groups you want to show changes for or leave this field blank to search for changes in all role groups.

4.  Click **Search**.

If any changes are found using the criteria you specified, a list of changes will be displayed in the results pane. Clicking a role group displays the changes to the role group in the details pane.

## Use the EAC to export the administrator audit log

If you want to create an XML file that contains changes made to your organization, you can use the Export Administrator Audit Log report in the EAC. Using the Export Administrator Audit Log report, you can specify a date range to search for audit log entries that contain changes made by users you specify. The XML file is then sent to a recipient as an email attachment. The maximum size of the XML file is 10 megabytes (MB).


> [!NOTE]
> Outlook Web App doesn't allow you to open XML attachments by default. You can either configure Exchange to allow XML attachments to be viewed using Outlook Web App, or you can use another email client, such as Microsoft Outlook, to view the attachment. For information about how to configure Outlook Web App to allow you to view an XML attachment, see <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">View or configure Outlook Web App virtual directories</A>.



1.  In the EAC, select **Compliance management** \> **Auditing**, and then click **Export the administrator audit log**.

2.  Select a date range using the **Start date** and **End date** fields.

3.  In the **Send the auditing report to** field, click **Select users** and then select the recipient you want to send the report to.

4.  Click **Export**.

If any log entries are found using the criteria you specified, an XML file will be created and sent as an email attachment to the recipient you specified.

## Use the Shell to search for audit log entries

You can use the Shell to search for audit log entries that meet the criteria you specify. For a list of search criteria, see [Administrator audit logging](administrator-audit-logging-exchange-2013-help.md). This procedure uses the **Search-AdminAuditLog** cmdlet and displays search results in the Shell. You can use this cmdlet when you need to return a set of results that exceeds the limits defined on the **New-AdminAuditLogSearch** cmdlet or in the EAC Audit Reporting reports.

If you want to send audit log search results in an email attachment to a recipient, see Use the Shell to search for audit log entries and send results to a recipient later in this topic.

To search the audit log for criteria you specify, use the following syntax.

    Search-AdminAuditLog - Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False >


> [!NOTE]
> The <STRONG>Search-AdminAuditLog</STRONG> cmdlet returns a maximum of 1,000 log entries by default. Use the <EM>ResultSize</EM> parameter to specify up to 250,000 log entries. Or, use the value <CODE>Unlimited</CODE> to return all entries.



This example performs a search for all audit log entries with the following criteria:

  - **Start date**   08/04/2012

  - **End date**   10/03/2012

  - **User IDs**   davids, chrisd, kima

  - **Cmdlets**   **Set-Mailbox**

  - **Parameters**   *ProhibitSendQuota*, *ProhibitSendReceiveQuota*, *IssueWarningQuota*, *MaxSendSize*, *MaxReceiveSize*

<!-- end list -->

    Search-AdminAuditLog -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima

This example searches for changes made to a specific mailbox. This is useful if you're troubleshooting or you need to provide information for an investigation. The following criteria are used:

  - **Start date**   05/01/2012

  - **End date**   10/03/2012

  - **Object ID**   contoso.com/Users/DavidS

<!-- end list -->

    Search-AdminAuditLog -StartDate 05/01/2012 -EndDate 10/03/2012 -ObjectID contoso.com/Users/DavidS

If your searches return many log entries, we recommend that you use the procedure provided in Use the Shell to search for audit log entries and send results to a recipient later in this topic. The procedure in that section sends an XML file as an email attachment to the recipients you specify, enabling you to more easily extract the data you're interested in.

For detailed syntax and parameter information, see [Search-AdminAuditLog](https://technet.microsoft.com/en-us/library/ff459250\(v=exchg.150\)).

## View details of audit log entries

The **Search-AdminAuditLog** cmdlet returns the fields described in the “Audit log contents section of [Administrator audit logging](administrator-audit-logging-exchange-2013-help.md). Of the fields returned by the cmdlet, two fields, **CmdletParameters** and **ModifiedProperties**, contain additional information that isn't viewable by default.

To view the contents of the **CmdletParameters** and **ModifiedProperties** fields, use the following steps. Or, you can use the procedure in Use the Shell to search for audit log entries and send results to a recipient later in this topic to create an XML file.

This procedure uses the following concepts:

  - [Arrays](https://technet.microsoft.com/en-us/library/aa998267\(v=exchg.150\))

  - [User-defined variables](https://technet.microsoft.com/en-us/library/bb123690\(v=exchg.150\))

<!-- end list -->

1.  Decide the criteria you want to search for, run the **Search-AdminAuditLog** cmdlet, and store the results in a variable using the following command.
    
        $Results = Search-AdminAuditLog <search criteria>

2.  Each audit log entry is stored as an array element in the variable `$Results`. You can select an array element by specifying its array element index. Array element indexes start at zero (0) for the first array element. For example, to retrieve the 5th array element, which has an index of 4, use the following command.
    
        $Results[4]

3.  The previous command returns the log entry stored in array element 4. To see the contents of the **CmdletParameters** and **ModifiedProperties** fields for this log entry, use the following commands.
    
        $Results[4].CmdletParameters
        $Results[4].ModifiedProperties

4.  To view the contents of the **CmdletParameters** or **ModifiedParameters** fields in another log entry, change the array element index.

## Use the Shell to search for audit log entries and send results to a recipient

You can use the Shell to search for audit log entries that meet the criteria you specify, and then send those results to a recipient you specify as an XML file attachment. The results are sent to the recipient within 15 minutes. For a list of search criteria, see [Administrator audit logging](administrator-audit-logging-exchange-2013-help.md).


> [!NOTE]
> Outlook Web App doesn't allow you to open XML attachments by default. You can either configure Exchange to allow XML attachments to be viewed using Outlook Web App, or you can use another email client, such as Microsoft Outlook, to view the attachment. For information about how to configure Outlook Web App to allow you to view an XML attachment, see <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">View or configure Outlook Web App virtual directories</A>.



To search the audit log for criteria you specify, use the following syntax.

    New-AdminAuditLogSearch -Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False > -StatusMailRecipients <recipient 1, recipient 2, ...> -Name <string to include in subject>

This example performs a search for all audit log entries with the following criteria:

  - **Start date**   08/04/2012

  - **End date**   10/03/2012

  - **User IDs**   davids, chrisd, kima

  - **Cmdlets**   **Set-Mailbox**

  - **Parameters**   *ProhibitSendQuota*, *ProhibitSendReceiveQuota*, *IssueWarningQuota*, *MaxSendSize*, *MaxReceiveSize*

The command sends the results to the davids@contoso.com SMTP address with "Mailbox limit changes" included in the subject line of the message.

    New-AdminAuditLogSearch -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima -StatusMailRecipients davids@contoso.com -Name "Mailbox limit changes"


> [!NOTE]
> The report that the <STRONG>New-AdminAuditLogSearch</STRONG> cmdlet generates can be a maximum of 10&nbsp;MB in size. If the search you perform returns a report larger than 10&nbsp;MB, change the search criteria you specified. For example, reduce the size of the date range and run multiple reports, each with a portion of the original date range.



For more information about the format of the XML file, see [Administrator audit log structure](administrator-audit-log-structure-exchange-2013-help.md).

For detailed syntax and parameter information, see [New-AdminAuditLogSearch](https://technet.microsoft.com/en-us/library/ff459243\(v=exchg.150\)).

