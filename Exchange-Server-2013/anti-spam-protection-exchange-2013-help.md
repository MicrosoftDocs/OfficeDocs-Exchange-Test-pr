---
title: 'Anti-spam protection: Exchange 2013 Help'
TOCTitle: Anti-spam protection
ms:assetid: 6af88a08-687d-40b1-8b22-80704184403d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ218660(v=EXCHG.150)
ms:contentKeyID: 48385197
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Anti-spam protection

 

_**Applies to:** Exchange Server 2013_


*Spammers*, or malicious senders, use a variety of techniques to send unwanted email into your organization. No single tool or process can eliminate all spam. However, Microsoft Exchange Server 2013 provides a layered, multipronged, and multifaceted approach to reducing these unwanted messages. Exchange uses transport agents to provide anti-spam protection, and the built-in agents that are available in Exchange 2013 are relatively unchanged from Microsoft Exchange Server 2010.

For more anti-spam features and easier management, you can elect to purchase Microsoft Exchange Online Protection (EOP). For a comparison of EOP and Exchange 2013 features, see [Benefits of anti-spam features in Exchange Online Protection over Exchange Server 2013](benefits-of-anti-spam-features-in-exchange-online-protection-over-exchange-server-2013-exchange-2013-help.md). To learn more about Office 365 anti-spam protection, see [Office 365 Email Anti-Spam Protection](https://support.office.com/en-us/article/office-365-email-anti-spam-protection-6a601501-a6a8-4559-b2e7-56b59c96a586?ui=en-us%26rs=en-us%26ad=us).

For information about the built-in anti-malware capabilities in Exchange 2013, see [Anti-malware protection](anti-malware-protection-exchange-2013-help.md).

**Contents**

Anti-spam agents on Mailbox servers

Anti-spam agents on Edge Transport servers

Anti-spam stamps

Strategy for anti-spam approach

## Anti-spam agents on Mailbox servers

Typically, you would enable the anti-spam agents on a mailbox server if your organization doesn't have an Edge Transport server, or doesn't do any prior anti-spam filtering before accepting incoming messages. For more information, see [Enable anti-spam functionality on Mailbox servers](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

Like all transport agents, each anti-spam agent is assigned a priority value. A lower value indicates a higher priority, so typically, an anti-spam agent with priority 1 will act on a message before an anti-spam agent with priority 9. However, the SMTP event where the anti-spam agent is registered is also very important in determining the order that anti-spam agents act on messages. A low priority anti-spam agent that's registered on an SMTP event early in the transport pipeline will act on a message before a high priority anti-spam agent that's registered on an SMTP event later in the transport pipeline.

Based on the default priority value of the anti-spam agent, and the SMTP event in the transport pipeline where the anti-spam agent is registered, the following list describes the agents and the default order in which they are applied to messages on a Mailbox server:

1.  **Sender Filter agent**   Sender filtering compares the sender on the MAIL FROM: SMTP command to an administrator-defined list of senders or sender domains who are prohibited from sending messages to the organization to determine what action, if any, to take on an inbound message. For more information, see [Sender filtering](sender-filtering-exchange-2013-help.md).

2.  **Sender ID agent**   Sender ID relies on the IP address of the sending server and the Purported Responsible Address (PRA) of the sender to determine whether the sender is spoofed or not. For more information, see [Sender ID](sender-id-exchange-2013-help.md).

3.  **Content Filter agent**   Content filtering assesses the contents of a message. For more information, see [Content filtering](content-filtering-exchange-2013-help.md).
    
    Spam quarantine is a feature of the Content Filter agent that reduces the risk of losing legitimate messages that are incorrectly classified as spam. Spam quarantine provides a temporary storage location for messages that are identified as spam and that shouldn't be delivered to a user mailbox inside the organization. For more information, see [Spam quarantine](spam-quarantine-exchange-2013-help.md).
    
    Content filtering also acts on the safelist aggregation feature. Safelist aggregation collects data from the anti-spam safe lists that Microsoft Outlook and Outlook Web App users configure and makes this data available to the Content Filter agent. For more information, see [Safelist Aggregation](safelist-aggregation-exchange-2013-help.md).

4.  **Protocol Analysis agent**   The Protocol Analysis agent is the underlying agent that implements the sender reputation functionality. Sender reputation relies on persisted data about the IP address of the sending server to determine what action, if any, to take on an inbound message. A sender reputation level (SRL) is calculated from several sender characteristics that are derived from message analysis and external tests. For more information, see [Sender reputation and the Protocol Analysis agent](sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md).

Return to top

## Anti-spam agents on Edge Transport servers

If your organization has an Edge Transport server installed in the perimeter network, all of the anti-spam agents that are available on a Mailbox server are installed and enabled by default on the Edge Transport server. However, the following anti-spam agents are only available on an Edge Transport server:

  - **Connection Filtering agent**   Connection filtering inspects the IP address of the remote server that's trying to send messages to determine what action, if any, to take on an inbound message. Connection filtering uses an IP Block list, IP Allow list, IP Block List provider services and IP Allow List provider services to determine whether the connection IP should be blocked or allowed. For more information, see [Connection Filtering on Edge Transport Servers](connection-filtering-on-edge-transport-servers-exchange-2013-help.md).

  - **Recipient Filter agent**   Recipient filtering compares the message recipients on the RCPT TO: SMTP command to an administrator-defined Recipient Block list. If a match is found, the message isn't permitted to enter the organization. The recipient filter also compares recipients on inbound messages to the local recipient directory to determine whether the message is addressed to valid recipients. When a message isn't addressed to valid recipients, the message is rejected. For more information, see [Recipient filtering on Edge Transport servers](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md).
    

    > [!NOTE]
    > Although the Recipient Filter agent is available on Mailbox servers, you shouldn't configure it. When recipient filtering on a Mailbox server detects one invalid or blocked recipient in a message that contains other valid recipients, the message is rejected. If you install the anti-spam agents on a Mailbox server, the Recipient Filter agent is enabled by default. However, it isn't configured to block any recipients.



  - **Attachment Filtering agent**   Attachment filtering blocks messages based on attachment file name, file name extension, or file MIME content type. You can configure attachment filtering to block a message and its attachment, to strip the attachment and allow the message to pass through, or to silently delete the message and its attachment. For more information, see [Attachment filtering on Edge Transport servers](attachment-filtering-on-edge-transport-servers-exchange-2013-help.md).

Based on the default priority value of the anti-spam agent, and the SMTP event in the transport pipeline where the anti-spam agent is registered, this is the default order in which the anti-spam agents are applied on an Edge Transport server:

1.  Connection Filtering agent

2.  Sender Filter agent

3.  Recipient Filter agent

4.  Sender ID agent

5.  Content Filter agent

6.  Protocol Analysis agent for sender reputation

7.  Attachment Filtering agent

Return to top

## Anti-spam stamps

Anti-spam stamps help you diagnose spam-related problems by applying diagnostic metadata, or stamps, such as sender-specific information, puzzle validation results, and content filtering results, to messages as they pass through the anti-spam features that filter inbound messages from the Internet. For more information, see [Anti-spam stamps](anti-spam-stamps-exchange-2013-help.md).

Return to top

## Strategy for anti-spam approach

Your strategy for how to configure the anti-spam features and establish the aggressiveness of your anti-spam agent settings requires that you plan and calculate carefully. If you set all anti-spam filters to their most aggressive levels and configure all anti-spam features to reject all suspicious messages, you're more likely to reject messages that aren't spam. On the other hand, if you don't set the anti-spam filters at a sufficiently aggressive level and don't set the spam confidence level (SCL) threshold low enough, you probably won't see a reduction in the spam that enters your organization.

It's a best practice to reject a message when Exchange detects a bad message through the Connection Filtering agent, Recipient Filter agent, or Sender Filter agent. This approach is better than quarantining such messages or assigning metadata, such as anti-spam stamps, to such messages. The Connection Filtering agent and Recipient Filter agent automatically block messages that are identified by the respective filters. The Sender Filter agent is configurable.

This best practice is recommended because the SCL that underlies connection filtering, recipient filtering, or sender filtering is relatively high. For example, with sender filtering, where the administrator has configured specific senders to block, there's no reason to assign the sender filtering data to such messages and to continue to process them. In most organizations, blocked messages should be rejected. (If you didn't want the messages rejected, you wouldn't have put them on the Blocked Senders List.)

The same logic applies to real-time block list services and recipient filtering, although the underlying confidence isn't as high as the IP Block list. You should be aware that the further along the mail flow path a message travels, the greater the probability of false positives, because the anti-spam features are evaluating more variables. Therefore, you may find that if you configure the first several anti-spam features in the anti-spam chain more aggressively, you can reduce the bulk of your spam. As a result, you'll save processing, bandwidth, and disk resources so that you can process more ambiguous messages.

Ultimately, you must plan to monitor the overall effectiveness of the anti-spam features. If you monitor carefully, you can continue to adjust the anti-spam features to work well together for your environment. With this approach, you should plan on a fairly non-aggressive configuration of the anti-spam features when you start. This approach lets you minimize the number of false positives. As you monitor and adjust the anti-spam features, you can become more aggressive about the type of spam and spam attacks that your organization experiences.

Return to top

## See Also


[Office 365 Email Anti-Spam Protection](https://support.office.com/en-us/article/office-365-email-anti-spam-protection-6a601501-a6a8-4559-b2e7-56b59c96a586?ui=en-us%26rs=en-us%26ad=us)

