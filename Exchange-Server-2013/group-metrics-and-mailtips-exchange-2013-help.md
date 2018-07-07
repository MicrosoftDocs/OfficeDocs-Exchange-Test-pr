---
title: 'Group metrics and MailTips: Exchange 2013 Help'
TOCTitle: Group metrics and MailTips
ms:assetid: 74a55072-4ba9-45bb-a18f-41afbf3de30b
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ674302(v=EXCHG.150)
ms:contentKeyID: 49319920
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Group metrics and MailTips

 

_**Applies to:** Exchange Server 2013_


Group metrics is the collection of the following data about distribution groups and dynamic distribution groups in your organization:

  - Number of members

  - Number of members who are external to your organization

Group metrics data is used to support MailTips in Microsoft Exchange Server 2013. MailTips are informative messages that are displayed to senders while they're composing messages. For more information about MailTips,including a full list of MailTips available in Exchange 2013, see [MailTips](mailtips-exchange-2013-help.md).

Group metrics data is used by the following MailTips:

  - **Large Audience**   This MailTip is displayed when a sender adds a distribution group whose membership count is considered a large audience as configured in your organization. By default, any message addressed to more than 25 recipients is considered a large audience.

  - **External Recipients**   This MailTip is displayed when a sender adds a distribution group that has members who are external to your organization.

MailTips are evaluated every time a sender adds a recipient to a message. To provide this information, Exchange calculates group metrics data as a background process that can be scheduled to run outside of your organization’s regular business hours. When evaluating recipients for MailTips, Exchange reads group metrics data.

## Group Metrics generation

In Exchange 2013, group metrics data is stored in the **msExchGroupMemberCount** and **msExchGroupExternalMemberCount** attributes on the group object in Active Directory. The following files in the %ExchangeInstallPath%GroupMetrics folder are also associated with group metrics:

  - **Cookie\_*\<nnnnnnnn\>*.dsc**   This text file contains information about the Mailbox server that is configured to generate group metrics data, and the last successful group metrics generation time. This allows group metrics to generate data for groups that were changed since the last group metrics generation.

  - **ChangedGroups.txt**   This file contains the list of groups that were updated the last time group metrics data was generated.

Group metrics generation is handled by an arbitration mailbox, which is also called an organization mailbox. When the *GMGen* parameter on an arbitration mailbox is set to `$true`, the arbitration mailbox is responsible for generating the group metrics data.

The Mailbox server generates full group metrics data for all distribution groups and dynamic distribution groups the first time the Group Metrics mailbox assistant runs, and incremental updates for any groups that were modified since the last full generation. By default, group metrics data is generated daily at a random time when the Exchange server workload is light. If the workload is constantly high, group metrics generation may be skipped.

To configure group metrics generation, see [Configure group metrics](configure-group-metrics-exchange-2013-help.md).

