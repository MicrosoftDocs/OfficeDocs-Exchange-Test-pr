---
title: 'Voice architecture changes: Exchange 2013 Help'
TOCTitle: Voice architecture changes
ms:assetid: 55d5ca4a-b0cd-45f1-9f47-e745ef208698
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150516(v=EXCHG.150)
ms:contentKeyID: 47560002
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Voice architecture changes

 

_**Applies to:** Exchange Server 2013_


The Microsoft Exchange Server 2013 architecture is different than the architecture in Exchange Server 2007 and Exchange Server 2010. In Exchange 2007 and Exchange 2010, the types of servers were separated into multiple server roles: Client Access, Mailbox, Hub Transport, and Unified Messaging. In Exchange 2013, the server roles are combined into two types of servers, and all components or services from those server roles are run on the same physical server or on two separate servers called Client Access and Mailbox. In the new model, the Client Access server running the Microsoft Exchange Unified Messaging Call Router service redirects Session Initialization Protocol (SIP) traffic that’s generated from an incoming call to a Mailbox server. Then a media (Realtime Transport Protocol (RTP) or secure RTP (SRTP)) channel is established from the VoIP gateway or IP Private Branch eXchange (PBX) to the Mailbox server that hosts the user’s mailbox. In Exchange 2013, the Mailbox server has the same processes as the Unified Messaging server role in Exchange 2007 and Exchange 2010. The Mailbox server runs both the Microsoft Exchange Unified Messaging service and UM worker processes. The Client Access server runs the Microsoft Exchange Unified Messaging Call Router service, which receives an incoming call and forwards it to the Mailbox server.

**Contents**

Support for the new Exchange architecture

UM ports

UM dial plans

UM Call Router performance counters

## Support for the new Exchange architecture

In Exchange 2013, the Client Access server is responsible for Autodiscover, Secure Sockets Layer (SSL), authentication, redirection, and proxy. The Client Access server is the entry point for any inbound calls or SIP requests for Unified Messaging (UM). The routing logic and SIP REDIRECT is implemented as a service that’s automatically included in a Client Access server. This service is known as the Microsoft Exchange Unified Messaging Call Router service. It’s installed and runs on each Client Access server in your organization. When a Client Access server receives a SIP INVITE for an incoming call, the Microsoft Exchange Unified Messaging Call Router service redirects the incoming call to the Mailbox server. Then a media channel (RTP or SRTP) is created between the VoIP gateway, IP PBX, or session border controller (SBC) and the Mailbox server. Although the Client Access server acts as a SIP redirector, it only handles SIP requests from VoIP gateways, IP PBXs, or SBCs. It doesn’t receive any media traffic. Media traffic that uses RTP or SRTP is only passed between the Mailbox server and SIP peers such as VoIP gateways, IP PBXs, or SBCs—not to the Client Access server. When you deploy Exchange 2013 and UM, you have to configure your VoIP gateways, IP PBXs, or SBCs to point to the Client Access servers that you’ve installed so that incoming calls will be routed correctly for UM.

In some cases, deploying multiple Client Access servers is a requirement, and the Client Access servers are deployed separately on different physical hardware from the Mailbox servers. Client Access servers can be grouped in an array by using an L4 or L5 hardware or software load balancer. However, there are no Active Directory Exchange object-based Client Access server arrays. Using a hardware or software load balancer in front of Client Access servers is an accepted practice in larger Exchange deployments.

When a Client Access server is installed, the Microsoft Exchange Unified Messaging Call Router service is running. The service does the following:

  - When initialized, it reads a local configuration file named msexchangeumcallrouter.config.

  - Performs speech grammar generation using an arbitration mailbox for an organization.

  - Supports Transmission Control Protocol (TCP) and/or Transport Layer Security (TLS) connections. This setting is configurable.

  - Will only stop if there’s a configuration error or if it can’t register the required ports.

In Exchange 2013, the Mailbox server isn’t responsible for answering SIP requests from incoming calls. It’s only responsible for receiving the SIP traffic from a Client Access server and then establishing an RTP or SRTP connection to the VoIP gateway, IP PBX, or SBC.

