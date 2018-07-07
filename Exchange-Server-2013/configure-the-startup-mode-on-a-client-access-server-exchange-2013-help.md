---
title: 'Configure the startup mode on a Client Access server: Exchange 2013 Help'
TOCTitle: Configure the startup mode on a Client Access server
ms:assetid: 71cc9061-9e3c-4b4a-8dbe-f590ca5bcee8
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673533(v=EXCHG.150)
ms:contentKeyID: 49315443
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Configure the startup mode on a Client Access server

 

_**Applies to:** Exchange Server 2013_


You can specify the startup mode for the Microsoft Exchange Unified Messaging Call Router service on a Client Access server. By default, the Client Access server will start up in TCP mode, but if you’re using Transport Layer Security (TLS) to encrypt Voice over IP (VoIP) traffic, you must configure the Client Access server to use TLS or Dual mode. We recommend that Client Access servers be configured to use Dual as the startup mode. This is because all Client Access and Mailbox servers can answer incoming calls for all UM dial plans, and those dial plans can have different security settings. If you change the startup mode, you must restart the Microsoft Exchange Unified Messaging Call Router service for the change to take effect.


> [!IMPORTANT]
> By default, Client Access servers are available to answer incoming calls. You don’t have to add a Client Access server to a UM dial plan to process UM calls unless you’re integrating UM and Microsoft Office Communications Server 2007 R2 or Microsoft Lync Server.



For additional management tasks related to Unified Messaging and Client Access servers, see [UM services procedures](um-services-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Client Access server (UM call router service)" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Verify that the Client Access server is installed, either on the same computer as the Mailbox server or on a separate computer.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to configure the startup mode on a Client Access server

1.  In the EAC, navigate to **Servers** \> **Servers**.

2.  In the list view, select the Exchange server you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **Exchange Server** page, click **Unified Messaging**.

4.  Under **UM Call Router settings** \> **UM startup mode**, select one of the following from the drop-down list:
    
      - **TCP**   Use this option if you aren’t using mTLS and are using only Unsecured dial plans.
    
      - **TLS**   Use this option if you are using mTLS and using only SIP Secured or Secured dial plans.
    
      - **DUAL**   Use this option if you are using mTLS and using Unsecured, SIP Secured, and Secured dial plans.

5.  After you select the UM startup mode, click **Save**.

## Use the Shell to configure the startup mode on a Client Access server

This example sets the startup mode for a Client Access server named `UMCallRouter1` to Dual mode.

    Set-UMCallRouterSettings -Server UMCallRouter1 -UMStartUpMode Dual

This example sets the startup mode for a Client Access server named `UMCallRouter1` to TLS mode.

    Set-UMCallRouterSettings -Server UMCallRouter1 -UMStartUpMode TLS

