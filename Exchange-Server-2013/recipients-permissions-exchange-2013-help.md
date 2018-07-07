---
title: 'Recipients Permissions: Exchange 2013 Help'
TOCTitle: Recipients Permissions
ms:assetid: 5b690bcb-c6df-4511-90e1-08ca91f43b37
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd638132(v=EXCHG.150)
ms:contentKeyID: 48385139
ms.date: 07/14/2016
mtps_version: v=EXCHG.150
---

# Recipients Permissions

 

_**Applies to:** Exchange Server 2013_


The permissions required to perform tasks to manage recipients vary depending on the procedure being performed or the cmdlet you want to run.

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1.  In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2.  Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3.  Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.
    

    > [!NOTE]
    > You must be assigned the Role Management management role to run the <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet. If you don't have permissions to run the <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.



If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).

## Mailbox server permissions

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
<td><p>Calendar repair, server configuration</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Delegating Mailbox servers</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Email address policies</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange Search</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Search – diagnostics</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p>
<p>Support Diagnostics role</p>

> [!NOTE]
> The Support Diagnostics role isn't assigned to a role group. For more information, see <A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">Add a role to a user or USG</A>.


</td>
</tr>
<tr class="even">
<td><p>Group metrics</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Import Export</p></td>
<td><p>Mailbox Import Export role</p>

> [!NOTE]
> The Mailbox Import Export role isn't assigned to a role group. For more information, see <A href="mailbox-import-export-role-exchange-2013-help.md">Mailbox Import Export role</A>.


</td>
</tr>
<tr class="even">
<td><p>Mailbox Assistants</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Mailbox moves</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Mailbox recovery</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Mailbox repair request</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Mailbox restore request</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Mailbox server configuration</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Manage Exchange Search Indexer service on a Mailbox server</p></td>
<td><p>Local Administrator on the Mailbox server</p></td>
</tr>
<tr class="odd">
<td><p>MAPI connectivity</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>OAB virtual directories</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Remove store mailbox</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
</tbody>
</table>


## Calendar and sharing permissions

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
<td><p>Calendar configuration</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
</tr>
<tr class="even">
<td><p>Calendar diagnostics</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p>
<p><a href="compliance-management-exchange-2013-help.md">Compliance Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
</tr>
<tr class="odd">
<td><p>Calendar processing</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
</tr>
<tr class="even">
<td><p>Notifications</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Organization relationships</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Sharing policies</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
</tbody>
</table>


## Resource mailbox configuration permissions

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
<td><p>Booking policies</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
</tr>
<tr class="even">
<td><p>Delegation</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Resource mailbox schema configuration</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
</tbody>
</table>


## Mailbox database permissions

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
<td><p>Mailbox databases</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
</tbody>
</table>


## Recipient provisioning permissions

This table contains the various permissions that are required to manage recipients.

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
<td><p>Address list, GAL</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Anti-spam</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Apps for Outlook</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
</tr>
<tr class="even">
<td><p>Applying sharing policies</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Arbitration</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Archive connectivity</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Assigning offline address books</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Automatic replies</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
</tr>
<tr class="odd">
<td><p>Calendar configuration</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Calendar repair</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Contact aggregation settings</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">View-only Organization Management</a></p></td>
</tr>
<tr class="even">
<td><p>Disconnected mailboxes</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
</tr>
<tr class="odd">
<td><p>Distribution groups</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Dynamic distribution groups</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Email addresses</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="even">
<td><p>Inbox rules</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
</tr>
<tr class="odd">
<td><p>Mail contacts</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Mail tips</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Mail user</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Mailbox folder permissions</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
</tr>
<tr class="odd">
<td><p>Mailbox folders</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>MAPI connectivity</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Message configuration</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
</tr>
<tr class="even">
<td><p>Message quotas</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Moderation</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Permissions and delegation</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Archive mailboxes</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Recipient data properties</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Remote mailboxes</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Retention and legal holds</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Send As</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Spelling configuration</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
</tr>
<tr class="odd">
<td><p>Unified Messaging</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="even">
<td><p>User mailboxes</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>User photos</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk</a></p></td>
</tr>
</tbody>
</table>


## Mailbox move and migration permissions

The table contains the permissions that are required to move on-premises mailboxes to different domains or forests and to migrate on-premises mailboxes to and from your cloud-based organization.


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
<td><p>Mailbox moves (local or cross-forest)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Mailbox moves (hybrid deployment)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Migration (on-boarding and off-boarding from the cloud)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Organization Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
</tbody>
</table>

