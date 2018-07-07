---
title: 'Exchange ActiveSync device settings with Exchange hybrid deployments: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync device settings with Exchange hybrid deployments
ms:assetid: 77f7cd72-2a8a-467e-9ffd-b93f5eeb2f69
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn931281(v=EXCHG.150)
ms:contentKeyID: 65051819
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
---

# Exchange ActiveSync device settings with Exchange hybrid deployments

 

_**Applies to:** Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_


Exchange ActiveSync devices are automatically reconfigured when a mailbox is moved from an Exchange on-premises organization to Office 365. Exchange ActiveSync will find the new mailbox location in Office 365 and update its configuration to talk directly to Office 365. The Exchange ActiveSync device won't try and contact the on-premises Exchange server after it's been successfully redirected to Office 365. With only a few exceptions (more on that below), the user no longer needs to manually set up their device for mail to keep working.

If you want to move a mailbox to Office 365, see [Move mailboxes between on-premises and Exchange Online organizations in hybrid deployments](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md).

For more information about hybrid deployments, see [Exchange Server Hybrid Deployments](exchange-server-hybrid-deployments-exchange-2013-help.md).

To use automatic redirection, your on-premises servers need to be running the latest releases of Exchange 2010, Exchange 2013, Exchange 2016, or later. You also need to have used the [Hybrid Configuration wizard](hybrid-configuration-wizard-exchange-2013-help.md) to set up your hybrid deployment. The Exchange ActiveSync redirection functionality uses the Outlook on the web target URL that's set on the organization relationship object. This object is configured when the Hybrid Configuration Wizard is run.

If your organization meets the requirements listed above, mobile devices should automatically be redirected to Office 365 when a user’s mailbox is moved, without any additional configuration. For the best experience, make sure your users’ mobile devices are running the latest versions of their operating systems and e-mail clients. Some mobile devices, such as those running the Android operating system, might take longer than expected to be redirected. Additionally, some devices might not correctly interpret the Exchange ActiveSync 451 redirection instructions sent by Exchange. For these devices, users will still need to manually reconfigure or recreate their email account on the device. If you have questions about whether a device supports Exchange ActiveSync 451 redirection, contact the device manufacturer.

Automatic Exchange ActiveSync redirection isn't supported in the following scenarios:

  - Moving mailboxes from Office 365 to an on-premises Exchange organization.

  - Moving mailboxes between on-premises Exchange organizations.

  - Moving mailboxes from Exchange 2007 servers to Office 365.

