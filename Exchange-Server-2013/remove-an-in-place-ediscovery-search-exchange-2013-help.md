---
title: 'Remove an In-Place eDiscovery search: Exchange 2013 Help'
TOCTitle: Remove an In-Place eDiscovery search
ms:assetid: 78461a78-1255-4a26-9d36-c6b8eb82a4f9
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd298078(v=EXCHG.150)
ms:contentKeyID: 49289315
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Remove an In-Place eDiscovery search

 

_**Applies to:** Exchange Server 2013_


In Microsoft Exchange Server 2013, you can use In-Place eDiscovery to search mailbox content. You can remove an In-Place eDiscovery search at any time. When you remove an In-Place eDiscovery search, search results are removed from the Discovery mailbox.


> [!WARNING]
> Deleting an In-Place eDiscovery search will remove any search results copied to a Discovery mailbox.



## What do you need to know before you begin?

  - Estimated time to completion: 2-5 minutes.

  - To remove an In-Place eDiscovery search that has In-Place Hold enabled, you must first remove the In-Place Hold from the search. For details, see [Create or remove an In-Place Hold](create-or-remove-an-in-place-hold-exchange-2013-help.md).

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "In-Place eDiscovery" entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## What do you want to do?

## Use the EAC to remove an In-Place eDiscovery search

1.  Navigate to **Compliance management** \> **In-place eDiscovery & hold**.

2.  In the list view, select the In-Place eDiscovery search you want to remove, and then click **Delete** ![Delete icon](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon").

## Use the Shell to remove an In-Place eDiscovery search

For an example of how to remove an In-Place eDiscovery search, see the “Examples” section in [Remove-MailboxSearch](https://technet.microsoft.com/en-us/library/dd298130\(v=exchg.150\)).

## How do you know this worked?

To verify that you have successfully removed an In-Place eDiscovery search, do one of the following:

  - Use the EAC to verify that the search is no longer displayed in the list view of the **In-place eDiscovery & hold** tab.

  - Use the **Get-MailboxSearch** cmdlet to retrieve In-Place eDiscovery searches. For an example of how to retrieve In-Place eDiscovery searches, see the “Examples” section in [Get-MailboxSearch](https://technet.microsoft.com/en-us/library/dd351021\(v=exchg.150\)).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


