---
title: 'Install or remove add-ins for Outlook for your organization: Exchange 2013 Help'
TOCTitle: Install or remove add-ins for Outlook for your organization
ms:assetid: 112f3ef7-9943-4a1e-8a42-e08e8e9f67f4
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ943752(v=EXCHG.150)
ms:contentKeyID: 51028419
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Install or remove add-ins for Outlook for your organization

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can install or remove add-ins for Outlook for your organization by using the EAC or the Shell.


> [!NOTE]
> By default, after you install an add-in for your organization, the add-in is available for all users in your organization. After installation, you can use the EAC or the Shell to make the add-in optional or required for your users, and to specify whether you want the add-in to be enabled or disabled. For information about how to change the default settings for an add-in, see <A href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Manage user access to add-ins for Outlook</A>. To limit availability of add-ins to specific users in your organization, you must use the Shell. For more information, see <A href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Manage user access to add-ins for Outlook</A>.



For additional management tasks, see [Add-ins for Outlook](add-ins-for-outlook-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Apps for Outlook" entry in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - You can assign administrators permission to install and manage add-ins for your organization. You can also assign users permission to install and manage add-ins for their own use. For more information, see [Specify the administrators and users who can install and manage add-ins for Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

  - Access to the Office Store isn’t supported for mailboxes or organizations in specific regions. If you don’t see **Add from the Office Store** as an option in the **Exchange admin center** under **Organization** \> **Add-ins** \> ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"), you may be able to install an add-in for Outlook from a URL or file location. For more information, contact your service provider.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Install an add-in for Outlook

## Use the EAC to add an add-in

1.  In the EAC, navigate to **Organization** \> **Add-ins**.

2.  Click **New** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"), and then choose the location that you want to install the add-in from.
    
      - **Add from the Office Store**. At the Office Store, select the app you want to install, and then click **Add**. Apps that work with Outlook Web App are listed under **Add-ins for Office and SharePoint** \> **Outlook**.
        

        > [!NOTE]
        > Access to the Office Store isn’t supported for mailboxes or organizations in specific regions. If you don’t see <STRONG>Add from the Office Store</STRONG> as an option in the <STRONG>Exchange admin center</STRONG> under <STRONG>Organization</STRONG> &gt; <STRONG>Add-ins</STRONG> &gt; <IMG title="Add Icon" alt="Add Icon" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif">, you may be able to install an add-in for Outlook from a URL or file location. For more information, contact your service provider.

    
      - **Add from URL**. In **URL**, enter the full URL for the add-in manifest file that you want to install.
    
      - **Add from file**. Select **Browse**, and then navigate to the location of the add-in manifest file that you want to install.

3.  Click **Save**.

## Use the Shell to add an add-in

This example shows you how to add an add-in from a URL.

    New-App -OrganizationApp -Url <URL location for add-in manifest file>

This example shows you how to add an add-in from a file.

    New-App -OrganizationApp -FileData <File location for add-in manifest file>


> [!TIP]
> When you use the Shell to install an add-in for your organization, you can install the add-in and configure settings for it at the same time.



For syntax and parameters, see [New-App](https://technet.microsoft.com/en-us/library/jj218722\(v=exchg.150\)).

## Remove an add-in for Outlook

## Use the EAC to remove an add-in

1.  In the EAC, navigate to **Organization** \> **Add-ins**.

2.  In the list view, select the app that you want to remove, and then click **Delete** ![Delete icon](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon").

## Use the Shell to remove an add-in

You can use the Shell to remove an add-in from your organization.


> [!NOTE]
> Run the following command to look up the display names and application IDs for all the add-ins for Outlook installed for your organization.



    Get-App -OrganizationApp |FL DisplayName,AppID

Run the following command to remove the custom add-in Finance Test Add-in from the organization.

    Remove-App -OrganizationApp -Identity <GUID for Finance Test Add-in>

For syntax and parameters, see [Remove-App](https://technet.microsoft.com/en-us/library/jj218709\(v=exchg.150\)).

## How do you know this worked?

To view the add-ins that are installed in your organization, do one the following:

  - In the EAC, navigate to **Organization** \> **Add-ins**, and then review the list of installed add-ins.

  - From the Shell, run `Get-App`, and then review the list of installed add-ins.