After a Client Access server redirects an incoming call to a Mailbox server, a media channel is established between the VoIP gateway, IP PBX, or SBC and the Mailbox server. After the media channel is established, the Microsoft Exchange Unified Messaging service on the Mailbox server plays the user’s voice mail greeting, processes call answering rules for the user, and invites the caller to leave a voice message. The Mailbox server then records the voice message, creates a transcription of the message, and deposits it in the user’s mailbox. However, if you’re integrating Exchange with Office Communications Server 2007 R2 or Lync Server, both the SIP and RTP or SRTP media channels for incoming calls are handled by Lync servers and the Mailbox server. In a Lync integrated environment, you don’t have VoIP gateways, IP PBXs, or SBCs. To Lync, the Mailbox server that’s running the Microsoft Exchange Unified Messaging service looks just like an Exchange 2010 UM server. The Mailbox server and the Client Access server that’s running the Microsoft Exchange Unified Messaging Call Router service are considered trusted peers because both servers must be added to a SIP dial plan. Lync routes the incoming call using the Inbound Routing component, which uses SIP to communicate with the Client Access server and then route the call to a Mailbox server.

Exchange 2010 UM administrators can configure a set of properties for Unified Messaging on each UM server. In Exchange 2013, UM components and configuration settings for UM are found on both Client Access and Mailbox servers. All the configuration settings that applied to a single computer running the Unified Messaging server role in Exchange 2010 are still available. However, some of those properties and configuration settings are set on a Client Access server that’s running the Microsoft Exchange Unified Messaging Call Router service, and others are available on a Mailbox server that’s running the Microsoft Exchange Unified Messaging service. In some cases, the same setting is available on both. The following list shows the cmdlets and parameters that are available on Client Access servers and Mailbox servers and where changes were made to a cmdlet to support deployment scenarios with previous versions of Unified Messaging.

  - **Set-UMService -DialPlans \<MultiValuedProperty\>**    Available on Exchange 2013 Mailbox servers and also works on Exchange 2007 and Exchange 2010 Unified Messaging servers.

  - **Set-UMCallRouterSettings -DialPlans \<MultiValuedProperty\>**    Available on Exchange 2013 Client Access servers but not available for Exchange 2007 and Exchange 2010 Unified Messaging servers.

  - **Set-UMService -MaxCallsAllowed \<Int32\>**    Available on Exchange 2013 Mailbox servers and also works on Exchange 2007 and Exchange 2010 Unified Messaging servers.

  - **Set-UMCallRouterSettings -MaxCallsAllowed \<Int32\>**   Not available on Exchange 2013 Client Access servers and not available for Exchange 2007 and Exchange 2010 Unified Messaging servers.

  - **Set-UMService -SipTcpListeningPort \<Int32\>**    Not configurable on Exchange 2013 Mailbox servers but works on Exchange 2007 and Exchange 2010 Unified Messaging servers.

  - **Set-UMService -SipTlsListeningPort \<Int32\>**   Not configurable on Exchange 2013 Mailbox servers but works on Exchange 2007 and Exchange 2010 Unified Messaging servers.

  - **Set-UMCallRouterSettings -SipTcpListeningPort \<Int32\>**    Available on Exchange 2013 Client Access servers but doesn’t work on Exchange 2007 and Exchange 2010 Unified Messaging servers.

  - **Set-UMCallRouterSettings -SipTlsListeningPort \<Int32\>**   Available on Exchange 2013 Client Access servers but doesn’t work on Exchange 2007 and Exchange 2010 Unified Messaging servers.

  - **Set-UMService - Status \<Enabled | Disabled | NoNewCalls\>**   Not available on Exchange 2013 Mailbox servers but works on Exchange 2007 and Exchange 2010 Unified Messaging servers.

  - **Set-UMCallRouterSettings - Status \<Enabled | Disabled | NoNewCalls\>**    Not available on Exchange 2013 Client Access servers and doesn’t work on Exchange 2007 and Exchange 2010 Unified Messaging servers.

  - **Set-UMService -UMStartupMode \<TCP | TLS | Dual\>**   Available on Exchange 2013 Mailbox servers and works on Exchange 2007 and Exchange 2010 Unified Messaging servers.

  - **Set-UMCallRouterSettings - UMStartupMode \<TCP | TLS | Dual\>**    Available on Exchange 2013 Client Access servers but doesn’t work on Exchange 2007 and Exchange 2010 Unified Messaging servers.

  - **Enable-UMService**    Not available on Exchange 2013 Mailbox servers but works on Exchange 2007 and Exchange 2010 Unified Messaging servers.

  - **Disable-UMService**    Not available on Exchange 2013 Mailbox servers but works on Exchange 2007 and Exchange 2010 Unified Messaging servers.

