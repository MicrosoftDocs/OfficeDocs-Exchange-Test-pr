---
title: 'Enable or disable POP3 access for a user: Exchange 2013 Help'
TOCTitle: Enable or disable POP3 access for a user
ms:assetid: 57e12f07-3b14-45bd-9a82-e6032d14214f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb691018(v=EXCHG.150)
ms:contentKeyID: 49315250
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Enable or disable POP3 access for a user

 

_**Applies to:** Exchange Server 2013_


You can enable or disable POP3 for a user.


> [!NOTE]
> After you've enabled or disabled POP3 for a user, you must restart the Microsoft Exchange POP3 service and the Microsoft Exchange POP3 Backend service. For more information about how to restart the POP3 service, see <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">Start and stop the POP3 services</A>.



For additional information related to managing user mailboxes, see [Manage user mailboxes](manage-user-mailboxes-exchange-2013-help.md).

For additional information related to POP3 and IMAP4, see [POP3 and IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 2 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipient provisioning permissions" section in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to enable or disable POP3 for a user

1.  In the EAC, navigate to **Recipients** \> **Mailboxes**.

2.  In the result pane, select the user for which you want to enable or disable POP3, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  In the **User Mailbox** dialog box, in the console tree, click **Mailbox Features**.
    
    In the result pane, under **Email Connectivity**, do one of the following:
    
      - To disable POP3 for the user, under **POP3: Enabled**, click **Disable**.
    
      - To enable POP3 for the user, under **POP3: Disabled**, click **Enable**.

4.  Click **Save**.

## Use the Shell to enable or disable POP3 for a user

This example enables POP3 for the user John Smith.

    Set-CASMailbox -Identity "John Smith" -POPEnabled $true

This example disables POP3 for the user John Smith.

    Set-CASMailbox -Identity "John Smith" -POPEnabled $false

## How do you know this worked?

1.  In the EAC, navigate to **Recipients** \> **Mailboxes**.

2.  In the result pane, select the user for which you want to enable or disable POP3, and then click **Edit**.

3.  In the **User Mailbox** dialog box, in the console tree, click **Mailbox Features**.
    
    In the result pane, look under **Email Connectivity**.
    
      - If POP3 is enabled for the user, you will see **POP3: Enabled**.
    
      - If POP3 is disabled for the user, you will see **POP3: Disabled**.

4.  Click **Save**.

