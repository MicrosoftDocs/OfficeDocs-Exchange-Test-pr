---
title: 'Allow or prevent call answering on a Mailbox server: Exchange 2013 Help'
TOCTitle: Allow or prevent call answering on a Mailbox server
ms:assetid: 4b860c09-6669-4e3d-b3dc-17b8018b3860
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997908(v=EXCHG.150)
ms:contentKeyID: 49315413
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Allow or prevent call answering on a Mailbox server

 

_**Applies to:** Exchange Server 2013_


You can allow the Microsoft Exchange Unified Messaging service on a Mailbox server to answer new calls or prevent it from doing so. By default, a Mailbox server is in an enabled state after it’s installed. When you’re setting the Mailbox server to accept incoming voice, fax, auto attendant and Outlook Voice Access calls, you use the **Set-ServerComponentState** cmdlet.

Configuring Maintenance Mode for a Mailbox server lets you take the server out of service. For a Mailbox server, out-of-service means that the server won’t host any active databases, all transport queues are empty, and the server won’t accept any incoming calls from Client Access servers, VoIP gateways, IP PBXs, SIP-enabled PBXs, or session border controllers (SBCs).

In Exchange 2007 and Exchange 2010, there was a status parameter that could be used to control the operational status of a Unified Messaging server. In Exchange 2013, no status parameter is available for that purpose on the **Set-UMService** cmdlet for a Mailbox server.


> [!IMPORTANT]
> It’s not required that Client Access and Mailbox servers be added to a UM dial plan before they can process calls for Unified Messaging, except when you’re integrating UM and Microsoft Office Communications Server 2007 R2 or Microsoft Lync Server. By default, all Client Access and Mailbox servers in an organization are available to answer incoming calls.



For additional management tasks related to Mailbox servers, see [UM services procedures](um-services-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 3 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Exchange Server Configuration Settings" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Verify that the Mailbox server is installed, either on the same computer as the Client Access server or on a separate computer.

  - If you’re putting a Mailbox server into Maintenance Mode, verify that there’s enough redundancy of all database copies to allow the server to go out of service.

  - Before taking a server out of Maintenance Mode, verify the health of the server and make sure it’s ready to go into service.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Use the Shell to allow or prevent call answering on a Mailbox server

This example enables a Mailbox server `UMMBXr-05x.contoso.com` to answer incoming voice, fax, auto attendant, and Outlook Voice Access calls from VoIP gateways, IP PBXs, SIP-enabled PBXs, and SBCs, and writes the change to the registry on the UMMBX-05x server.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

This example prevents a Mailbox server `UMMBX-05x.contoso.com` from answering incoming voice, fax, auto attendant, and Outlook Voice Access calls from VoIP gateways, IP PBXs, SIP-enabled PBXs, and SBCs, and writes the change only to Active Directory.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

