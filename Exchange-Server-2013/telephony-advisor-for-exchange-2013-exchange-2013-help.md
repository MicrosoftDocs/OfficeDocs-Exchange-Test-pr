---
title: 'Telephony advisor for Exchange 2013: Exchange 2013 Help'
TOCTitle: Telephony advisor for Exchange 2013
ms:assetid: e9f760f2-5901-4ed2-95a5-724555cc700e
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee364753(v=EXCHG.150)
ms:contentKeyID: 49315541
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Telephony advisor for Exchange 2013

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


Unified Messaging (UM) requires that you integrate Microsoft Exchange with the existing telephony system for your organization. A successful deployment requires you to make a careful analysis of your existing telephony infrastructure and to perform the correct planning steps to deploy Unified Messaging.

The planning phase can be a significant challenge to Exchange administrators who have little or no experience with a telephony network. To help address this challenge, see Resources to Help with Your UM Deployment later in this topic.

To see the supported VoIP gateways for Unified Messaging, determine whether your PBX is supported using a specific VoIP gateway model or manufacturer, whether your IP PBX is supported using a direct SIP connection, or to see supported session border controllers (SBCs) for Exchange Online UM, click one of the following links:

  - Supported VoIP gateways

  - Supported PBXs when using an AudioCodes VoIP gateway

  - Supported PBXs when using a dialogic VoIP gateway
    
      - PBXs supported when using a DMG1000 series Media Gateway
    
      - PBXs supported when using a DMG 2000 series Media Gateway
    
      - PBXs supported when using a DMG3000 series Media Gateway

  - Supported IP PBXs

  - Supported IP PBXs when using SIP media gateways

  - Exchange Unified Messaging, Office Communications Server 2007 R2, and Microsoft Lync Server

## Resources to help with your UM deployment

