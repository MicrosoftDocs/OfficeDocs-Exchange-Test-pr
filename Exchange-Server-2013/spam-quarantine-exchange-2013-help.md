---
title: 'Spam quarantine: Exchange 2013 Help'
TOCTitle: Spam quarantine
ms:assetid: 4535496f-de6a-43df-8e53-c9a97f65cccc
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997692(v=EXCHG.150)
ms:contentKeyID: 49248678
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Spam quarantine

 

_**Applies to:** Exchange Server 2013_


Many organizations are bound by legal or regulatory requirements to preserve or deliver all legitimate email messages. In Microsoft Exchange Server 2013, spam quarantine is a feature of the Content Filter agent that reduces the risk of losing legitimate messages. Spam quarantine provides a temporary storage location for messages identified as spam that shouldn't be delivered to a user mailbox inside the organization.

Messages identified by the Content Filter agent as spam are wrapped in a non-delivery report (NDR) and delivered to a spam quarantine mailbox inside the organization. You can manage messages delivered to the spam quarantine mailbox and take appropriate actions. For example, you can delete messages or let messages flagged as false positives in anti-spam filtering be routed to their intended recipients. In addition, you can configure the spam quarantine mailbox to automatically delete messages after a designated time period.

**Contents**

Spam confidence level

Spam quarantine

## Spam confidence level

When an external user sends email messages to a server running Exchange that runs the anti-spam features, the anti-spam features cumulatively evaluate characteristics of the messages and act as follows:

  - Those messages suspected to be spam are filtered out.

  - A rating is assigned to messages based on the probability that a message is spam. This rating is stored with the message as a message property called the spam confidence level (SCL) rating.

Spam quarantine uses the SCL rating to determine whether mail has a high probability of being spam. The SCL rating is a numeric value from 0 through 9, where 0 is considered less likely to be spam, and 9 is considered most likely to be spam.

You can configure mail that has a certain SCL rating to be deleted, rejected, or quarantined. The rating that triggers any of these actions is referred to as the *SCL quarantine threshold*. Within content filtering, you can configure the Content Filter agent to base its actions on the SCL quarantine threshold. For example, you can set the following conditions:

  - SCL delete threshold is set to 8.

  - SCL reject threshold is set to 7.

  - SCL quarantine threshold is set to 6.

  - SCL Junk Email folder threshold is set to 5.

Based on the preceding SCL thresholds, all email with an SCL of 6 will be delivered to the spam quarantine mailbox.

For more information, see [Manage content filtering](manage-content-filtering-exchange-2013-help.md).

Return to top

## Spam quarantine

When messages are received by the Exchange server that's running all default anti-spam agents, the content filter is applied as follows:

  - If the SCL rating is greater than or equal to the SCL quarantine threshold but less than either the SCL delete threshold or SCL reject threshold, the message goes to the spam quarantine mailbox.

  - If the SCL rating is lower than the spam quarantine threshold, it's delivered to the recipient's Inbox.

The message administrator uses Microsoft Outlook to monitor the spam quarantine mailbox for false positives. If a false positive is found, the administrator can send the message to the recipient's mailbox.

The message administrator can review the anti-spam stamps if either of the following conditions is true:

  - Too many false positives are filtered into the spam quarantine mailbox.

  - Not enough spam is being rejected or deleted.

For more information, see [Anti-spam stamps](anti-spam-stamps-exchange-2013-help.md).

You can then adjust the SCL settings to more accurately filter the spam coming into the organization. For more information, see [Spam Confidence Level Threshold](spam-confidence-level-threshold-exchange-2013-help.md).

To use spam quarantine, you need to follow these steps:

1.  Verify content filtering is enabled.

2.  Create a dedicated mailbox for spam quarantine.

3.  Specify the spam quarantine mailbox.

4.  Configure the SCL quarantine threshold.

5.  Manage the spam quarantine mailbox.

6.  Adjust the SCL quarantine threshold as needed.

For detailed instructions, see [Configure a spam quarantine mailbox](configure-a-spam-quarantine-mailbox-exchange-2013-help.md).

Return to top

