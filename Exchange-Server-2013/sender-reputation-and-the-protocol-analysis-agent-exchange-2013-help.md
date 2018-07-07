---
title: 'Sender reputation and the Protocol Analysis agent: Exchange 2013 Help'
TOCTitle: Sender reputation and the Protocol Analysis agent
ms:assetid: c4c34235-d545-41e7-ac2f-1dd43aaa3708
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124512(v=EXCHG.150)
ms:contentKeyID: 49248689
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Sender reputation and the Protocol Analysis agent

 

_**Applies to:** Exchange Server 2013_


Sender reputation is part of the Exchange anti-spam functionality that blocks messages according to many characteristics of the sender. Sender reputation relies on persisted data about the sender to determine what action, if any, to take on an inbound message. The Protocol Analysis agent is the underlying agent for sender reputation functionality.

When you configure anti-spam agents on an Exchange server, the agents act on messages cumulatively to reduce the number of unsolicited messages that enter the organization.

**Contents**

Calculation of the sender reputation level

Use of the SRL

Enabling and configuring the detection of open proxy servers

Setting the SRL block threshold

## Calculation of the sender reputation level

A sender reputation level (SRL) is calculated from the following statistics:

  - **HELO/EHLO analysis**   The HELO and EHLO SMTP commands are intended to provide the domain name, such as Contoso.com, or IP address of the sending SMTP server to the receiving SMTP server. Malicious users, or *spammers*, frequently forge the HELO/EHLO statement in various ways. For example, they type an IP address that doesn't match the IP address from which the connection originated. Spammers also put domains that are known to be locally supported at the receiving server in the HELO statement in an attempt to appear as if the domains are in the organization. In other cases, spammers change the domain that's passed in the HELO statement. The typical behavior of a legitimate user may be to use a different, but relatively constant, set of domains in their HELO statements.
    
    Therefore, analysis of the HELO/EHLO statement on a per-sender basis may indicate that the sender is likely to be a spammer. For example, a sender that provides many different unique HELO/EHLO statements in a specific time period is more likely to be a spammer. Senders who consistently provide an IP address in the HELO statement that doesn't match the originating IP address as determined by the Connection Filter agent are also more likely to be spammers. Remote senders who consistently provide a local domain name in the HELO statement that's in the same organization as the Exchange server are also more likely to be spammers.

  - **Reverse DNS lookup**   Sender reputation also verifies that the originating IP address from which the sender transmitted the message matches the registered domain name that the sender submits in the HELO or EHLO SMTP command.
    
    Sender reputation performs a reverse DNS query by submitting the originating IP address to DNS. The result that's returned by DNS is the domain name that's registered by using the domain naming authority for that IP address. Sender reputation compares the domain name that's returned by DNS to the domain name that the sender submitted in the HELO/EHLO SMTP command. If the domain names don't match, the sender is likely to be a spammer, and the overall SRL rating for the sender is increased.
    
    The Sender ID agent performs a similar task, but the success of the Sender ID agent relies on legitimate senders to update their DNS infrastructure to identify all the email-sending SMTP servers in their organization. By performing a reverse DNS lookup, you can help identify potential spammers.

  - **Analysis of SCL ratings on messages from a particular sender**   When the Content Filter agent processes a message, it assigns a spam confidence level (SCL) rating to the message. The SCL rating is a number from 0 through 9. A higher SCL rating indicates that a message is more likely to be spam. Data about each sender and the SCL ratings that their messages yield is persisted for analysis by sender reputation. Sender reputation calculates statistics about a sender according to the ratio between all messages from that sender that had a low SCL rating in the past and all messages from that sender that had a high SCL rating in the past. Additionally, the number of messages that have a high SCL rating that the sender has sent in the last day is applied to the overall SRL.

  - **Sender open proxy test**   An *open proxy* is a proxy server that accepts connection requests from anyone anywhere and forwards the traffic as if it originated from the local hosts. Proxy servers relay TCP traffic through firewall hosts to provide user applications transparent access across the firewall. Because proxy protocols are lightweight and independent of user application protocols, proxies can be used by many different services. Proxies can also be used to share a single Internet connection by multiple hosts. Proxies are usually set up so that only trusted hosts inside the firewall can cross through the proxies. A legitimate sender may be an open proxy because of an unintentional misconfiguration or malware.
    
    Open proxies provide an ideal way for malicious users to hide their true identities and launch denial of service attacks (DoS) or send spam. As more proxy servers are configured to be open by default, open proxies have become more common. Additionally, malicious users can use multiple open proxies together to hide the sender's originating IP address.
    
    When sender reputation performs an open proxy test, it does so by formatting an SMTP request in an attempt to connect back to the Exchange server from the open proxy. If an SMTP request is received from the proxy, sender reputation verifies that the proxy is an open proxy and updates the open proxy test statistic for that sender.

