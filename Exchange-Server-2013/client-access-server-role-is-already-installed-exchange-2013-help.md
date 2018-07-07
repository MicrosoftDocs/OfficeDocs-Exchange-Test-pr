---
title: 'Client Access server role is already installed: Exchange 2013 Help'
TOCTitle: Client Access server role is already installed
ms:assetid: 0103bf33-d553-445e-ba94-8c12e6cf507a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.caferolealreadyexists(v=EXCHG.150)
ms:contentKeyID: 46628785
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Client Access server role is already installed

 

_**Applies to:** Exchange Server_


Microsoft Exchange Server 2013 Setup has detected that you’re attempting to install the Client Access server role; however, the role is already installed on the computer.

If you want to reinstall the Client Access server role, you must first uninstall Exchange and then install the Client Access server role.

You may also receive this message if a previous installation of Exchange didn’t complete successfully. If this happens, uninstall Exchange and then reinstall the Client Access server role. If the installation continues to fail, do the following:

  - Make sure that your organization and the computer you're installing Exchange on meet the [Exchange 2013 system requirements](exchange-2013-system-requirements-exchange-2013-help.md).

  - Make sure that you've installed all the prerequisites required by Exchange, as described in [Exchange 2013 prerequisites](exchange-2013-prerequisites-exchange-2013-help.md).

  - Read the [Release notes for Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - View the Exchange Setup log located in \<*installation drive*\>:\\ExchangeSetupLogs\\ExchangeSetup.log, and look for errors or warnings that may have occurred during Setup.

  - Search the [Exchange Server forums](https://go.microsoft.com/fwlink/p/?linkid=14927). In your search query, specify the title of this topic.

  - Search the Internet using your favorite search engine. Be sure to include the title of this topic in your search.

Did you find what you’re looking for? Please take a minute to [send us feedback](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) about the information you were hoping to find.

