---
title: 'Clients and mobile devices permissions: Exchange 2013 Help'
TOCTitle: Clients and mobile devices permissions
ms:assetid: 57eca42a-5a7f-4c65-89f0-7a84f2dbea19
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd638131(v=EXCHG.150)
ms:contentKeyID: 48385114
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Clients and mobile devices permissions

 

_**Applies to:** Exchange Server 2013_


The permissions required to perform tasks for clients and mobile devices vary depending on the procedure being performed or the cmdlet you want to run. For more information about client and mobile device features, see [Clients and mobile](clients-and-mobile-exchange-2013-help.md).

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1.  In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2.  Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3.  Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.
    

    > [!NOTE]
    > You must be assigned the Role Management management role to run the <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet. If you don't have permissions to run the <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.



If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).


> [!NOTE]
> Some features may require that you have local administrator permissions on the server you want to manage. To manage these features, you must be a member of the Local Administrators group on that server.



## Client Access server permissions

You can configure any of the following features for the Client Access server.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissions required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client Access server array settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Client Access server settings</p></td>
<td><p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Client Access service email channel settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Client Access user settings</p></td>
<td><p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Client Access virtual directory settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>RPC Client Access settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Push notification proxy settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>OAuth authentication redirection settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
</tbody>
</table>


## Exchange ActiveSync permissions

You can configure any of the following for Exchange ActiveSync.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissions required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange ActiveSync Autoblock settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync mailbox policy settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync server settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync user settings</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync virtual directory settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Mobile device mailbox policy settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Mobile device user settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
</tbody>
</table>


## Autodiscover permissions

You can configure the following for the Autodiscover service.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissions required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autodiscover service configuration settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Delegated Setup</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
</tr>
<tr class="even">
<td><p>Autodiscover virtual directory settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
</tbody>
</table>


## Availability service permissions

You can configure the following for the Availability service.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissions required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Availability service address space settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Availability service configuration settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p></td>
</tr>
</tbody>
</table>


## Client throttling permissions

You can configure the following for client throttling.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissions required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client throttling settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p></td>
</tr>
</tbody>
</table>


## Exchange Web Services permissions

You can configure the following for Web Services virtual directories.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissions required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Web Services virtual directory settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Test Exchange Web Services</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Test Outlook Web Services</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
</tbody>
</table>


## Outlook Anywhere permissions

You can configure and manage the following settings for Outlook Anywhere.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissions required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook Anywhere configuration (enable, disable, change, view)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Delegated Setup</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
</tr>
<tr class="even">
<td><p>RPC over HTTP Proxy component</p></td>
<td><p>Local Server Administrator</p></td>
</tr>
<tr class="odd">
<td><p>Test Outlook Anywhere connectivity</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
</tbody>
</table>


## Outlook Web App permissions

You can use the following features to view Outlook Web App settings, control security and user access to Outlook Web App, and test Outlook Web App connectivity.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissions required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Graphics editor</p></td>
<td><p>Local Server Administrator</p></td>
</tr>
<tr class="even">
<td><p>IIS Manager</p></td>
<td><p>Local Server Administrator</p></td>
</tr>
<tr class="odd">
<td><p>ISA Server 2006</p></td>
<td><p>ISA Server Enterprise Administrator</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App mailbox policies</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Outlook Web App virtual directories</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Registry Editor</p></td>
<td><p>Local Server Administrator</p></td>
</tr>
<tr class="odd">
<td><p>S/MIME configuration</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Text editor</p></td>
<td><p>Local Server Administrator</p></td>
</tr>
<tr class="odd">
<td><p>View Outlook Web App mailbox policies</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Delegated Setup</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
</tr>
</tbody>
</table>


## POP3 and IMAP4 permissions

You can configure the following for POP3 and IMAP4.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissions required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IMAP4 settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>POP3 settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Test IMAP4 settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Test POP3 settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p></td>
</tr>
</tbody>
</table>


## Windows PowerShell virtual directory permissions

You can configure the following for Windows PowerShell.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissions required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Test Windows PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Windows PowerShell settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
</tbody>
</table>


## Text Messaging permissions

You can configure the following for text messaging.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissions required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Text messaging notification settings</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Text messaging settings</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Text messaging user settings</p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">MyTextMessaging role</a></p>
<p>Users can configure text messaging settings on their own mailbox. Administrators can't configure the text messaging settings on another user's mailbox.</p></td>
</tr>
</tbody>
</table>

