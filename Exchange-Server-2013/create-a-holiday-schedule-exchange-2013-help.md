---
title: 'Create a holiday schedule: Exchange 2013 Help'
TOCTitle: Create a holiday schedule
ms:assetid: 0c5c51e4-5b51-451b-ab93-2cebf644dc96
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb266921(v=EXCHG.150)
ms:contentKeyID: 49315352
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Create a holiday schedule

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can define the dates and times your organization will be closed for holidays and other occasions. Between the start dates and the end dates you specify, callers who reach the Unified Messaging (UM) auto attendant will hear a holiday greeting you specify when you configure the holiday schedule. After the caller hears the holiday greeting you've specified, the non-business hours greeting and menu prompts will be played for the caller.

You can also create a holiday schedule within an existing holiday schedule. When you create multiple holiday schedules, Unified Messaging lets you overlap your scheduled holiday times. For example, you can define a holiday schedule from December 15th through December 31st when your organization will be closed for construction, and you can define another holiday schedule from December 24th through December 26th. When callers call in to the auto attendant from December 15th through December 23rd and from December 27th through December 31st, they'll be presented with the holiday greeting that you've specified for this schedule. For example, "We are currently closed for construction." When callers call in to the auto attendant from December 24th through December 26th, they'll be presented with another holiday greeting, such as "We are currently closed for business so that our employees can enjoy the holidays with their families."

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

## Use the EAC to specify a holiday schedule for a UM auto attendant

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to change, and then on the toolbar, click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM Dial Plan** page, under **UM Auto Attendants**, select the UM auto attendant for which you want to set the holiday schedule. On the toolbar, click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM Auto Attendant** page \> **Business Hours**, under **Holiday schedule**, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

4.  On the **New Holiday** page, configure the following:
    
      - **Name**   Enter a name for your holiday schedule.
    
      - **Holiday greeting**   Browse to the .wav file you want to use as your greeting. This is a required field.
    
      - **Start date**   Use this list to select the date you want the holiday to start. The holiday schedule will start at midnight on the date specified in this list.
    
      - **End date**   Use this list to select the date you want the holiday to end. The holiday schedule will end at 11:59 P.M. on the date specified in this list.

5.  After you've configured your holiday schedule, click **OK**, and then click **Save**.

## Use the Shell to specify a holiday schedule for a UM auto attendant

This example configures a UM auto attendant named `MyUMAutoAttendant` that has business hours configured to be 10:45 to 13:15 (Sunday), 09:00 to 17:00 (Monday), and 09:00 to 16:30 (Saturday), and holiday times and their associated greetings configured to be "New Year" on January 2, 2013, and "Building Closed for Construction" from April 24, 2013 through April 28, 2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

