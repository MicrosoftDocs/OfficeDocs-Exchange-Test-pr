---
title: 'Search message tracking logs: Exchange 2013 Help'
TOCTitle: Search message tracking logs
ms:assetid: e1678327-bcd5-42d4-a363-67f33067fe9a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124926(v=EXCHG.150)
ms:contentKeyID: 50646519
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Search message tracking logs

 

_**Applies to:** Exchange Server 2013_


In Microsoft Exchange Server 2013, the message tracking log is a detailed record of all message activity as messages are transferred to and from the Transport service on Mailbox servers, mailboxes on Mailbox servers, and Edge Transport servers.

You can use the **Get-MessageTrackingLog** cmdlet in the Exchange Management Shell to search for entries in the message tracking log by using specific search criteria.

## What do you need to know before you begin?

  - Estimated time to complete: 30 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Message tracking" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - Searching the message tracking logs requires the Microsoft Exchange Transport Log Search service to be running. If you disable or stop this service, you can't search the message tracking logs or run delivery reports. However, stopping this service does not affect other features in Exchange.

  - The field names displayed by the results from the **Get-MessageTrackingLog** cmdlet are similar to the actual field names used in the message tracking logs. The biggest differences are:
    
      - The dashes are removed from the field names. For example **internal-message-id** is displayed as `InternalMessageId`.
    
      - The **date-time** field is displayed as `Timestamp`.
    
      - The **recipient-address** field is displayed as `Recipients`.
    
      - The **sender-address** field is displayed as `Sender`.

  - The **date-time** field in the message tracking log stores information in Coordinated Universal Time (UTC). However, you should enter your date-time search criteria for the *Start* or *End* parameters in the regional date-time format of the computer that you are using to perform the search.

  - You can't copy the message tracking log files from another Exchange server and then search them by using the **Get-MessageTrackingLog** cmdlet. Also, if you manually save an existing message tracking log file, the change in the file's date-time stamp breaks the query logic that Exchange uses to search the message tracking logs.

  - The Exchange 2013 **Get-MessageTrackingLog** cmdlet is able to search the message tracking logs on Exchange 2007 and Exchange 2010 servers in the same Active Directory site.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to search the message tracking logs

To search the message tracking log entries for specific events, use the following syntax.

    Get-MessageTrackingLog [-Server <ServerIdentity.] [-ResultSize <Integer> | Unlimited] [-Start <DateTime>] [-End <DateTime>] [-EventId <EventId>] [-InternalMessageId <InternalMessageId>] [-MessageId <MessageId>] [-MessageSubject <Subject>] [-Recipients <RecipientAddress1,RecipientAddress2...>] [-Reference <Reference>] [-Sender <SenderAddress>]

To view the 1000 most recent message tracking log entries on the server, run the following command:

    Get-MessageTrackingLog

This example searches the message tracking logs on the local server for all entries from 3/28/2013 8:00 AM to 3/28/2013 5:00 PM for all **FAIL** events where the message sender was pat@contoso.com.

    Get-MessageTrackingLog -ResultSize Unlimited -Start "3/28/2013 8:00AM" -End "3/28/2013 5:00PM" -EventId "Fail" -Sender "pat@contoso.com"

## Use the Shell to control the output of a message tracking log search

Use the following syntax.

    Get-MessageTrackingLog <SearchFilters> | <Format-Table | Format-List> [<FieldNames>] [<OutputFileOptions>]

This example searches the message tracking logs using the following search criteria:

  - Return results for the first 1,000 **Send** events.

  - Display the results in the list format.

  - Display only those field names that begin with `Send` or `Recipient`.

  - Write the output to a new file named `D:\Send Search.txt`

<!-- end list -->

    Get-MessageTrackingLog -EventId Send | Format-List Send*,Recipient* > "D:\Send Search.txt"

## Use the Shell to search the message tracking logs for message entries on multiple servers

Typically, the value in the **MessageID:** header field remains constant as the message travels throughout the Exchange organization. This property is named **InternetMessageId** in queue viewing utilities, and **MessageId** in the message tracking log viewing utilities. After you have determined the `MessageID:` value of a specific message, you can search for information about that message in the message tracking logs on every Mailbox server in your Exchange organization.

To search all message tracking log entries for a specific message across all Mailbox servers, use the following syntax.

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId <MessageID> | Select-Object <CommaSeparatedFieldNames> | Sort-Object -Property <FieldName>

This example searches the message tracking logs on all Exchange 2013 Mailbox servers using the following search criteria:

  - Find any entries related to a message that has a **MessageID:** value of `<ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com>`. Note that you can omit the angle bracket characters (`< ``>`). If you don't, you need to enclose the entire **MessageID:** value in quotation marks.

  - For each entry, display the fields **date-time**, **server-hostname**, **client-hostname**, **source**, **event-id**, and **recipient-address**.

  - Sort the results by the **date-time** field.

<!-- end list -->

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com | Select-Object Timestamp,ServerHostname,ClientHostname,Source,EventId,Recipients | Sort-Object -Property Timestamp

## Use the EAC to search the message tracking logs

You can use the Delivery Reports for administrators feature in the Exchange admin center (EAC) to search the message tracking logs for information about messages sent by or received by a specific mailbox in your organization. For more information see [Track messages with delivery reports](track-messages-with-delivery-reports-exchange-2013-help.md).

