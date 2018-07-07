---
title: 'UM protocols, ports, and services: Exchange 2013 Help'
TOCTitle: UM protocols, ports, and services
ms:assetid: 5997ce29-1755-48bb-8ff4-b08da549482a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998265(v=EXCHG.150)
ms:contentKeyID: 49315424
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# UM protocols, ports, and services

 

_**Applies to:** Exchange Server 2013_


Microsoft Exchange 2013 Unified Messaging (UM) requires that several TCP and User Datagram Protocol (UDP) ports be used to establish communication between servers running Exchange 2013 and other devices. By allowing access through these IP ports, you enable Unified Messaging to function correctly. This topic discusses the TCP and UDP ports used in Exchange 2013 Unified Messaging.

## Unified Messaging protocols and services

Exchange 2013 Unified Messaging features and services rely on static and dynamic TCP and UDP ports to ensure correct operation of Client Access servers running the Microsoft Exchange Unified Messaging Call Router service and Mailbox servers running the Microsoft Exchange Unified Messaging service.When Exchange 2013 is installed, static inbound Windows Firewall rules are added for Exchange. If you change the TCP ports that are used by Client Access and Mailbox servers, you may also need to reconfigure the Windows Firewall rules to allow Unified Messaging to work correctly.


> [!IMPORTANT]
> On Exchange 2013 Client Access and Mailbox servers running UM components and services, Exchange setup creates inbound firewall rules that allow inbound communication without any TCP port restrictions. The following inbound rules for UM services are added:



1.  **SESWorker (GFW) (TCP-In)**

2.  **UMCallRouter (GFW) (TCP-In)**

3.  **UMCallRouter (TCP-In)**

4.  **UMService (GFW) (TCP-In)**

5.  **UMService (TCP-In)**

6.  **UMWorkerProcess – RPC (TCP-In)**

7.  **UMWorkerProcess (GFW) (TCP-In)**

8.  **UMWorkerProcess (TCP-In)**

## Session Initiation Protocol

Session Initiation Protocol (SIP) is a protocol used for initiating, modifying, and ending an interactive user session that involves multimedia elements such as video, voice, instant messaging, online games, and virtual reality. It's one of the leading signaling protocols for Voice over IP (VoIP), together with H.323. Most VoIP standards-based solutions use either H.323 or SIP. However, several proprietary designs and protocols also exist. The VoIP protocols typically support features such as call waiting, conference calling, and call transfer.

SIP clients such as VoIP gateways and IP Private Branch eXchanges (PBXs) can use TCP and UDP port 5060 to connect to SIP servers, including Client Access servers running the Microsoft Exchange Unified Messaging Call Router service. SIP is used only for setting up and tearing down voice or video calls. All voice and video communications occur over Realtime Transport Protocol (RTP).

## Real-Time Transport Protocol

RTP defines a standard packet format for delivering audio and video over a specific network, such as the Internet. RTP carries only voice/video data over the network. Call setup and teardown are generally performed by SIP.

RTP doesn't require a standard or static TCP or UDP port to communicate with. RTP communications occur on an even number UDP port, and the next higher odd number port is used for TCP communications. Although there are no standard port range assignments, RTP is generally configured to use ports between 1024 and 65535, and Mailbox servers running the Microsoft Exchange Unified Messaging service follow this convention. It's difficult for RTP to traverse firewalls because it uses a dynamic port range.

## Unified Messaging Web services

The Unified Messaging Web services installed on Mailbox servers use IP for network communication between a client, the Mailbox server, and computers running other Exchange 2013 server roles. Several Exchange 2013 Outlook Web App and Outlook 2013 client features rely on Unified Messaging Web services to operate correctly.

The following Unified Messaging client features rely on Unified Messaging Web services:

  - Voice mail options available with Exchange 2013 Outlook Web App, including the Play on Phone feature and the ability to reset a PIN.

  - The Play on Phone feature found in an Outlook client.

## UM ports

