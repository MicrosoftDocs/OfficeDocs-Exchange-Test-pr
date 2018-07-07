---
title: 'Configure remote domain message reporting: Exchange 2013 Help'
TOCTitle: Configure remote domain message reporting
ms:assetid: 73dc686a-e7a3-44c7-b82f-f52ff9273199
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ649325(v=EXCHG.150)
ms:contentKeyID: 49318499
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Configure remote domain message reporting

 

_**Applies to:** Exchange Server 2013_


You can use the Exchange Management Shell to configure the way emails are sent and received through remote domains. The following demonstrates how to use the Exchange Management Shell configure the way Exchange handles delivery and non-delivery reports.

## What do you need to know before you begin?

  - Estimated time to complete: 10 minutes

  - You can only use the Shell to perform this procedure.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Remote domains" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to configure message reporting

You can use the **Set-RemoteDomain** cmdlet to configure the properties of a remote domain.

This example disables delivery reports to the remote domain named Contoso. This setting is enabled by default.

    Set-RemoteDomain Contoso -DeliveryReportEnabled $false

This example disables non-delivery reports to the remote domain. This setting is enabled by default.

    Set-RemoteDomain Contoso -NDREnabled $false

