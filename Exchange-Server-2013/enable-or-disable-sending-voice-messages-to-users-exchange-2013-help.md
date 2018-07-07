---
title: 'Enable or disable sending voice messages to users: Exchange 2013 Help'
TOCTitle: Enable or disable sending voice messages to users
ms:assetid: faa300d8-2534-40db-8ef9-428be8bb7934
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd351277(v=EXCHG.150)
ms:contentKeyID: 49315551
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Enable or disable sending voice messages to users

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can enable callers to send voice messages to users from a Unified Messaging (UM) auto attendant, or prevent them from doing so. By default, this option is enabled and lets callers send voice messages to users in the UM dial plan that's associated with the UM auto attendant. If you disable this option, the auto attendant won't invite callers to send a voice message during a system prompt.

For additional management tasks related to UM auto attendants, see [UM auto attendant procedures](um-auto-attendant-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM auto attendants" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM auto attendant has been created. For detailed steps, see [Create a UM auto attendant](create-a-um-auto-attendant-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to enable callers to send voice messages or prevent them from doing so

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Auto Attendants**, select the UM auto attendant you want to manage, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Auto Attendant** page \> **Address book and operator access**, under **Options for contacting users**, select the check box next to **Allow callers to leave voice messages for users** to enable callers to leave voice messages. To prevent callers from leaving voice messages, clear the check box.

4.  Click **Save**.


> [!NOTE]
> If you disable this option and also disable the <STRONG>Allow callers to dial users</STRONG> option, the <STRONG>Options for searching the address book</STRONG> are also disabled.



## Use the Shell to enable callers to send voice messages or prevent them from doing so

This example prevents callers who call in to a UM auto attendant named `MyUMAutoAttendant` from sending voice messages.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $false

This example enables callers who call in to a UM auto attendant named `MyUMAutoAttendant` to send voice messages.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $true

