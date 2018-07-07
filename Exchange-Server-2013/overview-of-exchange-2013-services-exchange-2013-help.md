---
title: 'Overview of Exchange 2013 services: Exchange 2013 Help'
TOCTitle: Overview of Exchange 2013 services
ms:assetid: 2ed45d18-2ff3-4099-b841-050eb16a416b
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee423542(v=EXCHG.150)
ms:contentKeyID: 74479247
ms.date: 10/20/2017
mtps_version: v=EXCHG.150
---

# Overview of Exchange 2013 services

 

_**Applies to:** Exchange Server 2013_


During the installation of Exchange Server 2013, Setup runs a set of tasks that install new services in Microsoft Windows. A service is a background process that can be launched during the startup of the server by the Windows Service Control Manager. Services are executable files designed to operate independently and without administrative intervention. A service can run using either a graphical user interface (GUI) mode or a console mode.

All previous versions of Exchange included components that are implemented as services. Each Exchange server role includes services that are part of (or may be needed by) the server role to perform its functions. Note that some services only become active when specific features are used.

The sections in this topic describe the various services that are installed by Exchange 2013 on Mailbox servers, Client Access servers, and Edge Transport servers. For services that are labeled as optional, you can disable the service if you determine your organization doesn't need the functionality that's provided by the service.

## Exchange services on Exchange 2013 Mailbox servers

The following table describes the Exchange services that are installed on Mailbox servers.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Service name</th>
<th>Service short name</th>
<th>Description and dependencies</th>
<th>Default startup type</th>
<th>Security context</th>
<th>Dependencies</th>
<th>Required or optional</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Provides Active Directory topology information to Exchange services. If this service is stopped, most Exchange services can't start.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Net.TCP Port Sharing Service</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Anti-spam Update</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Provides Exchange SmartScreen spam definition updates.</p>

> [!NOTE]
> On November 1, 2016, Microsoft stopped producing spam definition updates for the SmartScreen filters in Exchange and Outlook. The existing SmartScreen spam definitions will be left in place, but their effectiveness will likely degrade over time. For more information, see <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Deprecating support for SmartScreen in Outlook and Exchange</A>.


</td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Optional</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange DAG Management</p></td>
<td><p>MSExchangeDagMgmt</p></td>
<td><p>Provides storage and database layout management for Mailbox servers in database availability groups (DAGs).</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p>
<p>Net.TCP Port Sharing Service</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Diagnostics</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Provides an agent that monitors Exchange server health.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>None</p></td>
<td><p>Required</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange EdgeSync</p></td>
<td><p>MSExchangeEdgeSync</p></td>
<td><p>Replicates configuration and recipient data between the Mailbox server and UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) on subscribed Edge Transport servers over a secure LDAP channel.</p>
<p>If you don't have any subscribed Edge Transport servers, you can disable this service.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Optional</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Health Manager</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Part of managed availability that monitors the health of key components on the Exchange server.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Windows Event Log</p>
<p>Windows Management Instrumentation</p></td>
<td><p>Required</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange IMAP4 Backend</p></td>
<td><p>MSExchangeIMAP4BE</p></td>
<td><p>Receives proxied client connections from the from the IMAP4 service on Client Access servers. By default, this service isn't running, so IMAP4 clients can't connect to the Exchange server until this service is started.</p>
<p>If you don't have any IMAP4 clients, you can disable this service.</p></td>
<td><p>Manual</p></td>
<td><p>Network Service</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Optional</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Information Store</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>Manages the mailbox databases on the server. If this service is stopped, mailbox databases on the server are unavailable.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p>
<p>Remote Procedure Call (RPC)</p>
<p>Server</p>
<p>Windows Event Log</p>
<p>Workstation</p></td>
<td><p>Required</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Mailbox Assistants</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>Performs background processing of mailboxes in mailbox databases on the server.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Mailbox Replication</p></td>
<td><p>MSExchangeMailboxReplication</p></td>
<td><p>Processes mailbox moves and move requests.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p>
<p>Net.TCP Port Sharing Service</p></td>
<td><p>Required</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Mailbox Transport Delivery</p></td>
<td><p>MSExchangeDelivery</p></td>
<td><p>Receives SMTP messages from the Microsoft Exchange Transport service (on the local or remote Mailbox servers) and delivers them to a local mailbox database using RPC.</p></td>
<td><p>Automatic</p></td>
<td><p>Network Service</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Mailbox Transport Submission</p></td>
<td><p>MSExchangeSubmission</p></td>
<td><p>Receives RPC messages from a local mailbox database, and submits them over SMTP to the Microsoft Exchange Transport service (on the local or remote Mailbox servers).</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Required</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange POP3 Backend</p></td>
<td><p>MSExchangePOP3BE</p></td>
<td><p>Receives proxied client connections from the POP3 service on Client Access servers. By default, this service isn't running, so POP3 clients can't connect to the Exchange server until this service is started.</p></td>
<td><p>Manual</p></td>
<td><p>Network Service</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Optional</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Replication Service</p></td>
<td><p>MSExchangeRepl</p></td>
<td><p>Provides replication functionality for mailbox databases in a database availability groups (DAGs).</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Required</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange RPC Client Access</p></td>
<td><p>MSExchangeRPC</p></td>
<td><p>Manages client RPC connections for Exchange.</p></td>
<td><p>Automatic</p></td>
<td><p>Network Service</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Search</p></td>
<td><p>MSExchangeFastSearch</p></td>
<td><p>Provides indexing of mailbox content, which improves the performance of content search.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Required</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Search Host Controller</p></td>
<td><p>HostControllerService</p></td>
<td><p>Provides deployment and management services for applications on the local Exchange server.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>HTTP Service</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Server Extension for Windows Server Backup</p></td>
<td><p>WSBExchange</p></td>
<td><p>Enables Windows Server Backup to back and restore Exchange server data.</p></td>
<td><p>Manual</p></td>
<td><p>Local System</p></td>
<td><p>None</p></td>
<td><p>Optional</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Service Host</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Provides a service host for Exchange components that don't have their own services.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Throttling</p></td>
<td><p>MSExchangeThrottling</p></td>
<td><p>Provides user workload management that limits the rate of user operations (formerly known as user throttling).</p></td>
<td><p>Automatic</p></td>
<td><p>Network Service</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Required</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Transport</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>Provides SMTP server and transport stack.</p></td>
<td><p>Automatic</p></td>
<td><p>Network Service</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p>
<p>Microsoft Filtering Management Service</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Transport Log Search</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>Provides remote search capability for transport log files (for example, message tracking).</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Optional</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Unified Messaging</p></td>
<td><p>MSExchangeUM</p></td>
<td><p>Provides Unified Messaging (UM) features: allows voice and fax messages to be stored in Exchange and gives users telephone access to email, voice mail, calendar, contacts, or an auto attendant. If this service is stopped, Unified Messaging isn't available.</p>
<p>If you don't use UM, you can disable this service.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>CNG Key Isolation</p>
<p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Optional</p></td>
</tr>
</tbody>
</table>


