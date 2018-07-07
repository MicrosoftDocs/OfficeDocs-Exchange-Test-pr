---
title: 'Set the TLS listening port on a Client Access server: Exchange 2013 Help'
TOCTitle: Set the TLS listening port on a Client Access server
ms:assetid: f4401923-61fa-4dc5-95f8-c0d2f515b2ea
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673576(v=EXCHG.150)
ms:contentKeyID: 49315561
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Set the TLS listening port on a Client Access server

 

_**Applies to:** Exchange Server 2013_


You can configure the Transport Layer Security (TLS) port that's used to listen for SIP requests on a Client Access server running the Microsoft Exchange Unified Messaging Call Router service. By default, when you install a Client Access server, the SIP TLS listening port number is set to 5061.

You may have to configure the TLS listening port to 5061 if you want to:

  - Set the VoIP security setting on a UM dial plan to SIP Secured.

  - Set the VoIP security setting on a UM dial plan to Secured.

  - Integrate with Microsoft Office Communications Server 2007 R2 or Microsoft Lync Server.

  - Use mutual Transport Layer Security (mutual TLS) to encrypt network data between Client Access servers, Mailbox servers running the Microsoft Exchange Unified Messaging service, and VoIP gateways, Private Branch eXchanges (PBXs) enabled for Session Initiation Protocol (SIP), IP PBXs, or session border controllers (SBCs).

If you want to use mutual TLS between a UM IP gateway and a dial plan operating in either SIP Secured or Secured mode, when you create the UM IP gateway you must configure it with a fully qualified domain name (FQDN) and then configure the UM IP gateway to listen on TLS port 5061. You must also verify that any VoIP gateways, PBXs enabled for SIP, IP PBXs, or SBCs have also been configured to listen for mutual TLS requests on port 5061.

You can only configure Client Access server TCP and TLS ports. You can’t configure the ports for an Exchange 2013 Mailbox server. However, you can use the **Set-UMService** cmdlet to configure the TCP and TLS listening ports for Exchange 2010 UM servers.

For additional tasks related to Unified Messaging and Client Access servers, see [UM services procedures](um-services-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Client Access server (UM call router service)" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Verify that you have correctly installed Client Access and Mailbox servers.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to configure the TLS listening port on a Client Access server

1.  In the EAC, navigate to **Servers** \> **Servers**.

2.  In the list view, select the Exchange server you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **Exchange Server** page, click **Unified Messaging**.

4.  Under **UM Service settings**, under **TLS listening port**, enter the number for the TLS port, and then click **Save**.

## Use the Shell to configure the TLS listening port on a Client Access server

This example sets the TLS listening port on a Client Access server named `MyClientAccessServer` to 5561.

    Set-UMCallRouterSettings -Server MyClientAccessServer -SipTlsListeningPort 5561

