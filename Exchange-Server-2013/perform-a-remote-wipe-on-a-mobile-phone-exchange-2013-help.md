---
title: 'Perform a remote wipe on a mobile phone: Exchange 2013 Help'
TOCTitle: Perform a remote wipe on a mobile phone
ms:assetid: 67ba838e-031d-4a98-b277-170683b6f520
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998614(v=EXCHG.150)
ms:contentKeyID: 50935209
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Perform a remote wipe on a mobile phone

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Your users carry sensitive corporate information in their pockets every day. If one of them loses their mobile phone, your data can end up in the hands of another person. If one of your users loses their mobile phone, you can use the Exchange Administration Center (EAC) or the Exchange Management Shell to wipe their phone clean of all corporate and user information.


> [!NOTE]
> This topic also provides instructions for how to use Microsoft&nbsp;Outlook Web App to perform a remote wipe on a phone. The user must be signed in to Outlook Web App to perform a remote wipe.



## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mobile devices" entry in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

  - This procedure will clear all data on the mobile phone, including installed applications, photos, and personal information.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to wipe a user’s phone

You can use the EAC to wipe a user’s phone or cancel a remote wipe that has not yet completed.

1.  In the EAC, navigate to **Recipients** \> **Mailboxes**.

2.  Select the user, and under **Mobile Devices**, choose **View details**.

3.  On the **Mobile Device Details** page, select the lost mobile device, and then select **Wipe Data**.

4.  Select **Save**.

## Use the Shell to wipe a user’s phone

You can use the **Clear-MobileDevice** cmdlet in the Shell to wipe a user’s phone.

The following command wipes the device named WM\_TonySmith and sends a confirmation message to admin@contoso.com.

    Clear-MobileDevice -Identity WM_TonySmith -NotificationEmailAddresses "admin@contoso.com"

## Use Outlook Web App to wipe a user’s phone

Your users can wipe their own phone using Outlook Web App.

1.  In Outlook Web App, select **Settings \> Phone \> Mobile devices**.

2.  Select the mobile phone.

3.  Click or tap the **Wipe Device** icon.

## How do you know this worked?

There are several ways to verify that the remote wipe completed.

  - Run the **Clear-MobileDevice** cmdlet with the *–NotificationEmailAddresses* parameter configured. A message will be sent to the supplied email address when the remote wipe has completed.

  - In the EAC, check the status of the mobile device. The status will change from **Wipe Pending** to **Wipe Successful**.

  - In Outlook Web App, check the status of the mobile device. The status will change from **Wipe Pending** to **Wipe Successful**.

