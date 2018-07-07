---
title: 'Coexistence with Office Communications Server 2007 R2 and Lync Server: Exchange 2013 Help'
TOCTitle: Coexistence with Office Communications Server 2007 R2 and Lync Server
ms:assetid: f12d65c7-0b2c-46a1-a14a-802a76296fa1
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ851069(v=EXCHG.150)
ms:contentKeyID: 50067637
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Coexistence with Office Communications Server 2007 R2 and Lync Server

 

_**Applies to:** Exchange Server 2013_


Communications Server 2007 R2 and Lync Server provide many end-user features, including instant messaging (IM), presence, multiparty IM, and their voice mail functionality can be integrated with Exchange Unified Messaging (UM). For deployments that integrate Lync Server 2010 or 2013, users can be enabled for Enterprise Voice, which lets users who are enabled for voice mail access their voice mail by using Lync Server components.

When you integrate UM with the earlier versions of Office Communications Server or Lync Server, not all features are available. For users to take full advantage of the new enhanced end-user features such as high-resolution photos, the unified contact store, and Lync Archiving Integration, they must have user accounts on Lync Server 2013 and Exchange Server 2013, and must be using the latest version of the Lync 2013 client software. For example, the unified contact store isn’t available to users who’ve been enabled for Enterprise Voice on Lync Server 2010. Also, high-resolution photos can’t be displayed in Lync 2010.

When you’re integrating Exchange UM with Office Communications Server 2007 R2 or Lync Server 2010, you may need to install additional hotfixes, rollups, cumulative updates, and service packs on the Office Communications Server 2007 R2 or Lync 2010 servers that have been deployed in your organization. What you’re required to install will depend on your deployment topology and the product versions you’re integrating with Exchange UM.

## Required hotfixes, rollups, cumulative updates, and service packs

The following table shows the fixes that are required for each version of the products for integration with UM.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>Office Communications Server 2007 R2 cumulative update 10 or later.</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2010</p></td>
<td><p>Lync Server 2010 cumulative update 3 or later.</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p>No updates are required.</p></td>
</tr>
</tbody>
</table>

