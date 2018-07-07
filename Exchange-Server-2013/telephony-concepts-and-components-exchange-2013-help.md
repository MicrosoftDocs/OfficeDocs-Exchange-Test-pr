---
title: 'Telephony concepts and components: Exchange 2013 Help'
TOCTitle: Telephony concepts and components
ms:assetid: ce70bf6a-db85-411b-8b93-2987703963a9
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124606(v=EXCHG.150)
ms:contentKeyID: 49315524
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Telephony concepts and components

 

_**Applies to:** Exchange Online, Exchange Server 2013_


If you're planning and deploying Microsoft Exchange 2013 Unified Messaging (UM) on your network, you must understand Unified Messaging and telephony networks. This topic provides an overview of telephony infrastructure concepts and components that will help you plan and deploy servers running Exchange 2013 Unified Messaging.

**Contents**

Overview

Concepts and components

Circuit-switched networks

Packet-switched networks

PBX

IP PBX

SIP-enabled PBX

VoIP

IP gateways

## Overview

In versions of Microsoft Exchange before Exchange Server 2007, the Exchange administrator's main responsibility was managing email messages and, sometimes, managing a network infrastructure. Earlier versions of Exchange didn't have Unified Messaging capabilities. Exchange Server version 5.5, Exchange 2000 Server, and Exchange Server 2003 administrators focused on the Exchange environment and the network infrastructure, and relied heavily on telephony consultants to manage their telephony environment and infrastructure.

## Concepts and components

To successfully deploy Unified Messaging in Exchange 2013, you must have a good understanding of basic telephony concepts and telephony components. After you gain a good understanding of telephony basics, you can successfully integrate Exchange 2013 Unified Messaging into an Exchange 2013 organization. Basic concepts and components include the following:

  - Circuit-switched and packet-switched networks

  - Private Branch eXchange (PBX)

  - IP PBX

  - Voice over Internet Protocol (VoIP)

  - VoIP gateways

## Circuit-switched networks

In circuit-switched networks, such as the Public Switched Telephone Network (PSTN), multiple calls are transmitted across the same transmission medium. Frequently, the medium used in the PSTN is copper. However, fiber optic cable might also be used.

A circuit-switched network is a network in which there exists a dedicated connection. A dedicated connection is a circuit or channel set up between two nodes so that they can communicate. After a call is established between two nodes, the connection may be used only by these two nodes. When the call is ended by one of the nodes, the connection is canceled.


> [!NOTE]
> PSTN is a grouping of the world's public circuit-switched telephone networks. This grouping resembles the way that the Internet is a grouping of the world's public IP-based packet-switched networks.



There are two basic types of circuit-switched networks: analog and digital. Analog was designed for voice transmission. For many years, the PSTN was only analog, but today, circuit-based networks such as the PSTN have transitioned from analog to digital. To support an analog voice transmission signal over a digital network, the analog transmission signal must be encoded or converted into a digital format before it enters the telephony WAN. On the receiving end of the connection, the digital signal must be decoded or converted back into an analog signal format.

There are advantages and disadvantages to circuit-switched networks. Circuit-switched networks have several disadvantages. Circuit-switched networks can be relatively inefficient, because bandwidth can be wasted. This isn't the case when VoIP is used on a packet-switched network. VoIP shares the available bandwidth with all other network applications and makes more efficient use of the available bandwidth. Another disadvantage to circuit-switched networks is that you have to provision for the maximum number of telephone calls that will be required for peak usage times and then pay for the use of the circuit or circuits to support the maximum number of calls.

Circuit switching has one big advantage over packet-switched networks. In a circuit-switched network, when you use a circuit, you have the full circuit for the time that you're using the circuit without competition from other users. This isn't the case with packet-switched networks.


> [!NOTE]
> Synchronous Digital Hierarchy (SDH) has become the primary transmission protocol for most PSTN networks. SDH is carried over fiber optic networks.



Return to top

## Packet-switched networks

Packet switching is a technique that divides a data message into smaller units called packets. Packets are sent to their destination by the best route available, and then they are reassembled at the receiving end.

In packet-switched networks such as the Internet, packets are routed to their destination through the most expedient route, but not all packets traveling between two hosts travel the same route, even those from a single message. This almost guarantees that the packets will arrive at different times and out of order. In a packet-switched network, packets (messages or fragments of messages) are individually routed between nodes over data links that may be shared by other nodes. With packet switching, unlike circuit switching, multiple connections to nodes on the network share the available bandwidth.


> [!NOTE]
> With circuit switching, all packets go to the receiver in order and along a single path.



Packet-switched networks exist to enable data communication on the Internet throughout the world. A public data network or packet-switched network is the data counterpart to the PSTN.

Packet-switched networks are also found in such network environments as LAN and WAN networks. A WAN packet-switched environment relies on telephone circuits, but the circuits are arranged so that they retain a permanent connection with their endpoint. In a LAN packet-switched environment, such as with an Ethernet network, the transmission of the data packets relies on packet switches, routers, and LAN cables. In a LAN, the switch establishes a connection between two segments only long enough to send the current packet. Incoming packets are saved to a temporary memory area or buffer in memory. In an Ethernet-based LAN, an Ethernet frame contains the payload or data portion of the packet and a special header that includes the media access control (MAC) address information for the source and destination of the packet. When the packets arrive at their destination, they are put back in order by a packet assembler. A packet assembler is needed because of the different routes that the packets may take.

Packet-switched networking has made it possible for the Internet to exist and, at the same time, has made data networks—especially LAN-based IP networks—more available and widespread.

