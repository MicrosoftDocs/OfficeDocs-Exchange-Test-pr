---
title: 'Accessing public folders with Outlook 2016 for Mac: Exchange 2013 Help'
TOCTitle: Accessing public folders with Outlook 2016 for Mac
ms:assetid: bc9b8226-bd8b-4edc-882b-4f19cfe118eb
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Mt788631(v=EXCHG.150)
ms:contentKeyID: 74115363
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Accessing public folders with Outlook 2016 for Mac

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016, Office 365_


**Summary:** The most recent supported Exchange topologies that allow users to access public folders with Outlook 2016 for Mac.

With the releases of the [April 2016 update](https://go.microsoft.com/fwlink/?linkid=829202) for Outlook 2016 for Mac clients, [Cumulative Update 14 (CU14)](https://go.microsoft.com/fwlink/p/?linkid=849432) for Exchange 2013, and [Cumulative Update 2 (CU 2)](https://go.microsoft.com/fwlink/p/?linkid=849793) for Exchange 2016, users of Outlook 2016 for Mac can now access public folders in more types of topologies than they could before.

## Outlook for Mac limitations

All versions of Outlook for Mac can access Exchange public folders, but until recently these clients could not access public folders in the following deployment scenarios:

  - **Co-existence with legacy public folders.** When a user's mailbox is on an Exchange 2013 or Exchange 2016 server, the user could not use Outlook for Mac to access public folders deployed on servers running Exchange 2010 SP3 or later. Other clients can access these legacy public folders in this scenario.

  - **Hybrid topologies.** On-premises users with a mailbox based in Exchange Online could not use Outlook for Mac to access on-premises modern public folders. Similarly, users with an Exchange 2013 or Exchange 2016 mailbox on-premises could not use Outlook for Mac to access public folders deployed in Exchange Online.

## Outlook 2016 for Mac

With the April 2016 update for Outlook 2016 for Mac, as well as CU14 for Exchange 2013 and CU2 for Exchange 2016, the above scenarios will now work for Outlook 2016 for Mac clients.

The following table summarizes the supported topologies for users with Outlook 2016 for Mac clients trying to access public folders in Exchange 2013, Exchange 2016, and Exchange Online.


> [!NOTE]
> The scenarios shown in the following table assume that the April 2016 update for Outlook 2016 for Mac has been applied to all clients.




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
<th>Public folders are deployed on...</th>
<th>User mailbox is on Exchange 2010 SP3 or later</th>
<th>User mailbox is on Exchange 2013 CU13 or later</th>
<th>User mailbox is on Exchange 2016 CU2 or later</th>
<th>User mailbox is on Office 365/Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2010 SP3 or later</p></td>
<td><p>Supported</p></td>
<td><p>Supported</p></td>
<td><p>Supported</p></td>
<td><p>Not supported</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server 2013 CU13 or later</p></td>
<td><p>Not supported</p></td>
<td><p>Supported</p></td>
<td><p>Supported</p></td>
<td><p>Supported</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server 2016 CU2 or later</p></td>
<td><p>Not supported</p></td>
<td><p>Supported</p></td>
<td><p>Supported</p></td>
<td><p>Supported</p></td>
</tr>
<tr class="even">
<td><p>Office 365 / Exchange Online</p></td>
<td><p>Not supported</p></td>
<td><p>Supported</p></td>
<td><p>Supported</p></td>
<td><p>Supported</p></td>
</tr>
</tbody>
</table>


The following articles describe how to deploy public folders in your Exchange organization in a co-existence or hybrid topology. As long as your Outlook 2016 for Mac clients have installed the April 2016 update, they will be able to access public folders in the configurations detailed in these articles:

  - [Configure legacy public folders where user mailboxes are on Exchange 2013 servers](configure-legacy-public-folders-where-user-mailboxes-are-on-exchange-2013-servers-exchange-2013-help.md)

  - [Configure Exchange 2013 public folders for a hybrid deployment](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

  - [Configure Exchange Online public folders for a hybrid deployment](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

