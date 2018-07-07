---
title: 'Administrator audit logging: Exchange 2013 Help'
TOCTitle: Administrator audit logging
ms:assetid: 22b17eb8-d8ee-4599-b202-d6a7928c20d9
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd335144(v=EXCHG.150)
ms:contentKeyID: 50117641
ms.date: 03/05/2018
mtps_version: v=EXCHG.150
---

# Administrator audit logging

 

_**Applies to:** Exchange Server 2013_


You can use administrator audit logging in Microsoft Exchange Server 2013 to log when a user or administrator makes a change in your organization. By keeping a log of the changes, you can trace changes to the person who made the change, augment your change logs with detailed records of the change as it was implemented, comply with regulatory requirements and requests for discovery, and more.

By default, audit logging is enabled in new installations of Exchange 2013.

**Contents**

What gets audited

Audit logging configuration

Audit logs

Manual audit log entries

Active Directory replication

Admin Audit Log agent

## What gets audited

Cmdlets that are run directly in the Exchange Management Shell are audited. In addition, operations performed using the Exchange admin center (EAC) are also logged because those operations run cmdlets in the background.

Cmdlets, regardless of where they're run, are audited if a cmdlet is on the cmdlet auditing list and one or more parameters on that cmdlet are on the parameter auditing list. Audit logging is intended to show what actions have been taken to modify objects in an Exchange organization rather than what objects have been viewed.


> [!IMPORTANT]
> A cmdlet might not be logged if an error occurs before the cmdlet calls the Admin Audit Log cmdlet extension agent. If an error occurs after the Admin Audit Log agent is called, the cmdlet is logged along with the associated error. For more information, see the Admin Audit Log Agent section later in this topic.<BR>Changes made using Microsoft Exchange Server 2010 management tools are logged; however, changes using Microsoft Exchange Server 2007 management tools aren't logged.<BR>Changes to the audit log configuration are refreshed every 60 minutes on computers that have the Shell open at the time a configuration change is made. If you want to apply the changes immediately, close and then open the Shell again on each computer.<BR>A command may take up to 15 minutes after it's run to appear in audit log search results. This is because audit log entries must be indexed before they can be searched. If a command doesn't appear in the administrator audit log, wait a few minutes and run the search again.



## Audit logging configuration

By default, if audit logging is enabled, a log entry is created every time any cmdlet is run. If you don't want to audit every cmdlet that's run, you can configure audit logging to audit only the cmdlets and parameters you're interested in. You configure audit logging with the **Set-AdminAuditLogConfig** cmdlet. The parameters referenced in the following sections are used with this cmdlet.


> [!IMPORTANT]
> Changes to the administrator audit log configuration are always logged, regardless of whether the <STRONG>Set-AdministratorAuditLog</STRONG> cmdlet is included in the list of cmdlets being audited and whether audit logging is enabled or disabled.



When a command is run, Exchange inspects the cmdlet that was used. If the cmdlet that was run matches any of the cmdlets provided with the *AdminAuditLogConfigCmdlets* parameter, Exchange then checks the parameters specified in the *AdminAuditLogConfigParameters* parameter. If at least one or more parameters from the parameters list are matched, Exchange logs the cmdlet that was run in the mailbox specified using the *AdminAuditLogMailbox* parameter. The following sections contain more information about each aspect of the audit logging configuration.

For more information about managing audit logging configuration, see [Manage administrator audit logging](manage-administrator-audit-logging-exchange-2013-help.md).

Return to top

## Cmdlets

You can control which cmdlets are audited by providing a list of cmdlets, and their parameters, that you want to log. When you configure audit logging, you can specify to audit every cmdlet, or you can specify the cmdlets you want to audit by using the *AdminAuditLogConfigCmdlets* parameter. You can specify full cmdlet names, such as **New-Mailbox**, or you can specify partial cmdlet names and enclose those names in wildcard characters, such as an asterisk (`*`). For example, if you want to log when any cmdlet that contains the string `Transport` runs, you can specify a value of `*Transport*`. You can use a mix of full cmdlet names and partial cmdlet names at the same time to tailor the audit logging configuration to your needs.

