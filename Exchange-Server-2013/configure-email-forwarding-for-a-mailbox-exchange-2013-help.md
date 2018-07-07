---
title: 'Configure email forwarding for a mailbox: Exchange 2013 Help'
TOCTitle: Configure email forwarding for a mailbox
ms:assetid: c7a7afaf-577e-49d6-8cee-bb4c4a5d570b
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd351134(v=EXCHG.150)
ms:contentKeyID: 50387722
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure email forwarding for a mailbox

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Email forwarding lets you to set up a mailbox to forward email messages sent to that mailbox to another user’s mailbox in or outside of your organization.


> [!IMPORTANT]
> If you're using Office 365 for business, you should configure email forwarding in the <A href="https://go.microsoft.com/fwlink/p/?linkid=834774">Office 365 admin center: Configure email forwarding in Office 365</A>



If your organization uses an on-premises Exchange or hybrid Exchange environment, you should use the on-premises Exchange admin center (EAC) to create and manage shared mailboxes.

## Use the Exchange admin center to configure email forwarding

You can use the Exchange admin center (EAC) set up email forwarding to a single internal recipient, a single external recipient (using a mail contact), or multiple recipients (using a distribution group).

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipient Provisioning Permissions" entry in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

1.  In the EAC, navigate to **Recipients** \> **Mailboxes**.

2.  In the list of user mailboxes, click or tap the mailbox that you want to configure mail forwarding for, and then click or tap **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the mailbox properties page, click **Mailbox Features**.

4.  Under **Mail Flow**, select **View details** to view or change the setting for forwarding email messages.
    
    On this page, you can set the maximum number of recipients that the user can send a message to. For on-premises Exchange organizations, the recipient limit is unlimited. For Exchange Online organizations, the limit is 500 recipients.

5.  Check the **Enable forwarding** check box, and then click or tap **Browse**.

6.  On the **Select Recipient** page, select a user you want to forward all email to. Select the **Deliver message to both forwarding address and mailbox** check box if you want both the recipient and the forwarding email address to get copies of the emails sent. Click or tap **OK**, and then click or tap **Save**.

What if you want to forward mail to an address outside your organization? Or forward mail to multiple recipients? You can do that, too\!

  - **External addresses**Create a mail contact and then, in the steps above, select the mail contact on the **Select Recipient** page. Need to know how to create a mail contact? Check out [Manage mail contacts](manage-mail-contacts-exchange-2013-help.md).

  - **Multiple recipients**Create a distribution group, add recipients to it, and then in the steps above, select the mail contact on the **Select Recipient** page. Need to know how to create a mail contact? Check out [Create and manage distribution groups](create-and-manage-distribution-groups-exchange-2013-help.md).

## How do you know this worked?

To make sure that you’ve successfully configured email forwarding, do one of the following:

1.  In the EAC, go to **Recipients** \> **Mailboxes**.

2.  In the list of user mailboxes, click or tap the mailbox that you configured email forwarding for, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the mailbox properties page, click or tap **Mailbox Features**.

4.  Under **Mail Flow**, click or tap **View details** to view the mail forwarding settings.

## Additional information

This topic is for admins. If you want to forward your own email to another recipient, check out the following topics:

  - [Forward email to another email account](https://go.microsoft.com/fwlink/p/?linkid=510866)

  - [Manage email messages by using rules](https://go.microsoft.com/fwlink/p/?linkid=510869)

For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

