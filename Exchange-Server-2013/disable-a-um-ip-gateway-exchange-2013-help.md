---
title: 'Disable a UM IP gateway: Exchange 2013 Help'
TOCTitle: Disable a UM IP gateway
ms:assetid: fe3a8797-1230-49cb-a839-ccec238266b6
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb125257(v=EXCHG.150)
ms:contentKeyID: 49315554
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Disable a UM IP gateway

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


By default, when you create a Unified Messaging (UM) IP gateway, the status of the UM IP gateway is enabled. After the UM IP gateway is created, you can disable the operation of the gateway by setting its status to disabled. After you disable the UM IP gateway, the Voice over IP (VoIP) gateway, IP Private Branch eXchange (PBX), or session border controller (SBC) that it's configured to use can no longer process incoming Unified Messaging calls.

For additional management tasks related to UM IP gateways, see [UM IP gateway procedures](um-ip-gateway-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM IP gateways" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM IP gateway has been created and is enabled. For detailed steps, see [Create a UM IP gateway](create-a-um-ip-gateway-exchange-2013-help.md) and [Enable a UM IP gateway](enable-a-um-ip-gateway-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to disable a UM IP gateway

1.  In the EAC, navigate to **Unified Messaging** \> **UM IP Gateways**, select the UM IP gateway you want to disable, and then click the **Down arrow** ![Down Arrow Icon](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Down Arrow Icon").

2.  On the **Warning** page, click **Yes**.

## Use the Shell to disable a UM IP gateway

This example disables a UM IP gateway named `MyUMIPGateway` and stops it from accepting incoming calls from a VoIP gateway, IP PBX, or SBC.

    Disable-UMIPGateway -Identity MyUMIPGateway

This example disables a UM IP gateway named `MyUMIPGateway` and disconnects all current calls immediately.

    Disable-UMIPGateway -Identity MyUMIPGateway -Immediate $true

