---
title: 'Configure connectivity logging: Exchange 2013 Help'
TOCTitle: Configure connectivity logging
ms:assetid: 24e46a79-33ea-44e9-b03c-549db1c86a6f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa996827(v=EXCHG.150)
ms:contentKeyID: 49288901
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Configure connectivity logging

 

_**Applies to:** Exchange Server 2013_


Connectivity logging records the outbound connection activity that's used to transmit messages from a transport service on an Exchange server. Connectivity logging records the connection source, destination, number of messages and bytes transmitted, and connection failure information.

## What do you need to know before you begin?

  - Estimated time to complete: 15 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Transport service", "Front End Transport service", and "Mailbox Transport service" entries in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - You can use the Exchange admin center (EAC) to enabled or disabled connectivity logging, or set the connectivity log path for the Transport service only. For all other connectivity logging options in other transport services, you need to use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the EAC to configure connectivity logging in the Transport service

1.  In the EAC, navigate to **Servers** \> **Servers**.

2.  Select the Mailbox server you want to configure, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the server properties page, click **Transport Logs**.

4.  In the **Connectivity log** section, change any of the following:
    
      - **Enable connectivity log**   To disable connectivity logging on the server, clear the check box. To enable connectivity logging on the server, select the check box.
    
      - **Connectivity log path**   The value you specify must be on the local Exchange server. If the folder doesn't exist, it will be created for you when you click **Save**.
    
    When you are finished, click **Save**.

## Use the Shell to configure connectivity logging

To configure connectivity logging, run the following command:

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ConnectivityLogEnabled <$true | $false> -ConnectivityLogMaxAge <dd.hh:mm:ss> -ConnectivityLogMaxDirectorySize <Size> -ConnectivityLogMaxFileSize <Size> -ConnectivityLogPath <LocalFilePath>

This example sets the following connectivity log settings in the Transport service on the Mailbox server named Mailbox01:

  -  
    Sets the location of the connectivity log files to D:\\Hub Connectivity Log. Note that if the folder doesn't exist, it will be created for you.

  -  
    Sets the maximum size of a connectivity log file to 20 MB.

  -  
    Sets the maximum size of the connectivity log directory to 1.5 GB.

  -  
    Sets the maximum age of a connectivity log file to 45 days.

<!-- end list -->

    Set-TransportService Mailbox01 -ConnectivityLogPath "D:\Hub Connectivity Log" -ConnectivityLogMaxFileSize 20MB -ConnectivityLogMaxDirectorySize 1.5GB -ConnectivityLogMaxAge 45.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P>To configure the connectivity log settings in the Mailbox Transport service on a Mailbox server, use the <STRONG>Set-MailboxTransportService</STRONG> cmdlet. To configure the connectivity log settings in the Front End Transport service on a Client Access server, use the <STRONG>Set-FrontEndTransportService</STRONG> cmdlet.</P>
> <LI>
> <P>Setting the <EM>ConnectivityLogPath</EM> parameter to the value <CODE>$null</CODE>, effectively disables connectivity logging. However, if the value of the <EM>ConnectivityLogEnabled</EM> parameter is <CODE>$true</CODE>, event log errors are generated.</P>
> <LI>
> <P>Setting the <EM>ConnectivityLogMaxAge</EM> parameter to the value <CODE>00:00:00</CODE> prevents the automatic removal of connectivity log files because of their age.</P></LI></UL>



## How do you know this worked?

To verify that you have successfully configured connectivity logging, do the following:

1.  In the Shell, run the following command:
    
        <Get-TransportService | Get-FrontEndTransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List ConnectivityLog*

2.  Verify the values displayed are the values you configured.

