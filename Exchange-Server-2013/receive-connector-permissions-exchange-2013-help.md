---
title: 'Receive connector permissions: Exchange 2013 Help'
TOCTitle: Receive connector permissions
ms:assetid: 31af7139-6823-411b-81b3-e42edd83ee6c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673053(v=EXCHG.150)
ms:contentKeyID: 49289221
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Receive connector permissions

 

_**Applies to:** Exchange Server 2013_


The following table lists permission types and a description for each.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Receive connector permission</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-SMTP-Submit</p></td>
<td><p>The session must be granted this permission or it will be unable to submit messages to this Receive connector. If a session doesn't have this permission, the MAIL FROM and AUTH commands will fail.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Any-Recipient</p></td>
<td><p>This permission allows the session to relay messages through this connector. If this permission isn't granted, only messages that are addressed to recipients in accepted domains are accepted by this connector.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Any-Sender</p></td>
<td><p>This permission allows the session to bypass the sender address spoofing check.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Authoritative-Domain-Sender</p></td>
<td><p>This permission allows senders that have e-mail addresses in authoritative domains to establish a session to this Receive connector.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Authentication-Flag</p></td>
<td><p>This permission allows Exchange 2003 servers to submit messages from internal senders. Exchange 2010 will recognize the messages as being internal. The sender can declare the message as trusted. Messages that enter your Exchange system through anonymous submissions will be relayed through your Exchange organization with this flag in an untrusted state.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Routing</p></td>
<td><p>This permission allows the session to submit a message that has all received headers intact. If this permission isn't granted, the server will strip all received headers.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Headers-Organization</p></td>
<td><p>This permission allows the session to submit a message that has all organization headers intact. Organization headers all start with <strong>X-MS-Exchange-Organization-</strong>. If this permission isn't granted, the receiving server will strip all organization headers.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Forest</p></td>
<td><p>This permission allows the session to submit a message that has all forest headers intact. Forest headers all start with <strong>X-MS-Exchange-Forest-</strong>. If this permission isn't granted, the receiving server will strip all forest headers.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Exch50</p></td>
<td><p>This permission allows the session to submit a message that contains the XEXCH50 command. This command is needed for interoperability with Exchange 2003. The XEXCH50 command provides data such as the spam confidence level (SCL) for the message.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Bypass-Message-Size-Limit</p></td>
<td><p>This permission allows the session to submit a message that exceeds the message size restriction configured for the connector.</p></td>
</tr>
<tr class="odd">
<td><p>Ms-Exch-Bypass-Anti-Spam</p></td>
<td><p>This permission allows the session to bypass anti-spam filtering.</p></td>
</tr>
</tbody>
</table>

