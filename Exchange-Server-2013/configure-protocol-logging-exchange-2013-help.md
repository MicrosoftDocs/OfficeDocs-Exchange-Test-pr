---
title: 'Configure protocol logging: Exchange 2013 Help'
TOCTitle: Configure protocol logging
ms:assetid: c81cac9c-b990-492a-b899-5be8d08a6068
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124531(v=EXCHG.150)
ms:contentKeyID: 49289407
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Configure protocol logging

 

_**Applies to:** Exchange Server 2013_


Protocol logging records the SMTP conversations that occur on Send Connectors and Receive connectors as part of message delivery.

## What do you need to know before you begin?

  - Estimated time to complete: 15 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Transport Service", "Front End Transport service", "Mailbox Transport service", "Receive connectors" and "Send connectors" entries in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - You can use the Exchange admin center (EAC) to enable or disable protocol logging for Send connectors and Receive connectors in the Transport service on Mailbox servers, and for Receive connectors in the Front End Transport service on Client Access servers. You can also use the EAC to configure the protocol log paths for the Transport service only. For all other protocol logging options, you need to use the Shell.

  - Protocol logging is enabled or disabled on each individual connector. All the Receive connectors on the Exchange server share the same protocol log files and protocol log options. These protocol log settings are separate from the Send connector protocol log files and protocol log options that are on the same server.

  - 
    

    > [!WARNING]
    > Don't perform this procedure on an Edge Transport server that has been subscribed to the Exchange organization by using EdgeSync. Instead, make the changes in the Transport service on the Mailbox server. The changes are then replicated to the Edge Transport server next time EdgeSync synchronization occurs.



  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the EAC to configure protocol logging

To use the EAC to enable or disable protocol logging on a Send connector or a Receive connector in the Transport service on a Mailbox server, or on a Receive connector in the Front End Transport service on a Client Access server, do the following:

1.  In the EAC, navigate to **Mail flow** \> **Send connectors** or **Mail flow** \> **Receive connectors**.

2.  Select the connector you want to configure, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **General** tab in the **Protocol logging level** section, select one of the following options:
    
      - **None**   Protocol logging disabled on the connector.
    
      - **Verbose**   Protocol logging is enabled on the connector.
    
    When you are finished, click **Save**.

To use the EAC to configure the protocol log paths for the Send connectors and Receive connectors in the Transport service on a Mailbox server, do the following:

1.  In the EAC, navigate to **Servers** \> **Servers**.

2.  Select the Mailbox server you want to configure, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the server properties page, click **Transport logs**.

4.  In the **Protocol log** section, change any of the following settings:
    
      - **Send protocol log path**   The value you specify must be on the local Exchange server. If the folder doesn't exist, it will be created for you when you click **Save**.
    
      - **Receive protocol log path**   The value you specify must be on the local Exchange server. If the folder doesn't exist, it will be created for you when you click **Save**.
    
    When you are finished, click **Save**.

## How do you know this worked?

To verify that you have successfully used the EAC to configure the protocol log settings, do the following:

1.  Browse to the location you specified for the Send connector or the Receive connector protocol logs.

2.  If you enabled protocol logging, verify a log file is created. If you disabled protocol logging, verify the latest log file is no longer being updated.

## Use the Shell to enable or disable protocol logging on a Send connector or a Receive connector

To enable or disable protocol logging on a Send connector or a Receive connector, run the following command:

    <Set-SendConnector |Set-ReceiveConnector> <ConnectorIdentity> -ProtocolLoggingLevel <Verbose | None>

This example enables protocol logging for the Receive connector named Connection from Contoso.com.

    Set-ReceiveConnector "Connection from Contoso.com" -ProtocolLoggingLevel Verbose

## How do you know this worked?

To verify that you have successfully enabled or disabled protocol logging, do the following:

1.  In the Shell, run the following command:
    
        <Get-SendConnector |Get-ReceiveConnector> | Format-List Name,ProtocolLoggingLevel

2.  Verify the values displayed are the values you configured.

## Use the Shell to enable or disable protocol logging on the intra-organization Send connector

To enable or disable protocol logging on the implicit and invisible intra-organization Send connector that exists in the Transport service on a Mailbox server and in the Front End Transport service on a Client Access server, run the following command:

    <Set-TransportService | Set-FrontEndTransportService> -IntraOrgConnectorProtocolLoggingLevel <Verbose | None>

