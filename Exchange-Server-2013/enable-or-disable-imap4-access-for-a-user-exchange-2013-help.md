---
title: 'Enable or disable IMAP4 access for a user: Exchange 2013 Help'
TOCTitle: Enable or disable IMAP4 access for a user
ms:assetid: a685fae4-b6f1-42fe-8bdc-5f99f9617799
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb676481(v=EXCHG.150)
ms:contentKeyID: 49315252
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Enable or disable IMAP4 access for a user

 

_**Applies to:** Exchange Server 2013_


You can enable or disable IMAP4 for a user.


> [!NOTE]
> After you've enabled or disabled IMAP4 for a user, you must restart the Microsoft Exchange IMAP4 service and the Microsoft Exchange IMAP4 Backend service. For more information about how to restart the IMAP4 service, see <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">Start and stop the IMAP4 services</A>.



For additional information related to managing user mailboxes, see [Manage user mailboxes](manage-user-mailboxes-exchange-2013-help.md).

For additional information related to POP3 and IMAP4, see [POP3 and IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 2 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipient provisioning permissions" section in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to enable or disable IMAP4 for a user

1.  In the EAC, navigate to **Recipients** \> **Mailboxes**.

2.  In the result pane, select the user for which you want to enable or disable IMAP4, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  In the **User Mailbox** dialog box, in the console tree, click **Mailbox Features**.
    
    In the result pane, under **Email Connectivity**, do one of the following:
    
      - To disable IMAP4 for the user, under **IMAP4: Enabled**, click **Disable**.
    
      - To enable IMAP4 for the user, under **IMAP4: Disabled**, click **Enable**.

4.  Click **Save**.

## Use the Shell to enable or disable IMAP4 for a user

This example enables IMAP4 for the user John Smith.

    Set-CASMailbox -Identity "John Smith" -IMAPEnabled $true

This example disables IMAP4 for the user John Smith.

    Set-CASMailbox -Identity "John Smith" -IMAPEnabled $false

## How do you know this worked?

1.  In the EAC, navigate to **Recipients** \> **Mailboxes**.

2.  In the result pane, select the user for which you want to enable or disable IMAP4, and then click **Edit**.

3.  In the **User Mailbox** dialog box, in the console tree, click **Mailbox Features**.
    
    In the result pane, look under **Email Connectivity**.
    
      - If IMAP4 is enabled for the user, you will see **IMAP4: Enabled**.
    
      - If IMAP4 is not enabled for the user, you will see **IMAP4: Disabled**.

4.  Click **Save**.

