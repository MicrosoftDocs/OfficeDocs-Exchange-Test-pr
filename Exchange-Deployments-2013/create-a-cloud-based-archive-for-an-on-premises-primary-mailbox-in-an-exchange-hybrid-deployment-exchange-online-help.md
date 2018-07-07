---
title: 'Create a cloud-based archive for an on-premises primary mailbox in an Exchange hybrid deployment: Exchange Online Help'
TOCTitle: Create a cloud-based archive for an on-premises primary mailbox in a hybrid deployment
ms:assetid: ecc0a687-6c05-47bd-a079-a43d83cba9ea
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Mt791517(v=EXCHG.150)
ms:contentKeyID: 74253061
ms.date: 12/09/2017
mtps_version: v=EXCHG.150
---

# Create a cloud-based archive for an on-premises primary mailbox in an Exchange hybrid deployment

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


In an Exchange hybrid deployment, you can configure an on-premises primary mailbox with a cloud-based archive mailbox in Exchange Online.

Step 1: Enable a cloud-based archive mailbox for a primary on-premises mailbox

Step 2: Verify that the cloud-based archive mailbox is created

(Optional) Run directory synchronization

## Before you begin

  - The user with the on-premises primary mailbox must a user account in your Office 365 organization.

  - The Office 365 user account must be assigned an Exchange Online Archiving for Exchange Server license. The steps for assigning a license are included in the procedures in Step 1.

  - After you enable the cloud-based archive mailbox in Step 1, it might take up to 30 minutes for the cloud-based archive mailbox to be provisioned. This is because the cloud-base archive mailbox is created by the process of directory synchronization, where your on-premises Active Directory is synchronized with Azure Active Directory (Azure AD) in Office 365. By default, directory synchronization runs once every 30 minutes.

## Step 1: Enable a cloud-based archive mailbox for a primary on-premises mailbox

Use one of the following procedures to enable a cloud-based archive mailbox for an on-premises primary mailbox. Perform these steps in the Exchange admin center in your on-premises Exchange organization and in the Office 365 admin center.

Create a cloud-based archive mailbox for a new user

Create a cloud-based archive mailbox for an existing user

## Create a cloud-based archive mailbox for a new user

1.  In the EAC in your on-premises organization, go to **Recipients**  \> **Mailboxes**.

