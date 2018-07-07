---
title: 'Test UM connectivity to VoIP gateways and PBXs: Exchange 2013 Help'
TOCTitle: Test UM connectivity to VoIP gateways and PBXs
ms:assetid: 2aca8631-a99a-4e29-aff0-e462385f03b2
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa996906(v=EXCHG.150)
ms:contentKeyID: 55129209
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Test UM connectivity to VoIP gateways and PBXs

 

_**Applies to:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_


You can test the operation of Unified Messaging (UM) and related connected telephony equipment. When you perform the following procedure, the Client Access and Mailbox server tests the full end-to-end operation of the voice mail system. This includes the telephony components connected to the Client Access and Mailbox servers, including VoIP gateways, Private Branch eXchanges (PBXs), IP PBXs, and cabling.

For additional management tasks related to troubleshooting UM, see [UM services procedures](um-services-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 3 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox server (UM service)" and “Client Access Server (UM call router service)” entries in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - To perform the following procedures, you must log on to the Mailbox server by using an account that's a member of the local Administrators group.

  - Verify that the Mailbox server is installed, either on the same computer as the Client Access server or on a separate computer.

  - Verify that the Client Access server is installed, either on the same computer as the Mailbox server or on a separate computer.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Use the Shell to test the operation of the Unified Messaging and telephony components

This example tests the ability of the UM IP gateway to listen on TCP port 5060 for incoming SIP requests.

    Test-UMConnectivity -ListenPort 5060 -UMIPGateway MyIPGateway

This example tests the ability of the local Mailbox server to use an unsecured TCP connection instead of a secured mutual TLS connection to place a call through a UM IP gateway named `MyUMIPGateway` by using the telephone number 56780.

    Test-UMConnectivity -UMIPGateway MyUMIPGateway -Phone 56780 -Secured $false

This example tests the Outlook Voice Access number on a dial plan by using a SIP URI. This example can be used in an environment that includes Lync Server.

    Test-UMConnectivity -UMIPGateway OCSGateway1 -Phone "sip:SIPdialplan.contoso.com@contoso.com"


> [!NOTE]
> You can set the <CODE>-Timeout</CODE> parameter with a value of less than 5 seconds. However, we recommend that you always configure this parameter with a value of 5 seconds or more. Use mode 2 when the <CODE>&shy;UMIPGateway</CODE> parameter is specified in the command-line syntax.


