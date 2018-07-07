---
title: 'The COM+ Event System Service must be started before setup can continue_EventSystemStopped: Exchange 2013 Help'
TOCTitle: The COM+ Event System Service must be started before setup can continue_EventSystemStopped
ms:assetid: 3b8d2ba3-87fb-4749-b4d1-5dfec97e1ca4
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.eventsystemstopped(v=EXCHG.150)
ms:contentKeyID: 46628889
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# The COM+ Event System Service must be started before setup can continue\_EventSystemStopped

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft Exchange Server 2007 setup cannot continue because its attempt to install the Client Access Server or Edge Transport server roles failed because the COM+ Event System service is not started on the target computer.

Exchange 2007 setup requires the computer that you are installing Microsoft Exchange to have the COM+ Event System service status set to **Started**.

The COM+ Event System service supports system event notification for COM+ components, which provide automatic distribution of events to subscribing COM components.

Both the Client Access Server and Edge Transport server roles have dependencies on COM+ components that subscribe to the COM+ Event System service.

To resolve this issue, verify that the COM+ Event System service status is set to **Started** on the local computer, and then rerun Microsoft Exchange setup.

**To set the status of the COM+ Event System service to 'Started'**

1.  Right-click **My Computer**, and then click **Manage**.

2.  Expand the **Services and Applications** node, and then click the **Services** node.

3.  In the right pane, locate the **Com+ Event System**.

4.  Right-click **Com+ Event System**, and then click **Properties**.

5.  Set the **Startup Type** to **Automatic** and the **Service status** to **Started**.

6.  Click **Apply**, and then click **OK**.

