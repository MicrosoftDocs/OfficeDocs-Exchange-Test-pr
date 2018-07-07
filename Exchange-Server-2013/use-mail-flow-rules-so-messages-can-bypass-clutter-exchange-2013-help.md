---
title: 'Use mail flow rules so messages can bypass Clutter: Exchange 2013 Help'
TOCTitle: Use mail flow rules so messages can bypass Clutter
ms:assetid: 58e413f0-aa27-4307-bffd-4df03090a15e
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn896639(v=EXCHG.150)
ms:contentKeyID: 64174730
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Use mail flow rules so messages can bypass Clutter

 

_**Applies to:** Exchange Server 2013_


If you want to be sure that you receive particular messages, you can create an Exchange transport rule that makes sure that these messages bypass your clutter folder. Check out [Use Clutter to sort low priority messages in Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=528411) for more info on Clutter.

For additional management tasks related to transport rules, check out [Mail flow rules (transport rules) in Exchange Online](https://technet.microsoft.com/en-us/library/jj919238\(v=exchg.150\)) and the [New-TransportRule](https://technet.microsoft.com/en-us/library/bb125138\(v=exchg.150\)) PowerShell topic. If you're new to PowerShell, check out the following topics for help on using Powershell:

  - [Connect to Exchange Online using remote PowerShell](https://technet.microsoft.com/en-us/library/jj984289\(v=exchg.150\))

  - [Connect to Exchange using remote Shell](https://technet.microsoft.com/en-us/library/dd335083\(v=exchg.150\))

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Transport rules" entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Use the UI to create a transport rule to bypass the clutter folder

This example allows all messages with title "Meeting" to bypass clutter.

1.  In the Exchange admin center, navigate to **mail flow** \> **Rules**. Click ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") and then choose **Create a new rule...**.

2.  After you're done creating the new rule, click **save** to start the rule.

![Art example: If subject contains meeting, bypass clutter](images/Dn896639.75957aa4-4b2a-4142-92ff-07f8ccc64d82(EXCHG.150).png "Art example: If subject contains meeting, bypass clutter")

## Use the Shell to create a transport rule to bypass the clutter folder

This example allows all messages with title "Meeting" to bypass clutter.

    New-TransportRule -Name <name_of_the_rule> -SubjectContainsWords "Meeting" -SetHeaderName "X-MS-Exchange-Organization-BypassClutter" -SetHeaderValue "true"


> [!IMPORTANT]
> In this example, both "X-MS-Exchange-Organization-BypassClutter" and "true" is case sensitive.



For detailed syntax and parameter information, see [New-TransportRule](https://technet.microsoft.com/en-us/library/bb125138\(v=exchg.150\)).

## How do you know this worked?

You can check email message headers to see if the email messages are landing in the Inbox due to the clutter transport rule bypass. Pick an email message from a mailbox in your organization that has the clutter bypass transport rule applied. Look at the headers stamped on the message, and you should see the **X-MS-Exchange-Organization-BypassClutter: true** header. This means the bypass is working. Check out the [View the Internet header information for an email message](https://go.microsoft.com/fwlink/p/?linkid=822530) topic for info on how to find the header information.


> [!NOTE]
> Calendar items, like meetings accepted, sent or declined won't have these headers on them. We're working on extending clutter capabilities to these calendar items soon.


