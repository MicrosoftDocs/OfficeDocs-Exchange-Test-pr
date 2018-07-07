---
title: 'Exchange Server Supportability Matrix: Exchange 2013 Help'
TOCTitle: Exchange Server Supportability Matrix
ms:assetid: dbac2d40-da8b-469f-a265-1d1f948fe446
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ff728623(v=EXCHG.150)
ms:contentKeyID: 53873565
ms.date: 03/20/2018
mtps_version: v=EXCHG.150
---

# Exchange Server Supportability Matrix

 

_**Applies to:** Exchange Server 2007, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_


The Exchange Server Supportability Matrix provides a central source for Microsoft Exchange administrators to easily locate information about the level of support available for any configuration or required component for supported versions of Microsoft Exchange.

## Release model

The following table identifies the release model for each supported version of Exchange. The release model is identified by an X character.

For versions of Exchange prior to Exchange 2013, each update rollup package is cumulative with regard to the whole product. Therefore, if you apply an update rollup package to Exchange Server 2010, you apply all the fixes contained in that update rollup package. This includes all the fixes contained in each earlier update rollup package. When an update or a hotfix for earlier versions of Exchange is created, one or more of the binary files included in the update or included in the hotfix are cumulative. They are cumulative with regard to the contents of the files. However, they aren't cumulative with regard to the whole Exchange product. For more information, see [Exchange 2010 Servicing](https://go.microsoft.com/fwlink/p/?linkid=298627).

