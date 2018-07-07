---
title: 'Collaboration: Exchange 2013 Help'
TOCTitle: Collaboration
ms:assetid: f45c1be1-2a66-4610-a28d-4adc6d212769
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ218725(v=EXCHG.150)
ms:contentKeyID: 48385713
ms.date: 06/04/2016
mtps_version: v=EXCHG.150
---

# Collaboration

 

_**Applies to:** Exchange Server 2013_


Exchange 2013 provides the following rich features that can help your end users easily collaborate in email:

  - Site mailboxes

  - Public folders

  - Shared mailboxes

  - Distribution groups

Each of these features has a different user experience and feature set and should be used based on what the user needs to accomplish and what your organization can provide. For example, site mailboxes provide great documentation collaboration features. However site mailboxes rely on SharePoint Server 2013, so if you aren’t planning on deploying SharePoint, you should use public folders to share documents.

This topic compares these collaboration features to help you decide which features to offer your users.

## Site mailboxes

A site mailboxe is functionally comprised of a SharePoint 2013 site membership (owners and members), shared storage through an Exchange 2013 mailbox for email messages, and a SharePoint 2013 site to store and share. Essentially, site mailboxes bring Exchange email and SharePoint documents together. For users, a site mailbox serves as a central filing cabinet for the project, providing a place to file project email and documents that can be accessed and edited only by site members. In addition, site mailboxes have a specified lifecycle and are optimized to be used for projects that have set start and end dates. To fully implement site mailboxes, end users must use Outlook 2013.

To learn more, see [Site mailboxes](site-mailboxes-exchange-2013-help.md).

## Public folders

Public folders are designed for shared access and provide an easy and effective way to collect, organize, and share information with other people in your workgroup or organization.

Public folders organize content in a deep hierarchy that’s easy to browse. Users discover interesting and relevant content by browsing through branches of the hierarchy that are relevant to them. Users always see the full hierarchy in their Outlook folder view. Public folders are a great technology for distribution group archiving. A public folder can be mail-enabled and added as a member of the distribution group. Email sent to the distribution group is automatically added to the public folder for later reference. Public folders also provide simple document sharing and don’t require SharePoint Server 2013 to be installed in your organization. Finally, end users can use public folders with the following supported Outlook clients: Outlook 2007, Outlook 2010, and Outlook 2013.

To learn more, see [Public folders](public-folders-exchange-2013-help.md).

## Shared mailboxes

A shared mailbox is a mailbox that multiple designated users can access to read and send email messages and to share a common calendar. Shared mailboxes can provide a generic email address (such as info@contoso.com or sales@contoso.com) that customers can use to inquire about your company. If the shared mailbox has the Send As permission assigned when a delegated user responds to the email message, it can appear as though the mailbox (for example, sales@contoso.com) is responding, not the actual user.

To learn more, see [Shared mailboxes](shared-mailboxes-exchange-2013-help.md).

## Groups

Groups (also called distribution groups) are a collection of two or more recipients that appears in the shared address book. When an email message is sent to a group, it’s received by all members of the group. Distribution groups can be organized by a particular discussion subject (such as “Dog Lovers”) or by users who share a common work structure that requires them to communicate frequently.

To learn more, see [Recipients](recipients-exchange-2013-help.md).

## Which one to use?

The following table gives you a quick glance at each of the collaboration features to help you decide which one to use.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Site mailboxes</th>
<th>Public folders</th>
<th>Shared mailboxes</th>
<th>Groups</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Type of group</strong></p></td>
<td><p>Users who work together as a team on a specific project with definitive start and end dates.</p></td>
<td><p>With the proper permissions, everyone in your organization can access and search public folders. Public folders are ideal for maintaining history or distribution group conversations.</p></td>
<td><p>Delegates working on behalf of a virtual identity, and they can respond to email as that shared mailbox identity. Example: support@tailspintoys.com</p></td>
<td><p>Users who need to send email to a group of recipients with a common interest or characteristic.</p></td>
</tr>
<tr class="even">
<td><p><strong>Ideal group size</strong></p></td>
<td><p>Small</p></td>
<td><p>Large</p></td>
<td><p>Small</p></td>
<td><p>Large</p></td>
</tr>
<tr class="odd">
<td><p><strong>Access</strong></p></td>
<td><p>Site mailbox owners and members.</p></td>
<td><p>Accessible by anyone in your organization.</p></td>
<td><p>Users can be granted Full Access and/or Send As permissions. If granted Full Access permissions, users must also add the shared mailbox to their Outlook profile to access the shared mailbox.</p></td>
<td><p>For distribution groups, members, must be manually added. For dynamic distribution groups, members are added based on filtering criteria.</p></td>
</tr>
<tr class="even">
<td><p><strong>Shared calendar?</strong></p></td>
<td><p>No</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><strong>Email arrives in user’s personal Inbox?</strong></p></td>
<td><p>No. Email arrives in the site mailbox.</p></td>
<td><p>No. Email arrives in the public folder.</p></td>
<td><p>No. Email arrives in the Inbox of the shared mailbox.</p></td>
<td><p>Yes. Email arrives in the Inbox of a distribution group member.</p></td>
</tr>
<tr class="even">
<td><p><strong>Supported clients</strong></p></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>SharePoint 2013</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
</tr>
</tbody>
</table>

