---
title: 'View a UM hunt group: Exchange 2013 Help'
TOCTitle: View a UM hunt group
ms:assetid: f038f7b4-4de9-4373-bd58-09d49e37a3ed
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb125167(v=EXCHG.150)
ms:contentKeyID: 49315548
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# View a UM hunt group

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


When you view the properties for a Unified Messaging (UM) hunt group, you can view the properties associated with a single UM hunt group or with all UM hunt groups associated with a single UM IP gateway. If neither parameter is specified, all UM hunt groups will be returned. You can’t use the EAC to view UM hunt group properties; you must use the Shell.

After a UM hunt group has been created, the configured settings can't be changed. If you want to change a configuration setting such as the pilot identifier on a UM hunt group, you must delete the existing UM hunt group and create a new UM hunt group that has the correct settings.

For additional tasks related to UM hunt groups, see [UM hunt group procedures](um-hunt-group-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM hunt groups" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform this procedure, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform this procedure, confirm that a UM gateway has been created. For detailed steps, see [Create a UM IP gateway](create-a-um-ip-gateway-exchange-2013-help.md).

  - Before you perform this procedure, confirm that a UM hunt group has been created. For detailed steps, see [Create a UM hunt group](create-a-um-hunt-group-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to view the properties of a UM hunt group

This example displays all the UM hunt groups in the Active Directory forest.

    Get-UMHuntGroup

This example displays the details of a UM hunt group named `MyUMHuntGroup` in a formatted list.

    Get-UMHuntGroup -identity MyUMIPGateway\MyUMHuntGroup | Format-List


> [!NOTE]
> When you’re using the <STRONG>Get-UMHuntGroup</STRONG> cmdlet, you can’t enter only the name of the UM hunt group. You must also include the name of the UM IP gateway that’s associated with the UM hunt group.