With Exchange 2013, we changed the way we deliver hotfixes and service packs. Instead of the priority-driven hotfix release and update rollup model used by previous versions of Exchange, Exchange 2013 and later versions now adhere to a scheduled delivery model. In this model, cumulative updates are released every three months. A cumulative update (CU) for Exchange 2013 and later is released as a full refresh of that version of Exchange, similar to a product upgrade or a service pack release. For more information, see [Updates for Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Servicing release model</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cumulative updates</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Update rollups</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Security Hotfixes delivered separately</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


## Support lifecycle

For more information about the support lifecycle for a specific version of Exchange, or of the Microsoft Windows server or client operating systems, see the [Microsoft Support Lifecycle](https://go.microsoft.com/fwlink/p/?linkid=55839) page. For more information about the Microsoft Support Lifecycle, see the [Microsoft Support Lifecycle Policy FAQ](https://go.microsoft.com/fwlink/p/?linkid=158902).

## Exchange Server 2007 End-of life

Exchange 2007 reached end of support on April 11, 2017, per the [Microsoft Lifecycle Policy](https://go.microsoft.com/fwlink/p/?linkid=833210). As a reminder, after that date there will be no new security updates, non-security updates, free or paid assisted support options or online technical content updates. Furthermore, as adoption of Office 365 accelerates and cloud usage increases, custom support options for Office products will not be available. This includes Exchange Server as well as Office Suites; SharePoint Server; Office Communications Server; Lync Server; Skype for Business Server; Project Server and Visio. Having reached the end of support date for Exchange 2007, we encourage customers to complete their migration and upgrade plans. We recommend customers to leverage deployment benefits provided by Microsoft and Microsoft Certified Partners including [Microsoft FastTrack](https://go.microsoft.com/fwlink/p/?linkid=238431) for cloud migrations, and [Software Assurance Deployment & Planning Services](https://go.microsoft.com/fwlink/p/?linkid=833211) for on-premises upgrades.

## Supported operating system platforms

The following table identifies the operating system platforms on which each version of Exchange can run. Supported platforms are identified by an X character.


> [!IMPORTANT]
> Releases of Windows Server and Windows client that aren't listed in the table below are not supported for use with any version or release of Exchange.




<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Operating system platform</th>
<th>Exchange 2016 CU3 and later</th>
<th>Exchange 2016 CU2 and earlier</th>
<th>Exchange 2013 SP1 and later</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Vista SP2</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 SP2</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows 7 SP1</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
</tr>
<tr class="odd">
<td><p>Windows 8</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>Windows 8.1</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Windows 10</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p></p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


1Only for Exchange management tools

## Supported Active Directory environments

The following table identifies the Active Directory environments with which each version of Exchange can communicate. Supported environments are identified by an X character. An Active Directory server refers to both writable global catalog servers and to writable domain controllers. Read-only global catalog servers and read-only domain controllers aren't supported.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Operating system environment</th>
<th>Exchange 2016 CU3 and later</th>
<th>Exchange 2016 CU2 and earlier</th>
<th>Exchange 2013 SP1 and later</th>
<th>Exchange 2010 SP3 RU5 or later</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2003 SP2 Active Directory servers</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 SP2 Active Directory servers</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1 Active Directory servers</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012 Active Directory servers</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2 Active Directory servers</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016 Active Directory servers</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Forest functional level</th>
<th>Exchange 2016 CU3 and later</th>
<th>Exchange 2016 CU2 and earlier</th>
<th>Exchange 2013 SP1 and later</th>
<th>Exchange 2010 SP3 RU5 or later</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2003 forest functional level</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 forest functional level</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1 forest functional level</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012 forest functional level</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2 forest functional level</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016 forest functional level</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Web browsers supported for use with the premium version of Outlook Web App or Outlook on the web

The following table identifies the Web browsers supported for use together with the premium version of Outlook Web App or Outlook on the web. Supported browsers are identified by an X character.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Browser</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 and later</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Current release of Microsoft Edge</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Current or immediately previous release of Internet Explorer</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Firefox</p></td>
<td><p>Current or immediately previous release of Firefox</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="odd">
<td><p>Firefox 3.0.1 or later</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Firefox 12 or later</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Safari</p></td>
<td><p>Current release of Safari</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="even">
<td><p>Safari 3.1 or later</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Safari 5.0 or later</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome</p></td>
<td><p>Current release of Chrome</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="odd">
<td><p>Chrome 3.0.195 or later</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome 18 or later</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Web browsers supported for use with the basic version of Outlook Web App or Outlook on the web

The following table identifies the Web browsers supported for use together with the light (basic) version of Outlook Web App or Outlook on the web. . Supported browsers are identified by an X character.


> [!NOTE]
> Outlook Web App Basic (Outlook Web App Light) is supported for use in mobile browsers. However, if rendering or authentication issues occur in a mobile browser, determine whether the issue can be reproduced by using Outlook Web App Light in the full client of a supported browser. For example, test the use of Outlook Web App Light in Safari, Chrome, or Internet Explorer. If the issue can’t be reproduced in the full client, we recommend that you contact the mobile device vendor for help. In these cases, we collaborate with the vendor as appropriate.




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Browser</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Current release of Microsoft Edge</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Current or immediately previous release of Internet Explorer</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X<span></span></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Safari</p></td>
<td><p>Current release of Safari</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Firefox</p></td>
<td><p>Current or immediately previous release of Firefox</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome</p></td>
<td><p>Current release of Chrome</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="odd">
<td><p>Opera</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Web browsers supported for use of S/MIME with Outlook Web App or Outlook on the web

The following table identifies the Web browsers supported for the use of S/MIME together with Outlook Web App or Outlook on the web. Supported browsers are identified by an X character.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Browser</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 and later</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Current release of Microsoft Edge</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Current or immediately previous release of Internet Explorer</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Clients

The following table identifies the mailbox clients that are supported for use together with each version of Exchange. Supported clients are identified by an X character.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Client</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 and later</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>X4</p></td>
<td><p>X2</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2016</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Outlook for Mac for Office 365</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Phone 7.5</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Phone 8</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Phone 8.1</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Mobile 10</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Entourage 2008 (EWS)</p></td>
<td><p>X3</p></td>
<td><p>X3</p></td>
<td><p>X3</p></td>
</tr>
</tbody>
</table>


1Requires Outlook 2007 Service Pack 3 and the latest public update.

2Requires Outlook 2010 Service Pack 1 and the latest public update.

3EWS only. There is no DAV support for Exchange 2010.

4Supported with the latest Office service pack and public updates.

## Tools

The following table identifies the version of Microsoft Exchange that can be used together with the Microsoft Exchange Inter-Organization Replication tool (Exscfg.exe; Exssrv.exe). The tool is used to replicate public folder information (including free/busy information) between Exchange organizations. For more information, see [Microsoft Exchange Server Inter-Organization Replication](https://go.microsoft.com/fwlink/?linkid=22455). Supported versions are identified by an X character.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tool</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 and later</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Inter-Organization Replication tool</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Microsoft .NET Framework

The following table identifies the version of the Microsoft .NET Framework that can be used together with each version of Exchange. Supported versions are identified by an X character.


> [!IMPORTANT]
> <STRONG>Releases of .NET Framework that aren't listed in the table below are not supported on any version or release of Exchange.</STRONG> This includes minor and patch-level releases of .NET Framework.




> [!NOTE]
> When upgrading Exchange from an unsupported CU to the current CU and no intermediate CUs are available, you should upgrade to the latest version of .NET that's supported by Exchange first and then immediately upgrade to the current CU. This method doesn't replace the need to keep your Exchange servers up to date and on the latest, supported, CU.<BR>Microsoft makes no claim that an upgrade failure will not occur using this method, which may result in the need to contact Microsoft Support Services.




<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>.NET Framework</th>
<th>Exchange 2016 CU8 &amp; CU9</th>
<th>Exchange 2016 CU5 - CU7</th>
<th>Exchange 2013 CU19 &amp; CU20</th>
<th>Exchange 2013 CU16 - CU18</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>.NET Framework 3.5</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 3.5 SP1</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>.NET Framework 4.0</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1,2</p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 4.5</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1,2</p></td>
</tr>
<tr class="odd">
<td><p>.NET Framework 4.6.2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 4.7.1</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


1 If you are using Windows Server 2012, the .NET Framework 3.5 must be installed before you can use Exchange 2010 SP3.

2 Exchange 2010 uses only the .NET .NET Framework 3.5 and .NET .NET Framework 3.5 SP1 libraries. It doesn't use the .NET .NET Framework 4.5 libraries if they're installed on the computer. We support the installation of any major or minor version of .NET .NET Framework 4.5 (for example, .NET .NET Framework 4.5.1, .NET .NET Framework 4.5.2, and so on) as long as .NET .NET Framework 3.5 or .NET .NET Framework 3.5 SP1 are also installed on the computer.

## Windows Management Framework

The following table identifies the version of the Windows Management Framework, which contains the Windows PowerShell command-line interface, that can be used together with each version of Exchange. Supported versions are identified by an X character.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows PowerShell</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows PowerShell 2.0</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Management Framework</p></td>
<td><p>Version of Windows Management Framework built into the release of Windows Server you're installing Exchange on.</p></td>
<td><p>Version of Windows Management Framework built into the release of Windows Server you're installing Exchange on.</p></td>
<td><p>Version of Windows Management Framework built into the release of Windows Server you're installing Exchange on.1</p></td>
</tr>
</tbody>
</table>


1 Windows Management Framework 3.0 and Windows Management Framework 4.0 can be used to perform operating system-related management tasks on a computer that's running Exchange 2010 SP3 RU5 or later. However, Exchange 2010 cmdlets and Exchange 2010 scripts require Windows PowerShell 2.0. Using Exchange 2010 cmdlets and scripts with Windows Management Framework 3.0 or Windows Management Framework 4.0 isn't supported.

## Microsoft Management Console

The following table identifies the version of Microsoft Management Console (MMC) that can be used together with each version of Exchange. Supported versions are identified by an X character.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>MMC</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 or later</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MMC 3.0</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Windows Installer

The following table identifies the version of Windows Installer that is used together with each version of Exchange. Supported versions are identified by an X character.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows Installer</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 and later</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Installer 4.5</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Installer 5.0</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>

