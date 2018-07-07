---
title: Technical Overview of Policy Tips in Exchange Online and Exchange 2013
TOCTitle: Policy Tips
ms:assetid: 4266b83c-dd8a-4b3d-99ff-402e68fc810c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150512(v=EXCHG.150)
ms:contentKeyID: 47559988
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Policy Tips

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can help to prevent your organization’s Microsoft Outlook, Outlook Web App (OWA), and OWA for Devices email users from inappropriately sending sensitive information by creating data loss prevention (DLP) policies that include *Policy Tip* notification messages. Similar to MailTips that were introduced in Microsoft Exchange Server 2010, Policy Tip notification messages are displayed to users in Outlook while they are composing an email message. Policy Tip notification messages only show up if something about the sender’s email message seems to violate a DLP policy that you have in place and that policy includes a rule to notify the sender when the conditions that you establish are met. Watch this video to learn more.

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/dd629bb7-063d-49f3-b7e1-8f2e0aa4de13]

In order to show Policy Tips to your email senders, your rules must include the **Notify the sender with a Policy Tip** action. You can add this in the rules editor from the Exchange Administration Center. For more information, see [Manage policy tips](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).

The transport rule agent that enforces DLP policies does not differentiate between email message attachments, body text, or subject lines while evaluating messages and the conditions within your policies. For example, if a user creates an email message that includes a credit card number in the body of the message and then attempts to address the message to a recipient outside your organization, then a Policy Tip notification message can be shown to that user in Outlook or Outlook Web App reminding them of your enterprise’s expectations for such information. However, this type of notification will only show up if you have configured a DLP policy that restricts the example actions described; in this case adding an external email alias to the header of a message with credit card data. There is a great variety of conditions, actions, and exceptions you can choose from while creating DLP policies. This variety allows you to tailor your data loss prevention efforts in a way that meets your specific organization’s needs.

Any time you use either the notify sender action or an override action within a rule, we recommend that you also include the condition that the message was sent from within your organization. You can do this by using the policy rules editor to add the following condition: **The sender is located…** \> **inside the organization**. Learn more about changing existing DLP policies at [Manage DLP policies](manage-dlp-policies-exchange-2013-help.md). This is a best practice recommendation because the notify sender action is applied as part of your company’s message creation experience. The senders referred to by the action are the authors of messages within your company. The user interaction presented by Policy Tips cannot be acted upon by your users for incoming messages and will be ignored when the sender is located outside your organization. You can apply DLP policies to scan incoming messages and take a variety of actions, but when you do this, don’t add the notify sender action.

If email senders in your organization who are in the act of composing a message are made aware of your organizational expectations and standards in real time through Policy Tip notifications, then they are less likely to violate standards that your organization wants to enforce.


> [!NOTE]
> <UL>
> <LI>
> <P>Exchange Online: DLP is a premium feature that requires an Exchange Online Plan 2 subscription. For more information, see <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Exchange Online Licensing</A>.</P>
> <LI>
> <P>Exchange 2013: DLP is a premium feature that requires an Exchange Enterprise Client Access License (CAL). For more information about CALs and server licensing, see <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server Licensing</A>.</P>
> <LI>
> <P>If your organization is using Exchange 2013 SP1 or Exchange Online, Policy Tips are available to people sending mail from Outlook 2013, Outlook Web App, or OWA for Devices. However, if your organization is currently using Exchange 2013, Policy Tips are only available to people sending email from Outlook 2013.</P></LI></UL>



## Default text for Policy Tips and rule options

