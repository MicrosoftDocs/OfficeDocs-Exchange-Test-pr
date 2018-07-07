---
title: 'Set the TCP listening port on a Client Access server: Exchange 2013 Help'
TOCTitle: Set the TCP listening port on a Client Access server
ms:assetid: 5f48f21a-d8d4-48b2-868f-9a3647693841
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673530(v=EXCHG.150)
ms:contentKeyID: 49315433
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Set the TCP listening port on a Client Access server

 

_**Applies to:** Exchange Server 2013_


You can configure the TCP port that's used to listen for SIP requests on a Client Access server running the Microsoft Exchange Unified Messaging Call Router service. By default, when you install a Client Access server, the SIP TCP listening port number is set to 5060 and the Client Access server starts in TCP mode. The SIP TCP listening port can't be configured by using the EAC. You must configure the SIP TCP listening port number using the **Set-UMCallRouterSettings** cmdlet.

You may have to configure the TCP listening port to 5061 if your VoIP gateways, IP PBXs, or session border controllers (SBCs) are configured to use a TCP port other than the SIP standard 5060.

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

## Use the EAC to configure the TCP listening port on a Client Access server

1.  In the EAC, navigate to **Servers** \> **Servers**.

2.  In the list view, select the Exchange server you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **Exchange Server** page, click **Unified Messaging**.

4.  Under **UM Call Router settings**, under **TCP listening port**, enter the number for the TCP port, and click **Save**.

## Use the Shell to configure the TCP listening port on a Client Access server

This example sets the TCP listening port on a Client Access server named `MyClientAccessServer` to 5566.

    Set-UMCallRouterSettings -Server MyClientAccessServer -SipTCPListeningPort 5566

