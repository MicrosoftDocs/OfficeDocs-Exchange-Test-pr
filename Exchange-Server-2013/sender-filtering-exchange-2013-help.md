---
title: 'Sender filtering: Exchange 2013 Help'
TOCTitle: Sender filtering
ms:assetid: b833f864-ff10-46a0-a653-28fb9ba30896
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124354(v=EXCHG.150)
ms:contentKeyID: 49248686
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Sender filtering

 

_**Applies to:** Exchange Server 2013_


Sender filtering relies on the MAIL FROM: SMTP header to determine what action, if any, to take on an inbound email message. Sender filtering is provided by the Sender Filter agent.

The Sender Filter agent acts on messages from specific senders outside the organization. Administrators maintain a list of senders who are blocked from sending messages to the organization. As an administrator, you can block single senders (such as kim@contoso.com), whole domains (contoso.com), or domains and all subdomains (\*.contoso.com). You can also configure what action the Sender Filter agent should take when a message that has a blocked sender is found. You can configure the following actions:

  - The Sender Filter agent rejects the SMTP request with a `554 5.1.0 Sender Denied` SMTP session error and closes the connection.

  - The Sender Filter agent accepts the message and updates the message to indicate that the message came from a blocked sender. Because the message came from a blocked sender and it's marked as such, the Content Filter agent will use this information when it calculates the spam confidence level (SCL).

You can designate blocked senders and define how the Sender Filter agent should act on messages from blocked senders. For more information about how to configure the Sender Filter agent, see [Manage sender filtering](manage-sender-filtering-exchange-2013-help.md).


> [!IMPORTANT]
> The MAIL FROM: SMTP headers can be spoofed. Therefore, you shouldn't rely on the Sender Filter agent only. Use the Sender Filter agent and the Sender ID agent together. The Sender ID agent uses the originating IP address of the sending server to verify that the domain in the MAIL FROM: SMTP header matches the domain that's registered. For more information about the Sender ID agent, see <A href="sender-id-exchange-2013-help.md">Sender ID</A>.



## Using the Sender Filter agent to block messages

When the Sender Filter agent is enabled on an Exchange server, sender filtering blocks inbound messages that come from the Internet, but aren't authenticated. These messages are handled as external messages. You can disable the Sender Filter agent in individual computer configurations. For more information, see [Manage sender filtering](manage-sender-filtering-exchange-2013-help.md).

When you enable the Sender Filter agent on an Exchange server, the Sender Filter agent filters all messages that come through all Receive connectors on that computer. As noted earlier in this topic, only messages that come from external sources are filtered. *External sources* are defined as non-authenticated sources. These are considered anonymous Internet sources.

As a best practice, you shouldn't filter email messages from trusted partners or from inside your organization. When you run anti-spam filters, there's always a chance that the filters will detect false positives. You should configure anti-spam agents to run only on messages from potentially untrusted and unknown sources. This will reduce the chance that anti-spam filters will mishandle legitimate messages. You can enable and disable the Sender Filter agent to run on messages from any source. For more information, see [Manage sender filtering](manage-sender-filtering-exchange-2013-help.md).

You can configure the Sender Filter agent to block inbound messages that don't specify a sender and domain in the MAIL FROM: SMTP header. You can use this feature to prevent non-delivery report (NDR) attacks on the Exchange server. Most legitimate SMTP messages come from SMTP servers that provide a sender and domain in the MAIL FROM: SMTP command.

## Specifying the block action

After you've specified blocked senders and domains, you must specify how you want the Sender Filter agent to act on messages from blocked senders and domains. We recommend that you reject the messages. When you use the Sender Filter agent to block email addresses and domains that are specified by an Exchange administrator, the chance of false positives is relatively less than when you use other anti-spam agents. For example, the Content Filter agent is an anti-spam agent that relies on many different variables to determine whether a message is spam.

There are only two scenarios in which legitimate messages may be rejected by the Sender Filter agent:

  - If you mistype an email address or domain name, the wrong sender may be blocked.

  - If a domain name is reregistered to a legitimate company after you add the domain to your Blocked Senders list, you will unintentionally block legitimate messages.

In either of these cases, it may still make sense to reject the messages.