It's challenging to create guidelines for deploying telephony networks. They can be very different from one another because they can include VoIP gateways, IP PBXs, and PBXs with different configuration settings, firmware, and requirements. However, several resources are available to help you successfully deploy Unified Messaging:

  - **Unified Messaging specialists   **UM specialists are systems integrators who have received technical training about Exchange Unified Messaging conducted by the Exchange engineering team. To help ensure a smooth transition to Unified Messaging from legacy voice mail systems, Microsoft recommends that all customers engage a UM specialist. For contact information, visit [Microsoft Exchange Server 2013 Unified Messaging (UM) Specialists](http://go.microsoft.com/fwlink/p/?linkid=262708) or [Microsoft Pinpoint for Unified Messaging](https://go.microsoft.com/fwlink/p/?linkid=261951).

  - **Configuration Notes for Supported VoIP Gateways, IP PBXs and PBXs**   These configuration notes contain settings and other information that's very useful when you're configuring VoIP gateways, IP PBXs, and PBXs to communicate with the Unified Messaging servers that are on your network. For more information, see [Configuration notes for supported VoIP gateways, IP PBXs, and PBXs](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md).

  - **Configuration Notes for Supported Session Border Controllers**   These configuration notes contain settings and other information that's very useful when you're configuring session border controllers (SBCs) to communicate with the Unified Messaging servers in hybrid and Exchange Online UM deployments. For more information, see [Configuration notes for supported session border controllers](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md).
    

    > [!NOTE]
    > Exchange Online UM support for third-party PBX systems via direct connections from customer operated SBCs will end in July 2018. Please see the Exchange team blog <A href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">Discontinuation of support for session border controllers in Exchange Online unified messaging</A> for more information.



Before you engage a Unified Messaging specialist, you should be able to answer key questions that they'll ask. Having the answers to the following questions will help make the conversation between you and the UM specialist productive:

  - How many existing telephone or voice mail users, or both, are in your organization?

  - How many users do you intend to provide with Unified Messaging?

  - Which PBX or PBXs do you intend to use for integration with Unified Messaging?

  - How many PBXs does your organization have? Specify the vendors, types (circuit- or IP-based), models, and firmware versions.

  - Are the PBXs networked, and are they centralized or located in multiple locations?

  - What voice mail system or systems does your organization currently use? Specify the vendors, types, models, and firmware versions.

  - How are the voice mail systems integrated into your PBXs (Analog, T1/E1, PRI, Digital set emulation, VoIP, other)?

  - Are you currently using voice networking?

  - What type of fax system or systems does your organization use, and does the fax system or systems support inbound fax routing to Exchange?

  - Does your organization use automated attendants?

  - Do you need support for phone-only users, that is, users who won't have email access?

## Supported VoIP gateways

Integrating Unified Messaging with PBXs requires you to use one or more VoIP gateways to translate the circuit-switched protocols that are used by TDM-based PBXs to IP-based, packet-switched protocols that are used by Unified Messaging. VoIP gateway vendors with several models of VoIP and media gateways have been tested and are supported for Unified Messaging.

Interoperability testing of Unified Messaging with VoIP gateways, IP PBXs, and SBCs is now integrated with the Microsoft Unified Communications Open Interoperability Program. For more information, see [Microsoft Unified Communications Open Interoperability Program](http://go.microsoft.com/fwlink/p/?linkid=140722).

The [Microsoft Unified Communications Open Interoperability Program](http://go.microsoft.com/fwlink/p/?linkid=140722) qualification program for VoIP gateways, IP PBXs, and advanced VoIP gateways ensures that customers have a seamless setup and support experience when they're using qualified telephony VoIP gateways and IP PBXs with Microsoft Unified Communications software. Only products that meet rigorous and extensive testing requirements and conform to the specifications and test plans receive qualification.

For details about configuring supported VoIP gateways, IP PBXs, PBXs, and SBCs, see one of the following resources:

  - [Configuration notes for supported VoIP gateways, IP PBXs, and PBXs](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Configuration notes for supported session border controllers](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

Interoperability was verified for the following VoIP gateway vendors:

  - AudioCodes

  - Dialogic

  - The following table shows the VoIP gateway vendor, the VoIP gateway model, and the protocols that are supported by each model.

### Supported VoIP gateways for Unified Messaging

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Vendor</th>
<th>Model</th>
<th>Supported protocols</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>MediaPack 114/8 FXO</p></td>
<td><ul>
<li><p>Analog with In-Band DTMF</p></li>
<li><p>Analog with SMDI</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><ul>
<li><p>Analog with In-Band DTMF</p></li>
<li><p>Analog with SMDI</p></li>
<li><p>BRI Q.SIG</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP-to-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><ul>
<li><p>T1/E1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP-to-IP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG1000PBXDNIW</p></td>
<td><p>Digital Set Emulation</p></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG1000LSW</p></td>
<td><ul>
<li><p>Analog with In-Band DTMF</p></li>
<li><p>Analog with SMDI</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG2000</p></td>
<td><ul>
<li><p>T1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><ul>
<li><p>BRI Q.SIG</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NET</p></td>
<td><p>VX1200</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Sonus</p></td>
<td><p>SBC 1000/2000 2.2.1 or later</p></td>
<td><ul>
<li><p>TDM Signaling (ISDN): AT&amp;T 4ESS/5ESS, Nortel DMS- 100, Euro ISDN (ETSI 300-102), QSIG, NTT InsNet (Japan), ANSI National ISDN-2 (NI-2)</p></li>
<li><p>TDM Signaling (CAS): T1 CAS (E&amp;M, Loop start); E1 CAS (R2)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Quintum</p></td>
<td><p>Tenor DX Series</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Supported PBXs when using an AudioCodes VoIP gateway

The following table shows the PBXs that are supported using AudioCodes VoIP gateways, including MediaPack-114 FXO, MediaPack-118 FXO, and Mediant 2000.

### PBXs supported with an AudioCodes VoIP gateway

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX manufacturer</th>
<th>PBX model/type</th>
<th>AudioCodes model “x” - replace with 4 or 8 per need “y” - replace with 1, 2, 4, 8 or 16 per need</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>OmniPCX 4400</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Aastra</p></td>
<td><p>M1000, M2000</p></td>
<td><ul>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Magix/Merlin</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8300</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>S8700</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>IP Office</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>CallManager 4.x</p></td>
<td><ul>
<li><p>Mediant1000/IP-to-IP</p></li>
<li><p>Mediant2000/IP-to-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>Electra Elite</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>NEAX2400</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP/RS232</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NeXspan</p></td>
<td><p>S</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Communication Server-1000M, 1000S, 1000E</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridian 11c, 51c, 61c, 81c</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Panasonic</p></td>
<td><p>KX-TES824, KX-TEA308</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Panasonic</p></td>
<td><p>KX-TDA30, KX-TDA100, KX-TDA200, KX-TDA600</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Shortel</p></td>
<td><p>IP Telephony System</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 150E</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 3550</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Tadiran Telecom</p></td>
<td><p>Coral Flexicom, Coral IPX</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Supported PBXs when using a Dialogic VoIP gateway

Each Dialogic VoIP gateway model supports different PBXs. The following tables show the PBX manufacturer and model and which Dialogic VoIP gateway can be used. Each VoIP gateway uses different signaling methods, densities, and protocols.

## PBXs supported when using a DMG1000 series Media Gateway

The following table shows the PBXs that are supported with the low-density Dialogic Media Gateway (DMG1000). However, when an analog DMG1000 is used, supplemental signaling (RS232 SMDI, MD110, MCI protocols, or Inband DTMF signaling) is required.

### PBXs supported when using a low-density Dialogic DMG1000 series VoIP gateway

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX manufacturer</th>
<th>PBX model/type</th>
<th>DMG model and additional signaling</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>Aastra MD110 (formerly Ericsson MD110)</p></td>
<td><p>DMG1008LSW</p>
<p>Analog connectivity using the MD110 RS232 protocol</p></td>
</tr>
<tr class="even">
<td><p>Alcatel</p></td>
<td><p>Omni PCX 4400</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3 S8100, S8300, S8700, and S8710 (Communications Mgr SW V2.0 or later versions)</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Intercom</p></td>
<td><p> </p></td>
<td><p>DMG1008LSW</p>
<p>Analog connectivity using SMDI serial protocol</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>SX-200D, SX-200 Light, SX-2000 Light, SX-2000 S, SX-2000 VS, SX-200 ICP</p></td>
<td><p>DMG1008MTLDNIW</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2000, 2400, 2400 IPX</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridian 1 - Option 11, 21, 21A, 51, 61, 71, and 81</p>
<p>Meridian SL1 - Generic X11, Release 15 or later versions</p>
<p>Nortel Communication Server - 1000M, 1000S, 1000E with V3.0 or later versions</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>SL 100</p></td>
<td><p>DMG1008LSW</p>
<p>Analog connectivity using SMDI serial protocol</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E (European)</p></td>
<td><p>DMG1008LSW</p>
<p>Analog connectivity using Inband DTMF signaling</p></td>
</tr>
<tr class="odd">
<td><p>Siemens/ROLM</p></td>
<td><p>8000 (SW release 80003 or later versions)<br />
9000 (All versions)</p>
<p>9751 (All versions of SW release 9005)</p>
<p>9751 (SW release 9006.4 or later versions)</p></td>
<td><p>DMG1008RLMDNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Toshiba</p></td>
<td><p>CTX (SW version AR1ME021.00)</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="even">
<td><p>Others</p></td>
<td><p>Various</p></td>
<td><p>DMG1008LSW</p>
<p>Analog connectivity using either Inband DTMF or SMDI</p></td>
</tr>
</tbody>
</table>


## PBXs supported when using a DMG 2000 series Media Gateway

The following table shows the PBXs that are supported with the T1/E1 Dialogic Media Gateway (DMG2000). The DMG2000 gateway, which comes in single span (DMG2030DTIQ), dual span (DMG2060DTIQ), or quad span (DMG2120DTIQ) densities, supports the following protocols:

  - T1 CAS

  - T1 Q.SIG

  - E1 Q.SIG

  - T1 NI-2

  - T1 5ESS

  - T1 DMS100

If Channel Associated Signaling (CAS) signaling is used, supplemental signaling (RS232 SMDI, MD110, MCI protocols, or Inband DTMF signaling) is required. If Q.SIG signaling is used, the PBX must support the supplemental services that are associated with calling and called party information and the call transfer capabilities required by Unified Messaging.

### PBXs supported with the DMG2000 Media Gateway

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX manufacturer</th>
<th>PBX model/type</th>
<th>Required software version</th>
<th>Protocol and additional signaling</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>Omni PCX 4400</p></td>
<td><p>Version 3.2.712.5</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><p>Version 3 or later</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8500</p></td>
<td><p>Manager SW V2.0 or later versions</p></td>
<td><p>T1 CAS</p>
<p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Ericsson</p></td>
<td><p>MD110</p></td>
<td><p>Release MX1 TSW R2A (BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Intercom</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>CAS (w/ SMDI serial protocol)</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2400 IMX</p></td>
<td><p>Release 5200 Dec. 92 1b or later versions</p></td>
<td><p>CAS (w/ MCI serial protocol)</p></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>2400 IPX</p></td>
<td><p>R17 Release 03.46.001</p></td>
<td><p>T1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Meridian 1 - Option 11</p></td>
<td><p>Release 15 or later versions, and options 19 and 46 are required</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Communication Server 1000</p></td>
<td><p>Version 2121, Release 4</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>Release 9006.4 or later (Note: North American software load only)</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>V2 SMR 9 SMPO</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Mitel</p></td>
<td><p>SX-2000 S, SX-2000 VS</p></td>
<td><p>LW 34</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>3300</p></td>
<td><p>Version 5.1.4.8</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
</tbody>
</table>


## PBXs supported when using a DMG4008BRI series Media Gateway

The DMG4000 series Media Gateway comes with several TDM interface options. The DMG4008BRI supports 4-port/8-channel densities and supports the following protocols:

  - ISDN BRI Q.SIG

  - ETSI-DSS1 (Euro ISDN)

  - NET 3 (Belgium)

  - VN3 (France)

  - 1TR6 (Germany)

  - INS-64 (Japan)

  - 5ESS Custom (North America - AT\&T)

  - National ISDN (NI1 - North America)

The following table shows the PBXs that are supported using a Dialogic 4000 Media Gateway Series (DMG4008).

### PBXs supported using a DMG4008BRI Media Gateway

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX manufacturer</th>
<th>PBX model/type</th>
<th>Required software version</th>
<th>Protocol and additional signaling</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI-Q.SIG (ECMAV2)</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>S.0 B4400</p></td>
<td><p>BRI-Q.SIG (ECMAV2)</p></td>
</tr>
</tbody>
</table>


## Supported IP PBXs

IP PBXs are also supported by Unified Messaging. The following table shows the IP PBXs that are supported using a direct SIP connection to Unified Messaging.

### IP PBXs supported when using a direct SIP connection

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX manufacturer</th>
<th>PBX model/type</th>
<th>Required software version</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>MX-ONE</p></td>
<td><p>4.0</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Aura</p></td>
<td><p>5.2.1 with Service Pack 5 (SP5)</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Communication Server 2100</p></td>
<td><p>CS2100 SE13</p></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>Call Manager, Unified Communications Manager</p></td>
<td><p>5.1, 6.x, 7.0 and8.0</p></td>
</tr>
</tbody>
</table>


## IP PBXs supported when using SIP media gateways

IP PBXs using SIP media gateways are also supported by Unified Messaging. The following table shows the IP PBXs that are supported using IP to IP capabilities of SIP media gateways to connect to Unified Messaging.

### IP PBXs supported when using a SIP media gateway

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX manufacturer</th>
<th>PBX model/type</th>
<th>SIP gateway model</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco</p></td>
<td><p>Call Manager 4.x</p></td>
<td><p>AudioCodes Mediant 1000/2000 (IP-to-IP enabled)</p></td>
</tr>
</tbody>
</table>


## Exchange Unified Messaging, Office Communications Server 2007 R2, and Microsoft Lync Server

For on-premises and hybrid deployments, Exchange Unified Messaging can be deployed together with Microsoft Office Communications Server 2007 R2, Microsoft Lync Server 2010 or Lync Server 2013 to provide voice messaging, Instant Messaging (IM), enhanced user presence, audio-video conferencing, and an integrated email and messaging experience for users in your organization. For more information, see:

  - [Deploying Exchange 2013 UM and Lync Server overview](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=202010)

To find out more about the Microsoft Unified Communications Open Interoperability Program for enterprise telephony infrastructure, including finding qualified SIP PSTN gateways and IP PBXs and the process for telephony infrastructure vendors to join and participate in the program, see [Microsoft Unified Communications Open Interoperability Program](https://go.microsoft.com/fwlink/p/?linkid=132071).

