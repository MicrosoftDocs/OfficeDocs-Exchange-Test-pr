---
title: 'Delegate the installation of an Exchange 2013 server: Exchange 2013 Help'
TOCTitle: Delegate the installation of an Exchange 2013 server
ms:assetid: f2fc8680-0c7c-4a29-b8f5-d77404fec280
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb201741(v=EXCHG.150)
ms:contentKeyID: 62613983
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Delegate the installation of an Exchange 2013 server

 

_**Applies to:** Exchange Online, Exchange Server, Exchange Server 2013_


Exchange Server 2013 lets you delegate the installation of Exchange servers to people who aren't members of the Exchange 2013 Organization Management role group. This is often helpful in large companies where the people who install and set up servers aren't the same people who manage services, like Exchange. If this sounds like something you want to do, this topic is for you.

Normally, when Exchange is installed, the people installing it need to be members of the [Organization Management](organization-management-exchange-2013-help.md) role group. This is because when Exchange is installed, changes are made to Active Directory, and only Exchange administrators, who are members of the Organization Management role group, can make those changes. The following list shows the changes that are made:

  - A server object is created in the **CN=Servers,CN=Exchange Administrative Group (FYDIBOHF23SPDLT),CN=Administrative Groups,CN=\<Organization Name\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<Root Domain\>** configuration partition.

  - The following access control entries (ACEs) are added to the server object within the configuration partition for the Delegated Setup role group:
    
      - Full Control on the server object and its child objects
    
      - Deny access control entry for the Send As extended right
    
      - Deny access control entry for the Receive As extended right
    
      - Deny CreateChild and DeleteChild permissions for Exchange Public Folder Store objects
    

    > [!NOTE]
    > Public folders are administered at an organizational level; therefore, the creation and deletion of public folder stores is restricted to Exchange administrators.



  - The Active Directory computer account for the server is added to the Exchange Servers group.

  - The server is added as a provisioned server in the Exchange Admin Center.

In large companies, the people who install and set up new servers often aren't Exchange administrators. To enable them to install Exchange, an Exchange administrator can *provision* the server in Active Directory. When a server is provisioned, all of the changes needed for the new Exchange server to function are made to Active Directory separately from the actual installation of Exchange on a computer. An Exchange administrator can provision a new server in Active Directory hours or even days before Exchange is installed on the new computer. After a server has been provisioned, the person doing the installation needs only to be a member of the [Delegated Setup](delegated-setup-exchange-2013-help.md) role group to install Exchange. The Delegated Setup role group only allows members to install provisioned servers.

Keep the following in mind when thinking about using delegated setup:

  - At least one Exchange 2013 server has to already be installed before you can delegate the installation of additional servers. The person who installs the first server needs to be an Exchange administrator. For more information, check out [Checklist: Perform a new installation of Exchange 2013](checklist-perform-a-new-installation-of-exchange-2013-exchange-2013-help.md).

  - A delegated user can't uninstall an Exchange server. To uninstall an Exchange server, you need to be an Exchange administrator.

## How do I provision an Exchange 2013 server?

To provision a server for Exchange, you need to use Exchange 2013 command-line Setup. If you're not very familiar with the Windows Command Prompt, don't worry. This topic steps you through exactly what you need to do. Before we start, here are a couple of things to keep in mind:

  - You need to be a member of the Organization Management role group to provision a server.

  - You should have the latest release of Exchange 2013. You can get the download link from [Updates for Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

The command that you need to use to provision the server depends on whether you're running Setup from the computer you're provisioning or whether you're running it from another computer. Choose the command in the following steps that matches where you're running Setup:

1.  Press the Windows key + 'R' to open the **Run** window.

2.  In **Open**, type**cmd.exe**, and then press Enter to open a **Windows Command Prompt**.

3.  Change directories to where you downloaded and expanded the Exchange 2013 install files. If the install files are located in `C:\Downloads\Exchange 2013`, use the following command.
    
        CD "C:\Downloads\Exchange 2013"

4.  Choose the command that matches where you're running Setup:
    
      - **If you're running Setup on the computer that's being provisioned**, run the following command:
        
            Setup.exe /NewProvisionedServer /IAcceptExchangeServerLicenseTerms
    
      - **If you're running Setup on another computer**, run the following command:
        
            Setup.exe /NewProvisionedServer:<ComputerName> /IAcceptExchangeServerLicenseTerms

5.  After you provision the server, you need to make sure that you've added the users who should be able to install Exchange on provisioned servers to the Delegated Setup role group. To see how to add users to a role group, see [Manage Role Group Members](manage-role-group-members-exchange-2013-help.md).

When you're done with these steps, the computer will be ready for Exchange to be installed. Exchange 2013 can be installed on a provisioned server by using the steps in [Install Exchange 2013 using the Setup wizard](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).

## How do I know this worked?

To make sure the server was properly provisioned for Exchange, you can do the following:

1.  Go to **Start** \> **Administrative Tools**, and then open **Active Directory Users and Computers**.

2.  Select **Microsoft Exchange Security Groups**, double-click **Exchange Servers**, and then select the **Members** tab.

3.  On the **Members** tab, check to see if the server you just provisioned is listed as a member of the security group.

If your server is listed as a member of the Exchange Servers security group, it was properly provisioned. Someone who's a member of the Delegated Setup role group can now install Exchange on that server.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Did you find what you’re looking for? Please take a minute to [send us feedback](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) about the information you were hoping to find.

