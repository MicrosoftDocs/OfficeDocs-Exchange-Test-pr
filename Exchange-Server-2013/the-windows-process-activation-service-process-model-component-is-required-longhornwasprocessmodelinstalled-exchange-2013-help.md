---
title: 'The Windows Process Activation Service - Process Model component is required_LonghornWASProcessModelInstalled: Exchange 2013 Help'
TOCTitle: The Windows Process Activation Service - Process Model component is required_LonghornWASProcessModelInstalled
ms:assetid: 8cc13dbb-4921-4c07-8602-d26613d7730a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.longhornwasprocessmodelinstalled(v=EXCHG.150)
ms:contentKeyID: 46629022
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# The Windows Process Activation Service - Process Model component is required\_LonghornWASProcessModelInstalled

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Exchange Server 2010 setup cannot continue installation on the Windows Server 2008-or Windows Server 2008 R2-based computer because the Windows Process Activation Service - Process Model feature is not installed on the server.

The Windows Process Activation Service generalizes the Internet Information Services (IIS) process model, removing the dependency on HTTP. All the features of IIS that were previously available only to HTTP applications are now available to applications hosting Windows Communication Foundation (WCF) services, by using non-HTTP protocols. IIS 7.0 also uses Windows Process Activation Service for message-based activation over HTTP.

The Process Model hosts Web and WCF services. Introduced in IIS 6.0, the Process Model is a new architecture that features rapid failure protection, health monitoring, and recycling.

To resolve this issue, install the Windows Process Activation Service - Process Model feature on this server and then rerun Exchange 2010 setup.

**Install the Windows Process Activation Service - Process Model feature by using the Server Manager tool**

1.  Click **Start**, click **Administrative Tools** and then **Server Manager**.

2.  In the left navigation pane, right-click **Features**, and then click **Add Features**.

3.  On the **Select Features** pane, scroll down to **Windows Process Activation Service**.

4.  Select the check boxes for **Process Model**.

5.  Click **Next** from the **Select Features** pane, and then click **Install** at the **Confirm Installations Selections** pane.

6.  Click **Close** to leave the Add Role Services wizard.

