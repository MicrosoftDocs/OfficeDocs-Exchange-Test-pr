---
title: 'Remove Mailbox and Client Access servers from a SIP URI dial plan: Exchange 2013 Help'
TOCTitle: Remove Mailbox and Client Access servers from a SIP URI dial plan
ms:assetid: 367441e1-1a0f-42c8-9fa8-8abe80b3d015
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997238(v=EXCHG.150)
ms:contentKeyID: 53401614
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Remove Mailbox and Client Access servers from a SIP URI dial plan

 

_**Applies to:** Exchange Server 2013_


You can remove Client Access and Mailbox servers from SIP URI dial plans. When you’re deploying Microsoft Lync Server, to enable outbound calling to work correctly, you must manually add all Client Access and Mailbox servers to the SIP URI dial plans that you’ve created for Lync Server. However, you may need to remove a Client Access or Mailbox server from your Lync deployment, for example, if you’re performing maintenance or taking the server offline.

For additional management tasks related to UM dial plans, see [UM dial plan procedures](um-dial-plan-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM dial plans" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a SIP URI dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to remove a Mailbox server from a SIP URI dial plan

1.  In the EAC, navigate to **Servers** \> **Servers**.

2.  In the list view, select the Mailbox server you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **Exchange Server** page, click **Unified Messaging**.

4.  Under **UM Service settings** \> **Associated dial plans**, locate the SIP URI dial plan to remove, click **Remove** ![Remove icon](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Remove icon"), and then click **Save**. If you want to remove more than one SIP URI dial plan, press and hold the CTRL key, select the dial plans you want to remove, and then click **Save**.

## Use the Shell to remove a Mailbox server from a SIP URI dial plan

This example removes the Mailbox server named `MyMailboxServer` from a SIP URI dial plan named `MySIPDialPlan`.

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMService MyMailboxServer
    $s.dialplans-=$dp.identity
    Set-UMService -id MyMailboxServer -dialplans:$s.dialplans

In this example, there are three SIP URI dial plans: SipDP1, SipDP2 and SipDP3. This example removes the Mailbox server named `MyMailboxServer` from the SipDP3 dial plan.

    Set-UMService -id MyMailboxServer -DialPlans SipDP1,SipDP2

In this example, there are two SIP URI dial plans: SipDP1 and SipDP2. This example removes the Mailbox server named `MyMailboxServer` from the SipDP2 dial plan.

    Set-UMService -id MyMailboxServer -DialPlans SipDP1

This example removes the Mailbox server named `MyMailboxServer` from all SIP dial plans.

    Set-UMService -id MyUMServer -DialPlans $null

## Use the EAC to remove a Client Access server from a SIP URI dial plan

1.  In the EAC, navigate to **Servers** \> **Servers**.

2.  In the list view, select the Client Access server you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **Exchange Server** page, click **Unified Messaging**.

4.  Under **UM Call Router settings** \> **Associated dial plans**, locate the SIP URI dial plan to remove, click **Remove** ![Remove icon](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Remove icon"), and then click **Save**. If you want to remove more than one SIP URI dial plan, press and hold the CTRL key, select the dial plans you want to remove, and then click **Save**.

## Use the Shell to remove a Client Access server from a SIP URI dial plan

This example removes the Client Access server named `MyClientAccessServer` from a SIP URI dial plan named `MySIPDialPlan`.

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMCallRouterSettings MyClientAccessServer
    $s.dialplans-=$dp.identity
    Set-UMCallRouterSettings -id MyClientAccessServer -dialplans:$s.dialplans

In this example, there are three SIP URI dial plans: SipDP1, SipDP2 and SipDP3. This example removes the Client Access server named `MyClientAccessServer` from the SipDP3 dial plan.

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1,SipDP2

In this example, there are two SIP URI dial plans: SipDP1 and SipDP2. This example removes the Client Access server named `MyClientAccessServer` from the SipDP2 dial plan.

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1

This example removes the Client Access server named `MyClientAccessServer` from all SIP dial plans.

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans $null

