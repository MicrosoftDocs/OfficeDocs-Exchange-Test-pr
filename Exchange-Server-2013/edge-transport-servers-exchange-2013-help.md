---
title: 'Edge Transport servers: Exchange 2013 Help'
TOCTitle: Edge Transport servers
ms:assetid: cfff9f59-afac-447c-8297-afcebe49a52d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124701(v=EXCHG.150)
ms:contentKeyID: 61200300
ms.date: 09/29/2016
mtps_version: v=EXCHG.150
---

# Edge Transport servers

 

_**Applies to:** Exchange Server 2013_


Edge Transport servers minimize the attack surface by handling all Internet-facing mail flow, which provides SMTP (Simple Mail Transfer Protocol) relay and smart host services for your Exchange organization. Agents running on the Edge Transport server provide additional layers of message protection and security. These agents provide protection against spam and apply transport rules to control mail flow.

Because the Edge Transport server is installed in the perimeter network, it's never a member of your organization's internal Active Directory forest and doesn't have access to Active Directory information. However, the Edge Transport server requires data that resides in Active Directory—for example, connector information for mail flow and recipient information for antispam recipient lookup tasks. This data is synchronized to the Edge Transport server by the Microsoft Exchange EdgeSync service (EdgeSync). EdgeSync is a collection of processes run on an Exchange 2013 Mailbox server to establish one-way replication of recipient and configuration information from Active Directory to the Active Directory Lightweight Directory Services (AD LDS) instance on the Edge Transport server. EdgeSync copies only the information that's required for the Edge Transport server to perform anti-spam configuration tasks and to enable end-to-end mail flow. EdgeSync performs scheduled updates so the information in AD LDS remains current.

You can install more than one Edge Transport server in the perimeter network. Deploying more than one Edge Transport server provides redundancy and failover capabilities for your inbound message flow. You can load balance the SMTP traffic to your organization among Edge Transport servers by defining more than one MX record with the same priority value for your mail domain. You can achieve consistency in the configuration among multiple Edge Transport servers by using cloned configuration scripts.

The Edge Transport server role lets you manage the following message-processing scenarios.

## Internet mail flow

Edge Transport servers accept messages coming into the Exchange organization from the Internet. After the messages are processed by the Edge Transport server, where they are routed next depends on the configuration of your internal Exchange servers:

  - If the Client Access server and the Mailbox server are installed on separate computers, mail is routed to the Transport service on the Mailbox server. The Client Access server is bypassed for inbound SMTP mail flow.

  - If the Client Access server and the Mailbox server are installed on the same computer, mail is routed to the Front End Transport service on the Client Access server and then to the Transport service on the Mailbox server.

All messages sent to the Internet from inside the organization are routed to Edge Transport servers after the messages are processed by the Transport service on the Mailbox server. You can configure the Edge Transport server to use DNS to resolve MX resource records for external SMTP domains, or you can configure the Edge Transport server to forward messages to a smart host for DNS resolution.

## Anti-spam protection

In Exchange 2013, anti-spam features provide services to block unsolicited commercial email (spam) at the network perimeter.

Spammers use a variety of techniques to send spam into your organization. Edge Transport servers help prevent users from ever receiving spam by providing a collection of agents that work together to provide different layers of spam filtering and protection. Establishing tarpitting intervals on connectors makes email harvesting attempts ineffective.

## Edge Transport rules

Edge Transport rules are used to control the flow of messages sent to or received from the Internet. Edge Transport rules are configured on each Edge Transport server to help protect corporate network resources and data by applying an action to messages meeting specified conditions. Edge Transport rule conditions are based on data, such as specific words or text patterns in the message subject, body, header, or from address; the spam confidence level (SCL); or the attachment type. Actions determine how the message is processed when a specified condition is true. Possible actions include quarantining a message, dropping or rejecting a message, appending additional recipients, or logging an event. Optional exceptions exempt particular messages from having an action applied.

## Address rewriting

Address rewriting presents a consistent email address appearance to external recipients. You configure address rewriting on Edge Transport servers to modify the SMTP addresses on inbound and outbound messages. Address rewriting is especially useful for newly merged organizations that want to present a consistent email address appearance.

For more information about address rewriting, see [Address rewriting on Edge Transport servers](address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