2.  Click **New** ![Add Icon](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") \> **User mailbox**.

3.  On the **New user mailbox** page, create a mailbox for a new or existing user. For more information about creating a user mailbox, see [Create user mailboxes](https://technet.microsoft.com/en-us/library/jj991919\(v=exchg.150\)).

4.  Click **More options** to enable a cloud-based archive mailbox.

5.  Under **Archive**, click the **Create an in-place archive for this user** check box, and then click **Cloud-based archive**. The name of the domain that the archive mailbox will be provisioned in is displayed.
    
    ![Under Archive, click the checkbox and then click Cloud-based archive](images/Mt791517.43d0473e-30ad-4021-94bc-a9c5449f43ba(EXCHG.150).png "Under Archive, click the checkbox and then click Cloud-based archive")  

6.  Click **Save** to create the mailbox and the cloud-based archive.
    
    Note on the **Mailboxes** page, the value **User (Archive)** is displayed in the **Mailbox type** column for the selected mailbox.

7.  Wait up to 30 minutes for directory synchronization to create a corresponding user account in Office 365.
    

    > [!TIP]
    > In the Office 365 admin center, go to <STRONG>Health</STRONG> &gt; <STRONG>Directory sync status</STRONG> to see the last time that directory synchronization occurred.



8.  After verifying that directory synchronization has occurred after you created the new on-premises mailbox, in the Office 365 admin center, go to **Users** \> **Active users**, and then select the new Office 365 user account that was created for the new on-premises mailbox.

9.  On the user properties page that's displayed, click **Edit** in the **Product licenses** section.
    
    ![Click Edit in the details pane to assign a license to the selected user](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "Click Edit in the details pane to assign a license to the selected user")  

10. Under the **Location** drop-down menu, select a location for the user.

11. Expand the list of Office 365 Enterprise licenses, and then assign the **Exchange Online Archiving for Exchange Server** license, and then save the changes.
    
    In the **Status** column in the list of users, notice that a license is now assigned to the user.

12. Once again, wait up to 30 minutes for directory synchronization to provision a cloud-based archive mailbox. Go to Step 2 to see how to verify that the cloud-based archive mailbox has been created. After the archive mailbox is created, the user can access it by using Outlook or Outlook on the web.

Return to top

## Create a cloud-based archive mailbox for an existing user

1.  In the Office 365 admin center, go to **Users** \> **Active users**, and then select the user account that you want to create a cloud-base archive mailbox for.

2.  On the user properties page that's displayed, click **Edit** in the **Product licenses** section.
    
    ![Click Edit in the details pane to assign a license to the selected user](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "Click Edit in the details pane to assign a license to the selected user")  

3.  Under the **Location** drop-down menu, select a location for the user.

4.  Expand the list of Office 365 Enterprise licenses, and then assign the **Exchange Online Archiving for Exchange Server** license, and then save the changes.
    
    In the **Status** column in the list of users, notice that a license is now assigned to the user.

5.  In the EAC in your on-premises organization, go to **Recipients**  \> **Mailboxes**.

6.  In the list of mailboxes, select the user that you just assigned the assigned the license to.

7.  In the details pane, under **In-Place Archive**, click **Enable**.
    
    ![Click Enable in the details pane to enable the archive mailbox for the selected user](images/Mt791517.17ce99f7-d154-4e21-bec1-c938af1d4a0a(EXCHG.150).png "Click Enable in the details pane to enable the archive mailbox for the selected user")  

8.  On the **Create in-place archive** page, click **Cloud-based archive**, and then click **Ok**. The name of the domain that the archive mailbox will be provisioned in is displayed.
    
    ![On the Create in-place archive page, click Cloud-based archive](images/Mt791517.9ad047c9-ef47-47df-93cc-0fab872f1ae1(EXCHG.150).png "On the Create in-place archive page, click Cloud-based archive")  
    
    Note on the **Mailboxes** page, the value **User (Archive)** is displayed in the **Mailbox type** column for the selected mailbox.

9.  Wait up to 30 minutes for directory synchronization to create the cloud-based archive mailbox. Go to Step 2 to see how to verify that the cloud-based archive mailbox has been created. After the archive mailbox is created, the user can access it by using Outlook or Outlook on the web.
    

    > [!TIP]
    > In the Office 365 admin center, go to <STRONG>Health</STRONG> &gt; <STRONG>Directory sync status</STRONG> to see the last time that directory synchronization occurred.



Return to top

## Step 2: Verify that the cloud-based archive mailbox is created

As previously explained, there might be a delay between the time that you enable a cloud-based archive mailbox and when it's actually created. This is because directory synchronization has to run to create the cloud-based archive mailbox. Here are some ways to verify that the cloud-based archive mailbox has been created.

In your Exchange Online organization, run the following PowerShell command to display properties related to a user's archive mailbox. To connect to Exchange Online using remote PowerShell, see [Connect to Exchange Online PowerShell](https://go.microsoft.com/fwlink/?/linkid=396554).

    Get-MailUser <cloud mail user> | FL *archive*

The following screen shots show the properties that are returned when the provisioning of the cloud-based archive mailbox is pending and after the archive mailbox has been created.

**Mail user properties before the cloud-based archive mailbox is provisioned by directory synchronization**

![Cloud-based mail user properties before the cloud-based archive is provisioned](images/Mt791517.c6a42713-f061-4761-93c1-2b5478953e46(EXCHG.150).png "Cloud-based mail user properties before the cloud-based archive is provisioned")

Before directory synchronization provisions the cloud-based archive, the *ArchiveStatus* property is set to `None`. Also note that the *ArchiveGuid* and *ArchiveName* properties are empty.

**Mail user properties after the cloud-based archive mailbox is provisioned by directory synchronization**

![Cloud-based mail user properties after the cloud-based archive is provisioned](images/Mt791517.005fcc87-6253-4218-aafc-50f212de54fa(EXCHG.150).png "Cloud-based mail user properties after the cloud-based archive is provisioned")

After directory synchronization provisions the cloud-based archive, the *ArchiveStatus* property is set to `Active`, and the *ArchiveGuid* and *ArchiveName* properties are populated. At this point, the user will be able to access their cloud-based archive mailbox in Outlook or Outlook on the web.

![User can access their cloud-based archive mailbox in Outlook or Outlook on the web](images/Mt791517.8777bc4d-05c3-4489-8d8c-ff5429a0b2c3(EXCHG.150).png "User can access their cloud-based archive mailbox in Outlook or Outlook on the web")

You can also run the following PowerShell command in your on-premises Exchange organization to display properties related to a user's cloud-based archive mailbox.

    Get-Mailbox <on-premises user mailbox> | FL *archive*

**On-premises mailbox properties before the cloud-based archive mailbox is provisioned by directory synchronization**

![Mailbox properties before the cloud-based archive is provisioned](images/Mt791517.d5625bc8-03de-439a-8a0a-051ff537a0bf(EXCHG.150).png "Mailbox properties before the cloud-based archive is provisioned")

Before directory synchronization provisions the cloud-based archive, the *ArchiveStatus* property is set to `None` and the *ArchiveState* property is set to `HostedPending`.

**On-premises mailbox properties after the cloud-based archive mailbox is provisioned by directory synchronization**

![Mailbox properties after the cloud-based archive is provisioned](images/Mt791517.9b42d562-1b0a-4722-97aa-35d0ef6f9372(EXCHG.150).png "Mailbox properties after the cloud-based archive is provisioned")

After directory synchronization provisions the cloud-based archive, the *ArchiveStatus* property is set to `Active` and the *ArchiveState* property is set to `HostedProvisioned`. At this point, the user will be able to access their cloud-based archive mailbox in Outlook or Outlook on the web.

Return to top

## (Optional) Run directory synchronization

As previously explained, the cloud-base archive mailbox is created by the process of directory synchronization. By default, your on-premises Active Directory is synchronized with Azure AD in Office 365 once every 30 minutes. You can see when the last time directory synchronization occurred by going to **Health** \> **Directory sync status** in the Office 365 admin center.

In some cases, you might want to start directory synchronization to provision the cloud-based archive mailbox before the next scheduled synchronization. You can do this by running the following PowerShell command on the server where Azure AD Connect is installed.

    Start-ADSyncSyncCycle -PolicyType Delta

For more information, see [Azure AD Connect sync: Scheduler](https://go.microsoft.com/fwlink/p/?linkid=836813).

Return to top

