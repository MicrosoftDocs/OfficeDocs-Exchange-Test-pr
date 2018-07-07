---
title: 'View mobile device information for users: Exchange 2013 Help'
TOCTitle: View mobile device information for users
ms:assetid: 4fd263c0-ad61-416c-bd68-339bf66605cf
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997974(v=EXCHG.150)
ms:contentKeyID: 49345045
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# View mobile device information for users

 

_**Applies to:** Exchange Server 2013_


Users can configure multiple mobile devices for synchronization with Microsoft Exchange Server 2013. You can use the EAC or the Shell to view a list of mobile devices that are associated with a specific user.

For additional management tasks related to mobile devices, see [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mobile Device mailbox policy" entry in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to view mobile device information for users

The EAC displays a list of mobile devices that are currently synchronizing with a user’s mailbox. You can view mobile devices by family, model, phone number, or status.

1.  In the EAC, click **Recipients** \> **Mailboxes** and choose a mailbox.

2.  In the Details pane, scroll to **Phone and Voice Features** and click **View details** to display the **Mobile Device Details** screen.

## Use the Shell to view mobile device information for users

You can use the **Get-MobileDevice** cmdlet to view a list of mobile devices for a specific user.

1.  Run the following command.
    
        Get-MobileDevice -Mailbox useralias

