---
title: 'Help Identify My Issue with Automatic Checks - Directory Synchronization: Exchange 2013 Help'
TOCTitle: Help Identify My Issue with Automatic Checks - Directory Synchronization
ms:assetid: e6ea900a-c382-444c-a8ce-54d392bfeca3
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn793977(v=EXCHG.150)
ms:contentKeyID: 62632392
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Help Identify My Issue with Automatic Checks - Directory Synchronization

 

_**Applies to:** Exchange Server 2013_


You can use the automatic checks below to validate your configuration and help you update your environment.

If you already have an Office 365 user account, select Sign In. You don’t need an Azure ID account. You might be asked for a user account again when the checks run. If so, your user account is in the format of username@youroffice365login.domain and your password.


> [!NOTE]
> If you receive sync warning messages in the Office 365 portal, errors in the synchronization server event logs, or unhealthy directory synchronization notification emails from Microsoft Online Services, you may be having some kind of directory synchronization issue. The <A href="https://aka.ms/dsup">Directory Synchronization Troubleshooter</A> is a Web-based diagnostic tool designed to help identify common types of synchronization failures and prescribe targeted solutions to any issues found. The Directory Synchronization Troubleshooter must be run on the DirSync server.



## Prerequisites

We’ll check to see if you have Azure Active Directory Sign-in Assistant and the Azure Active Directory Module for Windows PowerShell installed.

The Azure Active Directory Sign-in Assistant comes in two versions: [32 bit](https://go.microsoft.com/fwlink/?linkid=286261) and [64 bit](https://go.microsoft.com/fwlink/?linkid=286262).

The Azure Active Directory Module for Windows PowerShell comes in two versions: [32 bit](https://go.microsoft.com/fwlink/?linkid=286258) and [64 bit](https://go.microsoft.com/fwlink/?linkid=286259).

## Directory Synchronization Checks


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
<td><p>Directory Sync</p></td>
<td><p>I’m not sure if all of my Active Directory user accounts meet the requirements for directory synchronization.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834884">Run this check</a></p></td>
</tr>
<tr class="odd">
<td><p>Directory Sync</p></td>
<td><p>I’m not sure if my Active Directory domain functional levels are correctly set to Windows Server 2003 or above.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">Run this check</a></p></td>
</tr>
<tr class="even">
<td><p>Directory Sync</p></td>
<td><p>I’m not sure if directory synchronization occurred in the last three hours.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">Run this check</a></p></td>
</tr>
<tr class="odd">
<td><p>Directory Sync</p></td>
<td><p>I’m not sure if my Active Directory has any duplicate user attributes that will block directory synchronization.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834883">Run this check</a></p></td>
</tr>
<tr class="even">
<td><p>Directory Sync</p></td>
<td><p>I’m not sure if directory synchronization is enabled in Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">Run this check</a></p></td>
</tr>
<tr class="odd">
<td><p>Directory Sync</p></td>
<td><p>I’m not sure if I can deploy Office 365 quote limitations.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834920">Run this check</a></p></td>
</tr>
<tr class="even">
<td><p>Directory Sync</p></td>
<td><p>I’m not sure if I can deploy Office 365 and use the default directory synchronization setup.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">Run this check</a></p></td>
</tr>
<tr class="odd">
<td><p>Directory Sync</p></td>
<td><p>I’m not sure if I use Active Directory and can support directory synchronization.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834886">Run this check</a></p></td>
</tr>
<tr class="even">
<td><p>Directory Sync</p></td>
<td><p>I’m not sure if all of my Active Directory groups meet the requirements for directory synchronization.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834913">Run this check</a></p></td>
</tr>
</tbody>
</table>

