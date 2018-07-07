---
title: 'UM services: Exchange 2013 Help'
TOCTitle: UM services
ms:assetid: f36835f2-1e5f-4e5a-88bc-0672af1e3498
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb125191(v=EXCHG.150)
ms:contentKeyID: 49315560
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# UM services

 

_**Applies to:** Exchange Server 2013_


Client Access servers running the Microsoft Exchange Unified Messaging Call Router service and Mailbox servers running the Microsoft Exchange Unified Messaging service enable you to deploy Unified Messaging (UM) and voice mail functionality for users in your organization.

Looking for management tasks related to UM services? See [UM services procedures](um-services-procedures-exchange-2013-help.md).

**Contents**

Client Access and Mailbox servers

Server configuration settings

Server operation

## Client Access and Mailbox servers

In Exchange 2013, the server roles found in Exchange 2007 and Exchange 2010 are combined into two types of servers, and all components or services from those server roles are run on the same physical server or on two separate servers called Client Access and Mailbox.

In this new model, the Client Access server is responsible for Autodiscover, Secure Sockets Layer (SSL), authentication, redirection, and proxying. The Client Access server is the entry point for any inbound calls or Session Initiation Protocol (SIP) requests for Unified Messaging. The routing logic and SIP REDIRECT is implemented as a service that’s automatically included on a Client Access server. This service is known as the Microsoft Exchange Unified Messaging Call Router service. It runs on each Client Access server in your organization.

When a Client Access server receives a SIP INVITE for an incoming call, the Microsoft Exchange Unified Messaging Call Router service redirects the incoming call to the Mailbox server. Then a media channel (RTP or SRTP) is created between the VoIP gateway, IP PBX, or session border controller (SBC) and the Mailbox server that hosts the user’s mailbox. Although the Client Access server acts as a SIP redirector, it only handles SIP requests from VoIP gateways, IP PBXs, or SBCs. It doesn’t receive any media traffic. Media traffic that uses RTP or SRTP is only passed between the Mailbox server and SIP peers such as VoIP gateways, IP PBXs, or SBCs. When you deploy Exchange 2013 and UM, you have to configure your VoIP gateways, IP PBXs, or SBCs to point to the Client Access servers that you’ve installed so that incoming calls will be routed correctly for UM.

In Exchange 2013, the Mailbox server handles the same processes as the Unified Messaging server role handled in Exchange 2007 and Exchange 2010. The Mailbox server runs both the Microsoft Exchange Unified Messaging service and UM worker processes.

When you’re installing your Client Access and Mailbox servers and deploying Unified Messaging, you don’t have to associate or add Client Access or Mailbox servers to UM dial plans. Client Access and Mailbox servers answer all incoming calls and then use the UM dial plans to locate users.

However, if you’re integrating Unified Messaging with Microsoft Office Communications Server 2007 R2 or Microsoft Lync Server, both the SIP and the RTP or SRTP media channels for incoming calls are handled by Lync servers and the Mailbox server. In a Lync integrated environment, you don’t have VoIP gateways, IP PBXs, or SBCs. To Lync, the Mailbox server that’s running the Microsoft Exchange Unified Messaging service looks just like an Exchange 2010 UM server. The Mailbox server and the Client Access server are considered trusted peers because both servers must be added to a SIP dial plan. Lync routes the incoming call using the Inbound Routing component, which uses SIP to communicate with the Client Access server and then route the call to a Mailbox server.

Return to top

## Server configuration settings

In Exchange 2013, all the UM components and configuration settings that applied to a single computer running the Unified Messaging server role in Exchange 2010 are still available. However, some of those components and configuration settings are found on a Client Access server and others are available on a Mailbox server. In some cases, the same setting is available on both. The following list shows the parameters and settings that are available on both a Client Access server and a Mailbox server.

  - \[-DialPlans \<MultiValuedProperty\>\]

  - \[-MaxCallsAllowed \<Int32\>\]

  - \[-SipTcpListeningPort \<Int32\>\]

  - \[-SipTlsListeningPort \<Int32\>\]

  - \[-Status \<Enabled | Disabled | NoNewCalls\>\]

  - \[-UMStartupMode \<TCP | TLS | Dual\>\]

For the Mailbox server, you’ll use the **Set-UMService**, **Get-UMService**, **Enable-UMService**, and **Disable-UMService** cmdlets to view or configure UM properties for the Microsoft Exchange Unified Messaging service. A different set of cmdlets, **Set-UMCallRouterSettings** and **Get-UMCallRouterSettings**, are used to view or configure the Microsoft Exchange Unified Messaging Call Router service properties on a Client Access server. This ensures that the existing **Get-UMServer**, **Set-UMServer**, **Enable-UMServer**, and **Disable-UMServer** cmdlets from Exchange 2007 and Exchange 2010 will work in a coexistence deployment with Exchange 2013 Mailbox servers. This also ensures that the cmdlets will work when the Mailbox and Client Access servers are installed on the same or different computers.

Return to top

## Server operation

When Client Access and Mailbox servers are installed, they’re automatically enabled so they can answer incoming and outgoing voice calls and route voice mail messages to the intended recipients in your Exchange organization.

You can allow the Microsoft Exchange Unified Messaging service on a Mailbox server or the Microsoft Exchange Unified Messaging Call Router service on a Client Access server to answer new calls, or prevent it from doing so. By default, a Mailbox or Client Access server is in an enabled state after it’s installed. When you’re setting the Mailbox or Client Access server to accept incoming voice, fax, auto attendant, and Outlook Voice Access calls, you use the **Set-ServerComponentState** cmdlet.

Configuring Maintenance Mode for an Exchange 2013 Mailbox or Client Access server lets you take the server out of service. For a Mailbox server, out-of-service means that the server won’t host any active databases, all transport queues are empty, and the server won’t accept any incoming calls from Client Access servers, VoIP gateways, IP PBXs, SIP-enabled PBXs, or SBCs. For a Client Access server, out-of-service means that the server won’t accept any incoming calls from VoIP gateways, IP PBXs, SIP-enabled PBXs or SBCs.

In Exchange 2007 and Exchange 2010, there was a status parameter that could be used to control the operational status of a Unified Messaging server. In Exchange 2013, no status parameter is available for that purpose on the **Set-UMService** cmdlet for a Mailbox server or the **Set-UMCallRouterSettings** cmdlet on a Client Access server.

Although the Client Access and Mailbox servers are set to enabled when they’re installed, neither server can correctly process and route incoming calls to UM-enabled users until a UM dial plan is linked with at least one UM IP gateway.

After a dial plan is linked with a UM IP gateway, the Client Access and Mailbox servers locate all UM IP gateways that are associated with the UM dial plan and VoIP gateways, IP PBXs, and SBCs. To detect and identify any configuration changes on either UM dial plans or UM IP gateways, the Client Access or Mailbox servers check the configuration every 10 minutes.

If the UM IP gateway identifies any changes to the configuration, the Client Access or Mailbox server reacts accordingly, and either starts using or stops using the appropriate VoIP gateway, IP PBX, or SBC. After the Client Access and Mailbox servers answer incoming calls for users linked with a UM dial plan and they’re correctly communicating with VoIP gateways, IP PBXs, and SBCs, you can run a set of diagnostic operations to verify that they’re operating correctly and that connectivity between the Exchange servers and VoIP gateways, IP PBXs, or SBCs is working correctly.

Return to top

