---
title: 'Testing and troubleshooting with the Test-UMConnectivity cmdlet: Exchange 2013 Help'
TOCTitle: Testing and troubleshooting with the Test-UMConnectivity cmdlet
ms:assetid: 08e67a99-e37f-4afd-bd58-455b62580af7
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa995978(v=EXCHG.150)
ms:contentKeyID: 55129207
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Testing and troubleshooting with the Test-UMConnectivity cmdlet

 

_**Applies to:** Exchange Online, Exchange Server 2013_


After you install the Client Access and Mailbox servers and configure Unified Messaging, you can use multiple diagnostic tests and a software-based telephone application to test telephony connectivity and the operation of the Unified Messaging services.

## Test-UMConnectivity

The **Test-UMConnectivity** cmdlet can be used to check connectivity to Client Access and Mailbox servers in several ways, depending on the parameters used with the cmdlet. For testing Unified Messaging functionality, you can use these tests:

  - **Local**   The **Test-UMConnectivity** cmdlet verifies Voice over IP (VoIP) communication with the Mailbox servers running on the same local computer.

  - **Local with TUILogon**   The **Test-UMConnectivity** cmdlet tries to establish VoIP communication with the Mailbox server running on the same computer. If it connects, it tries to sign in to one or more UM-enabled mailboxes by sending the extension number and PIN of the mailbox. If the *–TUILogon* parameter is supplied, the following parameter values must also be supplied with the appropriate information for the test mailbox:
    
      - *–Phone*   This parameter must contain the extension number for the test mailbox.
    
      - *–PIN*   This parameter must contain the PIN of the UM-enabled mailbox.
    
      - *–UMDialPlan   *This parameter must contain the dial plan linked with the test mailbox.

  - **Remote**   The **Test-UMConnectivity** cmdlet tries to connect to a remote Client Access server by placing a call through a VoIP gateway. After it connects, it performs connectivity checks on the remote Client Access server and the media paths.
    

    > [!NOTE]
    > If you receive the following message, you should restart the Microsoft&nbsp;Exchange Unified Messaging service because it has stopped or is not responding: "The Test-UMConnectivity task encountered an error while trying to make a call. Details: Unable to establish a connection."


