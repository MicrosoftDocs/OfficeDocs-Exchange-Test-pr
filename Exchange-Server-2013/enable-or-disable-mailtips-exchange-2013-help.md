---
title: 'Enable or disable MailTips: Exchange 2013 Help'
TOCTitle: Enable or disable MailTips
ms:assetid: 11ad3848-f303-4ad5-a21d-9b0883db4bda
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ649321(v=EXCHG.150)
ms:contentKeyID: 49318493
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Enable or disable MailTips

 

_**Applies to:** Exchange Server 2013_


You can use the Exchange Management Shell to configure various settings that define how you use MailTips in your organization.

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "MailTips" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - You can only use the Shell to perform this procedure.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to enable or disable MailTips

You use the **Set-OrganizationConfig** cmdlet to enable or disable MailTips in your organization. MailTips are enabled by default when you install a new Exchange organization. This example shows how to enable MailTips in your organization.

    Set-OrganizationConfig -MailTipsAllTipsEnabled $true

For detailed syntax and parameter information, see [Set-OrganizationConfig](https://technet.microsoft.com/en-us/library/aa997443\(v=exchg.150\)).

