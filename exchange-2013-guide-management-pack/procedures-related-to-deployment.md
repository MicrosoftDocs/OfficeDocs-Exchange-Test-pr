---
title: Procedures related to deployment
TOCTitle: Procedures related to deployment
ms:assetid: 6b7682bd-fe3d-43b9-a7db-66c0ac17656f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn195909(v=EXCHG.150)
ms:contentKeyID: 53181784
ms.author: dstrome
ms.date: 05/14/2016
mtps_version: v=EXCHG.150
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic" data-xmlns="http://www.w3.org/1999/xhtml" data-msxsl="urn:schemas-microsoft-com:xslt" data-cs="http://msdn.microsoft.com/en-us/">

<div data-asp="http://msdn2.microsoft.com/asp">

# Procedures related to deployment

</div>

<div id="mainSection">

<div id="mainBody">

<span> </span>

_**Topic Last Modified:** 2013-04-17_

This section contains the procedures that you can use as a reference when the Exchange Server 2013 Management Pack. For procedures related to post-deployment operation, see [Procedures related to post-deployment operation](procedures-related-to-post-deployment-operation.md).

<span id="VerifyDeployment"></span>

<div>

## Verify agent deployment status

Before you import the Exchange Server 2013 Management Pack, verify that the SCOM agents on your Exchange servers are operational and the operating system health is being reported correctly in SCOM.

Your user account needs to be a member of the Operations Manager Administrators role to perform this procedure.

1.  Log on to your SCOM server and open the SCOM console.

2.  Click **Monitoring** and then click **Windows Computers**.

3.  Make sure that all of your Exchange servers show **Healthy**.

![Healthy agents in SCOM console](images/Dn195909.7d1ff0bb-419e-40dc-babf-5fa2fb7229a8(EXCHG.150).png "Healthy agents in SCOM console")

</div>

<span id="VerifyProxy"></span>

<div>

## Verify agent proxy configuration

Before you import the Exchange Server 2013 Management Pack, verify that the agent proxy is enabled for discovery in SCOM. Otherwise, the agents on your Exchange servers won't report Exchange health status. You need to verify this configuration for all of your Exchange Servers.

Your user account needs to be a member of the Operations Manager Administrators role to perform this procedure.

1.  Log on to your SCOM server and open the SCOM console.

2.  In the Operations console, click **Administration**.

3.  Click **Agent Managed**. , right-click your Exchange server, and then select **Properties**.

4.  On the **Security** tab, verify that the **Allow this agent to act as a proxy and discover managed objects on other computers** check box is selected.

5.  Click **OK**.

</div>

<span id="VerifySecurity"></span>

<div>

## Verify agent security configuration

Due to the security model under which Exchange 2013 has been tested, running the SCOM agent on your Exchange servers under any account other than **LocalSystem** isn’t supported. If you run the agent under any account other than LocalSystem, the synthetic transactions fail to run. You may also experience other issues.

Your user account needs to be a member of the Server Management role group to perform this procedure.

1.  Log on to your Exchange server.

2.  Click **Start** \> **Administrative Tools** \> **Services**.

3.  Scroll down the list of services to find the **System Center Management** service.

4.  Verify that the **Log On As** column shows **Local System**.

5.  If the **Log on As** column shows anything else, change the service log on to Local System.
    
    1.  Right click on **System Center Management** service and select **Properties**.
    
    2.  Select the **Log On** tab.
    
    3.  Click **Local System account** option.
    
    4.  Click **OK**.

</div>

</div>

<span> </span>

</div>

</div>

</div>

