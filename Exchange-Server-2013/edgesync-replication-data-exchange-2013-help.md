---
title: 'EdgeSync replication data: Exchange 2013 Help'
TOCTitle: EdgeSync replication data
ms:assetid: c7dd137d-7ed4-4f16-9895-f354c449cf9b
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb232177(v=EXCHG.150)
ms:contentKeyID: 61200299
ms.date: 07/14/2016
mtps_version: v=EXCHG.150
---

# EdgeSync replication data

 

_**Applies to:** Exchange Server 2013_


When you deploy an Edge Transport server, it doesn't have access to Active Directory. To perform recipient lookup and safelist aggregation tasks, and to implement domain security by using Mutual Transport Layer Security (MTLS) authentication, the Edge Transport server needs data from Active Directory. This data is replicated to the Edge Transport server using EdgeSync; the Edge Transport server stores all replicated information in Active Directory Lightweight Directory Services (AD LDS).

This topic focuses on data replicated from Active Directory to AD LDS on an Edge Transport server subscribed to an Active Directory site. To learn more about EdgeSync and Edge Subscriptions, see [Edge Subscriptions](edge-subscriptions-exchange-2013-help.md).

Four types of data are replicated to AD LDS and used by the Edge Transport server:

Edge Subscription information

Configuration information

Recipient information

Topology information

## Edge Subscription information

Exchange 2013 extends both the Active Directory and AD LDS schemas to provide attributes on the **ms-Exch-ExchangeServer** object to represent the data needed to control EdgeSync synchronization. These attributes provide three functions to EdgeSync:

  - Automatic provisioning and maintenance of the credentials used to help secure the LDAP connection between a Mailbox server and a subscribed Edge Transport server.

  - Arbitrating the synchronization lock and lease process, ensuring that only one server at a time will try to synchronize with an individual Edge Transport server. For more information about the lock and lease process, see [Edge Subscriptions](edge-subscriptions-exchange-2013-help.md).

  - Optimizing EdgeSync synchronization to maintain a record of current synchronization status. Easily viewing synchronization status helps avoid excessive manual synchronization.

The schema extensions in the following table are specific to Edge Subscriptions. The values assigned to these attributes are maintained by the Edge Subscription and EdgeSync; they are not intended to be manually edited.

### Edge Subscription schema extensions

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ms-Exch-Server-EKPK-Public-Key</strong></p></td>
<td><p>The current public key for the certificate being used by the server. This value is stored by both Edge Transport servers and Mailbox servers. The public key is used to encrypt credentials used to authenticate the server during LDAP and SMTP communication.</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-EdgeSync-Credential</strong></p></td>
<td><p>The list of credentials EdgeSync uses to establish an authenticated LDAP session with AD LDS. On Mailbox servers, this attribute contains only credentials the Mailbox server uses to authenticate the subscribed Edge Transport servers. On Edge Transport servers, this attribute contains the credentials of each Mailbox server in the subscribed Active Directory site that participates in EdgeSync synchronization. This attribute is only present on Mailbox servers running EdgeSync synchronization and on subscribed Edge Transport servers.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ms-Exch-Edge-Sync-Lease</strong></p></td>
<td><p>Used to arbitrate between Mailbox servers when more than one Mailbox server tries to replicate to the same Edge Transport server.</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-Edge-Sync-Status</strong></p></td>
<td><p>Only present in AD LDS on the Edge Transport server object. This attribute tracks the status of replication to an AD LDS instance and includes information about replication.</p></td>
</tr>
</tbody>
</table>


Return to top

## Configuration information

When you subscribe an Edge Transport server to an organization, you can manage the configuration objects common to the Edge Transport server and the Exchange organization from inside the organization. These changes are then replicated to the Edge Transport server using EdgeSync. This process helps maintain a consistent configuration across all servers involved in message processing.

