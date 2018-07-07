---
title: 'Configure the large audience size for your organization: Exchange 2013 Help'
TOCTitle: Configure the large audience size for your organization
ms:assetid: 8a37911c-4339-4921-b5d3-0a5a774d4517
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ659068(v=EXCHG.150)
ms:contentKeyID: 49345052
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure the large audience size for your organization

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can use the Exchange Management Shell to configure various settings that define how you use MailTips in your organization.

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "MailTips" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - You can only use the Shell to perform this procedure.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to configure the large audience size for your organization

You use the **Set-OrganizationConfig** cmdlet to configure the large audience size for your organization. When senders address messages to more recipients than the size you configure, they are shown the Large Audience MailTip. The large audience size is set to 25 by default. This example configures the large audience size to 50 in your organization.

    Set-OrganizationConfig -MailTipsLargeAudienceThreshold 50

For detailed syntax and parameter information, see [Set-OrganizationConfig](https://technet.microsoft.com/en-us/library/aa997443\(v=exchg.150\)).

