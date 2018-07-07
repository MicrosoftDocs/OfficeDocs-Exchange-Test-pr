---
title: 'Trusted root certification authorities for federation trusts: Exchange 2013 Help'
TOCTitle: Trusted root certification authorities for federation trusts
ms:assetid: d4224bf5-69b3-484c-8a70-4f230d3dbdd9
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee332350(v=EXCHG.150)
ms:contentKeyID: 48385572
ms.date: 07/26/2017
mtps_version: v=EXCHG.150
---

# Trusted root certification authorities for federation trusts

 

_**Applies to:** Exchange Server 2013_


To establish a federation trust between your Microsoft Exchange Server 2013 organization and the [Azure Active Directory authentication system](https://go.microsoft.com/fwlink/p/?linkid=135986), you need a digital certificate installed on the Exchange server used to create the trust. We strongly recommend using a self-signed certificate. A self-signed certificate is created and installed automatically when using the **Enable federation trust** wizard in the Exchange admin center (EAC).

If you don't want to use the recommended self-signed certificate, you should request and install an X.509 Secure Sockets Layer (SSL) certificate from a certification authority (CA) trusted by Microsoft. Although certificates issued by other CAs may also be used to establish a federation trust with the Azure AD authentication system, they aren't certified by Microsoft to date.

The following table lists CAs currently trusted Microsoft. These CAs have been tested for use with Exchange 2013.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>CA friendly name</th>
<th>Issued by</th>
<th>Intended purposes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>Server authentication, client authentication</p></td>
</tr>
<tr class="even">
<td><p>Comodo</p></td>
<td><p>Comodo Certification Authority</p></td>
<td><p>Server authentication, client authentication</p></td>
</tr>
<tr class="odd">
<td><p>CyberTrust</p></td>
<td><p>Baltimore CyberTrust Root Certificate Authority</p></td>
<td><p>Server authentication, client authentication</p></td>
</tr>
<tr class="even">
<td><p>Digicert</p></td>
<td><p>Digicert Global Root Certification Authority</p></td>
<td><p>‎Server authentication, client authentication</p></td>
</tr>
<tr class="odd">
<td><p>Digicert High Assurance EV</p></td>
<td><p>Digicert Global Root Certification Authority</p></td>
<td><p>‎Server authentication, client authentication</p></td>
</tr>
<tr class="even">
<td><p>Entrust</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>Server authentication, client authentication</p></td>
</tr>
<tr class="odd">
<td><p>Entrust (2048)</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>Server authentication, client authentication</p></td>
</tr>
<tr class="even">
<td><p>Equifax</p></td>
<td><p>Equifax Secure Certification Authority</p></td>
<td><p>‎‎Server authentication, client authentication</p></td>
</tr>
<tr class="odd">
<td><p>GlobalSign</p></td>
<td><p>GlobalSign Certification Authority</p></td>
<td><p>‎Server authentication, client authentication</p></td>
</tr>
<tr class="even">
<td><p>Go Daddy</p></td>
<td><p>Go Daddy Class 2 Certification Authority</p></td>
<td><p>‎Server authentication, client authentication</p></td>
</tr>
<tr class="odd">
<td><p>Network Solutions</p></td>
<td><p>Network Solutions Certification Authority</p></td>
<td><p>Server authentication, client authentication</p></td>
</tr>
<tr class="even">
<td><p>PositiveSSL</p></td>
<td><p>Comodo Certification Authority</p></td>
<td><p>‎Server authentication, client authentication</p></td>
</tr>
<tr class="odd">
<td><p>SECOM</p></td>
<td><p>SECOM Trust Systems Certification Authority</p></td>
<td><p>‎Server authentication, client authentication</p></td>
</tr>
<tr class="even">
<td><p>UTN-UserFirst-Hardware</p></td>
<td><p>Comodo Certification Authority</p></td>
<td><p>Server authentication, client authentication</p></td>
</tr>
<tr class="odd">
<td><p>VeriSign</p></td>
<td><p>Class 3 Public Primary Certification Authority</p></td>
<td><p>Server authentication, client authentication</p></td>
</tr>
<tr class="even">
<td><p>VeriSign</p></td>
<td><p>VeriSign Trust Network</p></td>
<td><p>‎Server authentication, client authentication</p></td>
</tr>
</tbody>
</table>


For more information about certificate requirements for Federation, see [Federation](federation-exchange-2013-help.md).

