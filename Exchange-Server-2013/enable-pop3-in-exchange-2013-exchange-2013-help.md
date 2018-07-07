---
title: 'Enable POP3 in Exchange 2013: Exchange 2013 Help'
TOCTitle: Enable POP3
ms:assetid: e226a5f1-429d-4046-b925-da6cc151709e
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124934(v=EXCHG.150)
ms:contentKeyID: 49300732
ms.date: 03/28/2017
mtps_version: v=EXCHG.150
---

# Enable POP3 in Exchange 2013

 

_**Applies to:** Exchange Server 2013_


Learn how to enable POP3 client connectivity in Exchange 2016 using the Microsoft Management Console (MMC) or the Exchange Management Shell (EMS).

When you install Exchange Server 2016, POP3 client connectivity isn't enabled. To enable POP3 client connectivity, you need to start two POP3 services, the Microsoft Exchange POP3 service and the Microsoft Exchange POP3 Backend service. When you enable POP3, Exchange 2016 accepts unsecured POP3 client communications on port 110 and over port 995 using Secure Sockets Layer (SSL).

You manage both POP3 and POP3 Backend services on the same Exchange 2016 computer running the Mailbox server role. In Exchange 2016, Client Access services are part of the Mailbox server role so you no longer manage the services separately.

For more information about how to set up POP3 and IMAP4, see [POP3 and IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 2 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "POP3 and IMAP4 permissions" section in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Microsoft Management Console (MMC) to enable POP3

On the computer running the Mailbox server role:

1.  In the **Services** snap-in, in the console tree, click **Services (Local)**.

2.  In the result pane, right-click **Microsoft Exchange POP3**, and then click **Properties**.

3.  In the result pane, right-click **Microsoft Exchange POP3 Backend**, and then click **Properties**.

4.  On the **General** tab, under **Startup type**, select **Automatic**, and then click **Apply**.

5.  Under **Service status**, click **Start**, and then click **OK**.

## Use the Exchange Management Shell to enable POP3

On the computer running the Mailbox server role:

1.  Set the Microsoft Exchange POP3 service to start automatically.
    
        Set-service msExchangePOP3 -startuptype automatic

2.  Start the Microsoft Exchange POP3 service.
    
        Start-service msExchangePOP3

3.  Set the Microsoft Exchange POP3 Backend service to start automatically.
    
        Set-service msExchangePOP3BE -startuptype automatic

4.  Start the Microsoft Exchange POP3 Backend service.
    
        Start-service msExchangePOP3BE

## How do you know this worked?

On the Exchange 2016 Mailbox server, open Windows Task Manager. On the **Services** tab, the status for **MSExchangePOP3** and for **MSExchangePOP3BE** will show as **Running** if POP3 is enabled.

