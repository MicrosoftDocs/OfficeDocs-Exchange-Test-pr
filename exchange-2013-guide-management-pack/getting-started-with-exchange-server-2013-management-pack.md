---
title: Getting started with Exchange Server 2013 Management Pack
TOCTitle: Getting started with Exchange Server 2013 Management Pack
ms:assetid: 72d1609f-ab32-44d8-aa40-b1de587442d2
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn195908(v=EXCHG.150)
ms:contentKeyID: 53181782
ms.author: dstrome
ms.date: 05/14/2016
mtps_version: v=EXCHG.150
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic" data-xmlns="http://www.w3.org/1999/xhtml" data-msxsl="urn:schemas-microsoft-com:xslt" data-cs="http://msdn.microsoft.com/en-us/">

<div data-asp="http://msdn2.microsoft.com/asp">

# Getting started with Exchange Server 2013 Management Pack

</div>

<div id="mainSection">

<div id="mainBody">

<span> </span>

_**Topic Last Modified:** 2013-04-08_

The Exchange Server 2013 Management Pack adds a container in the **Monitoring** section of the SCOM console. When you expand the Exchange Server 2013 container, you'll see that there are only three views under it.

![Exchange 2013 Management Pack Containers](images/Dn195908.253b4ec5-2103-4b0c-a22e-5ebd24d08600(EXCHG.150).png "Exchange 2013 Management Pack Containers")

<div>

## Active Alerts – Is there anything wrong with Exchange?

The **Active Alerts** view shows you all the alerts that are raised and are currently active in your Exchange organization. You can click on any alert and see more information about the alert in the details pane. This view is essentially providing you with a Yes/No answer for "is there anything wrong in my Exchange deployment?" Each alert corresponds to one or more issues for a particular health set. Also, depending on the particular issue, there may be more than one alert raised.

</div>

<div>

## Organization Health – What is the impact?

If you see an alert for in the Active Alerts view, the first thing you want to do is check the **Organization Health** view. This is the primary source of information for the overall health of your organization. It gives you specifically what is impacted in your organization like Active Directory Sites and Database Availability Groups.

![Organization Health](images/Dn195908.603c920b-7b88-4956-87d9-09d93fa6cba3(EXCHG.150).png "Organization Health")

</div>

<div>

## Server Health – Which server do I need to troubleshoot?

The **Server Health** view provides details about individual servers in your organization. Here you can see the individual health of all your servers. Using this view, you can narrow down any issues to a particular server.

![Server Health](images/Dn195908.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "Server Health")

</div>

<div>

## Monitoring Categories

While going through the three views in the Exchange Server 2013 dashboard, you may have noticed that in addition to the **State** column, you have four additional health indicators.

![Exchange health indicators](images/Dn195908.dd10ed0b-abe5-41aa-8d43-b4fb10133984(EXCHG.150).png "Exchange health indicators")

Each of these health indicators give you an overview of specific aspects of your Exchange deployment.

  - **Customer Touch Points** This shows you what your users are experiencing. If this indicator is healthy, it means that the problem is probably not impacting your users. For example, assume that a DAG member is having problems, but the database failed over successfully. In this case, you will see unhealthy indicators for that particular DAG, but the customer touch points indicator will show healthy because the users are not experiencing any service interruption.

  - **Service Components** This shows you the state of the particular service associated with the component. For example, the service component indicator for OWA indicates whether the overall OWA service is healthy.

  - **Server Resources** This shows you the state of physical resources that impact the functionality of a server.

  - **Key Dependencies** This shows you the state of the external resources that the Exchange depends on like network connectivity, DNS or Active Directory.

Exchange Server 2013 management pack views provide a simple, but powerful view that makes it easy and fast to determine that your organization is healthy. However, the views are also structured in a way to quickly guide you to the root of the problem in case of an alert. See [Using the Exchange Server 2013 Management Pack for troubleshooting](using-the-exchange-server-2013-management-pack-for-troubleshooting.md) to learn more about using the Exchange Server 2013 Management Pack to resolve problems.

</div>

</div>

<span> </span>

</div>

</div>

</div>

