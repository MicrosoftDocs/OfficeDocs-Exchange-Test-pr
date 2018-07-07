---
title: 'Domains: Exchange 2013 Help'
TOCTitle: Domains
ms:assetid: 11748c2d-2e32-43a4-b77d-e0c17db6200b
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673041(v=EXCHG.150)
ms:contentKeyID: 49289175
ms.date: 07/14/2016
mtps_version: v=EXCHG.150
---

# Domains

 

_**Applies to:** Exchange Server 2013, Office 365_


Domains represent SMTP namespaces for which email directories and mailboxes are set up. By configuring the domains that interact with your Microsoft Exchange Server 2013 organization, you can configure how email to and from various domains is processed by Exchange.

## Accepted domains

An accepted domain is any SMTP namespace for which your Exchange organization sends or receives email. Accepted domains include those domains for which the Exchange organization is authoritative, as well as internal relay domains and external relay domains. An Exchange organization is authoritative when it handles mail delivery for recipients in the accepted domain. Accepted domains also include domains for which the Exchange organization receives mail and then relays it to an email server that's outside the organization.

For more information about accepted domains, see [Accepted domains](accepted-domains-exchange-2013-help.md).

## Remote domains

In Exchange 2013, you create remote domain entries to define the settings for message transfer between your Exchange organization and domains outside of your organization. When you create a remote domain entry, you control the types of messages that are sent to that domain. You can also apply message format policies and acceptable character sets for messages that are sent from users in your organization to the remote domain.

Settings for remote domains are global configuration settings for your Exchange organization. Remote domain settings are applied to messages during categorization. When recipient resolution occurs, the recipient domain is matched against the configured remote domains. If a remote domain configuration blocks a specific message type from being sent to recipients in that domain, the message is deleted. If you specify a particular message format for the remote domain, the message headers and content are modified. The settings apply to all messages that are processed by the Exchange organization.

For more information about remote domains, see [Remote domains](remote-domains-exchange-2013-help.md).

