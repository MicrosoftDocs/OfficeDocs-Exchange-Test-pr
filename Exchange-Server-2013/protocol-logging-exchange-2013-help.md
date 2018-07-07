---
title: 'Protocol logging: Exchange 2013 Help'
TOCTitle: Protocol logging
ms:assetid: 40da446b-bcc3-4a97-ace7-a54f6ddebd79
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997624(v=EXCHG.150)
ms:contentKeyID: 49287003
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Protocol logging

 

_**Applies to:** Exchange Server 2013_


Protocol logging records the SMTP conversations that occur between messaging servers as part of message delivery. These SMTP conversations occur on Send connectors and Receive connectors that exist in the Front End Transport service on Client Access servers, the Transport service on Mailbox servers, and the Mailbox Transport service on Mailbox servers. You can use protocol logging to diagnose mail flow problems.

By default, protocol logging is disabled on all Send connectors and Receive connectors. Protocol logging is enabled or disabled on each individual connector. Other protocol logging options are set for all the Receive connectors or all the Send connectors that exist in each individual transport service on the server. All the Receive connectors in a transport service share the same protocol log files and protocol log options. These protocol log files and protocol log options are separate from the Send connector protocol log files and protocol log options in the transport service on the same server.

The following options are available for the protocol logs of all Send connectors or all Receive connectors in each transport service on the Exchange server:

  - Specify the location of the Send connector or the Receive connector protocol log files.

  - Specify a maximum size for the Send connector or the Receive connector protocol log files. The default size is 10 megabytes (MB).

  - Specify a maximum size for the directory that contains the Send connector or Receive connector protocol log files. The default size is 250 MB.

  - Specify a maximum age for the Send connector or Receive connector protocol log files. The default age is 30 days.

By default, Exchange uses circular logging to limit the protocol logs based on file size and file age to help control the hard disk space used by the log files.

A special Send connector named the intra-organization Send connector exists in the Transport service on every Mailbox server, and in the Front End Transport service on every Client Access server. This connector is implicitly created, invisible, and requires no management. The intra-organization Send connector is used by the following transport services:

  - **Transport service on Mailbox servers**
    
      - Relays messages to the Transport service and the Mailbox Transport service on other Exchange 2013 Mailbox servers in the organization.
    
      - Relays messages to other Exchange 2007 or Exchange 2010 Hub Transport servers in the organization.
    
      - Relays messages to Edge Transport servers in the perimeter network.

  - **Front End Transport service on Client Access servers**   Relays messages to the Transport service on Exchange 2013 Mailbox servers in the organization.

An equivalent Send connector named the mailbox delivery Send connector exists in the Mailbox Transport service on every Mailbox server. This connector is also implicitly created, invisible, and requires no management. The mailbox delivery Send connector is used to relay messages to the Transport service and the Mailbox Transport service on other Mailbox servers in the organization.

By default, protocol logging for the mailbox delivery Send connector is also disabled. You can enable or disable protocol logging for the mailbox delivery Send connector by using the *MailboxDeliveryConnectorProtocolLoggingLevel* parameter on the **Set-MailboxTransportService** cmdlet. If you enable protocol logging for the mailbox delivery Send connector, logging occurs in the Send connector protocol logs for the Mailbox Transport service on the Mailbox server.

**Contents**

Structure of the protocol log files

Information written to the protocol log

## Structure of the protocol log files

By default, the protocol log files exist in the following locations:

  - **Receive connector protocol log files for the Transport service on Mailbox servers**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpReceive

  - **Receive connector protocol log files for the Mailbox Transport service on Mailbox servers**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpReceive

  - **Receive connector protocol log files for the Front End Transport service on Client Access servers**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpReceive

  - **Send connector protocol log files for the Transport service on Mailbox servers**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpSend

  - **Send connector protocol log files for the Mailbox Transport service on Mailbox servers**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpSend

  - **Send connector protocol log files for the Front End Transport service on Client Access servers**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpSend

The naming convention for log files in each protocol log directory is *prefixyyyymmdd-nnnn*.log. The placeholders represent the following information:

  - The placeholder *prefix* is SEND for Send connectors or RECV for Receive connectors.

  - The placeholder *yyyymmdd* is the Coordinated Universal Time (UTC) date on which the log file was created. The placeholder *yyyy* = year, *mm* = month, and *dd* = day.

  - The placeholder *nnnn* is an instance number that starts at the value of 1 for each day.

