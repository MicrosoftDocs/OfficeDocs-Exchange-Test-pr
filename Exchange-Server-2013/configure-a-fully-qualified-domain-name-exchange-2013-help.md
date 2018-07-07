---
title: 'Configure a fully qualified domain name: Exchange 2013 Help'
TOCTitle: Configure a fully qualified domain name
ms:assetid: af093f87-59b7-44a8-a9a2-8f17f0cc7db8
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee423553(v=EXCHG.150)
ms:contentKeyID: 49315493
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure a fully qualified domain name

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can configure a Unified Messaging (UM) IP gateway with either an IP address or a fully qualified domain name (FQDN). When you create a UM IP gateway, you must define the IP address or the FQDN configured on the VoIP gateway, IP PBX, or session border controller (SBC) that you're using. You can change the IP address or FQDN after the UM IP gateway is created.

If you create a UM IP gateway using an FQDN, you must create the appropriate HOST (A) records in your DNS forward lookup zone. If you create a UM IP gateway using an FQDN, and the DNS configuration for the UM IP gateway is changed, you must disable and then enable the UM IP gateway to make sure that its configuration information is updated correctly.

If you want to use mutual Transport Layer Security (mutual TLS) between a UM IP gateway and a dial plan operating in either SIP secured or Secured mode, you must configure the UM IP gateway with an FQDN. You must also configure it to listen on port 5061 and verify that the VoIP gateway, IP PBX, or SBC has also been configured to listen for mutual TLS requests on port 5061. To configure a UM IP gateway, run the following command: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.

For additional management tasks related to UM IP gateways, see [UM IP gateway procedures](um-ip-gateway-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 2 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM IP gateways" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM IP gateway has been created. For detailed steps, see [Create a UM IP gateway](create-a-um-ip-gateway-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to configure an FQDN

1.  In the EAC, navigate to **Unified Messaging** \> **UM IP Gateways**, select the UM IP gateway that you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM IP gateway** page, in **Address**, enter the FQDN for the VoIP gateway, PBX enabled for SIP, IP PBX, or SBC.

3.  Click **Save**.


> [!IMPORTANT]
> When you use an FQDN instead of an IP address on the UM IP gateway, verify that the correct DNS records have been created.



## Use the Shell to configure an FQDN

This example configures a UM IP gateway named `MyUMIPGateway` with an FQDN named voipgateway.contoso.com.

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com

This example configures a UM IP gateway named `MySBC` with an FQDN of sbc.contoso.com and listens for SIP requests on TCP port 5061.

    Set-UMIPGateway -Identity MySBC -Address sbc.contoso.com -Port 5061

