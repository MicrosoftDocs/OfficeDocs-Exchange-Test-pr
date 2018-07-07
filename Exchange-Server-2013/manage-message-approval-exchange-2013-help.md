---
title: 'Manage message approval: Exchange 2013 Help'
TOCTitle: Manage message approval
ms:assetid: 43a89f71-8002-4cb0-b3c8-1c2b2597f227
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd297936(v=EXCHG.150)
ms:contentKeyID: 49300488
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Manage message approval

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Sometimes it makes sense to have a second set of eyes on a message before the message is delivered. As an Exchange administrator, you can set this up. This process is called *moderation*, and the approver is called the *moderator*. Depending on which messages need approval, you can use one of two approaches:

  - Change the distribution group properties

  - Create a mail flow rule

This article explains:

  - How to decide which approval approach to use

  - How the approval process works

To learn how to implement common scenarios, see [Common message approval scenarios](common-message-approval-scenarios-exchange-2013-help.md).

## How to decide which approval approach to use

Here’s a comparison of the two approaches to message approval.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>What do you want to do?</th>
<th>Approach</th>
<th>First step</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Create a moderated distribution group where all messages to the group must be approved.</p></td>
<td><p>Set up message approval for the distribution group.</p></td>
<td><p>Go to the Exchange admin center (EAC) &gt; <strong>Recipients</strong> &gt; <strong>Groups</strong>, edit the distribution group, and then select <strong>Message approval</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Require approval for messages that match specific criteria or that are sent to a specific person.</p></td>
<td><p>Create a transport rule using the <strong>Forward the message for approval</strong> action.</p>
<p>You can specify message criteria, including text patterns, senders, and recipients. Your criteria can also contain exceptions.</p></td>
<td><p>Go to the EAC &gt; <strong>Mail flow</strong> &gt; <strong>Rules</strong>.</p></td>
</tr>
</tbody>
</table>


Return to top

## How the approval process works

When someone sends a message to a person or group that requires approval, if they’re using Outlook Web Access, they’re notified that their message might be delayed.

![Message showing message approval notification](images/Dd297936.80e2e5f1-0a1e-4c37-9076-794581155405(EXCHG.150).png "Message showing message approval notification")

The moderator receives an email with a request to approve or reject the message. The text of the message includes buttons to approve or reject the message, and the attachment includes the original message to review.

![Approval request message, including attachment](images/Dd297936.bf517f5a-b10e-40df-a48a-403b395b5962(EXCHG.150).png "Approval request message, including attachment")

The moderator can take one of three actions:

![Workflow showing options for approving a message](images/Dd297936.dc7a6ca9-c67d-487a-8713-4d628e07f4b3(EXCHG.150).png "Workflow showing options for approving a message")

1.  If approved, the message goes to the original intended recipients. The original sender isn’t notified.

2.  If rejected, a rejection message is sent to the sender. The moderator can add an explanation:
    
    ![Rejection notice, with comments from moderator](images/Dd297936.a663d36a-c67d-4155-b8f6-4b5dc8e105d9(EXCHG.150).png "Rejection notice, with comments from moderator")  

3.  If the approver either deletes or ignores the approval message, an expiration message is sent to the sender. This happens after two days in Exchange Online, and after five days in Exchange Server 2013. (In Exchange Server 2013, you can change this time period).

The message that’s waiting for approval gets temporarily stored in a system mailbox called the *arbitration mailbox*. Until the moderator decides to approve or reject the message, deletes the approval message, or lets the approval message expire, the original message is kept in the arbitration mailbox.

Return to top

## Questions and answers

**What’s the difference between the approver and owner of a distribution group?**

The owner of a distribution group is responsible for managing the distribution group membership, but he or she might not be able to moderate messages sent to it. For example, a person in IT might be the owner of a distribution group called All Employees, but only the Human Resources manager might be set up as the moderator.

**What happens when the moderator or approver sends a message to the distribution group?**

The message goes directly to the group, bypassing the approval process.

**What happens when only a subset of recipients needs approval?**

You can send a message to a group of recipients where only a subset of the recipients requires approval. Consider a message that's sent to 12 recipients, one of which is a moderated distribution group. The message is automatically split into two copies. One message is delivered immediately to the 11 recipients that don’t require approval, and the second message is submitted to the approval process for the moderated distribution group. If a message is intended for more than one moderated recipient, a separate copy of the message is automatically created for each moderated recipient and each copy goes through the appropriate approval process.

**What if my distribution group contains moderated recipients that require approval?**

A distribution group can include moderated recipients that also require approval. In this case, after the message to the distribution group is approved, a separate approval process occurs for each moderated recipient that's a member of the distribution group. However, you can also enable the automatic approval of the distribution group members after the message to the moderated distribution group is approved. To do this, you use the *BypassNestedModerationEnabled* parameter on the [Set-DistributionGroup](https://technet.microsoft.com/en-us/library/bb124955\(v=exchg.150\)) cmdlet.

**Is this process different if we have our own Exchange servers?**

By default, one arbitration mailbox is used for each Exchange organization. If you have your own Exchange servers and need more arbitration mailboxes for load balancing, follow the instructions for adding arbitration mailboxes in [Manage and troubleshoot message approval](manage-and-troubleshoot-message-approval-exchange-2013-help.md). Arbitration mailboxes are system mailboxes and don’t require an Exchange license.


> [!NOTE]
> <STRONG>If you have Exchange 2007:</STRONG> Microsoft Exchange Server 2007 doesn't support moderated recipients. If a message sent to a moderated distribution group is expanded on an Exchange 2007 Hub Transport server, the message bypasses moderation and is delivered to all members of the distribution group. If you have Exchange 2007 Hub Transport servers in your Exchange organization, you be sure to designate an Exchange Server 2013 Mailbox server as the expansion server for moderated distribution groups. This ensures that all messages sent to the distribution group are moderated.



Return to top

## Need more info?

[Manage mail flow rules](manage-mail-flow-rules-exchange-2013-help.md)

[Exchange Management Shell quick reference for Exchange 2013](exchange-management-shell-quick-reference-for-exchange-2013-exchange-2013-help.md)

[Exchange Online PowerShell](https://technet.microsoft.com/en-us/library/jj200677\(v=exchg.150\))

