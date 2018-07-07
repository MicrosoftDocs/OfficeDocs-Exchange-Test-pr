---
title: 'Remove an organization relationship: Exchange 2013 Help'
TOCTitle: Remove an organization relationship
ms:assetid: ff211394-f58b-4da7-bb3a-df6abcb5950e
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ657513(v=EXCHG.150)
ms:contentKeyID: 49289477
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Remove an organization relationship

 

_**Applies to:** Exchange Server 2013_


An organization relationship lets users in your Exchange organization share calendar free/busy information with an Office 365 organization or with another Exchange on-premises organization. You can remove an organization relationship to disable calendar sharing with the other organization.

Before you can share calendars with another organization, you have to set up an authentication relationship with the Azure Active Directory authentication system (also known as “federation”) and must meet minimum software requirements. To learn more about federated sharing, see [Sharing](sharing-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the “Calendar and Sharing Permissions” section in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## What do you want to do?

## Use the EAC to remove an organization relationship

1.  On an Exchange 2013 server in your on-premises organization, navigate to **organization** \> **sharing**.

2.  Under **Organization Sharing**, select an organization relationship, and then click **Delete** ![Delete icon](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon") to remove organization relationship.

3.  In the warning that appears, click **yes**.

## Use the Shell to remove an organization relationship

This example removes the organization relationship Contoso from the Exchange organization

    Remove-OrganizationRelationship -Identity "Contoso"

For detailed syntax and parameter information, see [Remove-OrganizationRelationship](https://technet.microsoft.com/en-us/library/ee332362\(v=exchg.150\)).

## How do you know this worked?

To verify that you have successfully removed the organization relationship, do one of the following:

  - In the EAC, navigate to **Organization** \> **Sharing** and verify that the organization relationship isn’t displayed in the list view under **Organization Sharing**.

  - Run the following Shell command to verify the organization relationship information is removed.
    
        Get-OrganizationRelationship | Format-List


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