Return to top

## PBX

A legacy PBX is a telephony device that acts as a switch for switching calls in a telephony or circuit-switched network.


> [!NOTE]
> A legacy PBX is a PBX that cannot pass IP packets. In many businesses, legacy PBXs have been replaced by IP PBXs.



A PBX is a telephony device used by most medium-size and larger-size companies. A PBX enables users or subscribers of the PBX to share a certain number of outside lines for making telephone calls considered external to the PBX. A PBX is a much less expensive solution than giving each user in a business a dedicated external telephone line. Telephone sets, in addition to fax machines, modems, and many other communication devices, can be connected to a PBX.

The PBX equipment is typically installed at a business's premises and connects calls between the telephones located and installed in the business site. A limited number of outside lines, also known as trunk lines, are typically available for making and receiving calls external to the business from an external source such as the PSTN.

Internal business calls made to external telephone numbers using a PBX are made by dialing 9 or 0 in some systems followed by the external number. An outgoing trunk line is automatically selected to complete the call. Conversely, the calls placed between users within the business don't ordinarily require special dialing digits or use of an external trunk line. This is because the internal calls are routed or switched by the PBX between telephones physically connected to the PBX.

In medium-size and larger-size businesses, the following PBX configurations are possible:

  - A single PBX that supports the whole business.

  - A grouping of two or more PBXs not networked or connected to each other.

  - A grouping of two or more PBXs connected together or networked.


> [!NOTE]
> An Exchange 2013 UM dial plan can span more than one PBX or IP PBX.



Return to top

## IP PBX

An IP PBX is a PBX that supports the IP protocol to connect phones using an Ethernet or packet-switched LAN and sends its voice conversations in IP packets. A hybrid IP PBX supports the IP protocol for sending voice conversations in packets, but also connects traditional analog and digital circuit-switched Time Division Multiplex (TDM) telephones. An IP PBX is telephone switching equipment that resides in a private business instead of the telephone company.

IP PBXs are frequently easier to administer than legacy PBXs, because administrators can easily configure their IP PBX services using an Internet browser or another IP-based utility. Plus, no additional wiring, cabling, or patch panels must be installed. With an IP PBX, moving an IP-based telephone is as simple as unplugging a telephone and plugging it in at a new location, instead of the costly service calls to move a telephone from legacy PBX vendors. Additionally, businesses that own an IP PBX don't have the additional infrastructure costs required to maintain and manage two separate circuit-switched and packet-switched networks.

## SIP-enabled PBXs

A SIP-enabled PBX is a telephony device that acts as a networking switch for switching calls in a telephony or circuit-switched network. However, the difference between a SIP-enabled PBX and a traditional PBX is that the SIP-enabled PBX can connect to the Internet and use the SIP protocol to make calls over the Internet.

SIP-enabled PBXs use a format for calls that includes a SIP URI containing a global E.164 number and the "user=phone" parameter. For example: sip:+14255551234@contoso.com;user=phone

The E164 number begins with a leading "+", and doesn’t contain a phone-context parameter or any separators. SIP-enabled PBXs support both TCP and UDP. UDP is still widely used with legacy systems. SIP-enabled PBXs also support Mutual Transport Layer Security (mutual TLS) and DNS lookups.

## VoIP

Voice over Internet Protocol (VoIP) is a technology that contains hardware and software that enables people to use an IP-based network as the transmission medium for telephone calls. In VoIP, voice data is sent in packets using IP instead of traditional circuit transmissions or the circuit-switched telephone lines of the PSTN. A VoIP gateway that you connect to your IP network uses VoIP protocols to send voice data packets between Exchange 2013 Client Access and Mailbox servers and a PBX system.

## VoIP gateways

A VoIP gateway is a third-party hardware device or product that connects a legacy PBX to your LAN. The VoIP gateway lets the PBX system communicate with your Exchange 2013 Mailbox and Client Access servers running the Microsoft Exchange Unified Messaging and Unified Messaging Call Router services.


> [!NOTE]
> The VoIP gateway can also connect to PBX systems that use VoIP instead of PSTN circuit-switched protocols.



Exchange 2013 Unified Messaging relies on the VoIP gateway's abilities to translate or convert TDM or telephony circuit-switched based protocols like ISDN and QSIG from a PBX to IP-based or VoIP-based protocols like Session Initiated Protocol (SIP), Realtime Transport Protocol (RTP), or T.38 for Realtime Facsimile Transport. The VoIP gateway is integral to the functionality and operation of Unified Messaging.


> [!IMPORTANT]
> After you install the VoIP gateway, IP PBX, or SIP-enabled PBX, you must create a UM IP gateway to represent the physical device. After you create a UM IP gateway, the Client Access and Mailbox servers linked with the UM IP gateway will send a SIP OPTIONS request to the VoIP gateway, IP PBX, or SIP-enabled PBX to ensure that the device is responsive. If the VoIP gateway doesn't respond to the SIP OPTIONS request from the Mailbox server, the Mailbox server will log an event with ID 1088 stating that the request failed. To resolve this issue, ensure that the VoIP gateway, IP PBX, or is available and online and that the Unified Messaging configuration on both the Client Access and Mailbox server is correct.



For more information about IP PBX and PBX configurations, see [PBX and IP PBX configurations](pbx-and-ip-pbx-configurations-exchange-2013-help.md).

Return to top

## For more information

[UM protocols, ports, and services](um-protocols-ports-and-services-exchange-2013-help.md)

[Telephony advisor for Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

