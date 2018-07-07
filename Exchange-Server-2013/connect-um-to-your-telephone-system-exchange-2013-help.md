---
title: 'Connect UM to your telephone system: Exchange 2013 Help'
TOCTitle: Connect UM to your telephone system
ms:assetid: 92c3e029-f732-4d6d-b147-2b3006d5f088
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673544(v=EXCHG.150)
ms:contentKeyID: 49315464
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Connect UM to your telephone system

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Unified Messaging (UM) combines voice messaging and email messaging into one mailbox that can be accessed from many different devices. Users can listen to their voice mail messages from their email Inbox or by using Outlook Voice Access from any telephone.

When you’re deploying UM in a Microsoft Exchange organization, you must install, deploy, and configure a single or multiple Voice over IP (VoIP) gateways to connect to the Private Branch eXchanges (PBXs) in your telephony network or install, deploy, and configure Session Initiation Protocol (SIP)-enabled PBXs or IP PBXs. If you’re upgrading your current voice mail system, you’ll need to deploy the devices that connect to your telephony network, install your Exchange Client Access and Mailbox servers, and then create the required UM components that allow your telephony network to connect to your data network. This enables incoming calls from the telephony network to connect to your VoIP gateways, IP PBXs, or SIP-enabled PBXs, and those devices to connect to your Exchange organization.

If you’re installing, deploying, and configuring either Microsoft Office Communications Server 2007 R2 or Microsoft Lync Server, you won’t use VoIP gateways, IP PBXs, or SIP-enabled PBXs to directly connect to Exchange Unified Messaging. Instead, a Lync Mediation Server and VoIP gateway or an advanced VoIP gateway that has the functionality of a Mediation Server and a VoIP gateway will allow you to connect to Exchange UM. UM users that are enabled for Enterprise Voice can retrieve, listen to, and respond to voice messages and make outbound calls. They also have access to other Lync-related features including presence and Instant Messaging (IM) by using Office Communicator or a Lync client.

The following information will help you set up and deploy UM and enable voice mail features for users in your organization:

  - [Connect a VoIP gateway, IP PBX, or session border controller to UM](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)   Learn how to connect VoIP gateways or IP PBXs to UM.

  - [Telephony advisor for Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)   Learn about supported VoIP gateways, IP PBXs, and PBXs.

  - [Configuration notes for supported VoIP gateways, IP PBXs, and PBXs](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)  Learn how to set up your VoIP gateways, IP PBXs, and PBXs.

