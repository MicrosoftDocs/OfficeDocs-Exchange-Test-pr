---
title: 'Configure routing table logging: Exchange 2013 Help'
TOCTitle: Configure routing table logging
ms:assetid: 7184f8f7-4eb8-468a-aafe-b2d72868f820
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb201696(v=EXCHG.150)
ms:contentKeyID: 49289301
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Configure routing table logging

 

_**Applies to:** Exchange Server 2013_


Routing table logging periodically records a snapshot of the routing table used by Microsoft Exchange Server 2013 to route messages to their destinations.

## What do you need to know before you begin?

  - Estimated time to complete: 15 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Transport service" and "Edge Transport server" entries in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - You can only use the Shell to perform this procedure.

  - To configure the time interval for automatic recalculation of the routing table, you modify the EdgeTransport.exe.config XML application configuration file. Changes you save to this file are applied after you restart the Microsoft Exchange Transport service. When you restart this service, mail flow on the server is temporarily interrupted.

  - Any customized per-server settings you make in Exchange XML application configuration files, for example, web.config files on Client Access servers or the EdgeTransport.exe.config file on Mailbox servers, will be overwritten when you install an Exchange Cumulative Update (CU). Make sure that you save this information so you can easily re-configure your server after the install. You must re-configure these settings after you install an Exchange CU.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to configure routing table logging

Run the following command:

    Set-TransportService <ServerIdentity> -RoutingTableLogMaxAge <dd.hh:mm:ss> -RoutingTableLogMaxDirectorySize <Size>  -RoutingTableLogPath <LocalFilePath>

This example sets the following routing table log settings on the Mailbox server named Mailbox01:

  - Sets the location of the routing table log files to D:\\Routing Table Log. Note that if the folder doesn't exist, it will be created for you.

  - Sets the maximum size of the routing table log folder to 70 MB.

  - Sets the maximum age of a routing table log file to 45 days.

<!-- end list -->

    Set-TransportService Mailbox01 -RoutingTableLogPath "D:\Routing Table Log" -RoutingTableLogMaxDirectorySize 70MB -RoutingTableLogMaxAge 45.00:00:00


> [!NOTE]
> Setting the <EM>RoutingTableLogMaxAge</EM> parameter to the value <CODE>00:00:00</CODE> prevents the automatic removal of routing table log files because of their age.



## How do you know this worked?

To verify that you have successfully configured routing table logging, do the following:

1.  In the Shell, run the following command:
    
        Get-TransportService <ServerIdentity> | Format-List RoutingTableLog*

2.  Verify the values displayed are the values you configured.

## Use the Command Prompt to configure the interval for automatic recalculation of the routing table in the EdgeTransport.exe.config file

1.  In a Command prompt window, open the EdgeTransport.exe.config application configuration file in Notepad by running the following command:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  Modify the following key in the `<appSettings>` section.
    
        <add key="RoutingConfigReloadInterval" value="<hh:mm:ss>" />
    
    For example, to change the interval for automatic recalculation of the routing table to 10 hours, use the following value:
    
        <add key="RoutingConfigReloadInterval" value="10:00:00" />

3.  When you are finished, save and close the EdgeTransport.exe.config file.

4.  Restart the Microsoft Exchange Transport service by running the following command:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## How do you know this worked?

To verify that you have successfully configured the interval for the automatic recalculation of the routing table, verify the routing table log is updated during the time interval you specified.

Note that the routing table will be recalculated and logged earlier than the value specified by the *RoutingConfigReloadInterval* key if any of the following conditions occur:

  - A routing configuration change is detected. For example, a Send connector or a Receive connector is added, removed, or modified, or the 6 hour Kerberos token renewal occurs.

  - The Microsoft Exchange Transport service is started.

