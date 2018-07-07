---
title: 'Common attachment blocking scenarios for mail flow rules: Exchange 2013 Help'
TOCTitle: Common attachment blocking scenarios for mail flow rules
ms:assetid: 5c576439-d55b-4c7f-90ed-a7f72cbb16c2
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn950026(v=EXCHG.150)
ms:contentKeyID: 65308308
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Common attachment blocking scenarios for mail flow rules

 

_**Applies to:** Exchange Online, Exchange Online Protection, Exchange Server 2013_


Your organization might require that certain types of messages be blocked or rejected in order to meet legal or compliance requirements, or to implement specific business needs. Here are some examples of common scenarios for blocking all attachments that you can set up using transport rules in Exchange:

  -  
    Example 1: Block messages with attachments, and notify the sender

  -  
    Example 2: Notify intended recipients when an inbound message is blocked

  -  
    Example 3: Modify the subject line for notifications

  -  
    Example 4: Apply a rule with a time limit

For additional examples showing how to block specific attachments, see:

  - [Use transport rules to inspect message attachments in Exchange 2013](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013)

  - [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/en-us/library/jj919236\(v=exchg.150\)) (Exchange Online, Exchange Online Protection)

The malware filter includes a Common Attachment Types Filter. In the Exchange admin center (EAC), go to **Protection**, then click **New** (![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon")) to add filters. In the Exchange Online portal, browse to **Protection**, and then select **Malware Filter**.

To get started implementing any of these scenarios to block certain message types:

1.  Sign in to the Exchange admin center.

2.  Go to **Mail flow** \>**Rules**.

3.  Click **New** (![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon")) and then select **Create a new rule**.

4.  In the **Name** box, specify a name for the rule, and then click **More options**.

5.  Select the conditions and actions you want.

**Note:** In the EAC, the smallest attachment size that you can enter is 1 kilobyte, which should detect most attachments. However, if you want to detect every possible attachment of any size, you need to use PowerShell to adjust the attachment size to 1 byte after you create the rule in the EAC. To learn how to open the Exchange Management Shell in your on-premises Exchange organization, see [Open the Shell](https://technet.microsoft.com/en-us/library/dd638134\(v=exchg.150\)). To learn how to use Windows PowerShell to connect to Exchange Online, see [Connect to Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554). To learn how to use Windows PowerShell to connect to Exchange Online Protection, see [Connect to Exchange Online Protection PowerShell](https://go.microsoft.com/fwlink/p/?linkid=627290).

Replace *\<Rule Name\>* with the name of the existing rule, and run the following command to set the attachment size to 1 byte:

    Set-TransportRule -Identity "<Rule Name>" -AttachmentSizeOver 1B

After you adjust the attachment size to 1 byte, the value that's displayed for the rule in the EAC is **0.00 KB**.

## Example 1: Block messages with attachments, and notify the sender

If you don't want people in your organization to send or receive attachments, you can set up a transport rule to block all messages with attachments.

In this example, all messages sent to or from the organization with attachments are blocked.

![Rule that blocks all attachments](images/Dn950026.38094183-166f-4ba5-a9cf-242e7d0f4e04(EXCHG.150).png "Rule that blocks all attachments")

If all you want to do is block the message, you might want to stop rule processing once this rule is matched. Scroll down the rule dialog box, and select the **Stop processing more rules** check box.

## Example 2: Notify intended recipients when an inbound message is blocked

If you want to reject a message but let the intended recipient know what happened, you can use the **Notify the recipient with a message** action.

You can include placeholders in the notification message so that it includes information about the original message. The placeholders must be enclosed in two percent signs (%%), and when the notification message is sent, the placeholders are replaced with information from the original message. You can also use basic HTML such as \<br\>, \<b\>, \<i\>, and \<img\> in the message.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Type of information</strong></p></td>
<td><p><strong>Placeholder</strong></p></td>
</tr>
<tr class="even">
<td><p>Sender of the message.</p></td>
<td><p>%%From%%</p></td>
</tr>
<tr class="odd">
<td><p>Recipients listed on the “To” line.</p></td>
<td><p>%%To%%</p></td>
</tr>
<tr class="even">
<td><p>Recipients listed on the “Cc” line.</p></td>
<td><p>%%Cc%%</p></td>
</tr>
<tr class="odd">
<td><p>Subject of the original message.</p></td>
<td><p>%%Subject%%</p></td>
</tr>
<tr class="even">
<td><p>Headers from the original message. This is similar to the list of headers in a delivery status notification (DSN) generated for the original message.</p></td>
<td><p>%%Headers%%</p></td>
</tr>
<tr class="odd">
<td><p>Date the original message was sent.</p></td>
<td><p>%%MessageDate%%</p></td>
</tr>
</tbody>
</table>


In this example, all messages that contain attachments and are sent to people inside your organization are blocked, and the recipient is notified.

![Rule that notifies recipients when an inbound message is blocked](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "Rule that notifies recipients when an inbound message is blocked")

## Example 3: Modify the subject line for notifications

When a notification is sent to the recipient, the subject line is the subject of the original message. If you want to modify the subject so that it is clearer to the recipient, you must use two transport rules:

  - The first rule adds the word "undeliverable" to the beginning of the subject of any messages with attachments.

  - The second rule blocks the message and sends a notification message to the sender using the new subject of the original message.


> [!IMPORTANT]
> The two rules must have identical conditions. Rules are processed in order, so the first rule adds the word "undeliverable", and the second rule blocks the message and notifies the recipient.



Here's what the first rule would look like if you want to add "undeliverable" to the subject:

![Rule that prepends Undeliverable to messages with attachments](images/Dn950026.2552b0bd-c69d-48b4-9e69-267fcaf20e70(EXCHG.150).png "Rule that prepends Undeliverable to messages with attachments")

And the second rule does the blocking and notification (the same rule from Example 2):

![Rule that notifies recipients when an inbound message is blocked](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "Rule that notifies recipients when an inbound message is blocked")

## Example 4: Apply a rule with a time limit

If you have a malware outbreak, you might want to apply a rule with a time limit so that you temporarily block attachments. For example, the following rule has both a start and stop day and time:

![Rule showing a time limit](images/Dn950026.bdc8c4d8-72fa-4c5b-97f2-5fe76d50e643(EXCHG.150).png "Rule showing a time limit")

## See Also


[Mail flow rules (transport rules) in Exchange 2013](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)  


[Mail flow rules (transport rules) in Exchange Online](https://technet.microsoft.com/en-us/library/jj919238\(v=exchg.150\))  
[Mail flow rules (transport rules) in Exchange Online Protection](https://technet.microsoft.com/en-us/library/dn271424\(v=exchg.150\))

