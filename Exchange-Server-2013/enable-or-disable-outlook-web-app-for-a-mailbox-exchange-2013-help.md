---
title: 'Enable or disable Outlook Web App for a mailbox: Exchange 2013 Help'
TOCTitle: Enable or disable Outlook Web App for a mailbox
ms:assetid: abc19646-6211-4f18-a060-e347452dcc53
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124124(v=EXCHG.150)
ms:contentKeyID: 50387721
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Enable or disable Outlook Web App for a mailbox

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can use the EAC or the Shell to enable or disable Outlook Web App for a user mailbox. When Outlook Web App is enabled, a user can use Outlook Web App to send and receive email. When Outlook Web App is disabled, the mailbox will continue to receive email messages, and a user can access it to send and receive email by using a MAPI client, such as Microsoft Outlook, or with a POP or IMAP email client, assuming that the mailbox is enabled to support access by those clients.


> [!NOTE]
> Support for Outlook Web App and MAPI, POP3, and IMAP4 email clients is enabled by default when a user mailbox is created.



For additional management tasks related to managing email client access to a mailbox, see the following topics:

  - [Enable or disable MAPI for a mailbox](enable-or-disable-mapi-for-a-mailbox-exchange-online-help.md)

  - [Enable or disable IMAP4 access for a user](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [Enable or disable POP3 access for a user](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## What do you need to know before you begin?

  - Estimated time to complete: 2 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Client Access user settings" entry in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to enable or disable Outlook Web App

1.  In the EAC, navigate to **Recipients** \> **Mailboxes**.

2.  In the list of user mailboxes, click the mailbox that you want to enable or disable Outlook Web App for, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the mailbox properties page, click **Mailbox Features**.

4.  Under **Email Connectivity**, do one of the following:
    
      - To disable Outlook Web App, under **Outlook Web App: Enabled**, click **Disable**.
        
        A warning appears asking if you're sure you want to disable Outlook Web App. Click **Yes**.
    
      - To enable Outlook Web App, under **Outlook Web App: Disabled**, click **Enable**.

5.  Click **Save** to save your change.


> [!NOTE]
> You can enable and disable Outlook Web App for multiple user mailboxes by using the EAC bulk edit feature. For more information about how to do this, see the "Bulk edit user mailboxes" section in <A href="manage-user-mailboxes-exchange-2013-help.md">Manage user mailboxes</A>.



## Use the Shell to enable or disable Outlook Web App

This example disables Outlook Web App for the mailbox of Yan Li.

    Set-CASMailbox -Identity "Yan Li" -OWAEnabled $false

This example enables Outlook Web App for the mailbox of Elly Nkya.

    Set-CASMailbox -Identity Ellyn@contoso.com -OWAEnabled $true

For detailed syntax and parameter information, see [Set-CASMailbox](https://technet.microsoft.com/en-us/library/bb125264\(v=exchg.150\)).

## How do you know this worked?

To verify that you’ve successfully enabled or disabled Outlook Web App for a user mailbox, do one of the following:

  - In the EAC, navigate to **Recipients** \> **Mailboxes**, click the mailbox, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

  - On the mailbox properties page, click **Mailbox Features**.

  - Under **Email Connectivity**, verify whether Outlook Web App is enabled or disabled.

Or

  - Run the following command in the Shell.
    
        Get-CASMailbox <identity>
    
    If Outlook Web App is enabled, the value for the *OWAEnabled* property is `True`. If Outlook Web App is disabled, the value is `False`.

