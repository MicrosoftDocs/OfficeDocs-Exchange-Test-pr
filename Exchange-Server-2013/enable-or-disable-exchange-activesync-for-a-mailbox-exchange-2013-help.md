---
title: 'Enable or disable Exchange ActiveSync for a mailbox: Exchange 2013 Help'
TOCTitle: Enable or disable Exchange ActiveSync for a mailbox
ms:assetid: dcf7c05b-b1b9-4b0f-800d-fec9f2ddc9e4
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124809(v=EXCHG.150)
ms:contentKeyID: 50387724
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Enable or disable Exchange ActiveSync for a mailbox

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can use the EAC or the Shell to enable or disable Microsoft Exchange ActiveSync for a user mailbox. Exchange ActiveSync is a client protocol that lets users synchronize a mobile device with their Exchange mailbox. Exchange ActiveSync is enabled by default when a user mailbox is created. To learn more, see [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 2 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Exchange ActiveSync settings" entry in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to enable or disable Exchange ActiveSync

1.  In the EAC, navigate to **Recipients** \> **Mailboxes**.

2.  In the list of user mailboxes, click the mailbox that you want to enable or disable Exchange ActiveSync for, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the mailbox properties page, click **Mailbox Features**.

4.  Under **Mobile Devices**, do one of the following:
    
      - To disable Exchange ActiveSync click **Disable Exchange ActiveSync**.
        
        A warning appears asking if you're sure you want to disable Exchange ActiveSync. Click **Yes**.
    
      - To enable Exchange ActiveSync, click **Enable Exchange ActiveSync**.

5.  Click **Save** to save your change.


> [!NOTE]
> You can enable and disable Exchange ActiveSync for multiple user mailboxes by using the EAC bulk edit feature. For more information about how to do this, see the "Bulk edit user mailboxes" section in <A href="manage-user-mailboxes-exchange-2013-help.md">Manage user mailboxes</A>.



## Use the Shell to enable or disable Exchange ActiveSync

This example disables Exchange ActiveSync for the mailbox of Yan Li.

    Set-CASMailbox -Identity "Yan Li" -ActiveSyncEnabled $false

This example enables Exchange ActiveSync for the mailbox of Elly Nkya.

    Set-CASMailbox -Identity Ellyn@contoso.com -ActiveSyncEnabled $true

For detailed syntax and parameter information, see [Set-CASMailbox](https://technet.microsoft.com/en-us/library/bb125264\(v=exchg.150\)).

## How do you know this worked?

To verify that you’ve successfully enabled or disabled Exchange ActiveSync for a user mailbox, do one of the following:

  - In the EAC, navigate to **Recipients** \> **Mailboxes**, click the mailbox, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

  - On the mailbox properties page, click **Mailbox Features**.

  - Under **Mobile Devices**, verify whether Exchange ActiveSync is enabled or disabled.

Or

  - Run the following command in the Shell.
    
        Get-CASMailbox <identity>
    
    If Exchange ActiveSync is enabled, the value for the *ActiveSyncEnabled* property is `True`. If Exchange ActiveSync is disabled, the value is `False`.

