---
title: 'Default settings for Exchange virtual directories: Exchange 2013 Help'
TOCTitle: Default settings for Exchange virtual directories
ms:assetid: d2d89ce6-4721-4737-a325-fba5ad9422e0
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Gg247612(v=EXCHG.150)
ms:contentKeyID: 50934224
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Default settings for Exchange virtual directories

 

_**Applies to:** Exchange Server 2013_


Exchange Server 2013 automatically configures multiple Internet Information Services (IIS) virtual directories during installation. This topic contains information about the default IIS authentication settings and default Secure Sockets Layer (SSL) settings for the Client Access and Mailbox servers.

## Client Access server

The following table lists the default settings on a stand-alone Exchange 2013 Client Access server.

### Default Client Access server IIS authentication and SSL settings

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Virtual directory</th>
<th>Authentication method</th>
<th>SSL settings</th>
<th>Management method</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Default website</p></td>
<td><ul>
<li><p>Anonymous</p></li>
</ul></td>
<td><ul>
<li><p>Required</p></li>
</ul></td>
<td><p>IIS management console</p></td>
</tr>
<tr class="even">
<td><p>aspnet_client</p></td>
<td><ul>
<li><p>Anonymous authentication</p></li>
</ul></td>
<td><ul>
<li><p>SSL required</p></li>
<li><p>Requires 128-bit encryption</p></li>
</ul></td>
<td><p>IIS management console</p></td>
</tr>
<tr class="odd">
<td><p>Autodiscover</p></td>
<td><ul>
<li><p>Anonymous authentication</p></li>
<li><p>Basic authentication</p></li>
<li><p>Windows authentication</p></li>
</ul></td>
<td><ul>
<li><p>SSL required</p></li>
<li><p>Requires 128-bit encryption</p></li>
</ul></td>
<td><p>Exchange Management Shell (Shell)</p></td>
</tr>
<tr class="even">
<td><p>ecp</p></td>
<td><ul>
<li><p>Anonymous authentication</p></li>
<li><p>Basic authentication</p></li>
</ul></td>
<td><ul>
<li><p>SSL required</p></li>
<li><p>Requires 128-bit encryption</p></li>
</ul></td>
<td><p>Exchange admin center (EAC) or Shell</p></td>
</tr>
<tr class="odd">
<td><p>EWS</p></td>
<td><ul>
<li><p>Anonymous authentication</p></li>
<li><p>Windows authentication</p></li>
</ul></td>
<td><ul>
<li><p>SSL required</p></li>
<li><p>Requires 128-bit encryption</p></li>
</ul></td>
<td><p>Shell</p></td>
</tr>
<tr class="even">
<td><p>Microsoft-Server-ActiveSync</p></td>
<td><ul>
<li><p>Basic authentication</p></li>
</ul></td>
<td><ul>
<li><p>SSL required</p></li>
<li><p>Requires 128-bit encryption</p></li>
</ul></td>
<td><p>EAC or Shell</p></td>
</tr>
<tr class="odd">
<td><p>OAB</p></td>
<td><ul>
<li><p>Windows authentication</p></li>
</ul></td>
<td><ul>
<li><p>Not required</p></li>
</ul></td>
<td><p>EAC or Shell</p></td>
</tr>
<tr class="even">
<td><p>owa</p></td>
<td><ul>
<li><p>Basic authentication</p></li>
</ul></td>
<td><ul>
<li><p>SSL required</p></li>
<li><p>Requires 128-bit encryption</p></li>
</ul></td>
<td><p>EAC or Shell</p></td>
</tr>
<tr class="odd">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>Anonymous authentication</p></li>
</ul></td>
<td><ul>
<li><p>Not required</p></li>
</ul></td>
<td><p>Shell</p></td>
</tr>
<tr class="even">
<td><p>Rpc</p></td>
<td><ul>
<li><p>Basic authentication</p></li>
<li><p>Windows authentication</p></li>
</ul></td>
<td><ul>
<li><p>SSL required</p></li>
<li><p>Requires 128-bit encryption</p></li>
</ul></td>
<td><p>Shell</p></td>
</tr>
<tr class="odd">
<td><p>RpcWithCert</p></td>
<td><p>By default, all authentication methods are disabled.</p></td>
<td><ul>
<li><p>Required</p></li>
</ul></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


## Mailbox server

The following table lists the default settings on a stand-alone Exchange 2013 Mailbox server.

### Default Mailbox server IIS authentication and SSL settings

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Virtual directory</th>
<th>Authentication method</th>
<th>SSL settings</th>
<th>Management method</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Default website</p></td>
<td><ul>
<li><p>Anonymous authentication</p></li>
</ul></td>
<td><ul>
<li><p>SSL required</p></li>
<li><p>Requires 128-bit encryption</p></li>
</ul></td>
<td><p>This virtual directory can’t be configured by the user.</p></td>
</tr>
<tr class="even">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>Anonymous authentication</p></li>
</ul></td>
<td><ul>
<li><p>Not required</p></li>
</ul></td>
<td><p>Shell</p></td>
</tr>
</tbody>
</table>

