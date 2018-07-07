---
title: 'Configure the group of users that can be contacted: Exchange 2013 Help'
TOCTitle: Configure the group of users that can be contacted
ms:assetid: 45d9d6d5-c9d6-4b73-8aa2-a23599a4381c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee423545(v=EXCHG.150)
ms:contentKeyID: 49315405
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure the group of users that can be contacted

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can specify the group of users that callers can contact when calling into a Unified Messaging (UM) auto attendant. By default, callers can contact users within the same dial plan that's associated with the UM auto attendant. However, you can change the grouping of users to allow callers to transfer calls or send voice messages to users who are located in the organization’s address book or to a specific set of users.

For additional management tasks related to UM auto attendants, see [Manage a UM auto attendant](manage-a-um-auto-attendant-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM auto attendants" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM auto attendant has been created. For detailed steps, see [Create a UM auto attendant](create-a-um-auto-attendant-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to configure the group of users that callers can contact

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Auto Attendants**, select the UM auto attendant you want to configure, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Auto Attendant** page \> **Address book and operator access**, under **Options for searching the address book**, choose from the following options:
    
      - **In this dial plan only**   Select this option to allow callers who connect to the UM auto attendant to locate and contact users who are in the dial plan associated with the UM auto attendant.
    
      - **In the entire organization**   Select this option to allow callers who connect to the UM auto attendant to locate and contact anyone listed in the organization’s address book. This includes all users who are mailbox-enabled.

4.  Click **Save**.

## Use the Shell to configure the group of users that callers can contact

This example sets the scope of the users that callers can contact to all users in the organization’s address book on a UM auto attendant named `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -ContactScope GlobalAddressList

