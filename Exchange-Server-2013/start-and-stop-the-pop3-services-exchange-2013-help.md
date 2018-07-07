---
title: 'Start and stop the POP3 services: Exchange 2013 Help'
TOCTitle: Start and stop the POP3 services
ms:assetid: 3d543921-d8c9-4d4b-99a1-82446b585ceb
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997475(v=EXCHG.150)
ms:contentKeyID: 49300479
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Start and stop the POP3 services

 

_**Applies to:** Exchange Server 2013_


By default, the two POP3 services, the Microsoft Exchange POP3 service and the Microsoft Exchange POP3 Backend service, aren’t started on computers running Microsoft Exchange Server 2013. You must start these two services to allow your email clients to connect to Exchange using POP3. When these services are running, Exchange 2013 accepts unsecured POP3 client communications on port 110 and over port 995 using Secure Sockets Layer (SSL).

The Microsoft Exchange POP3 service runs on Exchange 2013 computers that are running the Client Access server role. The Microsoft Exchange POP3 Backend service runs on the Exchange 2013 computer that’s running the Mailbox server role. In environments where the Client Access and Mailbox roles are running on the same computer, you manage both services on the same computer.

For additional information related to POP3 and IMAP4, see [POP3 and IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 2 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "POP3 and IMAP4 Permissions" section in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the Microsoft Management Console Services snap-in to start or stop the POP3 services

To start the POP3 services:

1.  On the computer running the Client Access server role, click **Start**, point to **Programs**, point to **Administrative Tools**, and then click **Services**. Right-click **Microsoft Exchange POP3**, and then click **Start**.

2.  On the computer running the Mailbox server role, click **Start**, point to **Programs**, point to **Administrative Tools**, and then click **Services**. In the result pane, right-click **Microsoft Exchange POP3 Backend**, and then click **Start**.

To stop the POP3 services:

1.  On the computer running the Client Access server role, click **Start**, point to **Programs**, point to **Administrative Tools**, and then click **Services**. Right-click **Microsoft Exchange POP3**, and then click **Stop**.

2.  On the computer running the Mailbox server role, click **Start**, point to **Programs**, point to **Administrative Tools**, and then click **Services**. Right-click **Microsoft Exchange POP3 Backend**, and then click **Stop**.

## Use the Shell to start or stop the POP3 services

To start the POP3 services:

1.  On the computer running the Client Access server role, from the Shell, run the following command to start the Microsoft Exchange POP3 service.
    
        Start-service MSExchangePOP3

2.  On the computer running the Mailbox server role, from the Shell, run the following command to start the Microsoft Exchange POP3 Backend service.
    
        Start-service MSExchangePOP3BE

To stop the POP3 services:

1.  On the computer running the Client Access server role, from the Shell, run the following command to stop the Microsoft Exchange POP3 service.
    
        Stop-service MSExchangePOP3

2.  On the computer running the Mailbox server role, from the Shell, run the following command to stop the Microsoft Exchange POP3 Backend service.
    
        Stop-service MSExchangePOP3BE

## Use net start to start or stop the POP3 services

To start the POP3 services:

1.  On the computer running the Client Access server role, at the command prompt, run the following command to start the Microsoft Exchange POP3 service.
    
        Net Start msExchangePOP3

2.  On the computer running the Mailbox server role, at the command prompt, run the following command to start the Microsoft Exchange POP3 Backend service.
    
        Net Start msExchangePOP3BE

To stop the POP3 services:

1.  On the computer running the Client Access server role, at the command prompt, run the following command to stop the Microsoft Exchange POP3 service.
    
        Net Stop MSExchangePOP3

2.  On the computer running the Mailbox server role, at the command prompt, run the following command to stop the Microsoft Exchange POP3 Backend service.
    
        Net Stop MSExchangePOP3BE

## How do you know this worked?

1.  On the Exchange Client Access server, open Windows Task Manager. On the **Services** tab, the status for **MSExchangePOP3** will show as **Running** if the Microsoft Exchange POP3 service is running.

2.  On the Exchange Mailbox server, open Windows Task Manager. On the **Services** tab, the status for **MSExchangePOP3BE** will show as **Running** if the Microsoft Exchange POP3 Backend service is running.

