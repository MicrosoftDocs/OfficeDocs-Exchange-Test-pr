---
title: 'Messaging policy and compliance: Exchange 2013 Help'
TOCTitle: Messaging policy and compliance
ms:assetid: 65f20a20-27a4-4f6e-9b27-f8705d65b8d9
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998599(v=EXCHG.150)
ms:contentKeyID: 48385169
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Messaging policy and compliance

 

_**Applies to:** Exchange Server 2013_


Email has become a reliable and ubiquitous communication medium for information workers in organizations of all sizes. Messaging stores and mailboxes have become repositories of valuable data. It’s important for organizations to formulate messaging policies that dictate the fair use of their messaging systems, provide user guidelines for how to act on the policies, and where required, provide details about the types of communication that may not be allowed.

Organizations must also create policies to manage email lifecycle, retain messages for the length of time based on business, legal, and regulatory requirements, preserve email records for litigation and investigation purposes, and be prepared to search and provide the required email records to fulfill eDiscovery requests.

Leakage of sensitive information such as intellectual property, trade secrets, business plans, and personally identifiable information (PII) collected or handled by your organization must also be protected.

## Messaging policy and compliance in Exchange 2013

The following table provides an overview of the messaging policy and compliance features in Microsoft Exchange Server 2013 and includes links to topics that will help you learn about and manage these features.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Description</th>
<th>Resources</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Messaging records management (MRM)</p></td>
<td><p>To comply with applicable regulations or meet legal or business requirements, organizations include email lifecycle policies as part of their messaging policy. Common questions that should be addressed by these policies include:</p>
<ul>
<li><p>How long should messages be retained?</p></li>
<li><p>Where should the messages be retained?</p></li>
<li><p>Should all messages be retained for the same period?</p></li>
</ul>
<p>Exchange 2013 includes MRM features that allow you to implement your organization’s email lifecycle policies. You can use MRM to apply uniform retention settings to all messages, use custom retention policies to apply a baseline retention setting for the mailbox, and optionally allow users to classify messages so that they can be retained for a specified duration.</p></td>
<td><p><a href="messaging-records-management-exchange-2013-help.md">Messaging records management</a></p></td>
</tr>
<tr class="even">
<td><p>In-Place Archiving</p></td>
<td><p><em>In-Place Archiving</em> helps you regain control of your organization's messaging data by eliminating the need for personal store (.pst) files and allowing users to store messages in an <em>archive mailbox</em> accessible in Outlook 2010 and later and Outlook Web App.</p></td>
<td><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">In-Place Archiving in Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>In-Place Hold</p></td>
<td><p>When a reasonable expectation of litigation exists, organizations are required to preserve electronically stored information (ESI), including email that's relevant to the case. In-Place Hold allows you to search and preserve messages matching query parameters. Messages are protected from deletion, modification, and tampering and can be preserved indefinitely or for a specified period.</p></td>
<td><p><a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">In-Place Hold and Litigation Hold</a></p></td>
</tr>
<tr class="even">
<td><p>In-Place eDiscovery</p></td>
<td><p>In-Place eDiscovery allows you to search mailbox data across your Exchange organization, preview search results, and copy them to a Discovery mailbox.</p></td>
<td><p><a href="in-place-ediscovery-exchange-2013-help.md">In-Place eDiscovery</a></p></td>
</tr>
<tr class="odd">
<td><p>Journaling</p></td>
<td><p>Journaling can help your organization respond to legal, regulatory, and organizational compliance requirements by recording inbound and outbound email communications. When planning for messaging retention and compliance, it's important to understand journaling, how it fits in your organization's compliance policies, and how Exchange 2013 can help you secure journaled messages.</p></td>
<td><p><a href="journaling-exchange-2013-help.md">Journaling</a></p></td>
</tr>
<tr class="even">
<td><p>Transport Rules</p></td>
<td><p>Using Transport rules, you can look for specific conditions for messages that pass through your organization and then take action on them. Transport rules let you apply messaging policies to email messages, secure messages, protect messaging systems, and prevent information leakage.</p></td>
<td><p><a href="mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md">Mail flow or transport rules</a></p></td>
</tr>
<tr class="odd">
<td><p>Data Loss Prevention (DLP)</p></td>
<td><p>DLP capabilities help you protect your sensitive data and inform users of your policies and regulations. DLP can also help you prevent users from mistakenly sending sensitive information to unauthorized people. When you configure DLP polices, you can identify and protect sensitive data by analyzing the content of your messaging system, which includes numerous associated file types. The DLP policy templates supplied in Exchange 2013 are based on regulatory standards such as PII and payment card industry data security standards (PCI-DSS). DLP is extensible, which allows you to include other policies that important to your organization. Additionally, the new Policy Tips capability allows you to inform users about policy violations before sensitive data is sent.</p></td>
<td><p><a href="technical-overview-of-dlp-data-loss-prevention-in-exchange.md">Data loss prevention</a></p></td>
</tr>
<tr class="even">
<td><p>Information Rights Management (IRM)</p></td>
<td><p>Information Rights Management (IRM) provides persistent online and offline protection for email messages and attachments using Active Directory Rights Management Services (AD RMS).</p></td>
<td><p><a href="information-rights-management-exchange-2013-help.md">Information Rights Management</a></p></td>
</tr>
<tr class="odd">
<td><p>S/MIME</p></td>
<td><p>Secure/Multipurpose Internet Mail Extensions (S/MIME) allows people who have Office 365 mailboxes and Exchange 2013 and Exchange Online to help protect sensitive information by sending signed and encrypted email within their organization. Administrators can enable S/MIME for Office 365 mailboxes by synchronizing user certificates between Office 365 and their on-premises server and then configuring Outlook Online to support S/MIME.</p></td>
<td><p><a href="s-mime-for-message-signing-and-encryption-exchange-2013-help.md">S/MIME for message signing and encryption</a></p></td>
</tr>
<tr class="even">
<td><p>Mailbox audit logging</p></td>
<td><p>Because mailboxes can potentially contain sensitive, high business impact (HBI) information and PII, it's important that you track who logs on to the mailboxes in your organization and what actions are taken. It's especially important to track access to mailboxes by users other than the mailbox owner (known as delegate users). Using mailbox audit logging, you can log mailbox access by mailbox owners, delegates (including administrators with full mailbox access permissions), and administrators.</p></td>
<td><p><a href="mailbox-audit-logging-exchange-2013-help.md">Mailbox audit logging</a></p>
<p><a href="exchange-auditing-reports-exchange-2013-help.md">Exchange auditing reports</a></p></td>
</tr>
<tr class="odd">
<td><p>Administrator audit logging</p></td>
<td><p>Administrator audit logs enable you to keep a log of changes made by administrators to Exchange server and organization configuration and to Exchange recipients. You might use administrator audit logging as part of your change control process or to track changes and access to configuration and recipients for compliance purposes.</p></td>
<td><p><a href="administrator-audit-logging-exchange-2013-help.md">Administrator audit logging</a></p></td>
</tr>
</tbody>
</table>

