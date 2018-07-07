---
title: 'Start the Microsoft Exchange Unified Messaging Call Router service: Exchange 2013 Help'
TOCTitle: Start the Microsoft Exchange Unified Messaging Call Router service
ms:assetid: 8b7e1a4c-87b3-4477-a95f-6b41cf2d38f0
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673542(v=EXCHG.150)
ms:contentKeyID: 49315458
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Start the Microsoft Exchange Unified Messaging Call Router service

 

_**Applies to:** Exchange Server 2013_


You can use the Services snap-in in Microsoft Management Console (MMC) or cmd.exe at a command prompt to start the Microsoft Exchange Unified Messaging Call Router service on a Client Access server. By default, the Microsoft Exchange Unified Messaging Call Router service is started after a Client Access server is installed. However, there may be times when you have to restart or stop the Microsoft Exchange Unified Messaging Call Router service manually, for example, when you've taken the Client Access server offline and have to bring it back online.

When the Microsoft Exchange Unified Messaging Call Router service is started on a Client Access server, the Client Access server is available to answer and process incoming UM calls.

For additional management tasks related to Client Access servers, see [UM services procedures](um-services-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - To perform the following procedures, you must log on to the Client Access server by using an account that's a member of the local Administrators group.

  - Verify that the Client Access server is installed, either on the same computer as the Mailbox server or on a separate computer.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the MMC Services snap-in to start the Microsoft Exchange Unified Messaging Call Router service

1.  Click **Start**, and then click **Control Panel**.

2.  In Control Panel, double-click **Administrative Tools**.

3.  In **Administrative Tools**, double-click **Services**.

4.  In the **Services** details pane, right-click **Microsoft Exchange Unified Messaging Call Router**, and then click **Start**.

## Use a command prompt to start the Microsoft Exchange Unified Messaging Call Router service

1.  Click **Start**, and then click **Run**.

2.  In the **Open** box, type the following command, and then press Enter.
    
        net start MSExchangeUMCR

