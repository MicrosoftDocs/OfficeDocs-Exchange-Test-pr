---
title: 'Upgrade Exchange 2013 to the latest cumulative update or service pack: Exchange 2013 Help'
TOCTitle: Upgrade Exchange 2013 to the latest cumulative update or service pack
ms:assetid: 928a4a0b-0082-4d50-a696-bfaf2782f42d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ983803(v=EXCHG.150)
ms:contentKeyID: 51407267
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Upgrade Exchange 2013 to the latest cumulative update or service pack

 

_**Applies to:** Exchange Online, Exchange Server, Exchange Server 2013_


If you have Microsoft Exchange Server 2013 installed, you can upgrade it to the latest Exchange 2013 cumulative update or service pack. You can use the Exchange 2013 Setup wizard to upgrade your current version of Exchange 2013. For more information about the latest Exchange 2013 cumulative update or service pack, see [Updates for Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md). To learn more about Exchange 2013, see [What's new in Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).


> [!WARNING]
> After you upgrade Exchange 2013 to a newer cumulative update or service pack, you can't uninstall the new version to revert to the previous version. If you uninstall the new version, you remove Exchange from the server.



## What do you need to know before you begin?

  - Estimated time to complete: 60 minutes

  - Make sure you read the release notes before you install Exchange 2013. For more information, see [Release notes for Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - Make sure that any server on which you plan to install the cumulative update or service pack meets the system requirements and prerequisites. For more information, see [Exchange 2013 system requirements](exchange-2013-system-requirements-exchange-2013-help.md) and [Exchange 2013 prerequisites](exchange-2013-prerequisites-exchange-2013-help.md).
    

    > [!WARNING]
    > Any customized per-server settings you make in Exchange XML application configuration files, for example, web.config files on Client Access servers or the EdgeTransport.exe.config file on Mailbox servers, will be overwritten when you install an Exchange Cumulative Update (CU). Make sure that you save this information so you can easily re-configure your server after the install. You must re-configure these settings after you install an Exchange CU.



  - After you install a cumulative update or service pack, you must restart the computer so that changes can be made to the registry and operating system.


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Install the Exchange 2013 cumulative update or service pack

You can install the cumulative update or service pack for Exchange 2013 by using either the Setup wizard or via unattended mode. For specific instructions, see the following topics:

  - [Install Exchange 2013 using the Setup wizard](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

  - [Install Exchange 2013 using unattended mode](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)

If the computer you've installed a service pack or cumulative update on is a member of a database availability group (DAG), follow the steps in [Performing maintenance on DAG members](managing-database-availability-groups-exchange-2013-help.md) section of the [Managing database availability groups](managing-database-availability-groups-exchange-2013-help.md) topic.

