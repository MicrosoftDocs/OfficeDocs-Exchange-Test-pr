---
title: 'Modify AD LDS configuration: Exchange 2013 Help'
TOCTitle: Modify AD LDS configuration
ms:assetid: 381f582c-15ec-43bc-b674-5399fad72c97
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997269(v=EXCHG.150)
ms:contentKeyID: 61200283
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Modify AD LDS configuration

 

_**Applies to:** Exchange Server 2013_


You can use the **ConfigureAdam.ps1** script (located in $env:ExchangeInstallPath\\Scripts) to modify the default Active Directory Lightweight Directory Services (AD LDS) configuration on Edge Transport servers before you subscribe the Edge Transport server to your Exchange organization.


> [!IMPORTANT]
> The <STRONG>ConfigureAdam.ps1</STRONG> script invokes the <STRONG>dsdbutil</STRONG> command to change the registry settings for AD&nbsp;LDS. The <STRONG>dsdbutil</STRONG> command is an AD&nbsp;LDS management tool intended for use only by experienced administrators; using <STRONG>ConfigureAdam.ps1</STRONG> is the recommended way of changing the AD&nbsp;LDS configuration.



The parameters in the following table are available for the **ConfigureAdam.ps1** script. You can use one, all, or any combination of these parameters to modify AD LDS.

### Parameters available for the ConfigureAdam.ps1 script

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Ldapport</em></p></td>
<td><p>Modifies the port used for LDAP communication. By default, the Edge Transport server uses the nonstandard port 50389.</p></td>
</tr>
<tr class="even">
<td><p><em>Sslport</em></p></td>
<td><p>Modifies the port used for secure LDAP communication. By default, the Edge Transport server uses the nonstandard port 50636.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogPath</em></p></td>
<td><p>Modifies the log file location. By default, the Edge Transport server creates log files in the path %ExchangeInstallPath%Transport Roles\Data\adam</p></td>
</tr>
<tr class="even">
<td><p><em>DataPath</em></p></td>
<td><p>Modifies the location of the directory database file. By default, the Edge Transport server stores the directory database in the path %ExchangeInstallPath%Transport Roles\Data\adam</p></td>
</tr>
</tbody>
</table>


## What do you need to know before you begin?

  - Estimated time to complete: five minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Edge Transport servers" section in [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md).

  - If you need to make any modifications to the Edge Transport server's AD LDS configuration, do so before subscribing the Edge Transport server to your Exchange organization. If you modify the AD LDS configuration of a subscribed Edge Transport server, you will then need to resubscribe the Edge Transport server to the Exchange organization.

  - Always use the script to modify the registry settings. Making manual registry changes to the AD LDS configuration might make the AD LDS instance unavailable.

  - If you need to modify the LDAP port or the SSL port used by AD LDS, first verify that the selected port isn't being used by another application. You can use the **netstat** command to view the ports being used on the Edge Transport server.

  - You can only use the Shell to perform this procedure.


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Modify the AD LDS configuration on an Edge Transport server

This example changes the LDAP port used by AD LDS to 5000. The ampersand (&) is part of the command syntax.

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000

This example makes the following changes to the AD LDS configuration. The ampersand (&) is part of the command syntax. Note the colon (:) used between each parameter and its value:

  - Changes the LDAP port to 5000

  - Changes the SSL port to 500

  - Changes the log path to D:\\Exchange Server\\Data\\ADLDS

  - Changes the data path to D:\\Exchange Server\\Data\\ADLDS

<!-- end list -->

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000 -SslPort:5001 -LogPath:"D:\Exchange Server\Data\ADLDS" -DataPath:"D:\Exchange Server\Data\ADLDS"

