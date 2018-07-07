---
title: 'Email addresses and address books: Exchange 2013 Help'
TOCTitle: Email addresses and address books
ms:assetid: b97d0f68-691a-42af-9a6c-4dcc37b28a42
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ657488(v=EXCHG.150)
ms:contentKeyID: 49289386
ms.date: 06/04/2016
mtps_version: v=EXCHG.150
---

# Email addresses and address books

 

_**Applies to:** Exchange Server 2013_


Recipients (which include users, resources, contacts, and groups) are any mail-enabled object in Active Directory to which Microsoft Exchange can deliver or route messages. For a recipient to send or receive email messages, the recipient must have an email address. Address books are the method by which users find each other in order to send email. There are many different methods for organizing address books. See Key terminology for detailed descriptions of address book features in Exchange Server 2013.

## Key terminology

The following terms define the core components associated with email addresses and address books in Exchange 2013.

  - **address book policies**  
    Address book policies (ABPs) allow you to segment users into specific groups to provide customized views of your organization’s global address list (GAL). When creating an ABP, you assign a GAL, an offline address book (OAB), a room list, and one or more address lists to the policy. You can then assign the ABP to mailbox users, providing them with access to a customized GAL in Outlook and Outlook Web App. The goal is to provide a simpler mechanism to accomplish GAL segmentation for on-premises organizations that require multiple GALs.

<!-- end list -->

  - **address lists**  
    An address list is a subset of a GAL. Each address list is a collection of one or more types of mail-enabled recipients (for example, users, contacts, groups, public folders, conferencing, and other resources). You can use address lists to organize recipients and resources, making it easier for users to find the recipients and resources they need. Address lists are updated dynamically. Therefore, when new recipients are added to your organization, they're automatically added to the appropriate address lists.

<!-- end list -->

  - **email address policies**  
    Email address policies generate the primary and secondary email addresses for your recipients so they can receive and send email. By default, Exchange contains an email address policy for every mail-enabled user.

<!-- end list -->

  - **hierarchical address books**  
    The hierarchical address book (HAB) enables end users to look for recipients in their address book using an organizational hierarchy, such as seniority or management structure. Normally, users are limited to the default GAL and its associated recipient properties and the structure of the GAL often doesn't accurately reflect the management or seniority relationships for recipients in your organization. Being able to customize an HAB that maps to your organization's unique business structure provides your users with an efficient method for locating internal recipients.

<!-- end list -->

  - **offline address books**  
    An offline address book (OAB) is a copy of a collection of address lists that has been downloaded so that a Microsoft Outlook user can access the information it contains while disconnected from the server.

## Email address and address book documentation

The following table contains links to topics that will help you learn about and manage email addresses and address books in Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Topic</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="address-lists-exchange-2013-help.md">Address lists</a></p></td>
<td><p>Learn more about address lists and GALs as methods for organizing your recipients for easy end user access.</p></td>
</tr>
<tr class="even">
<td><p><a href="address-book-policies-exchange-2013-help.md">Address book policies</a></p></td>
<td><p>Learn more about how to separate your address lists and GALs into separate virtual organizations.</p></td>
</tr>
<tr class="odd">
<td><p><a href="details-templates-exchange-2013-help.md">Details templates</a></p></td>
<td><p>Learn more about customizing the address cards in Outlook.</p></td>
</tr>
<tr class="even">
<td><p><a href="email-address-policies-exchange-2013-help.md">Email address policies</a></p></td>
<td><p>Learn more about proxy email addresses to make recipients more discoverable.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hierarchical-address-books-exchange-2013-help.md">Hierarchical address books</a></p></td>
<td><p>Learn more about how to customize the GAL and address lists to meet your organization’s unique business structure.</p></td>
</tr>
<tr class="even">
<td><p><a href="offline-address-books-exchange-2013-help.md">Offline address books</a></p></td>
<td><p>Learn more about providing users with offline access to your organization’s address lists.</p></td>
</tr>
</tbody>
</table>

