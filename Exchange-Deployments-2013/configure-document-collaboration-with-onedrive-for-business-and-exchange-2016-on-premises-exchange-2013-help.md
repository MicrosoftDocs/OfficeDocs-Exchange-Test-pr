---
title: 'Configure document collaboration with OneDrive for Business and Exchange 2016 on-premises: Exchange 2013 Help'
TOCTitle: Configure document collaboration with OneDrive for Business and Exchange 2016 on-premises
ms:assetid: 799518aa-7cfe-4708-92ee-98057ff168f5
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Mt589761(v=EXCHG.150)
ms:contentKeyID: 70319377
ms.date: 04/30/2016
mtps_version: v=EXCHG.150
---

# Configure document collaboration with OneDrive for Business and Exchange 2016 on-premises

 

_**Applies to:** Exchange Server 2016_


**Summary:** How to allow your on-premises Exchange Server 2016 users to take advantage of using document collaboration with OneDrive for Business and SharePoint Online while in a hybrid configuration.

Recently a new attachment option has been made available in Office 365. In Exchange 2016, this option, known as *document collaboration*, allows on-premises users to integrate attachments stored on OneDrive for Business directly in their Outlook on the web clients.


> [!NOTE]
> Beginning with the release of Exchange Server 2016, Outlook Web App is now known as Outlook on the web.



Traditionally, a user would send a file to others by attaching it to a message. One or more recipients then made changes in their respective copies of the file, requiring all of those eventually have to be merged at some point. In addition, these attached files take up storage space in each user's mailbox. With document collaboration, users instead insert a link to a file that is stored in a OneDrive for Business account, allowing the file to be edited by multiple people in the same source location, with no extra storage required.

Before the Exchange 2016 environment is properly configured for document collaboration, an Outlook on the web user's default attachments dialog will look similar to this:

![traditional attachment dialog](images/Mt589761.f8c74d70-42f9-48c6-b263-ce6cef8591a8(EXCHG.150).png "traditional attachment dialog")

After configuring your environment with the instructions below, Outlook on the web attachment dialogs will look similar to this:

![attachment dialog with modern attachments enabled](images/Mt589761.89eeae65-ce3a-4c47-b57e-db734a1de95b(EXCHG.150).png "attachment dialog with modern attachments enabled")

Users in your organization with on-premises mailboxes and who have a OneDrive for Business account in Office 365 are eligible to use the modern attachment method, which would allow them to share a document stored in OneDrive for Business with multiple recipients. The location of the recipients (online versus on-premises) won't matter.

Learn more about hybrid deployments at [Exchange Server Hybrid Deployments](exchange-server-hybrid-deployments-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 15 minutes

  - Review [Exchange Server Hybrid Deployments](exchange-server-hybrid-deployments-exchange-2013-help.md), and make sure you understand the areas that will be affected by configuring a hybrid deployment.

  - Review and complete all hybrid deployment requirements outlined in [Hybrid deployment prerequisites](hybrid-deployment-prerequisites-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](https://technet.microsoft.com/en-us/library/jj150484\(v=exchg.150\)).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="http://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="http://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="http://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configure Exchange 2016 to enable document collaboration in a hybrid environment

Verify that the following prerequisite steps have been completed, and then use the procedure that follows to enable document collaboration.

**Prerequisites**

  - Configure your Exchange hybrid environment using the [Hybrid Configuration wizard](hybrid-configuration-wizard-exchange-2013-help.md) (HCW).

  - Exchange 2016 must be installed in your on-premises organization. Exchange 2016 can coexist with earlier versions of Exchange, but document collaboration will only work for mailboxes on an Exchange 2016 server.

  - The authenticating server must be installed with all users synchronized. You can use the [Get-AuthServer](https://technet.microsoft.com/en-us/library/jj218613\(v=exchg.150\)) cmdlet to find your authenticating server. We recommend using the HCW from an Exchange 2016 server to make any necessary OAuth configurations.
    

    > [!IMPORTANT]
    > OAuth between Exchange 2016 and Office 365 need to be configured properly. For more information see <A href="https://technet.microsoft.com/en-us/library/dn594521(v=exchg.150)">Configure OAuth authentication between Exchange and Exchange Online organizations</A>.



  - Users must have the proper licenses. Users with a OneDrive for Business account need to be licensed for either SharePoint Online or OneDrive for Business. You can verify a user's license by selecting the user in the Office 365 portal and selecting the **Edit** button.
    

    > [!NOTE]
    > See <A href="http://go.microsoft.com/fwlink/p/?linkid=627455">Set up OneDrive for Business in Office 365</A> for more information.



Perform the following steps:

1.  Configure the default Outlook on the web mailbox policy so that sets the OneDrive for Business host URL.
    

    > [!NOTE]
    > You can go to the Office 365 SharePoint Online Tenant Admin to retrieve the OneDrive for Business host URL. For example, https://contoso-my.sharepoint.com is a My Site Host URL in Contoso’s O365 tenant.<BR>Even though the Outlook on the web mailbox policy that comes with Exchange 2016 is called "Default", it isn't automatically applied to any mailboxes unless you either make it the default policy, or assign it directly to a mailbox.

    
    Using the following example as a basis, use the Exchange Management Shell to configure the internal and external MySite URL on the Default Outlook on the web mailbox policy:
    
        Set-OwaMailboxPolicy Default -InternalSPMySiteHostURL https://Contoso-my.sharepoint.com -ExternalSPMySiteHostURL https://Contoso-my.sharepoint.com

2.  Next, either set the policy you just configured as the default policy, so that it will be applied to all mailboxes, or assign the policy to individual users.
    
    To make the policy the default Outlook on the web mailbox policy, type the following command in the Exchange Management Shell:
    
        Set-OwaMailboxPolicy Default -IsDefault 
    
    To assign the policy to an individual's mailbox, type the following command in the Exchange Management Shell:
    
        Set-CASMailbox <user mailbox> -OwaMailboxPolicy Default

3.  (Optional) On each Exchange 2016 server, restart **OWAApplicationPool**, which will allow the configuration to work immediately. If you don't run this command, it'll take a few minutes for your Exchange 2016 servers to apply the updated mailbox policy. In the Exchange Management Shell run:
    
        Restart-WebAppPool MSExchangeOWAAppPool

Once configured, Outlook on the web users will be offered a choice for the type of attachment they'd like to apply to their messages: traditional or modern.

![attachment options dialog, Share with OneDrive or Send as attachment](images/Mt589761.7d2f27c2-3638-479a-a577-029ac61e7d95(EXCHG.150).png "attachment options dialog, Share with OneDrive or Send as attachment")

