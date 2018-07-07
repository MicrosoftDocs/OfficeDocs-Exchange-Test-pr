---
title: 'Exchange ActiveSync virtual directory management tasks: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync virtual directory management tasks
ms:assetid: f0b339b7-e184-4392-a133-20523183459d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb125170(v=EXCHG.150)
ms:contentKeyID: 49318512
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Exchange ActiveSync virtual directory management tasks

 

_**Applies to:** Exchange Server 2013_


You can manage several of the Exchange ActiveSync application settings in Exchange Server 2013 through the Exchange ActiveSync virtual directory. A virtual directory is used by Internet Information Services (IIS) to allow access to a web application such as Exchange ActiveSync. Some of the virtual directory settings you can manage for Exchange ActiveSync include authentication, security, and reporting.

## Exchange ActiveSync virtual directory settings

You can modify the following properties and settings on the Exchange ActiveSync virtual directory:

  - **InternalURL** The InternalURL is the URL that internal clients can use to access the virtual directory. It is usually in the format https://servername/Microsoft-Server-ActiveSync. For example, if the server’s NetBIOS name is Sequoia, the InternalURL would be https://sequoia/Microsoft-Server-ActiveSync.

  - **ExternalURL** The ExternalURL is the URL that external clients can use to access the virtual directory. This URL should be accessible from outside your internal network. For example, your ExternalURL could be https://www.contoso.com/.

  - **Authentication settings** The two methods of authentication you can configure for the Exchange ActiveSync virtual directory are Basic authentication and Client certificate authentication.

