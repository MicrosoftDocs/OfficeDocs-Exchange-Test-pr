---
title: 'Azure: Help Identify My issue with Automatic Checks - DNS Records: Exchange 2013 Help'
TOCTitle: 'Azure: Help Identify My issue with Automatic Checks - DNS Records'
ms:assetid: 1ef42cde-4df4-401a-b8f2-494630996ca8
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn793619(v=EXCHG.150)
ms:contentKeyID: 62631020
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Azure: Help Identify My issue with Automatic Checks - DNS Records

 

_**Applies to:** Exchange Server 2013_


One of the most common configuration setup issues is incorrectly configuring DNS records. You can use the automatic checks listed below to validate your configuration and help you update your environment.

If you already have an Office 365 user account, select Sign In. You don’t need an Azure ID account. You might be asked for a user account again when the checks run. If so, your user account is in the format of username@youroffice365login.domain and your password.

## Prerequisites

We’ll check to see if you have Azure Active Directory Sign-in Assistant and the Azure Active Directory Module for Windows PowerShell installed.

The Azure Active Directory Sign-in Assistant comes in two versions: [32 bit](https://go.microsoft.com/fwlink/?linkid=286261) and [64 bit](https://go.microsoft.com/fwlink/?linkid=286262).

The Azure Active Directory Module for Windows PowerShell comes in two versions: [32 bit](https://go.microsoft.com/fwlink/?linkid=286258) and [64 bit](https://go.microsoft.com/fwlink/?linkid=286259).

## DNS Records Checks


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Application</p></td>
<td><p>Symptom</p></td>
<td><p>Check</p></td>
</tr>
<tr class="even">
<td><p>Domains</p></td>
<td><p>My custom domain (e.g. contoso.com) doesn’t seem to be configured with Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Run this check</a></p></td>
</tr>
<tr class="odd">
<td><p>Domains</p></td>
<td><p>My custom domain (e.g. contoso.com) doesn’t seem to be configured with Office 365 (I used a CNAME record)</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Run this check</a></p></td>
</tr>
<tr class="even">
<td><p>Domains</p></td>
<td><p>My custom domain (e.g. contoso.com) doesn’t seem to be configured with Office 365 (I used a TXT record)</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Run this check</a></p></td>
</tr>
<tr class="odd">
<td><p>Instant Messaging</p></td>
<td><p>My users are having trouble getting their Lync client to work</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834901">Run this check</a></p></td>
</tr>
<tr class="even">
<td><p>Instant Messaging</p></td>
<td><p>My users are having trouble getting their Lync client to work with other organizations</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834902">Run this check</a></p></td>
</tr>
<tr class="odd">
<td><p>Mail</p></td>
<td><p>I can’t get Outlook to automatically configure with Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834897">Run this check</a></p></td>
</tr>
<tr class="even">
<td><p>Mail</p></td>
<td><p>My email doesn’t seem to be routing to Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834898">Run this check</a></p></td>
</tr>
<tr class="odd">
<td><p>Mail</p></td>
<td><p>My organization is getting a good deal of SPAM</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834903">Run this check</a></p></td>
</tr>
<tr class="even">
<td><p>Mail</p></td>
<td><p>I can’t seem to get Exchange Hybrid working</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834904">Run this check</a></p></td>
</tr>
</tbody>
</table>

