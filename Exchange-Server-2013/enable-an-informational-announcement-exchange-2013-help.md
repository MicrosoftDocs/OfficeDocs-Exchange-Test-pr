---
title: 'Enable an informational announcement: Exchange 2013 Help'
TOCTitle: Enable an informational announcement
ms:assetid: 07f6c13e-3781-4127-9321-f0f85f054259
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb266918(v=EXCHG.150)
ms:contentKeyID: 50067616
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Enable an informational announcement

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can enable an informational announcement for a Unified Messaging (UM) auto attendant. When an informational announcement is enabled, it will play immediately after the business or non-business hours greeting. By default, an informational announcement isn't configured. To enable an informational announcement, create a .wav or .wma file to be used as the informational announcement, and then configure the auto attendant to use this sound file.

For additional management tasks related to UM auto attendants, see [UM auto attendant procedures](um-auto-attendant-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM auto attendants" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM auto attendant has been created. For detailed steps, see [Create a UM auto attendant](create-a-um-auto-attendant-exchange-2013-help.md).

  - Create a .wav or .wma file to be used for the informational announcement.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to enable an informational announcement

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan that you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Auto Attendants**, select the UM auto attendant for which you want to enable an informational announcement, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Auto Attendant** page, \> **Greetings**, under **Informational announcement** click **Change**, and then click **Browse** to locate the informational announcement file you created before you started this procedure.
    

    > [!IMPORTANT]
    > The file you use for the greeting must be a .wav or .wma file.



4.  After you've located the file, click **Open**, and then click **Save**.

## Use the Shell to enable an informational announcement

This example enables an informational announcement that uses the `MyInfoAnnouncement.wav` file for the UM auto attendant named `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -InfoAnnouncementEnabled $true -InfoAnnouncementFilename MyInfoAnnouncement.wav

