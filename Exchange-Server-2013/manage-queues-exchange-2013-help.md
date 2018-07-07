---
title: 'Manage queues: Exchange 2013 Help'
TOCTitle: Manage queues
ms:assetid: 37f11378-a884-4aff-ab55-689f40a46321
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997263(v=EXCHG.150)
ms:contentKeyID: 50646231
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Manage queues

 

_**Applies to:** Exchange Server 2013_


In Microsoft Exchange Server 2013, you can use the Queue Viewer in the Exchange Toolbox or the Exchange Management Shell to manage queues. For more information about using the queue management cmdlets in the Exchange Management Shell, see [Use the Exchange Management Shell to manage queues](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 15 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Queues" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## View queues

## Use Queue Viewer in the Exchange Toolbox to view queues

1.  Click **Start** \> **All Programs** \> **Microsoft Exchange 2013** \> **Exchange Toolbox**.

2.  In the **Mail flow tools** section, double-click **Queue Viewer** to open the tool in a new window.

3.  In Queue Viewer, click the **Queues** tab. A list of all queues on the server to which you're connected is displayed.

4.  You can use the **Export List** link in the action pane to export the list of queues. For more information, see [Export lists from Queue Viewer](export-lists-from-queue-viewer-exchange-2013-help.md).

## Use the Shell to view queues

To view queues, use the following syntax.

    Get-Queue [-Filter <Filter> -Server <ServerIdentity> -Include <Internal | External | Empty | DeliveryType> -Exclude <Internal | External | Empty | DeliveryType>]

This example displays basic information about all non-empty queues on the Exchange 2013 Mailbox server named Mailbox01.

    Get-Queue -Server Mailbox01 -Exclude Empty

This example displays detailed information for all queues that contain more than 100 messages on the Mailbox server on which the command is run.

    Get-Queue -Filter {MessageCount -gt 100} | Format-List

## Use the Shell to view queue summary information on multiple Exchange servers

The **Get-QueueDigest** cmdlet provides a high-level, aggregate view of the state of queues on all servers within a specific scope, for example, a DAG, an Active Directory site, a list of servers, or the entire Active Directory forest. Note that queues on a subscribed Edge Transport server in the perimeter network aren't included in the results. Also, **Get-QueueDigest** is available on an Edge Transport server, but the results are restricted to queues on the Edge Transport server.


> [!NOTE]
> By default, the <STRONG>Get-QueueDigest</STRONG> cmdlet displays delivery queues that contain ten or more messages, and the results are between one and two minutes old. For instructions on how to change these default values, see <A href="configure-get-queuedigest-exchange-2013-help.md">Configure Get-QueueDigest</A>.



To view summary information about queues on multiple Exchange servers, run the following command:

    Get-QueueDigest <-Server <ServerIdentity1,ServerIdentity2,..> | -Dag <DagIdentity1,DagIdentity2...> | -Site <ADSiteIdentity1,ADSiteIdentity2...> | -Forest> [-Filter <Filter>]

This example displays summary information about the queues on all Exchange 2013 Mailbox servers in the Active Directory site named FirstSite where the message count is greater than 100.

    Get-QueueDigest -Site FirstSite -Filter {MessageCount -gt 100}

This example displays summary information about the queues on all Exchange 2013 Mailbox servers in the database availability group (DAG) named DAG01 where the queue status has the value **Retry**.

    Get-QueueDigest -Dag DAG01 -Filter {Status -eq "Retry"}

## Resume queues

By resuming a queue, you restart outgoing activities on a queue that has a status of Suspended. The queue must have a status of Suspended for this action to have any effect. When you resume a queue, the status of messages in the queue doesn't change. Messages that have a status of Suspended remain suspended and don't leave the queue.

## Use Queue Viewer in the Exchange Toolbox to resume queues

1.  Click **Start** \> **All Programs** \> **Microsoft Exchange 2013** \> **Exchange Toolbox**.

2.  In the **Mail flow tools** section, double-click **Queue Viewer** to open the tool in a new window.

3.  In Queue Viewer, click the **Queues** tab. A list of all queues on the server to which you're connected is displayed.

4.  Click **Create Filter**, and enter your filter expression as follows:
    
    1.  Select **Status** from the queue property drop-down list.
    
    2.  Select **Equals** from the comparison operator drop-down list.
    
    3.  Select **Suspended** from the value drop-down list.

5.  Click **Apply Filter**. All queues on the server that are currently suspended are displayed.

6.  Select one or more queues from the list, right-click, and then select **Resume**.

## Use the Shell to resume queues

To resume queues, use the following syntax.

    Resume-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

This example resumes all queues on the local server that have a status of Suspended.

    Resume-Queue -Filter {Status -eq "Suspended"}

This example resumes the suspended delivery queue named contoso.com on the server named Mailbox01.

    Resume-Queue -Identity Mailbox01\contoso.com

## How do you know this worked?

To verify that you have successfully resumed a queue, do the following:

1.  Use the Queue Viewer or the **Get-Queue** cmdlet to find the queue you attempted to resume.

2.  Verify the queue **Status** property doesn't have the value `Suspended`.

## Retry queues

When a transport server can't connect to the next hop, the delivery queue is put in a status of Retry. When you retry a delivery queue by using Queue Viewer or the Shell, you force an immediate connection attempt and override the next scheduled retry time. If the connection isn't successful, the retry interval timer is reset. The delivery queue must be in a status of Retry for this action to have any effect.

## Use Queue Viewer in the Exchange Toolbox to retry a queue

1.  Click **Start** \> **All Programs** \> **Microsoft Exchange 2013** \> **Exchange Toolbox**.

2.  In the **Mail flow tools** section, double-click **Queue Viewer** to open the tool in a new window.

3.  In Queue Viewer, click the **Queues** tab. A list of all queues on the server to which you're connected is displayed.

4.  Click **Create Filter**, and enter your filter expression as follows:
    
    1.  Select **Status** from the queue property drop-down list.
    
    2.  Select **Equals** from the comparison operator drop-down list.
    
    3.  Select **Retry** from the value drop-down list.

5.  Click **Apply Filter**. All queues that currently have a **Retry** status are displayed.

6.  Select one or more queues from the list. Right-click, and then select **Retry Queue**. If the connection attempt is successful, the queue status changes to **Active**. If no connection can be made, the queue remains in a status of **Retry** and the next retry time is updated.

## Use the Shell to retry a queue

To retry queues, use the following syntax.

    Retry-Queue <-Identity QueueIdentity | -Filter QueueFilter [-Server ServerIdentity]>

This example retries all queues on the local server with the status of Retry.

    Retry-Queue -Filter {status -eq "retry"}

This example retries the queue named contoso.com that's in the `Retry` state on the server named Mailbox01.

    Retry-Queue -Identity Mailbox01\contoso.com

## How do you know this worked?

To verify that you have successfully retried a queue, do the following:

1.  Use the Queue Viewer or the **Get-Queue** cmdlet to find the queue you attempted to retry.

2.  Verify the queue **LastRetryTime** property matches the time you attempted to retry the queue.

## Resubmit messages in queues

Resubmitting a queue is similar to retrying a queue, except the messages are sent back to the Submission queue for the categorizer to reprocess. You can resubmit messages that have the following status:

  - Delivery queues that have the status of Retry. The messages in the queues can't be in the Suspended state.

  - Messages in the Unreachable queue that aren't in the Suspended state.

  - Messages in the poison message queue.

## Use the Shell to resubmit messages

To resubmit messages, use the following syntax.

    Retry-Queue <-Identity QueueIdentity | -Filter {Status -eq "Retry"} -Server ServerIdentity> -Resubmit $true

This example resubmits all messages located in any delivery queues with the status of Retry on the server named Mailbox01.

    Retry-Queue -Filter {Status -eq "Retry"} -Server Mailbox01 -Resubmit $true

This example resubmits all messages located in the Unreachable queue on the server Mailbox01.

    Retry-Queue -Identity Mailbox01\Unreachable -Resubmit $true

## Resubmit messages in the poison message queue

You resubmit messages in the poison message queue by resuming the message. You can use the Queue Viewer or the Shell to resubmit messages from the poison message queue. Note that the poison message queue is only visible in Queue Viewer when there are messages in the poison message queue.


> [!NOTE]
> The poison message queue contains messages that are determined to be harmful to the Exchange system after a server failure. The messages may be genuinely harmful in their content or format. Alternatively, they may be victims of a poorly written agent that crashed the Exchange server while it was processing the supposedly bad messages. If you're unsure of the safety of the messages in the poison message queue, you should export the messages to files so that you can examine them. For more information, see <A href="export-messages-from-queues-exchange-2013-help.md">Export messages from queues</A>.



## Use Queue Viewer in the Exchange Toolbox to resubmit messages in the poison message queue

1.  Click **Start** \> **All Programs** \> **Microsoft Exchange 2013** \> **Exchange Toolbox**.

2.  In the **Mail flow tools** section, double-click **Queue Viewer** to open the tool in a new window.

3.  In Queue Viewer, click the **Queues** tab. A list of all queues on the server to which you're connected is displayed.

4.  Click the poison message queue. In the action pane, select **View Messages**.

5.  Select one or more messages from the list, right-click, and select **Resume**.

## Use the Shell to resubmit messages in the poison message queue

To resubmit a message from the poison message queue, perform the following steps.

1.  Find the identity of the message by running the following command.
    
        Get-Message -Queue Poison | Format-Table Identity

2.  Use the identity of the message from the previous step in the following command.
    
        Resume-Message <PoisonMessageIdentity>
    
    This example resumes a message from the poison message queue that has the message Identity value of 222.
    
        Resume-Message 222

## How do you know this worked?

To verify that you have successfully resubmitted a message from the poison message queue, do the following:

1.  Use the Queue Viewer or the **Get-Queue** cmdlet to view the poison message queue where you attempted to resubmit the message.

2.  Verify the message is no longer in the poison message queue. Note that an empty poison message queue doesn't appear in the Queue Viewer or the **Get-Queue** cmdlet. Therefore, if the message you resubmitted was the only message in the poison message queue, and the poison message queue is no longer visible, that is also an indication of a successful message resubmission.

## Suspend queues

When you suspend a queue, you prevent messages from leaving the queue, but you don't change the status of messages in the queue. Messages that are in delivery through SMTP-send will finish operations. You can suspend a queue to stop mail flow, and then suspend one or more messages in the queue. When you resume the queue, the messages that were suspended won't leave the queue.

You can suspend a queue that has a status of Active or Retry. You can also suspend the Unreachable queue and the Submission queue.

If you suspend the Unreachable queue, items won't be resubmitted to the categorizer when configuration updates are received by the transport server until the queue is resumed. If you suspend the Submission queue, messages won't be picked up by the categorizer until the queue is resumed.

## Use Queue Viewer in the Exchange Toolbox to suspend a queue

1.  Click **Start** \> **All Programs** \> **Microsoft Exchange 2013** \> **Exchange Toolbox**.

2.  In the **Mail flow tools** section, double-click **Queue Viewer** to open the tool in a new window.

3.  In Queue Viewer, click the **Queues** tab. A list of all queues on the server to which you're connected is displayed. You can create a filter to display only queues that meet specific criteria.

4.  Select one or more queues, right-click, and then select **Suspend**.

## Use the Shell to suspend a queue

To suspend a queue, use the following syntax.

    Suspend-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

This example suspends all queues on the local server that have a message count equal to or greater than 1,000 and that have a status of Retry.

    Suspend-Queue -Filter {MessageCount -ge 1000 -and Status -eq "Retry"}

This example suspends the queue named contoso.com on the server named Mailbox01.

    Suspend-Queue -Identity Mailbox01\contoso.com

## How do you know this worked?

To verify that you have successfully suspended a queue, do the following:

1.  Use the Queue Viewer or the **Get-Queue** cmdlet to find the queue you attempted to suspend.

2.  Verify the queue **Status** property has the value `Suspended`.

