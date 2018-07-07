---
title: 'Spam Confidence Level Threshold: Exchange 2013 Help'
TOCTitle: Spam Confidence Level Threshold
ms:assetid: 0009b4af-be6d-41d2-98bc-b5487272c74a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa995744(v=EXCHG.150)
ms:contentKeyID: 49248673
ms.date: 11/17/2016
mtps_version: v=EXCHG.150
---

# Spam Confidence Level Threshold

 

_**Applies to:** Exchange Server 2013_



> [!NOTE]
> On November 1, 2016, Microsoft stopped producing spam definition updates for the SmartScreen filters in Exchange and Outlook. The existing SmartScreen spam definitions will be left in place, but their effectiveness will likely degrade over time. For more information, see <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Deprecating support for SmartScreen in Outlook and Exchange</A>.



In Microsoft Exchange Server 2013, you can define specific actions according to spam confidence level (SCL) thresholds. For example, you can define different thresholds for rejecting, deleting, or quarantining messages on an Exchange server that's running the Content Filter agent.

The combination of this SCL threshold configuration in the Content Filter agent and the SCL Junk Email folder configuration on the user's mailbox helps you implement a more comprehensive and precise anti-spam strategy. This more precise and detailed SCL threshold adjustment functionality in Exchange 2013 can help you reduce the overall cost of deploying and maintaining an anti-spam solution across your Exchange organization.

The Content Filter agent assigns an SCL rating to messages late in the anti-spam cycle, after other anti-spam agents have processed any inbound messages. Many of the other anti-spam agents that process inbound messages before they're processed by the Content Filter agent are deterministic in how they act on a message. For example, on an Edge Transport server the Connection Filter agent rejects any message sent from an IP address on a real-time block list. The Sender Filter agent and Recipient Filter agent process messages in a similarly deterministic manner.

In Exchange 2013, these deterministic anti-spam agents process messages first and therefore greatly reduce the number of messages that must be processed by the Content Filter agent. For more information about the order in which anti-spam agents process messages, see [Anti-spam protection](anti-spam-protection-exchange-2013-help.md).

Because content filtering isn't an exact, deterministic process, the ability to adjust the action that the Content Filter agent performs on different SCL values is important. By carefully adjusting the SCL threshold configuration, you can minimize the following:

  - Size of the spam quarantine storage

  - Number of legitimate email messages mistakenly quarantined

  - Number of legitimate email messages that reach the Microsoft Outlook user's Junk Email folder

  - Number of offensive spam email messages that reach the Outlook user's Inbox or Junk Email folder

  - Number of spam email messages that reach the Outlook user's Inbox

## SCL threshold actions

By adjusting SCL threshold actions, you can escalate the content filtering action taken on messages that have a greater risk of being spam. To understand this functionality, it's helpful to understand the different SCL threshold actions and how they're implemented:

  - **SCL delete threshold**   When the SCL value for a specific message is equal to or higher than the SCL delete threshold, the Content Filter agent deletes the message. There's no protocol-level communication that tells the sending system or sender that the message was deleted. If the SCL value for a message is lower than the SCL delete threshold value, the Content Filter agent doesn't delete the message. Instead, the Content Filter agent compares the SCL value to the SCL reject threshold.

  - **SCL reject threshold**   When the SCL value for a specific message is equal to or higher than the SCL reject threshold, the Content Filter agent deletes the message and sends a rejection response to the sending system. You can customize the rejection response. In some cases, a non-delivery report (NDR) is sent to the original sender of the message. If the SCL value for a message is lower than the SCL delete and SCL reject threshold values, the Content Filter agent doesn't delete or reject the message. Instead, the Content Filter agent compares the SCL value to the SCL quarantine threshold.

  - **SCL quarantine threshold**   When the SCL value for a specific message is equal to or higher than the SCL quarantine threshold, the Content Filter agent sends the message to a quarantine mailbox. Email administrators must periodically review the quarantine mailbox. If the SCL value for a message is lower than the SCL delete, reject, and quarantine threshold values, the Content Filter agent doesn't delete, reject, or quarantine the message. Instead, the Content Filter agent sends the message to the appropriate Mailbox server, where the per-recipient SCL Junk Email folder threshold value of the message is evaluated.

  - **SCL Junk Email folder threshold**   If the SCL value for a specific message exceeds the SCL Junk Email folder threshold, the message is delivered to the user's Junk Email folder. If the SCL value for a message is lower than the SCL delete, reject, quarantine, and Junk Email folder threshold values, the message is delivered to the user's Inbox.

