---
title: 'Authorize calls for auto attendant callers: Exchange 2013 Help'
TOCTitle: Authorize calls for auto attendant callers
ms:assetid: c6c94fad-64df-44aa-a198-980f017ef716
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb691238(v=EXCHG.150)
ms:contentKeyID: 50873811
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Authorize calls for auto attendant callers

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can enable dialing authorizations on a Unified Messaging (UM) auto attendant. Dialing authorizations on an auto attendant are used to prohibit users who call in to the auto attendant from making in-country/region or international telephone calls, or *outdialing*. Outdialing happens when Unified Messaging makes an outgoing call for a user after they've called into a phone number that is configured on a UM auto attendant.

For additional management tasks related to outdialing, see [Allowing users to make calls procedures](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM auto attendants" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM auto attendant has been created. For detailed steps, see [Create a UM auto attendant](create-a-um-auto-attendant-exchange-2013-help.md).

  - Before you perform these procedures, confirm that in-country/region and international dialing rules have been created on a UM dial plan. For detailed steps, see [Create dialing rules for users](create-dialing-rules-for-users-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to enable dialing authorizations on a UM auto attendant for in-country/region rule groups

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Auto Attendants**, select the UM auto attendant for which you want to create a dialing authorization, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Auto Attendant** page \> **Dialing authorization**, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") under **Authorized in-country/region dialing rule groups**.

4.  On the **Select Dialing Rule Groups to Allow** page, select the dialing rule group, click **OK**, and then click **Save**.

## Use the EAC to enable dialing authorizations on a UM auto attendant for international rule groups

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Auto Attendants**, select the UM auto attendant for which you want to create a dialing authorization, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Auto Attendant** page \> **Dialing authorization**, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") under **Authorized international dialing rule groups**.

4.  On the **Select Dialing Rule Groups to Allow** page, select the dialing rule group, click **OK**, and then click **Save**.

## Use the Shell to enable in-country/region and international dialing authorizations on a UM auto attendant

This example enables the InCountry/RegionGroup1, InCountry/RegionGroup2. InternationalGroup1, and InternationalGroup2 dialing authorizations on a UM auto attendant named `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

