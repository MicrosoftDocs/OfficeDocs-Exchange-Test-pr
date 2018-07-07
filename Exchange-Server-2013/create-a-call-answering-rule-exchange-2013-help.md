---
title: 'Create a call answering rule: Exchange 2013 Help'
TOCTitle: Create a call answering rule
ms:assetid: 0976f8f2-3449-44f1-b0d1-20c91622e827
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ898495(v=EXCHG.150)
ms:contentKeyID: 50873787
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Create a call answering rule

 

_**Applies to:** Exchange Server 2013, Exchange Server 2016_


You can use the Shell to create one or more call answering rules for a user. You can also use the **New-UMCallAnsweringRule** cmdlet in an Exchange Management Shell script to create call answering rules for multiple users.

Call answering rules are applied to incoming calls similar to the way Inbox rules are applied to incoming email messages. By default, when a user is enabled for Unified Messaging (UM), no call answering rules are configured. Even so, incoming calls are answered by the mail system and callers are prompted to leave a voice message.


> [!NOTE]
> Users that are UM-enabled can sign in to Outlook Web App to create, manage, and remove call answering rules.



For additional management tasks related to Call Answering Rules, see [Forwarding calls procedures](forwarding-calls-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM call answering rules" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform this procedure, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform this procedure, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Before you perform this procedure, confirm that the user's mailbox has been UM-enabled. For detailed steps, see [Enable a user for voice mail](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - You can only use the Shell to perform this procedure. To learn how to open the Exchange Management Shell in your on-premises Exchange organization, see [Open the Shell](https://technet.microsoft.com/en-us/library/dd638134\(v=exchg.150\)). To learn how to use Windows PowerShell to connect to Exchange Online, see [Connect to Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Use the Shell to create a call answering rule

This example creates the call answering rule `MyCallAnsweringRule` in the mailbox for Tony Smith with the priority of 2.

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith

This example creates the call answering rule `MyCallAnsweringRule` in the mailbox for Tony Smith and performs the following actions:

  - Sets the call answering rule to two caller IDs.

  - Sets the priority of the call answering rule to 2.

  - Sets the call answering rule to allow callers to interrupt the greeting.

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

This example creates the call answering rule `MyCallAnsweringRule` in the mailbox for Tony Smith and performs the following actions:

  -  
    Sets the priority of the call answering rule to 2.

  -  
    Creates key mappings for the call answering rule.

  -  
    If the caller reaches the voice mail for the user and the status of the user is set to Busy, the caller can:
    
      - Press the 1 key and be transferred to a receptionist at extension 45678.
    
      - Press the 2 key so the Find Me feature will be used for urgent issues, ring extension 23456 first, and then ring extension 45671.

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith -ScheduleStatus 0x4 - -KeyMappings "1,1,Receptionist,,,,,45678,","5,2,Urgent Issues,23456,23,45671,50,,"