Information is written to the log file until the file size reaches its maximum specified value, and a new log file that has an incremented instance number is opened. This process is repeated throughout the day. Circular logging deletes the oldest log files when the protocol log directory reaches its maximum specified size, or when a log file reaches its maximum specified age.

The protocol log files are text files that contain data in the comma-separated value file (CSV) format. Each protocol log file has a header that contains the following information:

  - **\#Software**   Name of the software that created the protocol log file. Typically, the value is Microsoft Exchange Server.

  - **\#Version**   Version number of the software that created the protocol log file. Currently, the value is 15.0.0.0.

  - **\#Log-Type**   Log type value of this field, which is either SMTP Receive Protocol Log or SMTP Send Protocol Log.

  - **\#Date**   UTC date-time when the log file was created. The UTC date-time is represented in the ISO 8601 date-time format: *yyyy-mm-dd*T*hh:mm:ss.fff*Z, where *yyyy* = year, *mm* = month, *dd* = day, T indicates the beginning of the time component, *hh* = hour, *mm* = minute, *ss* = second, *fff* = fractions of a second, and Z signifies Zulu, which is another way to denote UTC.

  - **\#Fields**   Comma-delimited field names used in the protocol log files.

Return to top

## Information written to the protocol log

The protocol log stores each SMTP protocol event on a single line in the protocol log. The information stored on each line is organized by fields. These fields are separated by commas. The following table describes the fields used to classify each protocol.

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
<td><p><strong>date-time</strong></p></td>
<td><p>UTC date-time of the protocol event. The UTC date-time is represented in the ISO 8601 date-time format: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, where <em>yyyy</em> = year, <em>mm</em> = month, <em>dd</em> = day, T indicates the beginning of the time component, <em>hh</em> = hour, <em>mm</em> = minute, <em>ss</em> = second, <em>fff</em> = fractions of a second, and Z signifies Zulu, which is another way to denote UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>connector-id</strong></p></td>
<td><p>Distinguished name (DN) of the connector associated with the SMTP event.</p></td>
</tr>
<tr class="odd">
<td><p><strong>session-id</strong></p></td>
<td><p>GUID that's unique for each SMTP session but is the same for each event associated with that SMTP session.</p></td>
</tr>
<tr class="even">
<td><p><strong>sequence-number</strong></p></td>
<td><p>Counter that starts at 0 and is incremented for each event in the same SMTP session.</p></td>
</tr>
<tr class="odd">
<td><p><strong>local-endpoint</strong></p></td>
<td><p>Local endpoint of an SMTP session. This consists of an IP address and TCP port number formatted as <em>&lt;IP address&gt;</em>:<em>&lt;port&gt;</em>.</p></td>
</tr>
<tr class="even">
<td><p><strong>remote-endpoint</strong></p></td>
<td><p>Remote endpoint of an SMTP session. This consists of an IP address and TCP port number formatted as <em>&lt;IP address&gt;</em>:<em>&lt;port&gt;</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>event</strong></p></td>
<td><p>Single character that represents the protocol event. The possible values for the event are as follows:</p>
<ul>
<li><p><strong>+</strong>   Connect</p></li>
<li><p><strong>-</strong>   Disconnect</p></li>
<li><p><strong>&gt;</strong>   Send</p></li>
<li><p><strong>&lt;</strong>   Receive</p></li>
<li><p><strong>*</strong>   Information</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>data</strong></p></td>
<td><p>Text information associated with the SMTP event.</p></td>
</tr>
<tr class="odd">
<td><p><strong>context</strong></p></td>
<td><p>Additional contextual information that may be associated with the SMTP event.</p></td>
</tr>
</tbody>
</table>


A single SMTP conversation that represents the sending or receiving of a single email message generates multiple SMTP events. These SMTP events cause multiple lines to be written to the protocol log. Multiple SMTP conversations that represent the sending or receiving of multiple email messages can occur at the same time. This creates protocol log entries from different SMTP conversations that are interspersed. You can use the session-id and sequence-number fields to sort the protocol log entries by SMTP conversation.

Return to top

