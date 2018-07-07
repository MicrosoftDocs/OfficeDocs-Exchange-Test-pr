---
title: 'Stop the Microsoft Exchange Unified Messaging service: Exchange 2013 Help'
TOCTitle: Stop the Microsoft Exchange Unified Messaging service
ms:assetid: 64fa5535-8150-45c6-82e6-d2346892a031
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998595(v=EXCHG.150)
ms:contentKeyID: 49315438
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Stop the Microsoft Exchange Unified Messaging service

 

_**Applies to:** Exchange Server 2013_


You can use the Services snap-in in Microsoft Management Console (MMC) or cmd.exe at a command prompt to stop the Microsoft Exchange Unified Messaging service on a Mailbox server. There may be times when you need to stop this service, for example, when you have to take the Mailbox server offline. When you stop the Microsoft Exchange Unified Messaging service, the Mailbox server won't be able to accept and process incoming calls.

For additional management tasks related to Mailbox servers, see [UM services procedures](um-services-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - To perform the following procedures, you must log on to the Mailbox server by using an account that's a member of the local Administrators group.

  - Verify that the Mailbox server is installed, either on the same computer as the Client Access server or on a separate computer.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the MMC Services snap-in to stop the Microsoft Exchange Unified Messaging service

1.  Click **Start**, and then click **Control Panel**.

2.  In Control Panel, double-click **Administrative Tools**.

3.  In **Administrative Tools**, double-click **Services**.

4.  In the **Services** details pane, right-click **Microsoft Exchange Unified Messaging**, and then click **Stop**.

## Use a command prompt to stop the Microsoft Exchange Unified Messaging service

1.  Click **Start**, and then click **Run**.

2.  In the **Open** box, type the following command, and then press Enter.
    
        net stop MSExchangeUM

