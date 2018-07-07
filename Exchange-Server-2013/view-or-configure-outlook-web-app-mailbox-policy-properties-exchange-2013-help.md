---
title: 'View or configure Outlook Web App mailbox policy properties: Exchange 2013 Help'
TOCTitle: View or configure Outlook Web App mailbox policy properties
ms:assetid: be012ffe-8fdb-4fb7-aebd-78b3a55593fa
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd351097(v=EXCHG.150)
ms:contentKeyID: 49315254
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# View or configure Outlook Web App mailbox policy properties

 

_**Applies to:** Exchange Online, Exchange Server 2013_


After you create an Outlook Web App mailbox policy, you can configure a variety of options to control the features available to users in Outlook Web App. For example, you can enable or disable Inbox rules or create a list of allowed file types for attachments.

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 3 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Outlook Web App mailbox policies" entry in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to view or configure Outlook Web App mailbox policies

1.  In the EAC, click **Permissions** \> **Outlook Web App policies**.

2.  In the result pane, click to select the mailbox policy you want to view or configure.

3.  Click the **Edit** button.

4.  
    
    On the **General** tab, you can view and edit the name of the policy.

5.  
    
    On the **Features** tab, use the check boxes to enable or disable features. By default, the most common features are displayed. To see all features that can be enabled or disabled, click **More options**.
    

    > [!NOTE]
    > Features settings for Outlook Web App mailbox policies override Outlook Web App virtual directory settings. You can change segmentation settings for individual users by using the <STRONG>Set-CASMailbox</STRONG> cmdlet in the Shell.



6.  
    
    On the **File Access** tab, use the **Direct file access** check boxes to configure the file access and viewing options for users. File access lets a user open or view the contents of files attached to an email message.
    
    File access can be controlled based on whether a user has signed in on a public or private computer. The option for users to select private computer access or public computer access is available only when you’re using forms-based authentication. All other forms of authentication default to private computer access.

7.  On the **Offline access** tab, use the option buttons to configure offline access availability.

8.  Click **Save** to update the policy.

## Use the Shell to configure Outlook Web App mailbox policies

This example enables calendar access in the default mailbox policy.

    Set-OwaMailboxPolicy -Identity Default -CalendarEnabled $true

For more information about syntax and parameters, see [Set-OwaMailboxPolicy](https://technet.microsoft.com/en-us/library/dd297989\(v=exchg.150\)).

## Use the Shell to view Outlook Web App mailbox policies

This example retrieves the properties of the Outlook Web App mailbox policy `Executives` in the organization `Fabrikam`.

    Get-OwaMailboxPolicy -Identity Fabrikam\Executives

For more information about syntax and parameters, see [Get-OwaMailboxPolicy](https://technet.microsoft.com/en-us/library/dd351095\(v=exchg.150\)).

## How do you know this worked?

To verify that you’ve successfully edited an Outlook Web App mailbox policy:

1.  In the EAC, click **Permissions** \> **Outlook Web App Policies**, and then choose a specific Outlook Web App mailbox policy.

2.  Click the **Edit** button to view the properties of the mailbox policy.

3.  Click **Save** or **Cancel** to close the properties page.

