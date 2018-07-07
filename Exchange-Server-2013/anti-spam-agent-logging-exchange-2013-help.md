---
title: 'Anti-spam agent logging: Exchange 2013 Help'
TOCTitle: Anti-spam agent logging
ms:assetid: dbd478d2-7993-4931-80db-5b2f7d4269bd
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124795(v=EXCHG.150)
ms:contentKeyID: 49287005
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Anti-spam agent logging

 

_**Applies to:** Exchange Server 2013_


Agent logs record the actions performed on a message by specific anti-spam agents in Microsoft Exchange Server 2013. Only the following agents can write information to the agent log:

  - Connection Filtering agent

  - Content Filter agent

  - Edge Rules agent

  - Recipient Filter agent

  - Sender Filter agent

  - Sender ID agent


> [!NOTE]
> The Connection Filtering agent and the Edge Rules agent aren't available on Mailbox servers.



The information written to the agent log depends on the agent, the SMTP event, and the action performed on the message.

You use the **Set-TransportService** cmdlet in the Exchange Management Shell to perform all agent log configuration tasks. The following options are available for the agent logs:

  - Enable or disable agent logging. The default is enabled.

  - Specify the location of the agent log files. The default value is %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog.

  - Specify a maximum size for the individual agent log files. The default size is 10 megabytes (MB).

  - Specify a maximum size for the directory that contains agent log files. The default size is 250 MB.

  - Specify a maximum age for the agent log files. The default age is 7 days.

Exchange uses circular logging to limit the agent logs based on file size and file age to help control the hard disk space used by the log files.

**Contents**

Overview of transport agents

Structure of the agent log files

Information written to the agent log

Search the agent logs

## Overview of transport agents

Agents can only act upon messages at specific points in the SMTP command sequence used to transport the messages through the Transport service on a Mailbox server or an Edge Transport server. These access points in the SMTP command sequence are called *SMTP events*. Each agent has a priority value that can be assigned. However, the SMTP events must always occur in a specific order. Therefore, the agent priority depends on the SMTP event. If two agents can act on a message during the same SMTP event, the agent that has the highest priority will act on the message first.

The following table lists the SMTP events in order of occurrence and the agents that write information to the agent log in order of priority from highest to lowest for each SMTP event.

### SMTP events in order of occurrence and the agents that write information to the agent log in order of priority for each SMTP event

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>SMTP event</th>
<th>Agent</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>OnConnect</strong></p></td>
<td><p>Connection Filtering agent</p></td>
</tr>
<tr class="even">
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>Connection Filtering agent</p>
<p>Sender Filter agent</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnRcptCommand</strong></p></td>
<td><p>Connection Filtering agent</p>
<p>Recipient Filter agent</p></td>
</tr>
<tr class="even">
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>Connection Filtering agent</p>
<p>Sender ID agent</p>
<p>Sender Filter agent</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>Edge Rules agent</p>
<p>Content Filtering agent</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> The Connection Filtering agent and the Edge Rules agent aren't available on Mailbox servers.



For more information about agents, SMTP events, and agent priority, see [Transport agents](transport-agents-exchange-2013-help.md).

Return to top

## Structure of the agent log files

The agent logs exist in %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog.

The naming convention for the agent log files is AGENTLOG*yyyymmdd-nnnn*.log. The placeholders represent the following information:

  - The placeholder *yyyymmdd* is the Coordinated Universal Time (UTC) date that the log file was created. The placeholder *yyyy* = year, *mm* = month, and *dd* = day.

  - The placeholder *nnnn* is an instance number that starts at the value of 1 for each day.

Information is written to the log file until the file size reaches its maximum specified value, and a new log file that has an incremented instance number is opened. This process is repeated throughout the day. Circular logging deletes the oldest log files when the agent log directory reaches its maximum specified size, or when a log file reaches its maximum specified age.

The agent log files are text files that contain data in the comma-separated value file (CSV) format. Each agent log file has a header that contains the following information:

  - **\#Software**   Name of the software that created the agent log file. Typically, the value is Microsoft Exchange Server.

  - **\#Version**   Version number of the software that created the agent log file. Currently, the value is 15.0.0.0.

  - **\#Log-Type**   Log type value, which is Agent Log.

  - **\#Date**   UTC date-time when the log file was created. The UTC date-time is represented in the ISO 8601 date-time format: *yyyy-mm-dd*T*hh:mm:ss.fff*Z, where *yyyy* = year, *mm* = month, *dd* = day, T indicates the beginning of the time component, *hh* = hour, *mm* = minute, *ss* = second, *fff* = fractions of a second, and Z signifies Zulu, which is another way to denote UTC.

  - **\#Fields**   Comma delimited field names used in the agent log files.

Return to top

## Information written to the agent log

The agent log stores each agent transaction on a single line in the log. The information stored on each line is organized by fields. These fields are separated by commas. The field name is generally descriptive enough to determine the type of information it contains. However, some of the fields may be blank. Or the type of information stored in the field may change based on the agent or the action performed on the message by the agent. The following table describes the fields used to classify each agent transaction.

