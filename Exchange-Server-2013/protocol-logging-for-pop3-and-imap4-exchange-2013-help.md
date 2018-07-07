---
title: 'Protocol logging for POP3 and IMAP4: Exchange 2013 Help'
TOCTitle: Protocol logging for POP3 and IMAP4
ms:assetid: 212ed3d5-0c98-4346-a860-1cfcac5d73c4
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd335141(v=EXCHG.150)
ms:contentKeyID: 50395394
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Protocol logging for POP3 and IMAP4

 

_**Applies to:** Exchange Server 2013_


You can use protocol logging to review the POP3 and IMAP4 connections in your Exchange environment. This can be useful if you're troubleshooting issues related to POP3 or IMAP4 performance.

## Enabling POP3 and IMAP4 protocol logging

You can enable, disable, or change protocol logging using the Exchange Management Shell. If you enable protocol logging using the Shell, the default protocol logging settings will be used. In most cases, the default settings will be sufficient.

Alternatively, you can enable, disable, and modify protocol logging options by editing the Microsoft.Exchange.Pop3.exe.config and Microsoft.Exchange.Imap4.exe.config configuration files located on your Microsoft Exchange Server 2013 Client Access server. For more information about how to manage POP3 and IMAP4 protocol settings, see [Configure protocol logging for POP3 and IMAP4](configure-protocol-logging-for-pop3-and-imap4-exchange-2013-help.md).

## Reviewing the protocol log

The protocol log files are text files that contain data in the comma-separated value (CSV) file format. The protocol log stores each protocol event on a single line. The information stored on each line is organized by fields. These fields are separated by commas. The following table describes the fields that are used to classify each protocol event.

### Fields used to classify each protocol event

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Field name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>date-time</p></td>
<td><p>The date and time of the protocol event. The value is formatted as <em>yyyy-mm-ddhh:mm:ss.fffZ</em>, where <em>yyyy</em> = year, <em>mm</em> = month, <em>dd</em> = day, <em>hh</em> = hour, <em>mm</em> = minute, <em>ss</em> = second, <em>fff</em> = fractions of a second, and <em>Z</em> signifies Zulu. Zulu is another way to indicate Coordinated Universal Time (UTC).</p></td>
</tr>
<tr class="even">
<td><p>connector-id</p></td>
<td><p>This field isn’t used for POP3 and IMAP4 protocol logging.</p></td>
</tr>
<tr class="odd">
<td><p>session-id</p></td>
<td><p>A GUID that uniquely identifies the SMTP session that is associated with a protocol event.</p></td>
</tr>
<tr class="even">
<td><p>sequence-number</p></td>
<td><p>A counter that starts at 0 and is incremented for each event in the same session.</p></td>
</tr>
<tr class="odd">
<td><p>local-endpoint</p></td>
<td><p>The local endpoint of a POP3 or IMAP4 session. This consists of an IP address and TCP port number, formatted as follows: <em>&lt;IP address&gt;</em>:<em>&lt;port&gt;</em>.</p></td>
</tr>
<tr class="even">
<td><p>remote-endpoint</p></td>
<td><p>The remote endpoint of a POP3 or IMAP4 session. This consists of an IP address and TCP port number, formatted as follows: <em>&lt;IP address&gt;</em>:<em>&lt;port&gt;</em>.</p></td>
</tr>
<tr class="odd">
<td><p>event</p></td>
<td><p>A single character that represents the protocol event. The possible values for the event are as follows:</p>
<ul>
<li><p>+   Connect</p></li>
<li><p>-   Disconnect</p></li>
<li><p>&gt;   Send</p></li>
<li><p>&lt;   Receive</p></li>
<li><p>*   Information</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>data</p></td>
<td><p>Text information that’s associated with the POP3 or IMAP4 event.</p></td>
</tr>
<tr class="odd">
<td><p>context</p></td>
<td><p>This field isn’t used for POP3 and IMAP4 protocol logging.</p></td>
</tr>
</tbody>
</table>