## Parameters

In addition to specifying which cmdlets you want to log, you can also indicate that cmdlets should only be logged if certain parameters on those cmdlets are used. Use the *AdminAuditLogConfigParameters* parameter to specify which parameters should be logged. As with cmdlets, you can specify full parameter names, such as `Database`, or partial parameter names enclosed in wildcard characters (`*`), such as `*Address*`, or a combination of both.

## Audit log age limit

By default, audit logging is configured to store audit log entries for 90 days. After 90 days, the audit log entry is deleted. You can change the audit log age limit using the *AdminAuditLogAgeLimit* parameter. You can specify the number of days, hours, minutes, and seconds that audit log entries should be kept. To specify a value, use the format `dd.hh:mm:ss` where the following applies:

  - **dd**   The number of days to keep the audit log entry.

  - **hh**   The number of hours to keep the audit log entry.

  - **mm**   The number of minutes to keep the audit log entry.

  - **ss**   The number of seconds to keep the audit log entry.

You must specify multiple years using the `dd` field. For example, 365 days equals one year; 730 days equals two years; 913 days equals two years and six months. For example, to set the audit log age limit to two years and six months, use the syntax `913.00:00:00`.


> [!WARNING]
> You can set the audit log age limit to a value that's less than the current age limit. If you do this, any audit log entry whose age exceeds the new age limit is deleted.<BR>If you set the age limit to 0, Exchange deletes all the entries in the audit log.<BR>We recommend that you grant permissions to configure the audit log age limit only to highly trusted users.



## Verbose logging

By default, the administrator audit log records only the cmdlet name, cmdlet parameters (and values specified), the object that was modified, who ran the cmdlet, when the cmdlet was run, and on what server the cmdlet was run. The administrator audit log doesn’t log what properties were modified on the object. If you want the audit log to also include the properties of the object that were modified, you can enable verbose logging by setting the *LogLevel* parameter to `Verbose`. When you enable verbose logging, in addition to the information logged by default, the properties modified on an object, including their old and new values, are included in the audit log.

## Test cmdlets

Cmdlets that begin with the verb **Test** aren't logged by default. You can indicate that **Test** cmdlets should be logged by setting the *TestCmdletLoggingEnabled* parameter to `$true`. Although you can enable logging of test cmdlets, we recommend that you do this only for short periods of time because test cmdlets can produce a large amount of information.

## Audit logs

Each time a cmdlet is logged, an audit log entry is created. Audit logs are stored in a hidden, dedicated arbitration mailbox that can only be accessed using the EAC or the **Search-AdminAuditLog** or **New-AdminAuditLogSearch** cmdlet. It can't be opened using Microsoft Outlook Web App or Microsoft Outlook. The following sections provide information about the following:

  - What's included in the logs

  - Reports available on the EAC **auditing** page

  - Audit log search cmdlets

## Audit log contents

Each audit log entry contains the information described in the following table. The audit log contains one or more audit log entries. The number of audit log entries is controlled by the audit log age limit specified using the **Set-AdminAuditLogConfig** cmdlet. Any audit log entry that exceeds the age limit is deleted.

### Audit log entry fields

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
<td><p><code>RunspaceId</code></p></td>
<td><p>This field is used internally by Exchange.</p></td>
</tr>
<tr class="even">
<td><p><code>ObjectModified</code></p></td>
<td><p>This field contains the object that was modified by the cmdlet specified in the <code>CmdletName</code> field.</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletName</code></p></td>
<td><p>This field contains the name of the cmdlet that was run by the user in the <code>Caller</code> field.</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletParameters</code></p></td>
<td><p>This field contains the parameters that were specified when the cmdlet in the <code>CmdletName</code> field was run. Also stored in this field, but not visible in the default output, is the value specified with the parameter, if any. For more information about how to access the additional information in this field, see <a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">Search the role group changes or administrator audit logs</a>.</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p>This field contains the properties that were modified on the object in the <code>ObjectModified</code> field. Also stored in this field, but not visible in the default output, are the old value of the property and the new value that was stored. For more information about how to access the additional information in this field, see <a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">Search the role group changes or administrator audit logs</a>.</p>