The Content Filter agent and the Junk Email folder process the SCL threshold value differently. The Content Filter agent takes action on the SCL threshold value that you configure. The Junk Email folder takes action on the SCL threshold value that you configure plus 1. For example, if you configure the Delete action to an SCL of 8 on the Content Filter agent, all messages with an SCL of 8 or greater are deleted. However, if you configure the Junk Email folder with an SCL threshold of 4, all messages with an SCL of 5 or greater are moved to the Junk Email folder.

For example, if you set the SCL delete threshold to 8, the SCL reject threshold to 7, the SCL quarantine threshold to 6, and the SCL Junk Email folder threshold to 4, all messages with an SCL of 5 or lower are delivered to the user's mailbox. Messages with an SCL value of 5 are put in the user's Junk Email folder. Messages with an SCL value of 4 or lower are put in the user's Inbox.

You can configure the SCL delete, reject, quarantine, and Junk Email folder settings in the following locations:

  - **On the Content Filter agent configuration (per-transport server SCL configuration)**   You use the **Set-ContentFilterConfig** cmdlet to enable or disable and set the SCL delete, reject, and quarantine thresholds on the Exchange server where you're running the Content Filter agent. Over time, as you analyze the spam functionality and metrics provided by the anti-spam logging and reporting features, you can make additional adjustments to these SCL threshold configurations as needed.
    
    The SCL parameters that are available on the **Set-ContentFilterConfig** cmdlet are described in the following table.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Parameter</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLDeleteEnabled</em></p></td>
    <td><p>This parameter enables or disables deleting a message without a non-delivery report (NDR) when the SCL value of the message is greater than or equal to the value specified by the <em>SCLDeleteThreshold</em> parameter. Valid input for this parameter is <code>$true</code> or <code>$false</code>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLDeleteThreshold</em></p></td>
    <td><p>Valid input for this parameter is an integer from 0 through 9 inclusive. The value of this parameter should be greater than the other SCL threshold parameters. This parameter is only meaningful if the value of the <em>SCLDeleteEnabled</em> parameter is <code>$true</code>.</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLRejectEnabled</em></p></td>
    <td><p>This parameter enables or disables rejecting a message with an NDR when the SCL value of the message is greater than or equal to the value specified by the <em>SCLRejectThreshold</em> parameter. Valid input for this parameter is <code>$true</code> or <code>$false</code>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLRejectThreshold</em></p></td>
    <td><p>Valid input for this parameter is an integer from 0 through 9 inclusive. The value of this parameter should be less than the <em>SCLDeleteThreshold</em> parameter, but greater than the other SCL threshold parameters This parameter is only meaningful if the value of the <em>SCLRejectEnabled</em> parameter is <code>$true</code>.</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLQuarantineEnabled</em></p></td>
    <td><p>This parameter enables or disables sending a message to the spam quarantine mailbox when the SCL value of the message is greater than or equal to the value specified by the <em>SCLQuarantineThreshold</em> parameter. Valid input for this parameter is <code>$true</code> or <code>$false</code>.</p>
    <p>For more information about the spam quarantine mailbox, see <a href="spam-quarantine-exchange-2013-help.md">Spam quarantine</a>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLQuarantineThreshold</em></p></td>
    <td><p>Valid input for this parameter is an integer from 0 through 9 inclusive. The value of this parameter should be less than the <em>SCLRejectThreshold</em> parameter, but greater than the <em>SCLJunkThreshold</em> parameter on the <strong>Set-OrganizationConfig</strong> or <strong>Set-Mailbox</strong> cmdlets. This parameter is only meaningful if the value of the <em>SCLQuarantineThreshold</em> parameter is <code>$true</code>.</p></td>
    </tr>
    </tbody>
    </table>


  - **On the organization configuration settings (organization-wide SCL configuration)**   You use the **Set-OrganizationConfig** cmdlet to set the SCL Junk Email folder threshold for all mailboxes in the organization.
    
    The SCL parameter that's available on the **Set-OrganizationConfig** cmdlet is described in the following table. For an example of using SCLJunkThreshold, see [Configure Anti-Spam Settings on Mailboxes](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Parameter</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkThreshold</em></p></td>
    <td><p>This parameter specifies the SCL value that a message must exceed for the message to be moved into the Junk Email folder of the recipient's mailbox. Valid input for this parameter is an integer from 0 through 9 inclusive. The value of this parameter should be less than the other SCL threshold parameters. For example, if you specify the value 4, then messages with an SCL value of 5 or higher are moved into the user's Junk Email folder.</p></td>
    </tr>
    </tbody>
    </table>


  - **On user mailboxes (per-recipient SCL configuration)**   You use the **Set-Mailbox** cmdlet to enable or disable and set per-recipient SCL delete, reject, quarantine, and Junk Email folder thresholds on individual mailboxes. You can only use the **Set-Mailbox** cmdlet to enable or disable the SCL Junk Email folder threshold on individual mailboxes. The per-recipient SCL delete, reject, and quarantine thresholds are stored in Active Directory and are replicated to subscribed Edge Transport servers by the Microsoft Exchange EdgeSync service. The per-recipient SCL threshold configurations are used by the Content Filter agent even if you've set per-transport server SCL configurations. Therefore, if you've set per-recipient SCL thresholds, the Content Filter agent uses the per-recipient SCL thresholds for specific users instead of the SCL configuration on the Content Filter agent. For examples, see [Configure Anti-Spam Settings on Mailboxes](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).
    

    > [!NOTE]
    > Per-recipient SCL thresholds are not enforced on mail received through distribution groups.

    
    The same SCL parameters are available on the **Set-Mailbox** cmdlet that are available on the **Set-ContentFilterConfig** and **Set-OrganizationConfig** cmdlets:
    
      - *SCLDeleteEnabled*
    
      - *SCLDeleteThreshold*
    
      - *SCLRejectEnabled*
    
      - *SCLRejectThreshold*
    
      - *SCLQuarantineEnabled*
    
      - *SCLQuarantineThreshold*
    
      - *SCLJunkThreshold*
    
    However, all the SCL parameters on the **Set-Mailbox** cmdlet also accept the value `$null`. If an SCL setting on a mailbox is blank (`$null`), the corresponding Content Filter agent setting or organization configuration setting is applied to the mailbox. If an SCL setting on a mailbox has the value of `$true` or `$false`, the setting on the mailbox overrides the corresponding organization-wide setting on the Content Filter agent or the organization configuration.
    
    The SCL parameter that's only available on the **Set-Mailbox** cmdlet is described in the following table.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Parameter</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkEnabled</em></p></td>
    <td><p>This parameter enables or disables delivering a message to the user's Junk Email folder when the SCL value of the message is greater than the value specified by the <em>SCLQuarantineThreshold</em> parameter. Valid input for this parameter is <code>$true</code>, <code>$false</code>, or <code>$null</code>.</p>
    <p>Note that junk email filtering is enabled by default for all user mailboxes in the organization. By default, the <em>Enabled</em> parameter is set to the value <code>$true</code> on the <strong>Set-MailboxJunkEmailConfiguration</strong> cmdlet for all user mailboxes.</p></td>
    </tr>
    </tbody>
    </table>
    
    For more information about configuring the SCL thresholds on a mailbox, see [Configure Anti-Spam Settings on Mailboxes](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).

## Monitoring the SCL thresholds

You can use several built-in scripts located in the `%ExchangeInstallPath%Scripts` folder, such as **get-AntispamSCLHistogram.ps1**, for gathering filtering result data. If the data indicates that you need to make immediate adjustments, reconfigure the SCL thresholds. Otherwise, collect data and analyze the spam reporting to determine whether adjustments are required.

