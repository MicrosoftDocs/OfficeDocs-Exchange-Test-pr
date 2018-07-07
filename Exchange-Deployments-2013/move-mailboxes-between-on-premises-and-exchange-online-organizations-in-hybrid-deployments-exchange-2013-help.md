---
title: 'Move mailboxes between on-premises and Exchange Online organizations in hybrid deployments: Exchange 2013 Help'
TOCTitle: Move mailboxes between on-premises and Exchange Online organizations in hybrid deployments
ms:assetid: d6289f7b-f67e-48db-9570-9fd3c9547548
ms:mtpsurl: https://technet.microsoft.com/en-us/library/o365e_hrcmoverequest_fl312271(v=EXCHG.150)
ms:contentKeyID: 50630965
ms.date: 10/02/2017
mtps_version: v=EXCHG.150
---

# Move mailboxes between on-premises and Exchange Online organizations in hybrid deployments

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


With an Exchange-based hybrid deployment, you can choose to either move on-premises Exchange mailboxes to the Exchange Online organization or move Exchange Online mailboxes to the Exchange organization. When you move mailboxes between the on-premises and Exchange Online organizations, you use migration batches to perform the remote mailbox move request. This approach allows you to move existing mailboxes instead of creating new user mailboxes and importing user information. This approach is different than migrating user mailboxes from an on-premises Exchange organization to Exchange Online as part of a complete Exchange migration to the cloud. The mailbox moves discussed in this topic are part of administrative Exchange management in a longer-term coexistence relationship between on-premises Exchange and Exchange Online organizations.

