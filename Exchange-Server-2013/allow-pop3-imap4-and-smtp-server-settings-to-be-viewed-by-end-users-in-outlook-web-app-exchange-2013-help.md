---
title: 'Allow POP3, IMAP4, and SMTP server settings to be viewed by end users in Outlook Web App: Exchange 2013 Help'
TOCTitle: Allow POP3, IMAP4, and SMTP server settings to be viewed by end users in Outlook Web App
ms:assetid: bd22bf7e-3bf7-45e6-8790-919b780166f6
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Gg298947(v=EXCHG.150)
ms:contentKeyID: 49300683
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Allow POP3, IMAP4, and SMTP server settings to be viewed by end users in Outlook Web App

 

_**Applies to:** Exchange Server 2013_


If you have users who use POP3 or IMAP4 to connect to their Microsoft Exchange Server 2013 mailboxes, they need to know the correct server settings to connect. After a default Exchange 2013 installation, your users can’t look up their own incoming POP3 or IMAP4 server settings or outgoing SMTP server settings. However, you can configure Exchange so that your users can look up their own settings using Microsoft Outlook Web App.

After you perform these procedures, your users can look up their server settings in Outlook Web App as follows:

1.  In Outlook Web App, click **Settings** \> **Options**.

2.  In **Options**, click **Account** \> **My account** \> **Settings for POP or IMAP access**.

For additional information related to POP3 and IMAP4, see [POP3 and IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - Procedures in this topic require specific permissions. See each procedure for its permissions information.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the Shell to allow POP3 and IMAP4 users to view their incoming POP3 and IMAP4 settings in Outlook Web App

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "POP3 settings" and "IMAP4 settings" entries in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

This example allows external POP3 server settings to be viewed by end users.

    Set-PopSettings -ExternalConnectionSettings {Dublin01.Contoso.com:995:SSL}

For detailed syntax and parameter information, see [Set-PopSettings](https://technet.microsoft.com/en-us/library/aa997154\(v=exchg.150\)).

This example allows external IMAP4 server settings to be viewed by end users.

    Set-ImapSettings -ExternalConnectionSettings {Dublin01.Contoso.com:993:SSL}

For detailed syntax and parameter information, see [Set-ImapSettings](https://technet.microsoft.com/en-us/library/aa998252\(v=exchg.150\)).

To apply these changes, you must restart IIS. You don’t need to restart the POP3 services. To restart IIS, from a command prompt, enter the following:

    iisreset

## How do you know this worked?

To verify that you’ve configured Exchange to allow users to view their POP3 server settings:

1.  Run the following command in the Shell.
    
        Get-PopSettings | format-list

2.  Verify that the *ExternalConnectionSettings* property is set.

To verify that you’ve configured Exchange to allow users to view their IMAP4 server settings:

1.  Run the following command in the Shell.
    
        Get-ImapSettings | format-list

2.  Verify that the *ExternalConnectionSettings* property is set.

## Use the Shell to allow POP3 and IMAP4 users to view their outgoing SMTP settings in Outlook Web App

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Receive connectors" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

This example allows internal and external SMTP server settings to be viewed by end users using Outlook Web App.

    Get-ReceiveConnector "*Client Frontend*" | Set-ReceiveConnector -Fqdn Server.Contoso.com -AdvertiseClientSettings $true 

For detailed syntax and parameter information, see [Set-ReceiveConnector](https://technet.microsoft.com/en-us/library/bb125140\(v=exchg.150\)).

## How do you know this worked?

To verify that you’ve configured Exchange to allow users to view their SMTP server settings:

1.  Run the following command in the Shell.
    
        Get-ReceiveConnector | format-list

2.  If the *AdvertiseClientSettings* property is set to `true`, users can view their SMTP server settings in Outlook Web App. If *AdvertiseClientSettings* is set to `false`, users can’t view their SMTP sever settings in Outlook Web App.

## For more information

After you make it possible for end users to view their POP3, IMAP4, and SMTP settings, you may also want to:

[Enable or disable POP3 access for a user](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[Enable or disable IMAP4 access for a user](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

