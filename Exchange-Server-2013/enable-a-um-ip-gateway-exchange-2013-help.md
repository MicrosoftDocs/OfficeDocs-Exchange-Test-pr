---
title: 'Enable a UM IP gateway: Exchange 2013 Help'
TOCTitle: Enable a UM IP gateway
ms:assetid: 2706ae06-c45d-41b7-abbe-378a9fca104a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa996857(v=EXCHG.150)
ms:contentKeyID: 49315375
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Enable a UM IP gateway

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


By default, when a Unified Messaging (UM) IP gateway is created, its status is set to enabled. However, you might need to disable the UM IP gateway to take it offline and not allow it to take incoming or outgoing calls. After you create a UM IP gateway, you can control its operation and functionality by setting its status variable to enabled or disabled.

For additional management tasks related to UM IP gateways, see [UM IP gateway procedures](um-ip-gateway-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM IP gateways" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM IP gateway has been created and has been disabled. For detailed steps, see [Create a UM IP gateway](create-a-um-ip-gateway-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to enable a UM IP gateway

1.  In the EAC, navigate to \> **Unified Messaging** \> **UM IP Gateways**, select the UM IP gateway you want to enable, and then click the **Up arrow** ![Up Arrow Icon](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "Up Arrow Icon").

2.  On the **Warning** page, click **Yes**.

## Use the Shell to enable a UM IP gateway

This example enables a UM IP gateway named `MyUMIPGateway`.

    Enable-UMIPGateway -Identity MyUMIPGateway

