---
title: 'Create an Outlook Web App mailbox policy: Exchange 2013 Help'
TOCTitle: Create an Outlook Web App mailbox policy
ms:assetid: 347207fa-cfb7-40a6-b19a-831dcdb54ad5
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd335191(v=EXCHG.150)
ms:contentKeyID: 49315248
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Create an Outlook Web App mailbox policy

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can create an Outlook Web App mailbox policy to apply a common set of policy settings. Outlook Web App mailbox policies are useful for applying and standardizing settings, for example, attachment settings, for specific groups of users.

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes.

  - You need to be assigned permissions before you can run this cmdlet. Although all parameters for this cmdlet are listed in this topic, you may not have access to some parameters if they're not included in the permissions assigned to you. To see what permissions you need, see the "Outlook Web App mailbox policies" entry in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to create an Outlook Web App mailbox policy

1.  In the EAC, click **Permissions** \> **Outlook Web App policies**.

2.  Click the **New** button.

3.  
    
    Enter a name for your policy.

4.  
    
    Use the check boxes to enable or disable features. By default, the most common features are displayed. To see all features that can be enabled or disabled, click **More options**.
    

    > [!NOTE]
    > Features settings for Outlook Web App mailbox policies override Outlook Web App virtual directory settings. You can change segmentation settings for individual users by using the <STRONG>Set-CASMailbox</STRONG> cmdlet in the Shell.



5.  Click **Save** to save the policy.

## Use the Shell to create an Outlook Web App mailbox policy

This example creates an Outlook Web App mailbox policy named `Policy1`.

  - In the Shell, run the following command.
    
        New-OwaMailboxPolicy -Name Policy1

For more information about syntax and parameters, see [New-OwaMailboxPolicy](https://technet.microsoft.com/en-us/library/dd351067\(v=exchg.150\)). For information about using the Shell to configure an Outlook Web App mailbox policy, see [Set-OwaMailboxPolicy](https://technet.microsoft.com/en-us/library/dd297989\(v=exchg.150\)).

## How do you know this worked?

To verify that you’ve successfully created an Outlook Web App mailbox policy:

  - In the EAC, click **Permissions** \> **Outlook Web App Policies**, and look for your new mailbox policy.

