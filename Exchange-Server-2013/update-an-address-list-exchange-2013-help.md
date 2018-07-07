---
title: 'Update an address list: Exchange 2013 Help'
TOCTitle: Update an address list
ms:assetid: 163e7099-cf14-4bb0-a84c-1401e9db670e
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa996375(v=EXCHG.150)
ms:contentKeyID: 49289182
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.UpdateAddressListWizardForm.ScheduleWizardPage
---

# Update an address list

 

_**Applies to:** Exchange Server 2013_


Address lists are a collection of recipient and other Active Directory objects. You apply an address list when the address list filter rule has been edited. To update the membership of the address list to include new recipients and remove those who no longer meet the filtering criteria, you must apply the address list.

For additional management tasks related to address lists, see [Address list procedures](address-list-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: This process may take a long time to finish depending on the number of recipients in the address list.

  - Some address lists contain thousands or tens of thousands of recipients depending on the size of your organization and the filters that you added to the address list. Updating address lists can take up a lot of computer resources. So, you may want to update the address list during off-peak hours.

  - If the address list contains more than 3,000 recipients, we recommend that you use the Exchange Management Shell to update the address list.

For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the EAC to update an address list

1.  Navigate to **Organization** \> **Address lists**.

2.  In the list view, select the address list that you want to update.

3.  In the details pane, click **Update**.

## Use the Shell to update an address list

This example updates the address list Washington State.

    Update-AddressList "Washington State"

If you have more than one address list with the same name, you must specify the full path to the address list you want to update. For example, if you want to update the address list Sales under North America but there is also a Sales address list under Europe, use the following command:

    Update-AddressList "North America\Sales"

For detailed syntax and parameter information, see [Update-AddressList](https://technet.microsoft.com/en-us/library/aa997982\(v=exchg.150\)).

