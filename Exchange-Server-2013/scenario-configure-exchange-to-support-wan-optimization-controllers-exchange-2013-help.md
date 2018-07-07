---
title: 'Scenario: Configure Exchange to support WAN Optimization Controllers: Exchange 2013 Help'
TOCTitle: 'Scenario: Configure Exchange to support WAN Optimization Controllers'
ms:assetid: 1f407698-0b71-45a3-867a-640ccf7351da
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee633456(v=EXCHG.150)
ms:contentKeyID: 50934213
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Scenario: Configure Exchange to support WAN Optimization Controllers

 

_**Applies to:** Exchange Server 2013_


In Microsoft Exchange Server 2013, Transport Layer Security (TLS) encryption is mandatory for all SMTP communication in the Transport service between Mailbox servers. This increases overall security of Transport service communication between Mailbox servers. However, in certain topologies where WAN Optimization Controller (WOC) devices are used, the TLS encryption of SMTP traffic may be undesirable. You can disable TLS for Transport service communication between Mailbox servers for these specific scenarios.

Consider the topology shown in the following figure. The assumption for this four-site topology is that the two central office sites and Branch Office 2 are well-connected, whereas the connection between Central Office Site 1 and Branch Office 1 is over a WAN link. The company has installed WOC devices on this link to compress and optimize traffic over the WAN.

**Sample network topology with WOC devices**

![Sample topology with WAN optimizers](images/Ee633456.52876869-52f1-4c0f-85b2-7a850643e8a1(EXCHG.150).gif "Sample topology with WAN optimizers")

In this topology, because Exchange 2013 uses TLS encryption for communication between Mailbox servers, the SMTP traffic that goes over the WAN link can't be compressed. Ideally, all SMTP traffic that goes over the WAN link should be unencrypted SMTP, while retaining TLS security within well-connected sites. Exchange 2013 gives you the option to disable TLS encryption for traffic between sites by configuring Receive connectors. Using this ability in Exchange 2013, you can configure an exception to the SMTP traffic between Central Office Site 1 and Branch Office 1, as shown in the following figure.

**Preferred logical message flow**

![Preferred logical message flow](images/Ee633456.e0fe62fa-1bad-4d43-9eaf-205a9b8d07e1(EXCHG.150).gif "Preferred logical message flow")

The recommended configuration is to limit the non-encrypted SMTP traffic to only those messages that pass over the WAN link. Therefore, the intrasite Transport service communication between Mailbox servers in all sites, and the cross-site Transport service communication between Mailbox servers that don't involve Branch Office 1 should all be TLS encrypted.

To achieve this end result, you need to do the following actions, in the specified order, on every Mailbox server in the sites that contain the WOC devices (Central Office Site 1 and Branch Office 1 in the sample topology):

1.  Enable downgraded Exchange Server authentication.

2.  Create a dedicated Receive connector to handle the traffic over the connection that has WOC devices.
    
    1.  Configure the remote IP address range property of the dedicated Receive connector to the IP address ranges of the Mailbox servers in the remote Active Directory site.
    
    2.  Disable TLS on the dedicated Receive connector.

In addition, you need to do the following actions to ensure all SMTP traffic over the WAN is handled by the dedicated Receive connectors you created:

  - Configure the Active Directory sites that will participate in the non-TLS communication as hub sites to force all message flow through the dedicated Receive connectors (Central Office Site 1 and Branch Office Site 1 in the sample topology).

  - Verify that the Active Directory IP site link costs are configured in a way that ensures the least cost routing path to your remote site (Branch Office 1 in the sample topology) goes through the network link that has the WOC devices. Assign an Exchange-specific cost to the Active Directory site links as necessary.

The following sections provide an overview of these steps. For step-by-step instructions on how to configure your organization for this scenario, see [Disable TLS between Active Directory sites](disable-tls-between-active-directory-sites-exchange-2013-help.md).

**Contents**

Downgrade authentication over TLS-disabled connections

Create and configure dedicated Receive connectors

Configure Hub sites

Configure Exchange-specific Active Directory site link costs

## Downgrade authentication over TLS-disabled connections