You have a range of possible options when you add sender notification rules to DLP policies. When you add a rule to notify the sender by using the **Notify the sender with a Policy Tip** action within a DLP policy, you can choose how restrictive to be. The notification options in the following table are available. For general information about editing policies, see [Manage DLP policies](manage-dlp-policies-exchange-2013-help.md). For specific information about creating Policy Tips, see [Manage policy tips](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Notification rule</th>
<th>Meaning</th>
<th>Default Policy Tip notification message that Outlook users will see</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Notify only</strong></p></td>
<td><p>Similar to MailTips, this causes an informative Policy Tip notification message about a policy violation. A sender can prevent this type of tip from showing up by using a Policy Tip options dialog box that can be accessed in Outlook.</p></td>
<td><p>This message may contain sensitive content. All recipients must be authorized to receive this content.</p></td>
</tr>
<tr class="even">
<td><p><strong>Reject message</strong></p></td>
<td><p>The message will not be delivered until the condition is no longer present. The sender is provided with an option to indicate that their email message does not contain sensitive content. This is also known as a false-positive override. If the sender indicates this, then Outlook will allow the message to leave the outbox so that the user’s report may be audited, but Exchange will block the message from being sent.</p></td>
<td><p>This message may contain sensitive content. Your organization won’t allow this message to be sent until that content is removed.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reject unless false positive override</strong></p></td>
<td><p>The result with this notification rule is similar to the <strong>Reject message</strong> notification rule. However, if you select this then Exchange will allow the message to be sent to the intended recipient, instead of blocking the message.</p></td>
<td><p><strong>Before the sender selects an option to override:</strong> This message may contain sensitive content. Your organization won’t allow this message to be sent until that content is removed.</p>
<p><strong>After the sender selects an option override:</strong> Your feedback will be submitted to your administrator when the message is sent.</p></td>
</tr>
<tr class="even">
<td><p><strong>Reject unless silent override</strong></p></td>
<td><p>The message will not be delivered until the condition is no longer present or the sender indicates an override. The sender is provided with an option to indicate that they wish to override the policy.</p></td>
<td><p><strong>Before the sender selects an option to override:</strong> This message may contain sensitive content. Your organization won’t allow this message to be sent until that content is removed.</p>
<p><strong>After the sender selects an option override:</strong> You have overridden your organization’s policy for sensitive content in this message. Your action will be audited by your organization.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reject unless explicit override</strong></p></td>
<td><p>The result with this notification rule is similar to the <strong>Reject unless silent override</strong> notification rule, except that in this case when the sender attempts to override the policy, they are required to provide a justification for overriding the policy.</p></td>
<td><p><strong>Before the sender selects an option to override:</strong> This message may contain sensitive content. Your organization won’t allow this message to be sent until that content is removed.</p>
<p><strong>After the sender selects an option override:</strong> You have overridden your organization’s policy for sensitive content in this message. Your action will be audited by your organization.</p></td>
</tr>
</tbody>
</table>


## Customize your Policy Tip notification messages

To customize the text of a Policy Tip notification that email senders see in their email program, select **Manage Policy Tips** on the Data Loss Prevention page. In order for any of your custom text to appear, a DLP policy rule must include the **Notify the sender with a Policy Tip** action. Add the action to a rule by using the DLP rules editor.

For procedures that explain how to create your own Policy Tips, see [Manage policy tips](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md). The custom text that you create can replace the default text shown in the previous table.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Policy Tip Notification Actions and Settings</th>
<th>Meaning</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Notify the sender</strong></p></td>
<td><p>Your text only appears when a <strong>Notify the sender, but allow them to send</strong> action is initiated.</p></td>
</tr>
<tr class="even">
<td><p><strong>Allow the sender to override</strong></p></td>
<td><p>Your text only appears when the following actions are initiated: <strong>Block the message unless it’s a false positive</strong>, <strong>Block the message, but allow the sender to override and send</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Block the message</strong></p></td>
<td><p>Your text only appears when a <strong>Block the message</strong> action is initiated.</p></td>
</tr>
<tr class="even">
<td><p><strong>Link to compliance URL</strong></p></td>
<td><p>The compliance URL is a link to a web page where you can explain your compliance and override policies. This link is displayed in the Policy Tip when a user clicks the <strong>More details</strong> link.</p></td>
</tr>
</tbody>
</table>


## For more information

[Data loss prevention](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Manage DLP policies](manage-dlp-policies-exchange-2013-help.md)

[Manage policy tips](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)

