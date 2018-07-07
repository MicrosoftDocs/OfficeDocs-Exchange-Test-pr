---
title: 'Remove an Outlook Protection Rule: Exchange 2013 Help'
TOCTitle: Remove an Outlook Protection Rule
ms:assetid: 569fc3be-b269-43f5-8797-73ab0691e685
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee633467(v=EXCHG.150)
ms:contentKeyID: 49319914
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Remove an Outlook Protection Rule

 

_**Applies to:** Exchange Server 2013_


Using Microsoft Outlook protection rules, you can protect messages with Information Rights Management (IRM) by applying an [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) template in Outlook 2010 before the messages are sent. To prevent an Outlook protection rule from being applied, you can disable the rule. Removing an Outlook protection rule removes the rule definition from Active Directory.

For additional management tasks related to IRM, see [Information Rights Management procedures](information-rights-management-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to completion: 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Rights protection" entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

  - You can't use the Exchange Administration Center (EAC) to remove Outlook protection rules. You must use the Shell.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to remove an Outlook protection rule

This example removes the Outlook protection rule OPR-DG-Finance.

    Remove-OutlookProtectionRule -Identity "OPR-DG-Finance"

For detailed syntax and parameter information, see [Remove-OutlookProtectionRule](https://technet.microsoft.com/en-us/library/dd297961\(v=exchg.150\)).

## Use the Shell to remove all Outlook protection rules

This example removes all Outlook protection rules in the Exchange organization.

    Get-OutlookProtectionRule | Remove-OutlookProtectionRule

For detailed syntax and parameter information, see [Get-OutlookProtectionRule](https://technet.microsoft.com/en-us/library/dd298004\(v=exchg.150\)) and [Remove-OutlookProtectionRule](https://technet.microsoft.com/en-us/library/dd297961\(v=exchg.150\)).

## How do you know this worked?

To verify that you have successfully removed an Outlook protection rule, use the [Get-OutlookProtectionRule](https://technet.microsoft.com/en-us/library/dd298004\(v=exchg.150\)) cmdlet to retrieve Outlook protection rules. For an example of how to retrieve Outlook protection rules, see [Examples](https://technet.microsoft.com/en-us/dd298004\(exchg.150\)#examples) in **Get-OutlookProtectionRule**.