This example enables protocol logging on the intra-organization Send connector in the Transport service on a Mailbox server named Mailbox01.

    Set-TransportService Mailbox01 -IntraOrgConnectorProtocolLoggingLevel Verbose

## How do you know this worked?

To verify that you have successfully enabled or disabled protocol logging on the intra-org Send connector, do the following:

1.  In the Shell, run the following command:
    
        <Get-TransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List IntraOrgConnectorProtocolLoggingLevel

2.  Verify the value displayed is the value you configured.

## Use the Shell to enable or disable protocol logging on the mailbox delivery Send connector

To enable or disable protocol logging on the implicit and invisible mailbox delivery Send connector that exists in the Mailbox Transport service on a Mailbox server, run the following command:

    Set-MailboxTransportService -MailboxDeliveryConnectorProtocolLoggingLevel <Verbose | None>

This example enables protocol logging on the mailbox delivery Receive connector in the Mailbox Transport service on a Mailbox server named Mailbox01.

    Set-MailboxTransportService Mailbox01 -MailboxDeliveryConnectorProtocolLoggingLevel Verbose

## How do you know this worked?

To verify that you have successfully enabled or disabled protocol logging on the mailbox delivery connector, do the following:

1.  In the Shell, run the following command:
    
        Get-MailboxTransportService <ServerIdentity> | Format-List MailboxDeliveryConnectorProtocolLoggingLevel

2.  Verify the value displayed is the value you configured.

## Use the Shell to configure protocol logging settings

To configure the protocol log settings, run the following command:

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ReceiveProtocolLogPath <LocalFilePath> -SendProtocolLogPath <LocalFilePath> -ReceiveProtocolLogMaxFileSize <Size> -SendProtocolLogMaxFileSize <Size> -ReceiveProtocolLogMaxDirectorySize <Size> -SendProtocolLogMaxDirectorySize <Size> -ReceiveProtocolLogMaxAge <dd.hh:mm:ss> -SendProtocolLogMaxAge <dd.hh:mm:ss>

This example sets the following protocol log settings in the Transport service on the Mailbox server named Mailbox01:

  -  
    Sets the location of all Receive connector protocol logs to D:\\Hub Receive SMTP Log and all Send connector protocol logs to D:\\Hub Send SMTP Log. Note that if the folder doesn't exist, it will be created for you.

  -  
    Sets the maximum size of a Receive connector protocol log file and a Send connector protocol log file to 20 MB.

  -  
    Sets the maximum size of the Receive connector protocol log folder and the Send connector protocol log folder to 400 MB.

  -  
    Sets the maximum age of a Receive connector protocol log file and a Send Connector protocol log file to 45 days.

<!-- end list -->

    Set-TransportService Mailbox01 -ReceiveProtocolLogPath "D:\Hub Receive SMTP Log" -SendProtocolLogPath "D:\Hub Send SMTP Log" -ReceiveProtocolLogMaxFileSize 20MB -SendProtocolLogMaxFileSize 20MB -ReceiveProtocolLogMaxDirectorySize 400MB -SendProtocolLogMaxDirectorySize 400MB -ReceiveProtocolLogMaxAge 45.00:00:00 -SendProtocolLogMaxAge 45.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P>To configure the protocol log settings in the Mailbox Transport service on a Mailbox server, use the <STRONG>Set-MailboxTransportService</STRONG> cmdlet. To configure the protocol log settings in the Front End Transport service on a Client Access server, use the <STRONG>Set-FrontEndTransportService</STRONG> cmdlet.</P>
> <LI>
> <P>Setting the <EM>SendProtocolLogPath</EM> or <EM>ReceiveProtocolLogPath</EM> parameters to the value <CODE>$null</CODE> effectively disables protocol logging for all Send connectors or all Receive connectors on the server. However, setting either of these parameters to <CODE>$null</CODE> when protocol logging is enabled for any other connectors on the server, including the intra-organization Send connector or the mailbox delivery Send connector, event log errors are generated.</P>
> <LI>
> <P>Setting the <EM>ReceiveProtocolLogMaxAge</EM> or <EM>SendProtocolLogMaxAge</EM> parameters to the value <CODE>00:00:00</CODE> prevents the automatic removal of protocol log files because of their age.</P></LI></UL>



## How do you know this worked?

To verify that you have successfully configured the protocol log settings, do the following:

1.  In the Shell, run the following command:
    
        <Get-TransportService | Get-MailboxTransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List SendConnectorProtocolLog*,ReceiveConnectorProtocolLog*

2.  Verify the values displayed are the values you configured.

