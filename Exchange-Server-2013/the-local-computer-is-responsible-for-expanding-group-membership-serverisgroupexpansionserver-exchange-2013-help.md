---
title: 'The local computer is responsible for expanding group membership_ServerIsGroupExpansionServer: Exchange 2013 Help'
TOCTitle: The local computer is responsible for expanding group membership_ServerIsGroupExpansionServer
ms:assetid: 52872561-60e6-4f3d-bbc6-6de0edf74b09
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.serverisgroupexpansionserver(v=EXCHG.150)
ms:contentKeyID: 46628907
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# The local computer is responsible for expanding group membership\_ServerIsGroupExpansionServer

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 setup cannot continue because its attempt to uninstall a Hub Transport role responsible for expanding group membership failed.

Exchange 2007 setup requires that distribution list expansion be removed from the current Bridgehead server before the Hub Transport role can be uninstalled.

The expansion of distribution lists enables identification of individual recipients who belong to the distribution list to be identified, or the identification of additional distribution lists for expansion. An expanded distribution list can return the path for any required delivery status notification (DSN). DSNs notify the Microsoft Exchange administrator or e-mail sender of the status of a particular e-mail message. Additionally, distribution list expansion identifies whether Out of Office messages or automatically generated replies should be sent to the sender of the original message.

To resolve this issue, move distribution group expansion to another server and rerun Microsoft Exchange setup.

**To change the expansion server for a distribution group or dynamic distribution group**

1.  Open the Exchange Management Console.

2.  In the console tree, expand **Recipient Configuration**.

3.  In the console tree, click **Distribution Group**.

4.  Create a filter to view all distribution groups and dynamic distribution groups that use the current Bridgehead server as an expansion server.
    
    1.  In the action pane, click **Create Filter**.
    
    2.  In the property drop-down list, click **Expansion Server**.
    
    3.  In the operator drop-down list, click **Equals**.
    
    4.  At the value box, click the **Browse** button to select the Bridgehead server that currently acting as the expansion server.


> [!NOTE]
> The following step is optional.



1.  Click **Add Expression** to specify additional filter criteria. Only messages that meet all filter criteria will be displayed.

2.  Click **Apply Filter**. The results that meet the filter criteria are displayed.

<!-- end list -->

1.  In the results pane, click the distribution group you want to change the expansion server for, and then click **Properties** in the action pane.

2.  On **Properties**, click the **Advanced** tab.

3.  In the Expansion server drop-down list, select a specific server from the list or select **Any server in the organization**.

4.  Repeat steps 5 through 7 for all distribution groups or for dynamic distribution groups that are using the Bridgehead server as their expansion server.