> [!IMPORTANT]
> This field is only populated if the <EM>LogLevel</EM> parameter on the <STRONG>Set-AdminAuditLogConfig</STRONG> cmdlet is set to <CODE>Verbose</CODE>.


</td>
</tr>
<tr class="even">
<td><p><code>Caller</code></p></td>
<td><p>This field contains the user account of the user who ran the cmdlet in the <code>CmdletName</code> field.</p></td>
</tr>
<tr class="odd">
<td><p><code>Succeeded</code></p></td>
<td><p>This field specifies whether the cmdlet in the <code>CmdletName</code> field ran successfully. The value is either <code>True</code> or <code>False</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Error</code></p></td>
<td><p>This field contains the error message generated if the cmdlet in the <code>CmdletName</code> field failed to complete successfully.</p></td>
</tr>
<tr class="odd">
<td><p><code>RunDate</code></p></td>
<td><p>This field contains the date and time when the cmdlet in the <code>CmdletName</code> field was run. The date and time are stored in Coordinated Universal Time (UTC) format.</p></td>
</tr>
<tr class="even">
<td><p><code>OriginatingServer</code></p></td>
<td><p>This field indicates the server on which the cmdlet specified in the <code>CmdletName</code> field was run.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>This field is used internally by Exchange.</p></td>
</tr>
<tr class="even">
<td><p><code>IsValid</code></p></td>
<td><p>This field is used internally by Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><code>ObjectState</code></p></td>
<td><p>This field is used internally by Exchange.</p></td>
</tr>
</tbody>
</table>


Return to top

## EAC auditing reports

The **auditing** page in the EAC has several reports that provide information about various types of compliance and administrative configuration changes. The following reports provide information about configuration changes in your organization:

  - **Administrator role group report**   This report enables you to search for changes to management role groups that you specify within a specified timeframe. The results that are returned include the role groups that have been changed, who changed them and when, and what changes were made. A maximum of 3,000 entries can be returned. If your search might return more than 3,000 entries, use the **Administrator audit log** report or the **Search-AdminAuditLog** cmdlet.

  - **Administrator audit log**   This report enables you to export the audit log entries recorded within a specified timeframe to a XML file and then send the file via email to a recipient you specify. For more information about the contents of the XML file, see [Administrator audit log structure](administrator-audit-log-structure-exchange-2013-help.md).