Sender reputation weighs each of these statistics and calculates an SRL for each sender. The SRL is a number from 0 through 9 that predicts the probability that a specific sender is a spammer or otherwise malicious user. A value of 0 indicates that the sender isn't likely to be a spammer; a value of 9 indicates that the sender is likely to be a spammer.

You can configure a block threshold from 0 through 9 at which sender reputation issues a request to the Sender Filter agent, and, therefore, blocks the sender from sending a message into the organization. When a sender is blocked, the sender is added to the Blocked Senders list for a configurable period. How blocked messages are handled depends on the configuration of the Sender Filter agent. The following actions are the options for handling blocked messages:

  - Reject

  - Delete and archive

  - Accept and mark as a blocked sender

If a sender is included in the IP Block list or Microsoft IP Reputation Service, sender reputation issues an immediate request to the Sender Filter agent to block the sender. To take advantage of this functionality, you must enable and configure the Microsoft Exchange Anti-spam Update Service.

By default, sender reputation sets a rating of 0 for senders that haven't been analyzed. After a sender has sent 20 or more messages, sender reputation calculates an SRL that's based on the statistics listed earlier in this topic.

Return to top

## Use of the SRL

Sender reputation acts on messages during two phases of the SMTP session:

  - **At the MAIL FROM: SMTP command**   Sender reputation acts on a message only if the message was blocked or otherwise acted on by the Connection Filter agent, Sender Filter agent, Recipient Filter agent, or Sender ID agent. In this case, sender reputation retrieves the sender's current SRL rating from the sender profile that's persisted about that sender on the Exchange server. After this rating is retrieved and evaluated, the Exchange server configuration dictates the behavior that occurs at a particular connection according to the block threshold.

  - **After the "end of data" SMTP command**   The end of data transfer (**EOD**) SMTP command is given when all the actual message data is sent. At this point in the SMTP session, many of the anti-spam agents have processed the message. As a by-product of anti-spam processing, the statistics that sender reputation relies on are updated. Therefore, sender reputation has the data to calculate or recalculate an SRL rating for the sender.

For more information, see [Manage sender reputation](manage-sender-reputation-exchange-2013-help.md).

Return to top

## Enabling and configuring the detection of open proxy servers

Sender reputation evaluates several sender characteristics to calculate an SRL. Among the characteristics that sender reputation evaluates are the results of a test for open proxy servers. Frequently, spammers route messages through open proxy servers on the Internet. By routing spam through open proxy servers, spammers can send messages that appear to originate from a different server than their own.

When sender reputation calculates an SRL, sender reputation tries to connect to the sender's originating IP address by using a variety of common proxy protocols, such as SOCKS4, SOCKS5, HTTP, Telnet, Cisco, and Wingate. Sender reputation formats a protocol-specific request in an attempt to connect back to the Edge Transport server from the open proxy server by using an SMTP request. If an SMTP request is received from the proxy server, sender reputation verifies that the proxy server is an open proxy server and adjusts the SRL rating according to this result. By default, detection of open proxy servers is enabled on sender reputation.

For more information about how to enable and configure detection of open proxy servers, see [Manage sender reputation](manage-sender-reputation-exchange-2013-help.md).

Return to top

## Setting the SRL block threshold

The SRL is a number from 0 through 9 that predicts the probability that a specific sender is a spammer or otherwise malicious user. You must set a threshold for sender blocking by SRL. This SRL block threshold defines the SRL value that must be exceeded for sender reputation to block a sender. By default, the SRL is set at 7. You should monitor the effectiveness of the agent at the default level. You may find that you can adjust the value to meet the needs of your organization. If you set other anti-spam agents aggressively, you may be able to set a higher SRL threshold for sender reputation than you would if the other anti-spam agents weren't set aggressively. For more information about how to adjust anti-spam configurations so that they work together to reduce spam, see [Anti-spam protection](anti-spam-protection-exchange-2013-help.md).

On an Edge Transport server, if the SRL block threshold is exceeded for a particular sender, sender reputation adds the sender to the IP Block list on the Connection Filter agent. Sometimes, spammers send batches of spam from a single sender. In this scenario, if sender reputation calculates an SRL that exceeds the SRL block threshold, the sender is added to the Sender Block List for a configurable duration of time. The default duration is 24 hours. After 24 hours, the sender is removed from the Sender Block List and can send messages again.

When a sender is added to the IP Block list, sender reputation deletes the profile for the sender. Sender reputation deletes the profile because the blocked sender's existing profile indicates that the sender's SRL exceeds the SRL block threshold. This would cause the blocked sender to be added to the IP Block list again as soon as the duration for sender blocking ends.

For more information, see [Manage sender reputation](manage-sender-reputation-exchange-2013-help.md).

Return to top

