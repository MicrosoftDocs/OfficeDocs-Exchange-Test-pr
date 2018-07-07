---
title: 'Connect UM to a supported VoIP gateway: Exchange 2013 Help'
TOCTitle: Connect UM to a supported VoIP gateway
ms:assetid: b8dfc8bd-2ee5-418d-b0a4-4fa2ec7e2a2e
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124360(v=EXCHG.150)
ms:contentKeyID: 49315511
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Connect UM to a supported VoIP gateway

 

_**Applies to:** Exchange Server 2013_


When you’re setting up Unified Messaging (UM), you must configure the Voice over IP (VoIP) gateways, IP PBXs, SIP-enabled PBXs, or session border controllers (SBCs) on your network to communicate with the Client Access servers running the Microsoft Exchange Unified Messaging Call Router service and the Mailbox servers running the Microsoft Exchange Unified Messaging service in your Exchange organization. You must also configure the Client Access and Mailbox servers to communicate with the VoIP gateways, IP PBXs, SIP-enabled PBXs, or SBCs.


> [!NOTE]
> After you've connected your Client Access and Mailbox servers to the VoIP gateways, IP PBXs, SIP-enabled PBXs, or SBCs on your data network you must create the required UM components and also enable users for Unified Messaging so they can use the voice mail system.



## Steps

Here are the basic steps for connecting VoIP gateways, IP PBXs, SIP-enabled PBXs, or SBCs to Client Access and Mailbox servers:

Step 1: Install the Client Access and Mailbox servers in your organization.

Step 2: Create and configure a Telephone Extension, SIP URI, or E.164 UM dial plan.

Step 3: Create and configure a UM IP gateway. You must create and configure a UM IP gateway for each VoIP gateway, IP PBX, SIP-enabled PBX, or SBC that will be accepting incoming calls and sending outgoing calls.

Step 4: Create a new UM hunt group if needed. If you create a UM IP gateway and don’t specify a UM dial plan, a UM hunt group will be automatically created.

See the following sections for information about each step.

## Step 1: Install your Client Access and Mailbox servers

When you’re deploying Exchange servers in your organization, you can install the Client Access and Mailbox servers on the same computer or install the Client Access server on a separate computer from the Mailbox server. To install the Client Access server, run Setup.exe from the installation media. You use the same command when you’re installing the Client Access server on a separate computer from the Mailbox server or installing it on the same computer. For details, see [Install Exchange 2013 using the Setup wizard](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md). If you want to add features and functionality to your existing Exchange server, you can use **Programs and Features** or Setup.exe.

## Step 2: Create and configure a UM dial plan

After you’ve installed the required servers, you must first create a UM dial plan. A UM dial plan contains the configuration settings that enable you to connect to your telephony network by linking to a single or multiple UM IP gateways. A UM IP gateway and UM hunt group are directly linked to a UM dial plan and are also required. For details, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

A UM dial plan establishes a link from the telephone extension number of a user to their UM-enabled mailbox. When you create a UM dial plan, you can configure the number of digits in the extension numbers, the Uniform Resource Identifier (URI) type, and the VoIP security setting for the dial plan.

There are three types of dial plans: Telephone Extension, Session Initiation Protocol (SIP) URI, and E.164. When you create and configure a UM dial plan, you must determine the type of information that’s sent from your IP PBX, SIP-enabled PBX, or PBX and whether the calls are being sent to a Client Access or Mailbox server in a telephone extension or E.164 format. If you’re deploying Microsoft Office Communications Server 2007 R2 or Microsoft Lync Server, you must create and configure a SIP URI dial plan.

## Step 3: Create and configure a UM IP gateway

After you create a UM dial plan, you must create a UM IP gateway to represent each VoIP gateway, IP PBX, or SBC on your network. When you create a UM IP gateway, you can configure it to use an IP address or a fully qualified domain name (FQDN). If you use an FQDN, you must make sure you've correctly configured a DNS host record for the IP gateway so the host name will be correctly resolved to an IP address.

