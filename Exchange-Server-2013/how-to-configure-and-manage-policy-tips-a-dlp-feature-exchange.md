---
title: How to configure and manage Policy Tips, a DLP feature Exchange
TOCTitle: Manage policy tips
ms:assetid: cec50a35-1d00-47b3-b72f-ac1bb0fd630e
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ619307(v=EXCHG.150)
ms:contentKeyID: 49289413
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Manage policy tips

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Policy Tips are informative notices that are displayed to email senders while they’re composing a message. The purpose of the Policy Tip is to educate users that they might be violating the business practices or policies that you are enforcing with the data loss prevention (DLP) policies that you have established. The following procedures will help you begin using Policy Tips. Watch this video to learn more.

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/dd629bb7-063d-49f3-b7e1-8f2e0aa4de13]

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 30 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the “Data loss prevention (DLP)” entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

  - Policy Tips will only show up for email senders when the following conditions are met:
    
    1.  Sender’s message client program is Microsoft Outlook 2013. If your organization has deployed Exchange 2013 SP1 or is using Exchange Online, Policy Tips also show up in Outlook Web App and OWA for Devices.
    
    2.  A transport rule exists that invokes Policy Tip notifications. You can create such a transport rule by configuring a DLP policy that includes the action **Notify the sender with a Policy Tip**.
    
    3.  The content of a message header, message body, or message attachment that is scanned by your transport agent meets the conditions established within the DLP policies or rules that also include Policy Tip notification rules. Put another way, the Policy Tip only shows up for end-users if they do something that causes the associated rule to take action.

  - The default Policy Tip notification text that is built into the system will be shown if you don’t use the Policy Tip settings feature to customize your Policy Tip text. To learn more about the default text, see [Policy Tips](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Create or modify a notify-only Policy Tip

This procedure results in an informational Policy Tip being shown to an email sender when the conditions of a specific rule are met. In Microsoft Outlook, the sender can prevent this tip from showing up by using a Policy Tip options dialog box. To configure custom Policy Tip text, see Create custom Policy Tip notification text.

## Use the EAC to configure notify-only Policy Tips

1.  In the EAC, go to **Compliance management** \> **Data loss prevention**.

2.  Double-click one of the policies that appear in your list of policies or highlight one item and select **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **Edit DLP policy** page, select **Rules**.

4.  To add Policy Tips to an existing rule, highlight the rule and select **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").
    
    To add a new blank rule that you can fully customize, select **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") and then select **Create a new rule** .

5.  In **Apply this rule if**, select, **The message contains sensitive information**. This condition is required.

6.  Select ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"), select the sensitive information types, select **Add**, select **OK**, and then select **OK**.

7.  In the **Do the following** box, select **Notify the sender with a Policy Tip**, and select an option in the **Choose whether the message is blocked or can be sent** drop-down list, and then select **OK**.

8.  If you want to add additional conditions or actions, at the bottom of the window, select **More options**.
    

    > [!NOTE]
    > Only the following conditions can be used: 
    > <UL>
    > <LI>
    > <P><STRONG>SentTo (The recipient is)</STRONG></P>
    > <LI>
    > <P><STRONG>SentToScope (The recipient is located)</STRONG></P>
    > <LI>
    > <P><STRONG>From (The sender is)</STRONG></P>
    > <LI>
    > <P><STRONG>FromMemberOf (The sender is a member of)</STRONG></P>
    > <LI>
    > <P><STRONG>FromScope (The sender is located)</STRONG></P></LI></UL>The following actions can’t be used: 
    > <UL>
    > <LI>
    > <P><STRONG>RejectMessageReasonText (Reject the message and include an explanation)</STRONG></P>
    > <LI>
    > <P><STRONG>RejectMessageEnhancedStatusCode (Reject the message with the enhanced status code of)</STRONG></P>
    > <LI>
    > <P><STRONG>DeletedMessage (Delete the message without notifying anyone)</STRONG></P></LI></UL>



9.  In the **Choose a mode for this rule** list, select whether you want the rule to be enforced. We recommend testing the rule first.

10. Select **Save** to finish modifying the rule and save your changes.

## How do you know this worked?

To verify that you have successfully created a Policy Tip that will only notify a sender, do the following:

1.  In the EAC, go to **Compliance management** \> **Data loss prevention**.

2.  Select the policy that you expect to contain a notification message.

3.  Select **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon") and then select **Rules**.

4.  Select the specific rule that you expect to contain a notification message.

5.  Confirm that your **Notify the sender** action appears in the lower portion of the rule summary.

## Create or modify a block-message Policy Tip

This procedure results in a Policy Tip being shown to an email sender that indicates a message is rejected and it will not be delivered until the problematic condition is no longer present. The sender is provided with an option to indicate that their email message does not contain the problematic condition. This is also known as a false-positive override. If the sender indicates this, then the message can leave the outbox and the user’s report may be audited. However, Exchange will block the message from being sent. To configure custom Policy Tip text, see Create custom Policy Tip notification text.

## Use the EAC to configure block-message Policy Tips

1.  In the EAC, go to **Compliance management** \> **Data loss prevention**.

2.  Double-click one of the policies that appear in your list of policies or highlight one item and select **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **Edit DLP policy** page, select **Rules**.

4.  To add Policy Tips to an existing rule, highlight the rule and select **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

5.  To add a new blank rule that you can fully customize, select **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

6.  To add an action that will reveal a Policy Tip, select **More options…** and then select the **Add action** button.

7.  From the drop down list, select **Notify the sender with a Policy Tip** and then select **Block the message**.

8.  Select **OK**, then select **Save** to finish modifying the rule and save your changes.

## How do you know this worked?

To verify that you have successfully created a reject message Policy Tip, do the following:

1.  In the EAC, go to **Compliance management** \> **Data loss prevention**.

2.  Select one time to highlight the policy that you expect to contain a notification message.

3.  Select **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon") and then select **Rules**.

4.  Select one time to highlight the specific rule that you expect to contain a notification message.

5.  Confirm that your **Notify the sender that the message can’t be sent** action appears in the lower portion of the rule summary.

## Create or modify a block-unless-override Policy Tip

There are four options for Policy Tips that can reject messages or prevent messages from leaving the sender’s outbox. To learn more about these options, see [Policy Tips](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

## Use the EAC to configure block-unless override Policy Tips

1.  In the EAC, go to **Compliance management** \> **Data loss prevention**.

2.  Double-select one of the policies that appear in your list of policies or highlight one item and select **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **edit DLP policy** page, select **Rules**.

4.  To add Policy Tips to an existing rule, highlight the rule and select **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").
    
    To add a new blank rule that you can fully customize, select **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") and then select **More options…** .

5.  To add the action that will reveal a Policy Tip, Select the **Add action** button.

6.  From the drop down list, select **Notify the sender with a Policy Tip** and then select **Block the message, but allow the sender to override and send**.

7.  Select **OK**, then select **Save** to finish modifying the rule and save your changes.

## How do you know this worked?

To verify that you have successfully created a reject unless override Policy Tip, do the following:

1.  In the EAC, go to **Compliance management** \> **Data loss prevention**.

2.  Select one time to highlight the policy that you expect to contain a notification message.

3.  Select **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon") and then select **Rules**.

4.  Select one time to highlight the specific rule that you expect to contain a notification message.

5.  Confirm that your **Block the message, but allow the sender to override and send** action appears in the lower portion of the rule summary.

## Create custom Policy Tip notification text

This optional procedure will help you to customize the Policy Tip notification text that email senders see in their email program. If you do this, your custom Policy Tip notification text will not appear unless you also configure a DLP policy rule with an action that will cause the notification to appear. Keep in mind that there are default system Policy Tip notifications that can be shown if you do not customize your Policy Tip notification text. To learn more about the default text, see [Policy Tips](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

## Use the EAC to create and manage custom Policy Tip notification text

1.  In the EAC, go to **Compliance management** \> **Data loss prevention**.

2.  Select **Policy Tip settings** ![Policy Tip Settings](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "Policy Tip Settings").

3.  To add a new Policy Tip with your own customized message, select **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"). For more information about the action choices available, see [Policy Tips](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).
    
    To modify an existing Policy Tip, highlight the tip and select **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").
    
    To delete an existing Policy Tip, highlight it and select **Delete** ![Delete icon](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon") and then confirm your action.

4.  Select **Save** to finish modifying the Policy Tip and save your changes.

5.  Select **Close** to finish managing your Policy Tips and save your changes.

## Use the Shell to create custom Policy Tip notification text

The following example creates a new English-language Policy Tip that will block a message from being sent. The text of this custom Policy Tip is changed to the following value: "This message appears to contain restricted content and will not be delivered."

    New-PolicyTipConfig -Name en\Reject -Value "This message appears to contain restricted content and will not be delivered."

For more information about DLP cmdlets, see [Policy and compliance cmdlets](https://technet.microsoft.com/en-us/library/dd298082\(v=exchg.150\)).

## Use the Shell to modify custom Policy Tip notification text

The following example modifies an existing English-language, notify-only Policy Tip. The text of this custom Policy Tip is changed to "Sending bank account numbers in email is not recommended."

    Set-PolicyTipConfig en\NotifyOnly "Sending bank account numbers in email is not recommended."

For more information about DLP cmdlets, see [Policy and compliance cmdlets](https://technet.microsoft.com/en-us/library/dd298082\(v=exchg.150\)).

## How do you know this worked?

To verify that you have successfully created custom Policy Tip text, do the following:

1.  In the EAC, go to **Compliance management** \> **Data loss prevention**.

2.  Select **Policy Tip settings** ![Policy Tip Settings](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "Policy Tip Settings").

3.  Select **Refresh** ![Refresh Icon](images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Refresh Icon").

4.  Confirm that your action, locale and text for that locale appear in the list.

## For more information

[Data loss prevention](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Policy Tips](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)

[Mail flow rules (transport rules) in Exchange 2013](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange 2013

[Mail flow rules (transport rules) in Exchange Online](https://technet.microsoft.com/en-us/library/jj919238\(v=exchg.150\)) Exchange Online

[Exchange 2010 MailTips](https://go.microsoft.com/fwlink/?linkid=265179)

