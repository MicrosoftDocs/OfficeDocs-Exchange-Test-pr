---
title: 'Add retention tags to or remove retention tags from a retention policy: Exchange 2013 Help'
TOCTitle: Add retention tags to or remove retention tags from a retention policy
ms:assetid: 3a5196ce-2764-453d-9bc1-5ec22d06b40d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd362328(v=EXCHG.150)
ms:contentKeyID: 49318576
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Add retention tags to or remove retention tags from a retention policy

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can add retention tags to a retention policy when the policy is created or any time thereafter. For details about how to create a retention policy, including how to simultaneously add retention tags, see [Create a Retention Policy](create-a-retention-policy-exchange-2013-help.md).

A retention policy can contain the following retention tags:

  - One or more retention policy tags (RPTs) for supported default folders

  - One default policy tag (DPT) with the **Move to Archive** action

  - One DPT with the **Delete and Allow Recovery** or the **Permanently Delete** action

  - One DPT for voice mail

  - Any number of personal tags

For more information about retention tags, see [Retention tags and retention policies](retention-tags-and-retention-policies-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to completion: 10 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Messaging records management" entry in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - Retention tags aren't applied to a mailbox until they're linked to a retention policy and the Managed Folder Assistant processes the mailbox. To start the Managed Folder Assistant so that it processes a mailbox, see [Configure the Managed Folder Assistant](configure-the-managed-folder-assistant-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the EAC to add or remove retention tags

1.  Go to **Compliance management** \>**Retention policies**.

2.  In the list view, select the retention policy to which you want to add retention tags and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  In **Retention Policy**, use the following settings:
    
      - **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon")   Click this button to add a retention tag to the policy.
    
      - **Remove** ![Remove icon](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Remove icon")   Select a tag from the list, and then click this button to remove the tag from the policy.

## Use the Shell to add or remove retention tags

This example adds the retention tags VPs-Default, VPs-Inbox, and VPs-DeletedItems to the retention policy RetPolicy-VPs, which doesn't already have retention tags linked to it.


> [!WARNING]
> If the policy has retention tags linked to it, this command replaces the existing tags.



    Set-RetentionPolicy -Identity "RetPolicy-VPs" -RetentionPolicyTagLinks "VPs-Default","VPs-Inbox","VPs-DeletedItems"

This example adds the retention tag VPs-DeletedItems to the retention policy RetPolicy-VPs, which already has other retention tags linked to it.

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Add((Get-RetentionPolicyTag 'VPs-DeletedItems').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

This example removes the retention tag VPs-Inbox from the retention policy RetPolicy-VPs.

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Remove((Get-RetentionPolicyTag 'VPs-Inbox').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

For detailed syntax and parameter information, see [Set-RetentionPolicy](https://technet.microsoft.com/en-us/library/dd335196\(v=exchg.150\)) and [Get-RetentionPolicy](https://technet.microsoft.com/en-us/library/dd298086\(v=exchg.150\)).

## How do you know this worked?

To verify that you have successfully added or removed a retention tag from a retention policy, use the [Get-RetentionPolicy](https://technet.microsoft.com/en-us/library/dd298086\(v=exchg.150\)) cmdlet to verify the *RetentionPolicyTagLinks* property.

This example use the **Get-RetentionPolicy** cmdlet to retrieve retention tags added to the Default MRM Policy and pipes them to the **Format-Table** cmdlet to output only the name property of each tag.

    (Get-RetentionPolicy "Default MRM Policy").RetentionPolicyTagLinks | Format-Table name