For the Mailbox server, you’ll use the **Set/Get/Enable/Disable-UMService** cmdlets to view or configure UM properties for the Microsoft Exchange Unified Messaging service on Exchange 2013 Mailbox servers or Exchange 2007 or Exchange 2010 Unified Messaging servers. A different set of cmdlets, **Set/Get-UMCallRouterSettings**, are used to view or configure the Microsoft Exchange Unified Messaging Call Router service properties on a Client Access server. This ensures that the existing **Get-UMServer**, **Set-UMServer**, **Enable-UMServer**, and **Disable-UMServer** cmdlets from Exchange 2007 and Exchange 2010 will work in a coexistence deployment with Exchange 2013 Mailbox servers. This also ensures that the cmdlets will work when the Mailbox and Client Access servers are installed on the same or different servers.

Return to top

## UM ports

The Microsoft Exchange Unified Messaging Call Router service found on a Client Access server uses SIP over either Transmission Control Protocol (TCP) or mutual Transport Layer Security (mutual TLS) to communicate with Mailbox servers that are running the Microsoft Exchange Unified Messaging service. To avoid TCP/User Datagram Protocol (UDP) port conflicts, the Microsoft Exchange Unified Messaging Call Router service and the Microsoft Exchange Unified Messaging service default to and listen on different TCP ports. They can accept both unsecured and secured connections, depending on whether mutual TLS is used with SIP and RTP traffic. By default, a Client Access server listens for SIP requests on both TCP port 5060 in Unsecured mode and TCP port 5061 in SIP Secured mode when mutual TLS is used. These ports are configurable using the **Set-UMCallRouterSettings** cmdlet. The Microsoft Exchange Unified Messaging Call Router service on the Client Access server doesn’t handle media (RTP or SRTP) traffic, so only TCP ports and no UDP ports are used. By default, a Mailbox server listens for SIP requests on both TCP port 5062 in Unsecured mode and TCP port 5063 in SIP Secured mode when mutual TLS is used. These ports aren’t configurable using Exchange Management Shell cmdlets. On the Mailbox server that runs the Microsoft Exchange Unified Messaging service, TCP ports can’t be configured on the Exchange server either by using the Shell or by configuring settings in the registry. The Microsoft Exchange Unified Messaging service on the Mailbox server will accept connections from a Client Access server on SIP ports 5062 and 5063. After the Client Access server redirects the SIP request to a Mailbox server, an RTP or SRTP media channel is created using a VoIP gateway, IP PBX, or SBC, and the Microsoft Exchange Unified Messaging worker process on the Mailbox server.

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
<td><p>SIP (Client Access server – Microsoft Exchange Unified Messaging Call Router service)</p></td>
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
<td><p>5065 and 5067 for TCP (unsecured). 5066 and 5068 for mutual TLS (secured). This is the case when <em>UMStartupMode</em> is set to <em>Dual</em>. If <em>UMStartUpMode</em> is set to <em>TCP</em> or <em>TLS</em>, ports 5065 and 5066 are used. The default <em>UMStartupMode</em> is <em>TCP</em>.</p></td>
<td><p>Not applicable</p></td>
<td><p>Ports can’t be changed.</p></td>
</tr>
<tr class="even">
<td><p>RTP (Mailbox server - UM worker process)</p></td>
<td><p>Not applicable</p></td>
<td><p>Ports between 1024 and 65535.</p></td>
<td><p>The range of ports can be changed through the registry (however, this isn’t a supported configuration):</p>
<p>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMinPort</p>
<p>HKLM\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMaxPort</p></td>
</tr>
</tbody>
</table>


Return to top

## UM dial plans

Mapping or associating UM dial plans to UM servers isn’t required in Exchange 2013 the way it was in Exchange 2007 and Exchange 2010. Client Access or Mailbox servers running UM services don’t need to be linked to a dial plan because all Client Access and Mailbox servers are expected to receive all incoming calls from VoIP gateways, IP PBXs, or SBCs. The exception is that SIP dial plans that are used with Lync 2013, Lync Server 2010, and Office Communications Server 2007 R2 must be associated with Client Access and Mailbox servers that you’ve deployed. Both types of Exchange servers must be added to each SIP dial plan to be included as trusted peers from Communications Server 2007 R2 or Lync Server. Otherwise, Communications Server 2007 R2 or Lync Server will reject outbound calls from users.

The following table summarizes the relationship between Client Access and Mailbox servers and UM dial plans.