A subset of the configuration data for the Exchange organization must also be maintained on the Edge Transport server. During EdgeSync synchronization, the configuration data the Edge Transport server needs is written to the configuration partition of AD LDS. The configuration data written to AD LDS includes:

  - **Mailbox servers**   The fully qualified domain name (FQDN) of each Mailbox server in the subscribed Active Directory site is made available to the local AD LDS store on the Edge Transport server. This information is used to derive a list of smart host servers for the inbound Send connector.

  - **Accepted domains**   All authoritative, internal relay, and external relay domains configured for the Exchange organization are written to AD LDS. Having the accepted domains available to the Edge Transport server enables the Exchange organization to perform domain filtering and reject invalid SMTP traffic into their organization as early as possible. For more information about accepted domains, see [Accepted domains](accepted-domains-exchange-2013-help.md).

  - **Message classifications**   If message classifications are available on the Edge Transport server, transport agents and content conversion can act on message classifications in the perimeter network. For example, the Attachment Filter agent can apply the Attachment Removed classification when it removes an attachment, sending informational text to a Microsoft Outlook user or an Outlook Web App user to tell the recipient what happened. Agents developed for use by third-party applications can use message classifications in a similar manner.

  - **Remote domains**   All remote domain entries configured for the Exchange organization are written to AD LDS. Remote domain entries control out-of-office message settings and message format settings for a remote domain. For more information about remote domains, see [Remote domains](remote-domains-exchange-2013-help.md).

  - **Send connectors**   By default, creating an Edge Subscription automatically creates the Send connectors required to enable end-to-end mail flow between the Exchange organization and the Internet at the time the Edge Transport Server is subscribed. Any existing Send connectors on the Edge Transport server are deleted. If you want to configure additional Send connectors, configure the Send connector inside the Exchange organization and then select the Edge Subscription as the source server for the connector. For more information, see [Edge Subscriptions](edge-subscriptions-exchange-2013-help.md).

  - **Internal SMTP servers**   The value for the *InternalSMTPServers* attribute is stored on the **TransportConfig** object for both the Exchange organization and the local Edge Transport server. During EdgeSync synchronization, the value stored on the local Edge Transport server object is overwritten with the value stored on this object for the Exchange organization. This attribute specifies a list of internal SMTP server IP addresses or IP address ranges that should be ignored by Sender ID and connection filtering.

  - **Domain Secure lists**   The *TLSReceiveDomainSecureList* and the *TLSSendDomainSecureList* attributes are stored on the **TransportConfig** object for both the Exchange organization and the local Edge Transport server. During EdgeSync synchronization, the value stored on the local Edge Transport server object is overwritten with the value stored on this object for the Exchange organization. These attributes specify the list of remote domains configured for mutual TLS authentication.

Return to top

## Recipient information

Recipient information replicated to AD LDS includes only a subset of recipient attributes. Only data required by the Edge Transport to perform certain antispam tasks is replicated. Recipient information replicated to AD LDS includes:

  - **Recipients**   The list of recipients in the Exchange organization is replicated to AD LDS. Each recipient is identified by assigned Active Directory GUID. If you configure a recipient's account to deny receipt of mail from outside the organization, that recipient isn't replicated to AD LDS. If you disable or delete a recipient's mailbox, that mailbox is no longer replicated to AD LDS.

  - **Proxy addresses**   All proxy addresses assigned to each recipient are replicated to AD LDS as hashed data. This is a one-way hash using Secure Hash Algorithm (SHA)-256. SHA-256 generates a 256-bit message digest of the original data. Storing proxy addresses as hashed data helps secure this information in case the Edge Transport server or AD LDS is compromised. Proxy addresses are referenced when the Edge Transport server performs the recipient lookup antispam task.

  - **Safe Senders List, Blocked Senders List, and Safe Recipients List**   Safe Senders Lists, Blocked Senders Lists and Safe Recipients Lists defined in each recipient's Outlook instance are aggregated and replicated to AD LDS. These settings are stored in the mailbox database where the recipient's mailbox resides. An Outlook user's safelist collection is the combined data from the user's Safe Senders List, Safe Recipients List, Blocked Senders List, and external contacts. Having safelist collection data available in AD LDS enables the Edge Transport server to screen senders appropriately, reducing operational overhead for filtering mail. This information is sent as hashed data.
    

    > [!IMPORTANT]
    > Although the safe recipient data is stored in Outlook and can be aggregated into the safelist collection on the AD&nbsp;LDS instance on the Edge Transport server, the content filtering functionality doesn't act on safe recipient data.



  - **Per recipient anti spam settings**   You can use the **Set-Mailbox** cmdlet to assign anti spam threshold settings per recipient that differ from the organization-wide anti spam settings. If you configure per recipient anti spam settings, these settings override organization-wide settings. By replicating these settings to AD LDS, the per recipient settings can be considered before the message is relayed to the Exchange organization. This information is sent as hashed data.

Return to top

## Topology information

The topology information includes notification of newly subscribed Edge Transport servers or removed Edge Subscriptions. This data is refreshed every five minutes.

Return to top

