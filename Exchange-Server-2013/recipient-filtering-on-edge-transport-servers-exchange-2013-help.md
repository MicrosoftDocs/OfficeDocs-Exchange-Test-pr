---
title: 'Recipient filtering on Edge Transport servers: Exchange 2013 Help'
TOCTitle: Recipient filtering on Edge Transport servers
ms:assetid: 994eefd9-3903-41e6-a882-1e333d6d2d18
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb123891(v=EXCHG.150)
ms:contentKeyID: 49248685
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Recipient filtering on Edge Transport servers

 

_**Applies to:** Exchange Server 2013_


Recipient filtering is an anti-spam feature in Microsoft Exchange Server 2013 that relies on the RCPT TO SMTP header to determine what action, if any, to take on an inbound message. Recipient filtering is performed by the Recipient Filter agent.

The Recipient Filter agent blocks messages according to the characteristics of the intended recipient in the organization. The Recipient Filter agent can help you prevent the acceptance of messages in the following scenarios:

  - **Nonexistent recipients**   You can prevent delivery to recipients that aren't in the organization's address book. For example, you may want to stop delivery to frequently misused account names, such as administrator@contoso.com or support@contoso.com.

  - **Restricted distribution lists**   You can prevent delivery of Internet mail to distribution lists that should be used only by internal users.

  - **Mailboxes that should never receive messages from the Internet**   You can prevent delivery of Internet mail to a specific mailbox or alias that's typically used inside the organization, such as Helpdesk.

The Recipient Filter agent acts on recipients stored in one or both of the following data sources:

  - **Recipient Block list**   An administrator-defined list of recipients who should never receive messages from the Internet.

  - **Recipient Lookup**   Queries Active Directory to verify the recipient exists in the organization. On an Edge Transport server, Recipient Lookup requires access to Active Directory information provided by EdgeSync to the local instance of Active Directory Lightweight Directory Services (AD LDS).

When you enable the Recipient Filter agent, one of the following actions is taken on inbound messages according to the characteristics of the recipients. These recipients are indicated by the RCPT TO header.

  - If the inbound message contains a recipient that is on the Recipient Block list, the Exchange server sends a `550 5.1.1 User unknown` SMTP session error to the sending server.

  - If the inbound message contains a recipient that doesn't match any recipients in Recipient Lookup, the Exchange server sends a `550 5.1.1 User unknown` SMTP session error to the sending server.

  - If the recipient isn't on the Recipient Block list and the recipient is in Recipient Lookup, the Exchange server sends a `250 2.1.5 Recipient OK` SMTP response to the sending server, and the next anti-spam agent in the chain processes the message.

**Contents**

Configuring recipient lookup

Tarpitting functionality

Multiple namespaces

## Configuring recipient lookup

One of the most effective ways to reduce spam is to validate recipients before accepting inbound messages from the Internet. You enable the blocking of messages sent to recipients who don't exist in the Exchange organization, and the blocking of specific recipients using the **Set-RecipientFilterConfig** cmdlet in the Exchange Management Shell. For more information, see [Manage recipient filtering on Edge Transport servers](manage-recipient-filtering-on-edge-transport-servers-exchange-2013-help.md).

If you have an Edge Transport server installed in your perimeter network, it's a good idea to configure the AD LDS instance that runs on the Edge Transport server to synchronize with Active Directory. By default, AD LDS is installed and configured on the Edge Transport server. However, you must configure AD LDS to communicate with an Active Directory domain-joined global catalog server by subscribing the Edge Transport server to your organization. For more information, see [Use an Exchange 2010 or 2007 Edge Transport server in Exchange 2013](use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md).

Return to top

## Tarpitting functionality

Recipient Lookup functionality enables the sending server to determine whether an email address is valid or invalid. As mentioned earlier, when the recipient of an inbound message is a known recipient, the Exchange server sends back a `250 2.1.5 Recipient OK` SMTP response to the sending server. This functionality provides an ideal environment for a directory harvest attack.

A *directory harvest attack* is an attempt to collect valid email addresses from a particular organization so that the email addresses can be added to a spam database. Because all spam income relies on trying to make people open email messages, addresses known to be active are a commodity that malicious users, or *spammers*, pay for. Because the SMTP protocol provides feedback for known senders and unknown senders, a spammer can write an automated program that uses common names or dictionary terms to construct email addresses to a specific domain. The program collects all email addresses that return a `250 2.1.5 Recipient OK` SMTP response and discards all email addresses that return a `550 5.1.1 User unknown` SMTP session error. The spammer can then sell the valid email addresses or use them as recipients for unsolicited messages.

To combat directory harvest attacks, Exchange 2013 includes tarpitting functionality. *Tarpitting* is the practice of artificially delaying server responses for specific SMTP communication patterns that indicate high volumes of spam or other unwelcome messages. The intent of tarpitting is to slow down the communication process for such email traffic so that the cost of sending spam increases for the person or organization sending the spam. Tarpitting makes directory harvest attacks too costly to automate efficiently.

If tarpitting isn't configured, the Exchange server immediately returns a `550 5.1.1 User unknown` SMTP session error to the sender when a recipient isn't located in Recipient Lookup. Alternatively, if tarpitting is configured, SMTP waits a specified number of seconds before it returns the `550 5.1.1 User unknown` error. This pause in the SMTP session makes automating a directory harvest attack more difficult and less cost-effective for the spammer. By default, tarpitting is configured for 5 seconds on Receive connectors.

To configure the delay before SMTP returns the `550 5.1.1 User unknown` error, you set the tarpitting interval using the *TarpitInterval* parameter on the **Set-ReceiveConnector** cmdlet. The syntax is:

    Set-ReceiveConnector <Receive Connector> -TarpitInterval <00:00:00 to 00:10:00>

The default value is `00:00:05` or 5 seconds. The name of the default Receive connector on an Edge Transport server is `Default internal receive connector <server name>`.

Use caution if you decide to change the tarpitting interval. An overly long interval could disrupt ordinary mail flow, whereas an overly brief interval may not be as effective in thwarting a directory harvest attack. If you change the tarpitting interval, do so in small increments and verify the results. For example, if 5 seconds isn't effective, try changing the interval to 10 seconds.

Return to top

## Multiple namespaces

The Recipient Filter agent performs recipient lookups only for authoritative domains. If your organization accepts and forwards messages on behalf of another domain that's configured as an internal relay or external relay domain, the Recipient Filter agent doesn't perform a recipient lookup on recipients in those domains. However, if the recipient is specified in the Recipient Block list, the recipient will still be blocked by the Recipient Filter agent.

Note that you can also configure accepted domains locally on an Edge Transport server. If the domain is configured as internal relay or external relay domain, the Recipient Filter agent on the Edge Transport server also doesn't perform a recipient lookup on recipients in those domains.

Return to top