## Exchange services on Exchange 2013 Client Access servers

The following table describes the Exchange services that are installed on Client Access servers.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Service name</th>
<th>Service short name</th>
<th>Description and dependencies</th>
<th>Default startup type</th>
<th>Security context</th>
<th>Dependencies</th>
<th>Required or optional</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Provides Active Directory topology information to Exchange services. If this service is stopped, most Exchange services can't start.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Net.TCP Port Sharing Service</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Diagnostics</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Provides an agent that monitors Exchange server health.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>None</p></td>
<td><p>Required</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Frontend Transport</p></td>
<td><p>MSExchangeFrontEndTransport</p></td>
<td><p>Proxies SMTP connections from external hosts to the Microsoft Exchange Transport service on Mailbox servers.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Health Manager</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Part of managed availability that monitors the health of key components on the Exchange server.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Windows Event Log</p>
<p>Windows Management Instrumentation</p></td>
<td><p>Required</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange IMAP4</p></td>
<td><p>MSExchangeIMAP4</p></td>
<td><p>Proxies IMAP4 client connections to the IMAP4 service on Mailbox servers. By default, this service isn't running, so IMAP4 clients can't connect to the Exchange server until this service is started.</p>
<p>If you don't have any IMAP4 clients, you can disable this service.</p></td>
<td><p>Manual</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Optional</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange POP3</p></td>
<td><p>MSExchangePOP3</p></td>
<td><p>Proxies POP3 client connections to the IMAP4 service on Mailbox servers. By default, this service isn't running, so POP3 clients can't connect to the Exchange server until this service is started.</p></td>
<td><p>Manual</p></td>
<td><p>Network Service</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Optional</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Search Host Controller</p></td>
<td><p>HostControllerService</p></td>
<td><p>Provides deployment and management services for applications on the local Exchange server.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>HTTP Service</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Service Host</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Provides a service host for Exchange components that don't have their own services.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Required</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Unified Messaging Call Router</p></td>
<td><p>MSExchangeUMCR</p></td>
<td><p>Redirects UM client connections to the Unified Messaging service on Mailbox servers.</p>
<p>If you don't use UM, you can disable this service.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>CNG Key Isolation</p>
<p>Microsoft Exchange Active Directory Topology</p></td>
<td><p>Optional</p></td>
</tr>
</tbody>
</table>


## Exchange services on Exchange 2013 Edge Transport servers

The following table describes the Exchange services that are installed on Edge Transport servers.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Service name</th>
<th>Service short name</th>
<th>Description</th>
<th>Default startup type</th>
<th>Security context</th>
<th>Dependencies</th>
<th>Required or optional</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>ADAM_MSExchange</p></td>
<td><p>Stores configuration data and recipient data on the Edge Transport server. This service represents the named instance of the UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) that's automatically created by Exchange Setup.</p></td>
<td><p>Automatic</p></td>
<td><p>Network Service</p></td>
<td><p>COM+ Event System</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Anti-spam Update</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Provides Exchange SmartScreen spam definition updates.</p>

> [!NOTE]
> On November 1, 2016, Microsoft stopped producing spam definition updates for the SmartScreen filters in Exchange and Outlook. The existing SmartScreen spam definitions will be left in place, but their effectiveness will likely degrade over time. For more information, see <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Deprecating support for SmartScreen in Outlook and Exchange</A>.


</td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Optional</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Credential Service</p></td>
<td><p>MSExchangeEdgeCredential</p></td>
<td><p>Monitors credential changes in UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) and installs the changes on the Edge Transport server.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Diagnostics</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Provides an agent that monitors Exchange server health.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>None</p></td>
<td><p>Required</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Health Manager</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Part of managed availability that monitors the health of key components on the Exchange server.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Windows Event Log</p>
<p>Windows Management Instrumentation</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Service Host</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Provides a service host for Exchange components that don't have their own services.</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Required</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Transport</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>Provides SMTP server and transport stack.</p></td>
<td><p>Automatic</p></td>
<td><p>Network Service</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Required</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Transport Log Search</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>Provides remote search capability for transport log files (for example, message tracking).</p></td>
<td><p>Automatic</p></td>
<td><p>Local System</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Optional</p></td>
</tr>
</tbody>
</table>

