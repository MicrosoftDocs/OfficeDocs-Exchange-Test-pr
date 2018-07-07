---
title: 'Delete a UM IP gateway: Exchange 2013 Help'
TOCTitle: Delete a UM IP gateway
ms:assetid: 569d3741-67dd-4597-8d28-010011be0c12
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998214(v=EXCHG.150)
ms:contentKeyID: 49315422
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Delete a UM IP gateway

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


When you delete a Unified Messaging (UM) IP gateway, Exchange servers can no longer accept incoming calls from the Voice over IP (VoIP) gateway, Session Initiation Protocol (SIP)–enabled Private Branch eXchange (PBX), IP PBX, or session border controller (SBC) associated with the UM IP gateway.


> [!IMPORTANT]
> You should delete a UM IP gateway only when you fully understand the implications of disabling communication with a VoIP gateway, IP PBX, or SBC.



For additional tasks related to UM IP gateways, see [UM IP gateway procedures](um-ip-gateway-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM IP gateways" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM IP gateway has been created. For detailed steps, see [Create a UM IP gateway](create-a-um-ip-gateway-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to delete a UM IP gateway

1.  In the EAC, navigate to **Unified Messaging** \> **UM IP Gateways**, select the UM IP gateway you want to delete, and then click **Delete** ![Delete icon](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon").

2.  On the **Warning** page, click **Yes**.

## Use the Shell to delete a UM IP gateway

This example deletes the UM IP gateway named `MyUMIPGateway`.

    Remove-UMIPGateway -Identity MyUMIPGateway

