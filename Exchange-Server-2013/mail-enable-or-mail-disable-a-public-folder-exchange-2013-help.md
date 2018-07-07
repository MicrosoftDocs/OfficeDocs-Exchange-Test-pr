---
title: 'Mail-enable or mail-disable a public folder: Exchange 2013 Help'
TOCTitle: Mail-enable or mail-disable a public folder
ms:assetid: 3d69f76d-ff3c-46c1-b962-6a1baa425d8a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997560(v=EXCHG.150)
ms:contentKeyID: 49289237
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Mail-enable or mail-disable a public folder

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Public folders are designed for shared access and provide an easy and effective way to collect, organize, and share information with other people in your workgroup or organization. Mail-enabling a public folder allows users to post to the public folder by sending an email message to it. When a public folder is mail-enabled additional settings become available for the public folder in the Exchange admin center (EAC), such as email addresses and mail quotas. In the Shell, before a public folder is mail-enabled, you use the **Set-PublicFolder** cmdlet to manage all of its settings. After the public folder is mail-enabled, you use the **Set-PublicFolder** and the **Set-MailPublicFolder** cmdlets to manage the settings.

If you want users on the Internet to send mail to a mail-enabled public folder, you need to set addition permissions using the **Add-PublicFolderClientPermission** cmdlet.

For additional management tasks related to managing public folders, see [Public folder procedures](public-folder-procedures-exchange-2013-help.md).

For additional management tasks related to public folders, see [Public folder procedures in Office 365 and Exchange Online](https://technet.microsoft.com/en-us/library/jj966272\(v=exchg.150\)).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes

  - To ensure that users on the Internet can send e-mail messages to a mail-enabled public folder, the public folder needs to have at least the *CreateItems* access right granted to the Anonymous account. If you want to learn how to do this, check out Allow anonymous users to send email to a mail-enabled public folder.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Sharing and collaboration permissions](sharing-and-collaboration-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the EAC to mail-enable or mail-disable a public folder

1.  Navigate to **Public folders** \> **Public folders**.

2.  In the list view, select the public folder that you want to mail-enable or mail-disable.

3.  In the details pane, under **Mail settings**, click **Enable** or **Disable**.

4.  A warning box displays asking if you are sure you want to enable or disable email for the public folder. Click **Yes** to continue.

If you want external users to send mail to this public folder, make sure you follow the steps in Allow anonymous users to send email to a mail-enabled public folder.

## Use the Shell to mail-enable a public folder

This example mail-enables the public folder Help Desk.

    Enable-MailPublicFolder -Identity "\Help Desk"

This example mail-enables the public folder Reports under the Marketing public folder, but hides the folder from address lists.

    Enable-MailPublicFolder -Identity "\Marketing\Reports" -HiddenFromAddressListsEnabled $True

If you want external users to send mail to this public folder, make sure you follow the steps in Allow anonymous users to send email to a mail-enabled public folder.

For detailed syntax and parameter information, see [Enable-MailPublicFolder](https://technet.microsoft.com/en-us/library/aa998824\(v=exchg.150\)).

## Use the Shell to mail-disable a public folder

This example mail-disables the public folder Marketing\\Reports.

    Disable-MailPublicFolder -Identity "\Marketing\Reports"

For detailed syntax and parameter information, see [Disable-MailPublicFolder](https://technet.microsoft.com/en-us/library/bb123781\(v=exchg.150\)).

## Allow anonymous users to send email to a mail-enabled public folder

You can use either Outlook or the Shell to set permissions on a public folder's Anonymous account. You can't use the EAC to set permissions on the Anonymous account.

**Use Outlook to set permissions for the Anonymous account**

1.  Open Outlook using an account that's been granted Owner permissions on the email-enabled public folder you want anonymous users to send mail to.

2.  Navigate to **Public folders - \<user's name\>**.

3.  Navigate to the public folder you want to change.

4.  Right-click on the public folder, click **Properties** and then select the **Permissions** tab.

5.  Select the **Anonymous** account, select **Create items** under **Write**, and then click **OK**.

**Use the Shell to set permissions for the Anonymous account**

This example sets the `CreateItems` permission for the Anonymous account on the "Customer Feedback" mail-enabled public folder.

    Add-PublicFolderClientPermission "\Customer Feedback" -AccessRights CreateItems -User Anonymous

For detailed syntax and parameter information, see [Add-PublicFolderClientPermission](https://technet.microsoft.com/en-us/library/bb124743\(v=exchg.150\)).

