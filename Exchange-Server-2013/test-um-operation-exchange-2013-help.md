---
title: 'Test UM operation: Exchange 2013 Help'
TOCTitle: Test UM operation
ms:assetid: 06c9ab4e-8272-47b1-a217-e366f7e9dbaa
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa995957(v=EXCHG.150)
ms:contentKeyID: 55129206
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Test UM operation

 

_**Applies to:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_


This topic explains how to use the Shell to test the operation of your voice mail system. When you perform the following procedure, the Mailbox server running the Microsoft Exchange Unified Messaging service initiates a diagnostic Session Initiation Protocol (SIP) call, and then returns a health state variable of UM services.

This diagnostic test can be run only on a local Mailbox server, and you can't test the operation of the Mailbox server using the EAC.

For additional management tasks related to Client Access and Mailbox servers, see [UM services procedures](um-services-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 3 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox server (UM service)" and “Client Access Server (UM call router service)” entries in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - To perform the following procedures, you must log on to the Mailbox server by using an account that's a member of the local Administrators group.

  - Verify that the Mailbox server is installed, either on the same computer as the Client Access server or on a separate computer.

  - Verify that the Client Access server is installed, either on the same computer as the Mailbox server or on a separate computer.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Use the Shell to test the operation of the Unified Messaging services

This example performs connectivity and operational tests on the local Mailbox server, and then displays the Voice over IP (VoIP) connectivity information.

    Test-UMConnectivity

This example tests the ability for a local Client Access server to listen for incoming unencrypted SIP requests on TCP port 5060.

    Test-UMConnectivity -ListenPort 5060

This example tests the ability for a local Client Access server to listen for incoming encrypted SIP requests on TCP port 5061.

    Test-UMConnectivity -ListenPort 5061


> [!NOTE]
> Use mode 1 when the <CODE>-UMIPGateway</CODE> parameter isn't specified.




> [!NOTE]
> You can set the <CODE>-Timeout</CODE> parameter with a value of less than 5&nbsp;seconds. However, we recommend that you always configure this parameter with a value of 5&nbsp;seconds or more.


