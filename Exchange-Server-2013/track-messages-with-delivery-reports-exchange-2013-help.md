---
title: 'Track messages with delivery reports: Exchange 2013 Help'
TOCTitle: Track messages with delivery reports
ms:assetid: a14e4e62-08ca-4a7b-92e1-d39fe3e0a9e5
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150554(v=EXCHG.150)
ms:contentKeyID: 47560081
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Track messages with delivery reports

 

_**Applies to:** Exchange Server 2013_


Delivery Reports is a message tracking tool in the Exchange Administration Center (EAC) that you can use to search for delivery status on email messages sent to or from users in your organization's address book, with a certain subject. You can track delivery information about messages sent by or received from any specific mailbox in your organization. The content of the message body isn't returned in a delivery report, but the subject line is displayed in the results. You can track messages for up to 14 days after they were sent or received.


> [!NOTE]
> Delivery Reports tracks messages sent by people using the Microsoft Outlook or Outlook Web App email clients. It doesn't track messages sent from POP or IMAP email clients, such as Windows Mail, Outlook Express, or Mozilla Thunderbird.



## What do you need to know before you begin?

  - Estimated time to complete each procedure: Time to complete will vary based on the scope of your search.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Message tracking" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## What do you want to do?

Use the EAC to track messages

Use the EAC to review a delivery report

## Use the EAC to track messages

1.  In the EAC, navigate to **Mail Flow** \> **Delivery Reports**.

2.  Enter the following information:
    
      - **\* Mailbox to search:** Click **Browse** to select the mailbox from the address book and then click **OK**. Selecting the mailbox to search is required.
    
      - Select one of the following:
        
          - **Search for messages sent to   **Use this option to search for messages sent to specific users. Click **Select users** and then pick users from the address book by selecting a user from the list and clicking **Add**. You can select more than one user here. When you're finished selecting users, click **OK** to return to the **Delivery Reports** page. If you select this option, you can also leave the field blank to find messages sent to anyone.
        
          - **Search for messages received from   ** Use this option to search for messages received from a specific user. Again, just select the user from the address book and click **OK** to return to the **Delivery Reports** page. If you select this option, you have to specify a sender.
    
      - **Search for these words in the subject line   **Enter subject line information here, or leave it blank to expand your search.

3.  When you are finished, click **Search**. If you want to start over, click **Clear**.

## Use the EAC to review a delivery report

To view delivery information, select a message in the **Search results** pane and click **Details**.

The delivery report shows delivery status and detailed delivery information for the message you have selected from the **Search results** pane. At the top of the report, you'll see the following fields:

  - **Subject   **The subject line of the message appears as the heading of the report.

  - **From   **Alias, display name, or email address of the person who sent the message.

  - **To**   Alias, display name, or email address for each recipient of the message.

  - **Sent   **Date and time the message was sent.

## Summary to date section

This section appears in the delivery report if a message was sent to more than one person or recipient. The top of this section tells you the total number of recipients that the message was sent to and gives brief delivery information for each recipient.

  - **Summary to date   **Displays total number of recipients, and if there are messages Pending, Delivered, or Unsuccessful. Click the hyperlinks to sort by status.

  - **Search box**   The search box is useful if you sent the message to a group of more than 30 recipients. In the search box, type an email address that you want to get delivery information about and click the magnifying glass.

  - **To   **Shows the email address of the recipient.

  - **Status   **This column displays the status of the message for each recipient.

## Detailed report information

This section contains detailed delivery information for a message sent to the recipient you select in the Summary to date section.

  - **Delivery Report for**   The email address of the selected recipient is shown here.

  - **Submitted**   Date and time that the message was submitted for delivery by the system.

Depending on the delivery status of the message, you may see a variety of status states, including:

  - **Delivered   **Indicates successful delivery.

  - **Deferred   **Indicates that a message is delayed.

  - **Pending   **If message delivery is pending because a message meets the criteria for an organization-wide rule or policy or because it’s subject to message approval, the status message explains what action a rule is performing or that the message must be approved by a moderator before delivery.

  - **Moderator**   The status indicates whether the message was approved or rejected by the moderator.

  - **Groups Expanded   **If a message was sent to a group, the individual users are shown in the **Summary to date** section so you can see the delivery status for each recipient. If you need to remove or add a user to a group during a delivery report investigation, you can modify a group by clicking **Edit Groups**.

  - **Failed**   Shows the date, time, and reason for a message delivery failure. For example, an organization-wide rule may be blocking message delivery or the message couldn't be delivered.

When you're done reviewing the report, click **Close**. Delivery reports aren't saved, but you can re-run a report at any time. Remember there is a two-week search window.

## How do you know this worked?

If your search was successful, messages that fit the search criteria are listed in the **Search results** pane. To view the delivery information for a specific message, select it and then click **Details**. If no messages are displayed in the **Search results** pane, change the search criteria and then re-run the search.