After you install a VoIP gateway, IP PBX, or SBC, you must create a UM IP gateway to represent the physical hardware device. After you've created a UM IP gateway, the Client Access server that use the UM IP gateway will send a SIP OPTIONS request to the VoIP gateway, IP PBX, or SBC to ensure that it’s responsive. If the VoIP gateway, IP PBX, SIP-enabled PBX, or SBC doesn't respond, the Client Access server will log an event with ID 1088 stating that the request failed. To resolve this issue, make sure that the VoIP gateway, IP PBX, or SBC is available and online and that the Unified Messaging configuration is correct.

Client Access and Mailbox servers will communicate only with a VoIP gateway, IP PBX, or SBC that’s listed as a trusted SIP peer. In some cases, if two VoIP gateways, IP PBXs, or SBCs are configured to use the same IP address, an event with ID 1175 will be logged. This event may occur if you've configured your DNS zones with fully qualified domain names (FQDNs) for the VoIP gateways on your network. Unified Messaging protects against unauthorized requests by retrieving the internal URL of the Unified Messaging Web Services virtual directory that’s located on the Mailbox server and then using the URL to build the list of FQDNs for the trusted SIP peers. After two FQDNs are resolved to the same IP address, this event will be logged.

You must restart the Microsoft Exchange Unified Messaging service if a UM IP gateway is configured to use an FQDN and the DNS record of the UM IP gateway is changed after the service has been started. If you don't restart the service, the Mailbox server won't be able to locate the UM IP gateway. This occurs because a Mailbox server maintains a cache for all UM IP gateways in memory and DNS resolution is performed only when the service is restarted or when the configuration of a VoIP gateway, IP PBX, or SBC has changed.

Exchange Unified Messaging supports various VoIP gateway vendors and other vendors of IP PBXs, SIP-enabled PBXs, and SBCs. Each of the supported VoIP gateways is designed to connect to a variety of third-party PBX systems.

For detailed information about VoIP gateways, see the following topics:

  - [Create a UM IP gateway](create-a-um-ip-gateway-exchange-2013-help.md)

  - [Configuration notes for supported VoIP gateways, IP PBXs, and PBXs](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Connect a VoIP gateway, IP PBX, or session border controller to UM](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)

For details, see [Connect your voice mail system to your telephone network](connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md).

## Step 4: Create a new UM hunt group (if needed)

Hunt group is a term used to describe a group of Private Branch eXchange (PBX) or IP PBX extension numbers that are shared by users. Hunt groups are used to efficiently distribute calls into or out of a specific business unit. Creating and defining a hunt group minimizes the chance that a caller who places an incoming call will receive a busy signal when the call is received.

UM hunt groups mirror the hunt groups that are used on PBXs and IP PBXs. When you configure your PBXs or IP PBXs, you must create and configure one or more UM hunt groups. UM hunt groups act as a link between the UM IP gateway and the UM dial plan.

Depending on how you create your UM IP gateway, you may have to create one or multiple new UM hunt groups. If you don’t link a UM IP gateway with a dial plan when you create the UM IP gateway, a single UM hunt group is created by default. If you link a UM IP gateway to a UM dial plan when you create the UM IP gateway, all incoming calls will be sent through the UM IP gateway and those calls will be accepted by Client Access and Mailbox servers. If you don’t link a UM IP gateway to a UM dial plan when you create the UM IP gateway, you’ll need to create a UM hunt group with the correct pilot identifier for incoming calls to be forwarded from an UM IP gateway to a dial plan.

If you have multiple Outlook Voice Access and auto attendant numbers and have linked a UM IP gateway to a dial plan, you’ll need to delete the UM hunt group that was created by default and create multiple UM hunt groups. For details about how to create a UM hunt group, see [Create a UM hunt group](create-a-um-hunt-group-exchange-2013-help.md).