For information about how to use these reports, see [Search the role group changes or administrator audit logs](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

For information about the other reports included on the **auditing** page see [Exchange auditing reports](exchange-auditing-reports-exchange-2013-help.md).

## Search-AdminAuditLog cmdlet

When you run the **Search-AdminAuditLog** cmdlet, all the audit log entries that match the search criteria you specify are returned. You can specify the following search criteria:

  - **Cmdlets**   Specifies the cmdlets you want to search for in the administrator audit log.

  - **Parameters**   Specifies the parameters, separated by commas, you want to search for in the administrator audit log. You can only search for parameters if you specify a cmdlet to search for.

  - **End date**   Scopes the administrator audit log results to log entries that occurred on or before the specified date.

  - **Start date**   Scopes the administrator audit log results to log entries that occurred on or after the specified date.

  - **Object IDs**   Specifies that only administrator audit log entries that contain the specified changed objects should be returned

  - **User IDs**   Specifies that only the administrator audit log entries that contain the specified IDs of the user who ran the cmdlet should be returned.

  - **Successful completion**   Specifies whether only administrator audit log entries that indicated a success or failure should be returned.

Each audit log entry returned contains the information described in the table in Audit Log Contents. By default, only the first 1,000 log entries that match the criteria you specify are returned. However, you can override this default and return more or fewer entries using the *ResultSize* parameter. You can specify a value of `Unlimited` with the *ResultSize* parameter to return all log entries that match the specified criteria.

For information about how to use the **Search-AdminAuditLog** cmdlet, see [Search the role group changes or administrator audit logs](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

## New-AdminAuditLogSearch cmdlet

The **New-AdminAuditLogSearch** cmdlet searches the audit log just like the **Search-AdminAuditLog** cmdlet. However, instead of displaying the results of the audit log search in the Shell, the **New-AdminAuditLogSearch** cmdlet performs the search and then sends the results of the search to a recipient you specify via an email message. The results are included as an XML attachment to the email message.

You can use the same search criteria with the **New-AdminAuditLogSearch** cmdlet that's used on the **Search-AdminAuditLog** cmdlet. For a list of the search criteria, see Search-AdminAuditLog Cmdlet.

After you run the **New-AdminAuditLogSearch** cmdlet, Exchange may take up to 15 minutes to deliver the report to the specified recipient. The XML file attached report can be a maximum of 10 megabytes (MB). The XML file contains the same information described in the table in Audit Log Contents. For more information about the structure of the XML file, see [Administrator audit log structure](administrator-audit-log-structure-exchange-2013-help.md).


> [!NOTE]
> Outlook Web App doesn't allow you to open XML attachments by default. You can either configure Exchange to allow XML attachments to be viewed using Outlook Web App, or you can use another email client, such as Microsoft Outlook, to view the attachment. For information about how to configure Outlook Web App to allow you to view an XML attachment, see <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">View or configure Outlook Web App virtual directories</A>.



For information about how to use the **New-AdminAuditLogSearch** cmdlet, see [Search the role group changes or administrator audit logs](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

Return to top

## Manual audit log entries

In addition to logging Exchange cmdlets when they're run, Exchange 2013 enables you to manually write log entries to the audit log. Exchange 2013 supports this using the **Write-AdminAuditLog** cmdlet. Situations where you might want to add a manual log entry include the following:

  - Custom script entry and exit

  - Change control information

  - Maintenance start and end times

With the **Write-AdminAuditLog** cmdlet, you specify a string of text to include in the audit log using the *Comment* parameter. The *Comment* parameter accepts an alphanumeric string up to 500 characters. Included in the manual audit log entry along with the comment string is all of the same information captured when an Exchange cmdlet is logged. For a description of each field included in the audit log, see the table in Audit Log Contents.

You can retrieve manual audit log entries the same way as any other log entry, using the EAC **auditing** page or using the **Search-AdminAuditLog** or **New-AdminAuditLogSearch** cmdlets.

To view the contents of the *Comment* parameter on the **Write-AdminAuditLog** cmdlet in a manual audit log entry, see [Search the role group changes or administrator audit logs](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

## Active Directory replication

Administrator audit logging relies on Active Directory replication to replicate the configuration settings you specify to the domain controllers in your organization. Depending on your replication settings, the changes you make may not be immediately applied to all servers running Exchange 2013 or Exchange 2010 in your organization.

## Admin Audit Log agent

The Admin Audit Log built-in cmdlet extension agent performs administrator audit logging of cmdlet operations in Exchange 2013. This agent reads the audit log configuration and then performs an evaluation of each cmdlet run in your organization. If the criteria you've specified in the audit log configuration matches the cmdlet that's being run, the agent generates an audit log.

The Admin Audit Log agent is enabled by default, which is required for audit logging to function. It can't be disabled, and its priority can't be changed. For more information about cmdlet extension agents, see [Cmdlet extension agents](cmdlet-extension-agents-exchange-2013-help.md).

