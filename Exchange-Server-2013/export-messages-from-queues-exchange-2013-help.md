---
title: 'Export messages from queues: Exchange 2013 Help'
TOCTitle: Export messages from queues
ms:assetid: 688b342c-f380-4fe0-afce-7e38cf490627
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998625(v=EXCHG.150)
ms:contentKeyID: 50646234
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Export messages from queues

 

_**Applies to:** Exchange Server 2013_


When you export a message from a queue to a file, the message isn't removed from the queue. A copy of the message is made in the specified location as a plain text file. The resulting file can be viewed in an application, such as a text editor or an email client application, or the message file can be resubmitted by using the Replay directory on any other Mailbox server or Edge Transport server inside or outside the Exchange organization.

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 15 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Queues" entry in [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - The messages must be in a Suspended state for the export process to be successful. You can export messages from delivery queues, the Unreachable queue, or the poison message queue. Messages in the poison message queue are already in the Suspended state. You can't suspend or export messages that are in the Submission queue.

  - You can't use Queue Viewer in the Exchange Toolbox to export messages. However, you can use Queue Viewer to locate, identify, and suspend the messages before you export them using the Shell.

  - Verify the following information about the target directory location for the message files:
    
      - The target directory must exist before you export any messages. The directory won't be created for you. If an absolute path isn't specified, the current Exchange Management Shell working directory is used.
    
      - The path may be local to the Exchange server, or it may be a Universal Naming Convention (UNC) path to a share on a remote server.
    
      - Your account must have the **Write** permission to the target directory.
    
      - When you specify a file name for the exported messages, be sure to include the .eml file name extension so the files can be opened easily by email client applications or processed correctly by the Replay directory.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to export a specific message from a specific queue

To export a specific message from a specific queue, run the following command:

    Export-Message -Identity <MessageIdentity> | AssembleMessage -Path <FilePath>\<FileName>.eml

This example exports a copy of a message that has the **InternalMessageID** value 1234 that's located in the contoso.com delivery queue on the server named Mailbox01 to the file named export.eml in the path D:\\Contoso Export.

    Export-Message -Identity Exchange01\Contoso.com\1234 | AssembleMessage -Path "D:\Contoso Export\export.eml"

## Use the Shell to export all messages from a specific queue

To export all messages from a specific queue and use the **InternetMessageID** value of each message as the file name, use the following syntax.

    Get-Message -Queue <QueueIdentity> | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

Note that the **InternetMessageID** value contains angled brackets (\> and \<), which need to be removed because they aren't allowed in file names.

This example exports a copy of all the messages from the contoso.com delivery queue on the server named Mailbox01 to the local directory named D:\\Contoso Export.

    Get-Message -Queue Mailbox01\Contoso.com | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

## Use the Shell to export specific messages from all the queues on a server

To export specific messages from all queues on a server and use the **InternetMessageID** value of each message as the file name, use the following syntax.

    Get-Message -Filter {<MessageFilter>} [-Server <ServerIdentity>] | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

Note that the **InternetMessageID** value contains angled brackets (\> and \<), which need to be removed because they aren't allowed in file names.

This example exports a copy of all the messages from senders in the contoso.com domain from all queues on the server named Mailbox01 to the local directory named D:\\Contoso Export.

    Get-Message -Filter {FromAddress -like "*@contoso.com"} -Server Mailbox01 | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}


> [!NOTE]
> If you omit the <EM>Server</EM> parameter, the command operates on the local server.


