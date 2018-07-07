---
title: 'Manage user access to add-ins for Outlook: Exchange Online Help'
TOCTitle: Manage user access to add-ins for Outlook
ms:assetid: e5833dec-a23a-439e-ac03-92671817bff8
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ943757(v=EXCHG.150)
ms:contentKeyID: 51028424
ms.date: 04/17/2018
mtps_version: v=EXCHG.150
---

# Manage user access to add-ins for Outlook

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can use the EAC or Exchange Online PowerShell to manage user access to add-ins for Outlook.

  - Using the Exchange admin center (EAC), you can manage basic add-in access settings for your users at an organizational level. For example, you can configure whether an add-in is enabled or disabled for your users. You can also specify whether an add-in is required or optional for your users.

  - With Exchange Online PowerShell, you can manage all the settings that you can with the EAC, as well as other settings. For example, you can limit availability to specific users in your organization.

For additional management tasks, see [Add-ins for Outlook](add-ins-for-outlook-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - To learn how to use Windows PowerShell to connect to Exchange Online, see [Connect to Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Add-ins for Outlook” entry in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Specify whether an add-in is available, enabled, or disabled

## Use the EAC to specify whether an add-in is available, enabled, or disabled

1.  In the EAC, navigate to **Organization** \> **Add-ins**.

2.  In the list view, select the add-in that you want to change settings for, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  If you don’t want your users to use the add-in, clear the **Make this add-in available to users in your organization** check box, and then click **Save**.

4.  If you want your users to be able to use the add-in, select **Make this add-in available to users in your organization**, and then select the option you want.
    
      - **Optional, enabled by default**   Use this setting if you want to allow your users to turn off the add-in.
    
      - **Optional, disabled by default**   Use this setting if you want to allow your users to turn on the add-in.
    
      - **Mandatory, always enabled. Users can’t disable this add-in**   Use this setting if you don’t want your users to turn off the add-in.

5.  Click **Save**.

## Use Exchange Online PowerShell to specify whether an add-in is available, enabled, or disabled

You can use Exchange Online PowerShell to specify whether an add-in is available, enabled, or disabled.


> [!NOTE]
> Run the following command to look up the display names and add-in IDs for all the add-ins for Outlook installed for your organization.



    Get-app -Organizationadd-in | Format-List DisplayName,add-inID

If you want an add-in to be disabled and hidden from all your users, run the following command.

    Set-app <add-in ID> -Organizationadd-in -Enabled $false

If you want the add-in to be enabled by default, but you want your users to be able to turn it off, run the following command.

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser Enabled

If you want the add-in to be disabled by default, but you want your users to be able to turn it on, run the following command.

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser Disabled

If you want the add-in to be required for your users, run the following command.

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser AlwaysEnabled

For detailed syntax and parameters, see [Set-App](https://technet.microsoft.com/en-us/library/jj218630\(v=exchg.150\)).

## How do you know this worked?

1.  In the EAC, navigate to **Organization** \> **Add-ins**.

2.  Review the values in the **User Default** and **Provided To** columns.

Or

1.  From Exchange Online PowerShell, run `Get-app -Organizationadd-in | Format-List DisplayName,add-inId,Enabled,Default*`.

2.  Review the values for **DefaultStateForUser** and **Enabled**.

## Limit availability to specific users

## Use Exchange Online PowerShell to limit availability to specific users

If you want only members of your Marketing team distribution group to be able to use the LinkedIn add-in, run the following commands.

    $a = Get-DistributionGroupMember Marketing

    Set-app <add-in ID for the LinkedIn add-in> -Organizationadd-in -ProvidedTo SpecificUsers -UserList $a.Identity -DefaultStateForUser Enabled}

For detailed syntax and parameters, see [Set-App](https://technet.microsoft.com/en-us/library/jj218630\(v=exchg.150\)).

## How do you know this worked?

To verify that you’ve successfully limited access for specific users, do the following:

1.  From Exchange Online PowerShell, run `Get-app -Organizationadd-in | Format-List DisplayName,add-inId,Enabled,Default*,ProvidedTo,UserList`.

2.  Review the value for **ProvidedTo**.