### Fields used to classify each agent transaction

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
<td><p><strong>Timestamp</strong></p></td>
<td><p>UTC date-time of the agent event. The UTC date-time is represented in the ISO 8601 date-time format: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, where <em>yyyy</em> = year, <em>mm</em> = month, <em>dd</em> = day, T indicates the beginning of the time component, <em>hh</em> = hour, <em>mm</em> = minute, <em>ss</em> = second, <em>fff</em> = fractions of a second, and Z signifies Zulu, which is another way to denote UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionId</strong></p></td>
<td><p>Unique SMTP session identifier. This identifier is represented as a 16-digit hexadecimal number.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalEndpoint</strong></p></td>
<td><p>Local IP address and port number that accepted the message. SMTP sessions typically use port 25.</p></td>
</tr>
<tr class="even">
<td><p><strong>RemoteEndpoint</strong></p></td>
<td><p>IP address and port number of the previous SMTP server that connected to this server to deliver the message. When Internet mail flows through an Edge Transport server in the perimeter network, the value of <strong>RemoteEndpoint</strong> in the agent log on the Mailbox server will be the IP address of the Edge Transport server. Even though the message is transmitted by SMTP, the port number used by the sending server will be a random number larger than 1,024.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnteredOrgFromIP</strong></p></td>
<td><p>IP address of the remote SMTP server that first connected to the Exchange organization to deliver the message. On an Edge Transport server, the value of <strong>RemoteEndpoint</strong> and <strong>EnteredOrgFromIP</strong> are the same. Anti-spam agents use the IP address in <strong>EnteredOrgFromIP</strong> to examine a message.</p></td>
</tr>
<tr class="even">
<td><p><strong>MessageId</strong></p></td>
<td><p>Value of the <code>MessageID</code> header field. If this value is blank, the Exchange transport server assigns an arbitrary value, but only if the message is accepted. After a value is assigned, the value of <code>MessageID</code> is constant for the lifetime of the message.</p></td>
</tr>
<tr class="odd">
<td><p><strong>P1FromAddress</strong></p></td>
<td><p>Sender email address specified in <code>MAIL FROM</code> in the message envelope. This value is used to transport the message between SMTP messaging servers. This value serves as a comparison to the value of <strong>P2FromAddresses</strong> to determine whether the sender address in the message header is forged.</p></td>
</tr>
<tr class="even">
<td><p><strong>P2FromAddresses</strong></p></td>
<td><p>Sender email address specified in the <code>From</code> header field or in the <code>Sender</code> header field in the message header.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Recipient</strong></p></td>
<td><p>Email address of the recipients. Although the original message may contain multiple recipients, only one recipient is displayed per line in the agent log.</p></td>
</tr>
<tr class="even">
<td><p><strong>NumRecipients</strong></p></td>
<td><p>Total number of recipients in the original message.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agent</strong></p></td>
<td><p>Name of the agent that took the action. The possible values are as follows:</p>
<ul>
<li><p>Content Filter agent</p></li>
<li><p>Recipient Filter agent</p></li>
<li><p>Sender Filter agent</p></li>
<li><p>Sender ID agent</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Event</strong></p></td>
<td><p>SMTP event where the action was taken by the agent. The value of <strong>Event</strong> depends on the agent. The SMTP events available to each agent are described in the first table earlier in this topic. The possible values for <strong>Event</strong> are as follows:</p>
<ul>
<li><p>OnConnect</p></li>
<li><p>OnEndOfHeaders</p></li>
<li><p>OnEndOfData</p></li>
<li><p>OnMailCommand</p></li>
<li><p>OnRcptCommand</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Action</strong></p></td>
<td><p>Action performed on the message by the agent. The possible values for <strong>Action</strong> are as follows:</p>
<ul>
<li><p>AcceptMessage</p></li>
<li><p>DeleteMessage</p></li>
<li><p>DeleteRecipients</p></li>
<li><p>Disconnect</p></li>
<li><p>QuarantineMessage</p></li>
<li><p>QuarantineRecipients</p></li>
<li><p>RejectAuthentication</p></li>
<li><p>RejectCommand</p></li>
<li><p>RejectConnection</p></li>
<li><p>RejectMessage</p></li>
<li><p>RejectRecipients</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>SmtpResponse</strong></p></td>
<td><p>Enhanced SMTP response as defined in RFC 2034.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reason</strong></p></td>
<td><p>Reason for the action supplied by the agent.</p></td>
</tr>
<tr class="even">
<td><p><strong>ReasonData</strong></p></td>
<td><p>Descriptive details for the action supplied by the agent.</p></td>
</tr>
</tbody>
</table>


Return to top

## Search the agent logs

You can use the **Get-AgentLog** cmdlet and the **Get-AntiSpamFilteringReport.ps1** script to search the agent logs.

The **Get-AntiSpamFilteringReport.ps1** script is located in `%ExchangeInstallPath%Scripts`. You need to run the script in the Shell from the Scripts folder. To change your location in the Shell to the Scripts folder, run the following command:

    Cd $env:ExchangeInstallPath\Scripts

To run the script in the Scripts folder, use the following syntax:

    .\Get-AntiSpamFilteringReport.ps1 -report <ReportValue> [<OptionalParameters>]

For details about using the script, run the following command:

    Get-Help -Detailed .\Get-AntiSpamFilteringReport.ps1

Return to top

