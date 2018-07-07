---
title: 'Benefits of anti-spam features in Exchange Online Protection over Exchange Server 2013: Exchange 2013 Help'
TOCTitle: Benefits of anti-spam features in Exchange Online Protection over Exchange Server 2013
ms:assetid: 00e37a3c-3fbc-488f-bdad-d52a3c80fd72
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673032(v=EXCHG.150)
ms:contentKeyID: 49289144
ms.date: 05/26/2016
mtps_version: v=EXCHG.150
---

# Benefits of anti-spam features in Exchange Online Protection over Exchange Server 2013

 

_**Applies to:** Exchange Server 2013_


The following are benefits of using Exchange anti-spam protection in the cloud (Microsoft Exchange Online or Microsoft Exchange Online Protection) as opposed to Microsoft Exchange Server 2013, which has most of the same built-in anti-spam capabilities as Microsoft Exchange Server 2010:

  - **More control and easier configuration**   Administrators can use the Exchange admin center (EAC) web-based management console in order to customize spam filtering settings so that they best meet the needs of your organization. There is no anti-spam user interface in Exchange Server 2013. EOP anti-spam protection features are included in Exchange Online

  - **Stronger connection filtering**   In Exchange 2013, connection filtering IP Allow lists and IP Block lists are available only if you install an Edge Transport server in your perimeter network. For more information, see [Edge Transport servers](edge-transport-servers-exchange-2013-help.md). In the cloud, you can choose to skip spam filtering on email messages sent from trusted senders (gathered from various third-party sources), ensuring that these messages are not mistakenly marked as spam. Also, the hosted filtering service uses Microsoft’s own block lists and lists aggregated from vendors to provide greater IP-level filtering.

  - **Stronger content filtering**   You can easily configure your content filter policy to:
    
      - Filter messages written in specific languages.
    
      - Filter messages sent from specific countries or regions.
    
      - Mark bulk email messages (such as advertisements and marketing emails) as spam.
    
      - Search for attributes in a message and act upon the message if it matches a specific advanced spam option attribute. If you are concerned about phishing, some of these options offer a combination of Sender ID and SPF technologies to authenticate and verify that messages are not spoofed.
    
    In addition to the above content filter options that you can configure in the EAC, the hosted filtering service uses additional URL lists to block suspicious messages that contain specific URLs within their message body.

  - **Quicker updates**   Spam updates are propagated more quickly across the network. In Exchange Server 2013 updates occur two times per month, whereas the service is updated multiple times per hour.

  - **Outbound filtering**   Outbound spam filtering is always enabled if you use the hosted service for sending outbound email, thereby protecting organizations using the service and their intended recipients.

