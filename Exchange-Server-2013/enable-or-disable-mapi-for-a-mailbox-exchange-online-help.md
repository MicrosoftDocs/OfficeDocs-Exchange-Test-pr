---
title: 'Enable or disable MAPI for a mailbox: Exchange Online Help'
TOCTitle: Enable or disable MAPI for a mailbox
ms:assetid: c2c6718c-a2c0-4ed2-b4ed-364c3cb1f592
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124497(v=EXCHG.150)
ms:contentKeyID: 49901606
ms.date: 12/29/2017
mtps_version: v=EXCHG.150
---

# Enable or disable MAPI for a mailbox

 

_**Applies to:** Exchange Online, Exchange Server 2013_

You can use the Exchange admin center or the Exchange Management Shell to enable or disable MAPI for a user mailbox. When MAPI is enabled, a user's mailbox can be accessed by Outlook or other MAPI email clients. When MAPI is disabled, it can't be accessed by Outlook or other MAPI clients. But the mailbox will continue to receive email messages, and a user can access it to send and receive email by using Outlook Web App, a POP email client, or an IMAP client, assuming that the mailbox is enabled to support access by those clients.


> [!NOTE]
> Support for Outlook Web App and MAPI, POP3, and IMAP4 email clients is enabled by default when a user mailbox is created.



For additional management tasks related to managing email client access to a mailbox, see the following topics:

  - [Enable or disable Outlook Web App for a mailbox](enable-or-disable-outlook-web-app-for-a-mailbox-exchange-2013-help.md)

  - [Enable or disable IMAP4 access for a user](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [Enable or disable POP3 access for a user](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## What do you need to know before you begin?

  - Estimated time to complete: 2 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Client Access user settings" entry in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the EAC to enable or disable MAPI

1.  In the EAC, navigate to **Recipients**  \> **Mailboxes**.

2.  In the list of user mailboxes, click the mailbox that you want to enable or disable MAPI, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the mailbox properties page, click **Mailbox Features**.

4.  Under **Email Connectivity**, do one of the following.
    
      - To disable MAPI, under **MAPI: Enabled**, click **Disable**.
        
        A warning appears asking if you're sure you want to disable MAPI. Click **Yes**.
    
      - To enable MAPI, under **MAPI: Disabled**, click **Enable**.

5.  Click **Save** to save your change.

## Use the Exchange Management Shell to enable or disable MAPI

This example disables MAPI for the mailbox of Ken Sanchez.

    Set-CASMailbox -Identity "Ken Sanchez" -MAPIEnabled $false

This example enables MAPI for the mailbox of Esther Valle.

    Set-CASMailbox -Identity "Esther Valle" -MAPIEnabled $true

For detailed syntax and parameter information, see [Set-CASMailbox](https://technet.microsoft.com/en-us/library/bb125264\(v=exchg.150\)).

## How do you know this worked?

To verify that you’ve successfully enabled or disabled MAPI for a user mailbox, do one of the following:

  - In the EAC, navigate to **Recipients**  \> **Mailboxes**, click the mailbox, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

  - On the mailbox properties page, click **Mailbox Features**.

  - Under **Email Connectivity**, verify whether MAPI is enabled or disabled.

Or

  - Run the following command in the Exchange Management Shell.
    
        Get-CASMailbox <identity>
    
    If MAPI is enabled, the value for the *MapiEnabled* property is `True`. If MAPI is disabled, the value is `False`.