Kerberos authentication is used with TLS encryption in Exchange. When you disable TLS on the Transport service communication between Mailbox servers, you need to perform another form of authentication. When Exchange 2013 communicates with other servers running Exchange that don't support **X-ANONYMOUSTLS**, it falls back to using Generic Security Services Application Programming Interface (GSSAPI) authentication. All Transport service communications between Exchange 2013 Mailbox servers use **X-ANONYMOUSTLS**. When you configure the Transport service on your Mailbox server to use downgraded Exchange Server authentication, you are in effect enabling GSSAPI authentication for Transport service communication with other Exchange 2013 Mailbox servers.

Return to top

## Create and configure dedicated Receive connectors

You need to create Receive connectors that will solely be responsible for handling the non-TLS encrypted traffic. Using separate Receive connectors for this purpose ensures that all traffic that doesn't pass through the WAN link remains protected by TLS encryption.

To restrict the dedicated Receive connectors to only the traffic over the WAN, you need to configure the remote IP address range property. Exchange always uses the connector with the most specific remote IP address range. Therefore, these new connectors will be preferred over the default Receive connector configured to receive messages from anywhere.

Going back to the sample topology, assume that the class C subnet 10.0.1.0/24 is used for the Central Office Site 1 and 10.0.2.0/24 is used for the Branch Office 1. To prepare for disabling TLS between these two sites, you need to:

1.  Create a Receive connector named WAN on each Mailbox server in Central Office Site 1 and Branch Office 1.

2.  Configure the remote IP address range of 10.0.2.0/24 on each dedicated Receive connector in Central Office Site 1.

3.  Configure the remote IP address range of 10.0.1.0/24 on each dedicated Receive connector in Branch Office 1.

4.  Disable TLS on all of the dedicated Receive connectors.

The end result is shown in the following figure (with the remote IP address range property of the Receive connectors named WAN shown in parentheses). Only a single Mailbox server is shown in Branch Office 1, and Branch Office 2 is omitted for clarity purposes.

**Receive connector configuration**

![Receive connector configuration](images/Ee633456.1821b3db-1f7a-4ae7-afbc-5c99e117f976(EXCHG.150).gif "Receive connector configuration")

Return to top

## Configure Hub sites

By default, an Exchange 2013 Mailbox server will attempt a direct connection to the Mailbox server closest to the final destination of a specific message. In the sample topology, if a user in Branch Office 2 sends a message to a user in Branch Office 1, the Mailbox server in Branch Office 2 will connect to the Mailbox server in Branch Office 1 directly to deliver that message. That connection will be encrypted and therefore not desirable in the specific topology. To have such messages pass through the Mailbox servers on Central Office Site 1, thereby ensuring they aren't encrypted while in transit over the WAN link, Central Office Site 1 and Branch Office 1 need to be configured as hub sites. In short, any site where you have a Mailbox server with a Receive connector with TLS disabled needs to be configured as a hub site, so you can force servers in other sites to route traffic through that site. For more information, see [Configure Exchange mail routing settings in Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

Return to top

## Configure Exchange-specific Active Directory site link costs

Configuring hub sites alone isn't sufficient to ensure that all traffic is unencrypted over the WAN link. This is because Exchange will route messages through hub sites only if the hub site lies within the least cost routing path. For example, assume that the IP site link costs for our sample topology are configured in Active Directory as shown in the following figure (Central Office Site 2 is omitted for clarity).

**IP site link costs for the sample topology**

![IP site link costs for sample topology](images/Ee633456.099deb15-795a-417a-b6aa-925b3bedf8b4(EXCHG.150).gif "IP site link costs for sample topology")

In this case, the path from Branch Office 2 to Branch Office 1 that goes through the hub site has a total cost of 12 (6+6), whereas the cost of the direct path is 10. Therefore, none of the messages from Branch Office 2 to Branch Office 1 will go through Central Office Site 1 and therefore all of that traffic will still be TLS encrypted.

To avoid this issue, you need to designate an Exchange-specific cost that is higher than 12 for the IP site link between Branch Office 2 and Branch Office 1, as shown in the following figure. This will ensure that all messages go through the unencrypted channel between Central Office Site 1 and Branch Office 1.

**Sample topology configured with Exchange-specific IP site link costs**

![Sample topology with Exchange costs](images/Ee633456.cd036fe0-c37d-479e-a4c1-235e17e90ca7(EXCHG.150).gif "Sample topology with Exchange costs")

For more information, see [Configure Exchange mail routing settings in Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

Return to top

