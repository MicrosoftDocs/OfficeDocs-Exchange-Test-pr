---
title: 'Unsupported characters for Exchange 2013 object names: Exchange 2013 Help'
TOCTitle: Unsupported characters for Exchange 2013 object names
ms:assetid: 76fa4e23-f0f6-473b-9227-70ded907578f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn169553(v=EXCHG.150)
ms:contentKeyID: 53875525
ms.date: 06/04/2016
mtps_version: v=EXCHG.150
---

# Unsupported characters for Exchange 2013 object names

 

_**Applies to:** Exchange Server 2013_


This article describes characters that you can’t use in object or component names in Exchange 2013. When you create names for objects or components in Exchange 2013, the names can’t contain unsupported characters, even though you may be able to create an object using an unsupported character. Also, if you try to import or connect to objects whose names contain unsupported characters, you may receive an error message or experience unexpected behavior.

## Unsupported characters

The following table lists characters that aren’t supported for use in the names of Exchange-related objects or components. The table also lists the scenario in which problems may occur if unsupported characters are used. Note that there is a maximum length of 64 characters for each object listed in the table.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange object or component</th>
<th>Exchange scenario</th>
<th>Unsupported characters</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Email domain name</p></td>
<td><p>Simple Mail Transfer Protocol (SMTP) connector</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>Host name of connector address space</p></td>
<td><p>Mail flow</p></td>
<td><p><code>..</code> (two periods)</p></td>
</tr>
<tr class="odd">
<td><p>Host name for Exchange servers</p></td>
<td><p>SMTP</p></td>
<td><p><code>_</code> (underscore)</p></td>
</tr>
<tr class="even">
<td><p>Organization or site name</p></td>
<td><p>Running the Setup program or moving mailboxes</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization internal directory name</p></td>
<td><p>Directory</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>Public folder tree name</p></td>
<td><p>Viewing and creating the public folder</p></td>
<td><p><code>: ;</code></p></td>
</tr>
<tr class="odd">
<td><p>Recipient name</p></td>
<td><p>SMTP</p></td>
<td><p><code>' &quot;</code></p></td>
</tr>
<tr class="even">
<td><p>Recipient policy SMTP address</p></td>
<td><p>Viewing the public folder hierarchy</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>Recipient policy SMTP address host name</p></td>
<td><p>Mail flow</p></td>
<td><p><code>..</code> (two periods)</p></td>
</tr>
<tr class="even">
<td><p>Site internal directory name</p></td>
<td><p>Viewing the public folder hierarchy</p></td>
<td><p><code>? ( ) *</code></p></td>
</tr>
<tr class="odd">
<td><p>Smart host name</p></td>
<td><p>SMTP</p></td>
<td><p>Leading or trailing spaces</p></td>
</tr>
</tbody>
</table>

