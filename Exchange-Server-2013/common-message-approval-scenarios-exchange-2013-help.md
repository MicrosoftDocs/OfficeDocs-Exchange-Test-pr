---
title: 'Common message approval scenarios: Exchange 2013 Help'
TOCTitle: Common message approval scenarios
ms:assetid: 5c13a07e-c21d-4502-a9f9-fb801197e1dd
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd298007(v=EXCHG.150)
ms:contentKeyID: 49300524
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Common message approval scenarios

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Your organization may require certain types of messages be approved in order to meet legal or compliance requirements, or to implement a specific business workflow. Here are some examples of common scenarios that you can set up by using Exchange:

  - Example 1: Avoid mail storms to a large distribution group

  - Example 2: Forward messages to a sender’s manager for approval

  - Example 3: Set up a message approval chain

  - Example 4: Forward messages that match one of several criteria

  - Example 5: Forward a message that contains sensitive information

## Example 1: Avoid mail storms to a large distribution group

To control messages to a large distribution group, you can require that a moderator approve messages that are sent to that group. If there are no criteria for which messages require approval, the simplest way to set this up is to configure the group to require message approval.

In this example, all messages to the All Employees group must be approved, except if the senders are members of the distribution group named Legal Team.

![Message approval settings for a distribution group](images/Dd298007.77721509-93f9-4a90-8d77-986db2b0acf4(EXCHG.150).png "Message approval settings for a distribution group")

To require that messages to a specific distribution group be approved, in the Exchange admin center (EAC), go to **Recipients** \> **Groups**, edit the distribution group, and then select **Message approval**.

## Example 2: Forward messages to a sender’s manager for approval

Here are some common types of messages for which you might want to require manager approval:

  - Messages sent from a user to certain distribution groups or recipients

  - Messages sent to external users or partners

  - Message sent between two groups

  - Messages sent with specific content, such as the name of a specific customer

  - Messages sent by a trainee

To require that a message be sent for approval, first, create a rule using the **Send messages to a moderator** template, and select that the messages should go to the sender’s manager, as shown in the following screenshots.

![Use a template to create the new rule](images/Dd298007.051a5653-1a09-4db4-908f-48b56cc8d13f(EXCHG.150).png "Use a template to create the new rule")

Then, define which messages need approval.

Here’s an example where all messages sent out by a trainee, Garth Fort, to recipients outside the organization requires a manager’s approval.

![Rule that forwards messages to the user's manager](images/Dd298007.7f94c22e-b5ba-45a3-9ccd-31996b6c863a(EXCHG.150).png "Rule that forwards messages to the user's manager")

To get started, go to EAC \> **Mail flow** \> **Rules**, and create a new rule using the **Send messages to a moderator** template.


> [!IMPORTANT]
> Some conditions and actions, including forwarding to the sender’s manager, are hidden by default in the <STRONG>New rule</STRONG> page. To see all the conditions and actions, select <STRONG>More options</STRONG>.



## Example 3: Set up a message approval chain

You can require multiple levels of approval for messages. For example, you can require that messages to a specific customer be approved first by a customer relationship manager and then by a compliance officer, or you can require that expense reports be approved by two levels of managers.

To create this type of multiple-level approval, create one transport rule for each level of approval. Each rule detects the same patterns in the messages, as follows:

  - The first rule forwards the message to the first approver. When the first approver accepts the message, the message automatically goes to the approver in the second rule.

  - If all approvers in the chain select **Approve** when they receive the approval request, when the last approval in the chain is complete, the original message is sent to the intended recipients.

  - If anyone in the approval chain selects **Reject** when they receive the approval request, the sender receives a rejection message.

  - If any of the approval requests aren’t approved within the expiration time (2 days for Exchange Online, 5 days for Exchange Server 2013), the sender receives an expiration message.

The following example assumes that you have a customer called Blue Yonder Airlines, and you want both the customer relationship manager and the compliance officer to approve all messages that go to this customer. You create two rules, one for each approver. The first rule goes to the first-level approver. The second rule goes to the second-level approver.

![Two rules used for two levels of approval](images/Dd298007.29686c05-eaa0-42b9-86ad-d577f656392c(EXCHG.150).png "Two rules used for two levels of approval")

The first rule identifies all messages with the company name Blue Yonder Airlines in the subject or message, and it sends these messages to the internal customer relationship manager for Blue Yonder Airlines, Garret Vargas.

![Rule for first-level approver](images/Dd298007.e22d1c04-85c5-4227-88e6-b118d5593350(EXCHG.150).png "Rule for first-level approver")

The second rule sends these messages to the compliance officer, Tony Krijnen.

![Second-level approval rule, with same criteria](images/Dd298007.5d888786-8e48-4459-ab86-8a4b9a016d58(EXCHG.150).png "Second-level approval rule, with same criteria")

## Example 4: Forward messages that match one of several criteria

Within a transport rule, all conditions configured within the rule must be true for the rule to match. If you want the same actions applied for either condition, you should create a separate rule for each one.

To do this, on the **Rules** page in EAC, create a rule for the first condition. Then select the rule, select **Copy**, and change the conditions in the new rule to match the second condition.

Be careful when you create multiple rules with “OR” conditions so you don’t end up with a message being sent multiple times to the approver. To avoid this, add an exception to the second rule so it ignores messages that matched the first rule.

For example, a single rule can’t check whether a message has “sales quote” in either the subject or in the attachment title. To avoid the message being sent multiple times to the approver, if the first rule checks for “sales quote” in the subject or body of the message, the second rule that checks for “sales quote” in attachment content needs an exception that contains the first rule’s criteria.

![Use an exception for the second rule](images/Dd298007.c39bbdcf-c619-4f84-8922-114ad1da824d(EXCHG.150).png "Use an exception for the second rule")


> [!NOTE]
> Exceptions are hidden by default in the <STRONG>New rule</STRONG> page. To see all the conditions and actions, select <STRONG>More options</STRONG>.



## Example 5: Forward a message that contains sensitive information

If you have the [Data loss prevention](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)(DLP) feature, many types of sensitive information are predefined. With DLP, you see that the message contains a sensitive information condition. Whether or not you have DLP, you can create conditions that identify specific sensitive information patterns that are unique to your organization.

Here’s an example where messages with sensitive information require approval. In this example, messages that contain a credit card number require approval.

![Rule that forwards mail with sensitive information](images/Dd298007.7ec1ca74-5d20-42ea-a9ee-3a8b25beb7df(EXCHG.150).png "Rule that forwards mail with sensitive information")

## See Also


[Manage message approval](manage-message-approval-exchange-2013-help.md)

