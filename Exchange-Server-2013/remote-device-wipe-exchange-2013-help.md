---
title: 'Remote device wipe: Exchange 2013 Help'
TOCTitle: Remote device wipe
ms:assetid: cd615210-cd8a-48de-b3e3-8f9ec39ca380
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124591(v=EXCHG.150)
ms:contentKeyID: 49352799
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Remote device wipe

 

_**Applies to:** Exchange Server 2013_


Mobile phones, tablets, and other devices can store sensitive corporate data and provide access to many corporate resources. If a mobile device is lost or stolen, that data can be compromised. Through Microsoft Exchange mobile device mailbox policies, you can add a password requirement to your mobile devices. This requires users to enter a password to access their mobile devices. We recommend that, in addition to requiring a device password, you configure your mobile devices to automatically prompt for a password after a period of inactivity. The combination of a device password and inactivity locking provides enhanced security for your corporate data.

In addition to these features, Exchange Server 2013 provides a remote device wipe feature. You can issue a remote device wipe command from the Exchange Management Shell or the Exchange Administration Center (EAC). Users can issue their own remote device wipe commands from the Microsoft Outlook Web App user interface.

The remote device wipe feature also includes a confirmation function that writes a time stamp in the sync state data of the user's mailbox. This time stamp is displayed in Outlook Web App and in the user's mobile phone properties dialog box in the EAC.


> [!IMPORTANT]
> A remote device wipe can reset a mobile phone to the factory default condition. Although the remote device wipe protocol as implemented in Exchange 2013 only requires the deletion of personal corporate data, all current mobile device manufacturers interpret the command as one that wipes all data on the phone. Many mobile device operating systems also wipe all data on any storage card that’s inserted in the mobile device. If you’re performing a remote device wipe on a mobile phone in your possession and want to keep the data on the storage card, we recommend removing the storage card before you initiate the remote device wipe.




> [!WARNING]
> After a remote device wipe has occurred, data recovery is very difficult. However, no data removal process leaves a mobile device as free from residual data as when it's new. Recovery of data from a mobile device may still be possible using sophisticated tools.



## Remote device wipe vs. local device wipe

Local device wipe occurs when a mobile device wipes itself without the request coming from the server. If your organization has implemented mobile device mailbox policies that specify a maximum number of unsuccessful password attempts and that maximum is exceeded, the mobile device performs a local device wipe. The result of a local device wipe is the same as that of a remote device wipe. The device is returned to its factory default condition. When a mobile device performs a local device wipe, no confirmation is sent to the Exchange server.

