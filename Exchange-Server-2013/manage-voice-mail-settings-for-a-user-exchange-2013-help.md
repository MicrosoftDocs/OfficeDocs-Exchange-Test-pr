---
title: 'Manage voice mail settings for a user: Exchange 2013 Help'
TOCTitle: Manage voice mail settings for a user
ms:assetid: 73957938-048a-4f9c-bd0f-a3c2c3dcd638
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998851(v=EXCHG.150)
ms:contentKeyID: 49315437
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Manage voice mail settings for a user

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can view or set the Unified Messaging (UM) and voice mail features and configuration settings for a user that’s been enabled for UM and voice mail. For example, you can do the following:

  - Reset their Outlook Voice Access PIN.

  - Add a personal operator extension number.

  - Add other extension numbers.

  - Enable or disable Automatic Speech Recognition (ASR).

  - Enable or disable Call Answering Rules.

  - Enable or disable access to their email or calendar.


> [!NOTE]
> Some of the settings and features can only be configured by using the Shell.



For additional management tasks related to users who are enabled for voice mail, see [Voice mail-enabled user procedures](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailboxes" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Before you perform these procedures, confirm that the existing user is currently enabled for Unified Messaging. For detailed steps, see [Enable a user for voice mail](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to view or configure a UM-enabled user's properties

1.  In the EAC, navigate to **Recipients** \> **Mailboxes**.

2.  In the list view, select the mailbox for which you want to change the UM mailbox policy.

3.  In the details pane, under **Phone and Voice Features** \> **Unified Messaging**, click **View details**.

4.  On the **UM Mailbox** page, click **UM mailbox settings** to view or change the following UM properties for an existing UM-enabled user:
    
      - **PIN Status**   This display-only field shows the status of the user's mailbox. By default, when a user is UM-enabled, the PIN status is listed as **Not locked out**. However, if the user has input an incorrect Outlook Voice Access PIN multiple times, the status is listed as **Locked Out**.
    
      - **UM mailbox policy**   This box shows the name of the UM mailbox policy associated with the UM-enabled user. You can click **Browse** to locate and specify the UM mailbox policy to be associated with this UM mailbox.
    
      - **Personal operator extension**   Use this box to specify the operator extension number for the user. By default, an extension number isn't configured. The length of the extension number can be from 1 through 20 characters. This enables incoming calls for the UM-enabled user to be forwarded to the extension number that you specify in this box.
        
        You can configure other types of operator extension numbers on dial plans and auto attendants. However, those extensions are generally meant for company-wide receptionists or operators. The personal operator extension setting could be used when an administrative assistant or personal assistant answers incoming calls before they're answered for a particular user.

5.  On the **UM Mailbox** page, under **Other extensions**, you can add, change, and view extension numbers for the user.
    
      - To add an extension number, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"). On the **Add another extension** page, use **Browse** to select the UM dial plan, and then enter the extension number in the **Extension number** box.
    
      - To remove an extension number, select the extension number you want to remove, and then click **Remove** ![Remove icon](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Remove icon").

6.  If you make any changes, click **Save**.

## Use the Shell to configure features for a UM-enabled user

This example disables Play on Phone and missed call notifications, but enables text message (SMS) notifications.


> [!NOTE]
> For on-premises and hybrid deployments, when you’re integrating Unified Messaging and Lync Server, missed call notifications aren’t available to users who have a mailbox located on an Exchange 2007 or Exchange 2010 Mailbox server. A missed call notification is generated when a user disconnects before the call is sent to a Mailbox server.



    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -MissedCallNotificationEnabled $false -PlayonPhoneEnabled $false -SMSMessageWaitingNotificationEnabled $true

This example prevents a user from accessing the calendar, but enables access to email when the user is using Outlook Voice Access.

    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -Extension 523456 -FAXEnabled $true -TUIAccessToCal $false -TUIAccessToEmail True

This example prevents a user from accessing the calendar and email when the user is using Outlook Voice Access.

    Set-UMMailbox -Identity tony@contoso.com -TUIAccessToCalendarEnabled $false -TUIAccessToEmailEnabled $false

This example prevents a user from creating call answering rules, receiving incoming faxes, and using Outlook Voice Access, but enables Automatic Speech Recognition (ASR).

    Set-UMMailbox -Identity tony@contoso.com -AutomaticSpeechRecognitionEnabled $true -CallAnsweringRulesEnabled $false -FaxEnabled $false -SubscriberAccessEnabled $false 

## Use the Shell to view a UM-enabled user's properties

This example displays a list of all the UM-enabled mailboxes in the forest in a formatted list.

    Get-UMMailbox | Format-List

This example displays the UM mailbox properties for tonysmith@contoso.com.

    Get-UMMailbox -Identity tonysmith@contoso.com


> [!IMPORTANT]
> When you’re running Exchange 2007 and Exchange 2013 and the user’s mailbox is located on an Exchange 2007 Mailbox server, running the <STRONG>Get-UMMailbox</STRONG> cmdlet won’t work correctly. To resolve the issue, run the <STRONG>Get-UMMailbox</STRONG> cmdlet from an Exchange 2007 server or a computer running the Exchange 2007 administrative tools.