For more information about migrating on-premises Exchange organizations to Exchange Online, see [Ways to migrate multiple email accounts to Office 365](https://go.microsoft.com/fwlink/p/?linkid=524030).


> [!IMPORTANT]
> You must have configured a hybrid deployment between your on-premises and Exchange Online organizations to complete the mailbox moves procedures in this topic. For more information about hybrid deployments, see <A href="exchange-server-hybrid-deployments-exchange-2013-help.md">Exchange Server Hybrid Deployments</A>.<BR><BR>Before you move Unified Messaging-enabled (UM) mailboxes to Exchange Online, you need to make sure that on-premises Skype for Business 2015, Skype for Business Online, and Exchange Online, all meet the requirements specified in <A href="hybrid-deployment-prerequisites-exchange-2013-help.md">Hybrid deployment prerequisites</A>. For information on how to map your on-premises UM mailbox policies to policies in Exchange Online, see <A href="https://technet.microsoft.com/en-us/library/bb124903(v=exchg.150)">Set-UMMailboxPolicy</A>.



## What do you need to know before you begin?

  - Estimated time to complete: 10 minutes to configure the migration batch, but total time to complete the migration depends on the number of mailboxes included in each migration batch.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox Move and Migration Permissions" section in the [Recipients Permissions](https://technet.microsoft.com/en-us/library/dd638132\(v=exchg.150\)) topic.

  - Hybrid deployment is configured between your on-premises and Exchange Online organizations.

  - If you're running Exchange 2013, make sure the Mailbox Replication Proxy Service (MRSProxy) is enabled on your on-premises Exchange 2013 Client Access servers.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](https://technet.microsoft.com/en-us/library/jj150484\(v=exchg.150\)).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Step 1: Create a migration endpoint

Prior to performing on-boarding and off-boarding remote move migrations in an Exchange hybrid deployment, we recommend that you create Exchange remote migration endpoints. The migration endpoint contains the connection settings for an on-premises Exchange server that is running the MRS proxy service, which is required to perform remote move migrations to and from Exchange Online.

For step-by-step procedures, see Create migration endpoints.

## Step 2: Enable the MRSProxy service

If the MRSProxy service isn’t already enabled for your on premises Exchange 2013 Client Access servers, follow these steps in the Exchange admin center (EAC):

1.  Open the EAC, and then navigate to **Servers** \> **Virtual Directories**.

2.  Select the Client Access server, and then select the **EWS** virtual directory and click **Edit** ![Edit icon](images/JJ906432.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  Select the **MRS Proxy enabled** check box, and then click **Save**.

## Step 3: Use the EAC to move mailboxes

You can use the remote move migration wizard on the **Office 365** tab in the EAC on an Exchange server to either move existing user mailboxes in the on-premises organization to the Exchange Online organization or to move Exchange Online mailboxes to the on-premises organization. Choose one of the following procedures:

## Move on-premises mailboxes to Exchange Online

You can use the remote move migration wizard on the **Office 365** tab in the EAC on an Exchange server to move existing user mailboxes in the on-premises organization to the Exchange Online organization. Follow these steps:

1.  Open the EAC, and then navigate to **Office 365** \> **Recipients** \> **Migration**.

2.  Click **Add** ![Add Icon](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"), and then select **Migrate to Exchange Online**.

3.  On the **Select a migration type** page, select **Remote move migration** and then click **Next**.

4.  On the **Select the users** page, click **Add**  ![Add Icon](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") and select the on-premises users to move to Office 365 and click **Add** and then click **OK**. Click **Next**.

5.  On the **Enter the Windows user account credential** page, enter the on-premises administrator account name in the **On-premises administrator name** text field and enter the associated password for this account in the **On-premises administrator password** text field. For example, “corp\\administrator” and a password. Click **Next**.
    

    > [!NOTE]
    > If you’ve already created a migration endpoint, you’ll receive an endpoint confirmation prompt for this step. If you’ve created two or more migration endpoints, you must choose an endpoint from the migration endpoint drop-down menu.



6.  On the **Confirm the migration endpoint** page, verify that the FDQN of your on-premises Exchange server is listed when the wizard confirms the migration endpoint. For example, “mail.contoso.com”. Click **Next**.
    

    > [!NOTE]
    > The MRSProxy service on the Exchange servers automatically throttles the mailbox move requests when you select multiple mailboxes to move to Exchange Online. The total time to complete the mailbox move depends on the total number of mailboxes selected, the size of the mailboxes, and the configuration of the MRSProxy. To learn more about customizing the MRSProxy, see <A href="https://technet.microsoft.com/en-us/library/bb232205(v=exchg.150)">Message throttling</A>.



7.  On the **Move configuration** page, enter a name for the migration batch in the **New migration batch name** text field. Use the down arrow ![Down Arrow Icon](images/JJ906432.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Down Arrow Icon") to select the **Target delivery domain for the mailboxes that are migrating to Office 365**. In most hybrid deployments, this is the primary SMTP domain used for the Exchange Online organization mailboxes. For example, contoso.mail.onmicrosoft.com. Verify that the **Move primary mailbox along with archive mailbox** option is selected, and then click **Next**.

8.  On the **Start the batch** page, select at least one recipient to receive the batch complete report. Verify that the **Automatically start the batch** option is selected, and then select the **Automatically complete the migration batch** check box. Click **New**.

## Move Exchange Online mailboxes to the on-premises organization

You can use the remote move migration wizard on the **Office 365** tab in the EAC on an Exchange server to move existing user mailboxes in the on-premises organization to the Exchange Online organization:

1.  Open the EAC and navigate to **Office 365** \> **Recipients** \> **migration**.

2.  Click **Add** ![Add Icon](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"), and then select **Migrate from Exchange Online**.

3.  On the **Select the users** page, select **Select the users that you want to move** and then click **Next**.

4.  On the **Select the users** page, click **Add** ![Add Icon](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") and then select the Exchange Online users to move to the on-premises organization, click **Add** and then click **OK**. Click **Next**.

5.  On the **Confirm the migration endpoint** page, verify that the FDQN of your on-premises Exchange server is listed when the wizard confirms the migration endpoint. For example, “mail.contoso.com”. Click **Next**.
    

    > [!NOTE]
    > The MRSProxy service on the Exchange servers automatically throttles the mailbox move requests when you select multiple mailboxes to move to Exchange Online. The total time to complete the mailbox move depends on the total number of mailboxes selected, the size of the mailboxes, and the properties of the MRSProxy. To learn more about customizing the MRSProxy, see <A href="https://technet.microsoft.com/en-us/library/bb232205(v=exchg.150)">Message throttling</A>.



6.  On the **Move configuration** page, enter a name for the migration batch in the **New migration batch name** text field. Then enter the target delivery domain in the **Target delivery domain for the mailboxes that are migrating to Office 365** field. In most hybrid deployments, this is the primary SMTP domain used for both on-premises and Exchange Online organization mailboxes. For example, contoso.com.

7.  Choose whether to also move the archive mailbox for the selected user and enter the database name you’d like to move this mailbox to in the **Target database** text field. For example, Mailbox Database 123456789. Click **Next**.

8.  On the **Start the batch** page, select at least one recipient to receive the batch complete report. Verify that **Automatically start the batch** is selected, and then select the **Automatically complete the migration batch** check box. Click **New**.

## Step 4: Remove completed migration batches

After your mailbox moves have completed, we recommend removing the completed migration batches to minimize the likelihood of errors if the same users are moved again.

To remove a completed migration batch:

1.  Open the EAC and navigate to **Office 365** \> **Recipients** \> **Migrations**.

2.  Click a completed migration batch, and then click **Delete** ![Delete icon](images/JJ906432.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon").

3.  On the deletion warning confirmation dialog, click **Yes**.

## Step 5: Re-enable offline access for Outlook on the web

Offline access in Outlook on the web (formerly called Outlook Web App) lets users access their mailbox when they're not connected to a network. If you migrate Exchange mailboxes to Exchange Online, users have to reset the offline access setting in their browser to use Outlook on the web offline. For more information about offline access in Outlook on the web, the browsers that support it, and how to turn it on, see [Using Outlook Web App offline](https://go.microsoft.com/fwlink/p/?linkid=286942).

## How do you know this worked?

When you move existing user mailboxes between the on-premises and Exchange Online organizations, the successful completion of the remote move wizard will be your first indication that moving the mailbox will complete as expected.

Because the mailbox move process takes several minutes to complete, you can also verify that the move is working correctly by opening the EAC and selecting **Office 365** \> **Recipients** \> **Migration** to display the move status for the mailboxes selected in the remote move wizard. The value of the **Status** is **Syncing** during the mailbox move, and it’s **Completed** when the mailbox has successfully moved to either the on-premises or Exchange Online organization.

After the mailbox move has completed, you can check that the remote mailbox located on the on-premises or Exchange Online organization has been successfully moved by verifying the mailbox properties. To do this, navigate to **Recipients** \> **Mailboxes** in the EAC for either the on-premises organization or Exchange Online organization. The user mailbox should show a **Mailbox Type** of **Office 365** for Exchange Online mailboxes and **User** for on-premises mailboxes.

You can also run the following cmdlet in the Exchange Management Shell to verify the status of the migration batch.

    Get-MigrationBatch -Identity <batch name>

Having problems? Ask for help in the Office 365 forums. To access the forums, you'll need to sign in using an account that's granted administrator access to your cloud-based service. Visit the forums at: [Office 365 Forums](https://go.microsoft.com/fwlink/p/?linkid=201915)

## New to Office 365?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="The short icon for LinkedIn Learning" alt="The short icon for LinkedIn Learning" /> <strong>New to Office 365?</strong><br />
Discover free video courses for <a href="https://support.office.com/en-us/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>, brought to you by LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