The Microsoft Exchange Unified Messaging Call Router service found on a Client Access server uses SIP over either Transmission Control Protocol (TCP) or mutual Transport Layer Security (mutual TLS) to communicate with Mailbox servers that are running the Microsoft Exchange Unified Messaging service. To avoid TCP/User Datagram Protocol (UDP) port conflicts, the Microsoft Exchange Unified Messaging Call Router service and Microsoft Exchange Unified Messaging service default to and listen on different TCP ports. They can accept both unsecured and secured connections, depending on whether mutual TLS is used with SIP and RTP traffic. By default, a Client Access server listens for SIP requests on both TCP port 5060 in Unsecured mode and TCP port 5061 in SIP Secured mode when mutual TLS is used. These ports are configurable using the **Set-UMCallRouterSettings** cmdlet. The Microsoft Exchange Unified Messaging Call Router service on the Client Access server doesn’t handle media (RTP or SRTP) traffic, so only TCP ports and no UDP ports are used. By default, a Mailbox server listens for SIP requests on both TCP port 5062 in Unsecured mode and TCP port 5063 in SIP Secured mode when mutual TLS is used. These ports aren’t configurable using Exchange Management Shell cmdlets. The Microsoft Exchange Unified Messaging service on the Mailbox server will accept connections from a Client Access server on SIP ports 5062 and 5063. After the Client Access server redirects the SIP request to a Mailbox server, an RTP or SRTP media channel is created using a VoIP gateway, IP PBX, or SBC, and the Microsoft Exchange Unified Messaging worker process on the Mailbox server.

The following table summarizes the Exchange 2013 ports and protocols, and whether the ports can be changed.

### UM listening ports

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocol</th>
<th>TCP port</th>
<th>UDP port</th>
<th>Can the ports be changed?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SIP (Client Access server – Microsoft Unified Messaging Call Router service)</p></td>
<td><p>5060 (unsecured), 5061 (secured). The service listens on both ports.</p></td>
<td><p>Not applicable</p></td>
<td><p>Yes, using the <strong>Set-UMCallRouterSettings</strong> cmdlet.</p></td>
</tr>
<tr class="even">
<td><p>SIP (Mailbox server – Microsoft Exchange Unified Messaging service)</p></td>
<td><p>5062 (unsecured), 5063 (secured). The service listens on both ports.</p></td>
<td><p>Not applicable</p></td>
<td><p>Ports can’t be changed.</p></td>
</tr>
<tr class="odd">
<td><p>SIP (Mailbox server - UM worker process)</p></td>
<td><p>5065 and 5067 for TCP (unsecured). 5065 and 5067 for mutual TLS (secured). If you have set it to Dual mode 5066 and 5068 are also used.</p></td>
<td><p>Not applicable</p></td>
<td><p>Ports can’t be changed.</p></td>
</tr>
<tr class="even">
<td><p>RTP (Mailbox server - UM worker process)</p></td>
<td><p>Not applicable</p></td>
<td><p>Ports between 1024 and 65535.</p></td>
<td><p>Ports can be changed in the msexchangeum.config configuration file. The msexchangeum.config file is located in the \Program Files\Microsoft\Exchange\V15\bin folder on an Exchange 2013 Unified Messaging server.</p></td>
</tr>
</tbody>
</table>


## Lync Server and UM ports

Exchange 2013 Unified Messaging supports Network Address Translation (NAT) traversal and allows for the RTP media to a Mailbox server to be tunneled through a NAT firewall. However, for this to work, you must also have Microsoft Office Communications Server 2007 R2 and Microsoft Lync Server 2010 or Microsoft Lync 2013 deployed in your environment. If you deploy both Exchange 2013 and Communications Server 2007 R2 or Microsoft Lync Server 2010 or Lync 2013 on your network, this deployment will enable Mailbox servers running the Microsoft Exchange Unified Messaging service to communicate with endpoints outside a NAT firewall. The Mailbox server is associated with a Communications Server 2007 R2, Microsoft Lync Server 2010, or a Lync 2013 pool and obtains the appropriate authentication tokens from the A/V Authentication service on a computer serving that particular Communications Server 2007 or Lync Server pool.

The A/V Authentication service is used to allow RTP voice media to traverse NAT devices and firewalls. This is necessary because media gateways handle signaling only and cannot transport voice securely across a NAT device or firewall. When you configure a Mediation Server in Communications Server 2007 R2, Lync Server 2010, or Lync 2013, you specify the A/V Edge server on which the A/V Authentication service is running so that the Mediation Server will know where to forward the incoming media packets.

For more information about how to deploy Communications Server 2007 R2 or Lync Server 2010 or 2013 and Exchange 2013 Unified Messaging, see the following:

  - [Deploying Exchange 2013 UM and Lync Server overview](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Checklist: Integrate Exchange 2013 UM with Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)

