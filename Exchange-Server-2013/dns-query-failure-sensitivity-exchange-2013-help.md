---
title: 'DNS query failure sensitivity: Exchange 2013 Help'
TOCTitle: DNS query failure sensitivity
ms:assetid: a3c3980c-20ca-4b54-a2e6-76d49af620b4
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb676467(v=EXCHG.150)
ms:contentKeyID: 50934223
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# DNS query failure sensitivity

 

_**Applies to:** Exchange Server 2013_


In Microsoft Exchange Server 2013, you can adjust the DNS query sensitivity for slightly faster message delivery when DNS errors are encountered for the destination domain. However, depending on the DNS errors, this adjustment may cause delivery failures in certain circumstances.

## DNS queries and remote message delivery

The Exchange server that's responsible for delivering messages to external recipients must be able to find a destination messaging server that accepts mail for the external recipients. Depending on the destination, the messages are put in one or more remote delivery queues as they await delivery to the remote recipients. For more information about delivery queues, see [Queues](queues-exchange-2013-help.md).

The Exchange server queries the configured DNS servers to find the DNS records that are required to deliver the message. The DNS servers are queried in the order in which they're listed. If one of the DNS servers is unavailable, the query goes to the next DNS server on the list. The DNS servers are queried for the following information:

  - **Mail exchange (MX) records for the domain part of the external recipient**   The MX record contains the fully qualified domain name (FQDN) of the messaging server that's responsible for accepting messages for the domain, and a preference value for that messaging server. A lower preference value indicates a preferred messaging server. The preference value is important if the domain has more than one MX record. To optimize fault tolerance, most organizations use multiple messaging servers and multiple MX records that have different preference values.

  - **Address (A) records for the destination messaging servers**   Every messaging server that's used in an MX record should have a corresponding A record. The A record is used to find the IP address of the destination messaging server. The subscribed Edge Transport server uses the IP address to open an SMTP connection with the destination messaging server. Although it's technically possible to use the FQDN of a canonical name (CNAME) record in an MX record, this practice violates RFC 974, RFC 1034, RFC 1912, and RFC 2181, and is therefore not supported by most messaging servers.
    
    The required combination of iterative DNS queries and recursive DNS queries that start with a root DNS server is used to resolve the FQDN of the messaging server that's found in the MX record into an IP address.

In Exchange 2013, there's a DNS query limit that's not configurable of 5 seconds for each DNS server, and a one-minute limit for the entire DNS query.

## Potential DNS problems

Even when the DNS settings on the Exchange server are configured correctly, problems with the DNS records for a specific domain or problems with any of the DNS servers that are used to find the authoritative DNS server for a specific domain may still occur. Generally, these problems are beyond your control and need to be resolved by the parties that own those DNS servers. These DNS-related errors may be caused by one or more of the following conditions:

  - Invalid DNS records for the destination domain

  - Problems with DNS server utilization

  - Problems with DNS server replication

In Exchange 2013, when a DNS query results in errors, the query continues to the next DNS server only if that DNS server hasn't already returned an error for the current query.

You can control the DNS query failure sensitivity by modifying the `%ExchangeInstallPath%bin\EdgeTransport.exe.config` XML application configuration file. This file is associated with the Microsoft Exchange Transport service. Changes you save to this file are applied after you restart the Microsoft Exchange Transport service. When you restart this service, mail flow on the server is temporarily interrupted. The DNS query failure sensitivity is controlled by the *DnsFaultTolerance* key in the EdgeTransport.exe.config file. This key uses the following values:

  - **Lenient**   When the DNS query encounters a combination of valid MX records and invalid MX records, the DNS query continues until the DNS query time-out value of one minute is reached. The invalid MX records are discarded, and the valid MX record that has the lowest preference value is used to deliver the message to the destination messaging server. This is the default value.

  - **Normal**   When the DNS query first encounters an invalid MX record, any resolved MX records that have a preference value that's greater than or equal to the invalid MX records are immediately discarded. The remaining MX record that has the lowest preference value is used to deliver the message to the destination messaging server without waiting for the whole DNS query to time out. Although this behavior may result in faster message delivery, the potential drawback of this behavior is the DNS query may have no valid MX records if the following conditions are true:
    
      - The invalid MX record is the first MX record for the destination domain.
    
      - The valid MX records have the same precedence value as the invalid MX records.

In both `Normal` mode and `Lenient` mode, the results of the DNS query for an invalid MX record are never cached. The next time that a DNS query is executed, it will try to resolve the MX records for the destination domain.


> [!NOTE]
> Any customized per-server settings you make in Exchange XML application configuration files, for example, web.config files on Client Access servers or the EdgeTransport.exe.config file on Mailbox servers, will be overwritten when you install an Exchange Cumulative Update (CU). Make sure that you save this information so you can easily re-configure your server after the install. You must re-configure these settings after you install an Exchange CU.