### Linking UM dial plans

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Topology</th>
<th>Dial plan</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client Access and Mailbox on the same server (without Communications Server 2007 R2 or Lync Server 2010 non-SIP dial plans)</p></td>
<td><p>Dial plans are no longer required to be associated with a Client Access or Mailbox server. You aren’t allowed to add the Client Access or Mailbox servers to a dial plan. If you run the <strong>Set-UMService</strong> cmdlet, it will generate an error if you try to associate a Mailbox server with a non-SIP dial plan.</p></td>
</tr>
<tr class="even">
<td><p>Client Access and Mailbox on different servers (without Communications Server 2007 R2 or Lync Server 2010 non-SIP dial plans)</p></td>
<td><p>Dial plans are no longer required to be associated with Client Access or Mailbox servers. You aren’t allowed to add Client Access or Mailbox servers to a dial plan. If you run the <strong>Set-UMService</strong> cmdlet, it will generate an error if you try to associate a Mailbox server with a non-SIP dial plan.</p></td>
</tr>
<tr class="odd">
<td><p>Client Access and Mailbox server on the same physical server (with Communications Server 2007 R2 and Lync Server 2010 with SIP dial plans)</p></td>
<td><p>For a single SIP dial plan, add all Client Access and Mailbox servers to the SIP dial plan. For multiple SIP dial plans, add all Client Access and Mailbox servers to each SIP dial plan. This will make both servers trusted peers of Office Communications Server 2007 R2 or Lync Server. You must use the same certificate in your Office Communications Server 2007 R2 or Lync Server deployment as you do on each Client Access and Mailbox server.</p></td>
</tr>
<tr class="even">
<td><p>Client Access and Mailbox server on different physical servers (with Communications Server 2007 R2 and Lync Server 2010 with SIP dial plans)</p></td>
<td><p>For a single SIP dial plan, add all Client Access and Mailbox servers to the SIP dial plan. For multiple SIP dial plans, add all Client Access and Mailbox servers to each SIP dial plan. This will make both servers trusted peers of Office Communications Server 2007 R2 or Lync Server. If the certificates being used on the Client Access and Mailbox servers are different, you must use the same certificate in your Office Communications Server 2007 R2 or Lync Server deployment as you do on each Client Access and Mailbox server in your organization.</p></td>
</tr>
</tbody>
</table>


Return to top

## UM Call Router performance counters

Past versions of Exchange included the Unified Messaging server role, which ran the Microsoft Exchange Unified Messaging service. Because of the architecture changes in Exchange 2013, the Client Access server runs the Microsoft Exchange Unified Messaging Call Router service and the Mailbox server runs the Microsoft Exchange Unified Messaging service. The same performance counters for the Microsoft Exchange Unified Messaging service are available to administrators as in earlier versions of Exchange UM. However, there are also additional performance counters that you can use on the Client Access server to verify the status of the Microsoft Exchange Unified Messaging Call Router service and for troubleshooting.

To support the new Client Access Unified Messaging Call Router service in Exchange 2013, the following performance counters are now available.

### Performance counters

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Performance counter category</th>
<th>Counter name</th>
<th>Description</th>
<th>Threshold</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>% of Inbound Calls Rejected by the Microsoft Exchange Unified Messaging Call Router Service over the Last Hour</p></td>
<td><p>Shows the percentage of inbound calls that were rejected by the Microsoft Exchange Unified Messaging Call router service over the last hour.</p></td>
<td><p>Should always be less than 5 percent, but should be 0 at all times.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Calls Disconnected on Irrecoverable Internal Error for the Microsoft Exchange Unified Messaging Call Router Service</p></td>
<td><p>Shows the number of calls disconnected after an internal system error occurred.</p></td>
<td><p>Should be 0 at all times.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Total Inbound Calls Rejected by the Microsoft Exchange Unified Messaging Call Router Service</p></td>
<td><p>Shows the total number of inbound calls that were rejected by the Microsoft Exchange Unified Messaging Call Router service since the service was started.</p></td>
<td><p>Should be 0 at all times.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Total number of calls received by the Microsoft Exchange Unified Messaging Call Router Service</p></td>
<td><p>Shows the total number of inbound calls that were received by the Microsoft Exchange Unified Messaging Call Router service since the service was started.</p></td>
<td><p>Should be 0 or greater.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>% of Inbound Calls Rejected by the Microsoft Exchange Unified Messaging Call Router Service Over the Last Hour</p></td>
<td><p>Shows the percentage of inbound calls that were rejected by the Microsoft Exchange Unified Messaging Call Router service over the last hour.</p></td>
<td><p>Should be less than 5 percent.</p></td>
</tr>
</tbody>
</table>


Return to top

