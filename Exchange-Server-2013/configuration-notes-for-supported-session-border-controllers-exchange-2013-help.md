---
title: 'Configuration notes for supported session border controllers: Exchange 2013 Help'
TOCTitle: Configuration notes for supported session border controllers
ms:assetid: d161f94a-a243-4294-93b3-2bf1dc17b59f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673565(v=EXCHG.150)
ms:contentKeyID: 49315528
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configuration notes for supported session border controllers

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


Session border controllers (SBCs) enable you to connect your on-premises telephony network to a Microsoft datacenter over a dedicated public WAN connection. An SBC sits on the edge of your on-premises IP network and connects to a second SBC in a Microsoft datacenter.

SBCs require the use of digital certificates to encrypt all traffic between your on-premises organization and the Microsoft datacenter. You must obtain a digital certificate for the network border element, such as a session border controller, that you’re using to communicate with Exchange hybrid and online deployments. Digital certificates establish trust between your on-premises organization and the Microsoft datacenter and enable mutual Transport Layer Security (mutual TLS). After this trust is established, the network border elements at your on-premises organization and at the Microsoft datacenter exchange session keys, and use these keys to encrypt the subsequent data traffic.

In hybrid or online deployments, a UM IP gateway represents an SBC. The subject common name in the certificate must match the fully qualified domain name (FQDN) value in the Address box on the UM IP gateway that you create. For example, if you specify the FQDN address sbcexternal.contoso.com on your UM IP gateway, make sure that the subject name and subject alternative name in the certificate contain the same value: sbcexternal.contoso.com. The name that you use is case-sensitive, so make sure the case is the same on both the certificate and the UM IP gateway. If you’re using an Acme Packet SBC and the common name doesn’t match the UM IP gateway’s FQDN, the call will be rejected with a 403 error.


> [!NOTE]
> Because SBCs are designed to sit on the network edge, they also function as a firewall. If you set up an SBC behind your organization’s firewall, it can cause configuration problems and is unsupported for connecting to Office 365.



## Supported session border controllers

The following SBCs have been successfully tested for interoperability with Exchange hybrid and online deployments. Note that the capabilities and compatibilities of SBCs can vary, and the way you set them up can be different depending on other equipment on your network. Consult with the SBC manufacturer to see whether there are specific configuration notes for Unified Messaging in a hybrid or online deployment.


> [!NOTE]
> Exchange Online UM support for third-party PBX systems via direct connections from customer operated SBCs will end in July 2018. Please see the Exchange team blog <A href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">Discontinuation of support for session border controllers in Exchange Online unified messaging</A> for more information.




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Vendor</strong></p></td>
<td><p><strong>Model</strong></p></td>
<td><p><strong>Configuration notes</strong></p></td>
<td><p><strong>Comments</strong></p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.acmepacket.com">Acme Packet</a></p></td>
<td><p>Net-Net 3820 or 4500</p></td>
<td><p><strong>Please contact the hardware vendor for up to date instructions on how to set up their device.</strong></p></td>
<td><p>Dedicated SBC</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>Please contact the hardware vendor for up to date instructions on how to set up their device.</strong></p></td>
<td><p>Dedicated SBC</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>Please contact the hardware vendor for up to date instructions on how to set up their device.</strong></p></td>
<td><p>SBC and IP gateway</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.cisco.com/c/dam/en/us/solutions/collateral/enterprise-networks/unified-access/cube-asr-release-10-0.pdf">Cisco</a></p></td>
<td><p>ASR 1000</p>

> [!NOTE]
> Must have IOS 15.4(3)S3 or later installed.


</td>
<td><p><strong>Please contact the hardware vendor for up to date instructions on how to set up their device.</strong></p></td>
<td><p>Dedicated SBC</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.ingate.com/">Ingate</a></p></td>
<td><p>SIParator</p></td>
<td><p><strong>Please contact the hardware vendor for up to date instructions on how to set up their device.</strong></p></td>
<td><p>Dedicated SBC</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.net.com">NET</a></p></td>
<td><p>VX1200 &amp; VX1800</p></td>
<td><p><strong>Please contact the hardware vendor for up to date instructions on how to set up their device.</strong></p></td>
<td><p>SBC option for a VoIP gateway product</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.sonus.net/">Sonus</a></p></td>
<td><p>SBC 1000/2000 2.2.1 or later</p></td>
<td><p><strong>Please contact the hardware vendor for up to date instructions on how to set up their device.</strong></p></td>
<td><p>Dedicated SBC</p></td>
</tr>
</tbody>
</table>

