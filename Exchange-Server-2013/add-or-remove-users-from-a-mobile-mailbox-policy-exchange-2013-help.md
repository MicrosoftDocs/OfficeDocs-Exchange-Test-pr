---
title: 'Add or remove users from a mobile mailbox policy: Exchange 2013 Help'
TOCTitle: Add or remove users from a mobile mailbox policy
ms:assetid: 4ca8e395-c074-4165-b788-16fae3e2ccab
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997929(v=EXCHG.150)
ms:contentKeyID: 49318497
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Add or remove users from a mobile mailbox policy

 

_**Applies to:** Exchange Server 2013_


A mobile device mailbox policy allows you to apply a common set of security and mobile device settings to a group of users. You can create multiple mobile device mailbox policies.


> [!WARNING]
> When you install Microsoft Exchange Server 2013, a default mobile device mailbox policy is created and all users are automatically assigned this policy.



For additional management tasks related to mobile device mailbox policies, see [Mobile device mailbox policies](mobile-device-mailbox-policies-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mobile Device mailbox policy" entry in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

  - You must have one mobile device mailbox policy available in the EAC in **Mobile** \> **Mobile Device Mailbox Policies**.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Change a user’s mobile device mailbox policy

You can use the EAC or the Shell to change a user’s mobile device mailbox policy.

## Use the EAC to change a user’s mobile device mailbox policy

You change a single user’s mobile device mailbox policy using the EAC.

1.  In the EAC, click **Recipients** \> **Mailboxes** and then select a mailbox.

2.  In the Details pane, scroll to **Phone and Voice Features** and select **View details** to display the **Mobile Device Details** screen.

3.  The mobile device mailbox policy that’s currently assigned is displayed. To change the mobile device mailbox policy, click **Browse**.

4.  Choose the appropriate mobile device mailbox policy from the list, click **OK** and then click **Save**.

## Use the Shell to add a user to a mobile device mailbox policy

You can change a single user’s mobile device mailbox policy using the **Set-CASMailbox** cmdlet in the Shell.

1.  In the Shell, run the following command.
    
        Set-CASMailbox -Identity tony@contoso.com -ActiveSyncMailboxPolicy "Sales" 

## How do you know this worked?

To verify that you’ve successfully changed a user’s mobile device mailbox policy, do one of the following:

1.  In the EAC, click **Recipients** \> **Mailboxes**, and then choose a specific recipient. In the Details pane, scroll down to **Phone and Voice Features** and click **View details**.

2.  In the Shell, run the following command.
    
        Get-CASMailbox -Identity tony@contoso.com 

## Change the mobile device mailbox policy for multiple users at the same time

If you want to change the mobile device mailbox policy for multiple users at the same time, you can use the bulk edit functionality in the EAC or use the Shell to change the mobile device mailbox policy for a filtered set of users.

## Use the bulk edit tool in the EAC to change the mobile device mailbox policy for multiple users

You can update the mobile device mailbox policy for multiple users at once using the Bulk Edit functionality.

1.  In the EAC, click **Recipients** \> **Mailboxes**.

2.  Select multiple users.

3.  In the Details pane, scroll down to **Exchange ActiveSync** and click **Update a policy**.

4.  Click **Browse** to choose a mobile device mailbox policy.

5.  Click **OK** and then click **Save**.

## Use the Shell to change the mobile device mailbox policy for a filtered set of users

You can use the Shell to change the mobile device mailbox policy for a filtered set of users. You can filter users on a variety of attributes.

1.  In the Shell, run the following command.
    
        Get-Mailbox | where { $_.CustomAttribute1 -match "Manager"
         } | Set-CASMailbox -activesyncmailboxpolicy(Get-ActiveSyncMailboxPolicy "Contoso").Identity
    

    > [!NOTE]
    > You can substitute <CODE>CustomAttribute1</CODE> for any of the properties on the <STRONG>Get-Mailbox</STRONG> object. To view the full list, type: <CODE>Get-Mailbox username |fl</CODE>.



## How do you know this worked?

To verify that you’ve successfully changed a user’s mobile device mailbox policy, do one of the following:

1.  In the EAC, click **Recipients** \> **Mailboxes**, and choose a specific recipient. In the Details pane, scroll down to **Phone and Voice Features** and click **View details**.

2.  In the Shell, run the following command.
    
        Get-CASMailbox -Identity tony@contoso.com

