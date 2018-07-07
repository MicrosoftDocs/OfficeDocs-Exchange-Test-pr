---
title: 'Authorize calls for a group of users: Exchange 2013 Help'
TOCTitle: Authorize calls for a group of users
ms:assetid: 7fc36757-868c-4bde-b793-6ae630da155c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb232099(v=EXCHG.150)
ms:contentKeyID: 50873801
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Authorize calls for a group of users

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can enable dialing authorizations on a Unified Messaging (UM) mailbox policy. You can use dialing authorizations on a mailbox policy to prohibit authenticated Outlook Voice Access users that are linked to the UM mailbox policy from making in-country/region or international telephone calls, or *outdialing*. Outdialing happens when Unified Messaging places an outgoing call for a user after they've called in to an Outlook Voice Access phone number that is configured on a UM dial plan. When you configure a setting on a UM mailbox policy, that setting applies to all UM-enabled users linked with the UM mailbox policy.

For additional management tasks related to outdialing, see [Allowing users to make calls procedures](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailbox policies" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Before you perform these procedures, confirm that in-country/region and international dialing rules have been created on a UM dial plan. For detailed steps, see [Create dialing rules for users](create-dialing-rules-for-users-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to enable dialing authorizations on a UM mailbox policy for in-country/region dialing rule groups

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Mailbox Policies**, select the UM mailbox policy for which you want to create a dialing authorization, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Mailbox Policy** page \> **Dialing authorization**, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") under **Authorized in-country/region dialing rule groups**.

4.  On the **Select Dialing Rule Groups to Allow** page, select the dialing rule group, click **OK**, and then click **Save**.

## Use the EAC to enable dialing authorizations on a UM mailbox policy for international dialing rule groups

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Mailbox Policies**, select the UM mailbox policy for which you want to create a dialing authorization, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Mailbox Policy** page \> **Dialing authorization**, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") under **Authorized international dialing rule groups**.

4.  On the **Select Dialing Rule Groups to Allow** page, select the dialing rule group, click **OK**, and then click **Save**.

## Use the Shell to enable in-country/region and international dialing authorizations on a UM mailbox policy

This example enables the InCountry/RegionGroup1, InCountry/RegionGroup2, InternationalGroup1, and InternationalGroup2 dialing authorizations on a UM mailbox policy named `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

