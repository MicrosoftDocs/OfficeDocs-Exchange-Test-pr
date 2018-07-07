---
title: 'Install Exchange 2013 using the Setup wizard: Exchange 2013 Help'
TOCTitle: Install Exchange 2013 using the Setup wizard
ms:assetid: da690d47-3384-4430-a69e-0cd4d3bf80a7
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124778(v=EXCHG.150)
ms:contentKeyID: 48385623
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.ExSetupUI.SetupWizardForm.IntroductionPage
---

# Install Exchange 2013 using the Setup wizard

 

_**Applies to:** Exchange Server 2013_


This topic explains how to use the Microsoft Exchange Server 2013 Setup wizard to install the Exchange 2013 Mailbox and Client Access roles on a computer. For more information about planning and deploying Exchange 2013, see [Planning and deployment](planning-and-deployment-for-exchange-2013-installation-instructions.md).

If you want to install the Exchange 2013 Edge Transport role on a computer, see [Install the Exchange 2013 Edge Transport role using the Setup wizard](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md). The Edge Transport role can't be installed on the same computer as the Mailbox or Client Access server roles.


> [!TIP]
> Have you heard about the Exchange Server Deployment Assistant? It's a free online tool that helps you quickly deploy Exchange 2013 in your organization by asking you a few questions and creating a customized deployment checklist just for you. If you want to learn more about it, go to <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server Deployment Assistant</A>.




> [!NOTE]
> After you install any server roles on a computer running Exchange 2013, you can't use the Exchange 2013 Setup wizard to add any additional server roles to this computer. If you want to add more server roles to a computer, you must either use Add or Remove Programs from Control Panel or use Setup.exe from a Command Prompt window.



For information about tasks to complete after installation, see [Exchange 2013 post-Installation tasks](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 60 minutes

  - Make sure you've read the release notes prior to installing Exchange 2013. For more information, see [Release notes for Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - Each organization requires at a minimum one Client Access server and one Mailbox server in the Active Directory forest. Additionally, each Active Directory site that contains a Mailbox server must also contain at least one Client Access server. If you're separating your server roles, we recommend installing the Mailbox server role first.

  - The computer you install Exchange 2013 on must have a supported operating system (such as Windows Server 2008 R2 with Service Pack 1 (SP1) or Windows Server 2012), have enough disk space, be a member of an Active Directory domain, and satisfy other requirements. For information about system requirements, see [Exchange 2013 system requirements](exchange-2013-system-requirements-exchange-2013-help.md).

  - To run Exchange 2013 setup, you must install Microsoft .NET Framework 4.5, Windows Management Framework 3.0, and other required software. To understand the prerequisites for all server roles, see [Exchange 2013 prerequisites](exchange-2013-prerequisites-exchange-2013-help.md).

  - You must ensure the account you use is delegated membership in the Schema Admins group if you haven't previously prepared the Active Directory schema. If you're installing the first Exchange 2013 server in the organization, the account you use must have membership in the Enterprise Admins group. If you've already prepared the schema and aren't installing the first Exchange 2013 server in the organization, the account you use must be a member of the Exchange 2013 Organization Management role group.
    
    Administrators who are members of the Delegated Setup role group can deploy Exchange 2013 servers that have been previously provisioned by a member of the Organization Management management role group.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> After you install Exchange on a server, you must not change the server name. Renaming a server after you have installed an Exchange server role is not supported.



## Install Exchange Server 2013

If you're installing the first Exchange 2013 server in the organization, and the Active Directory preparation steps have not been performed, the account you use must have membership in the Enterprise Administrators group. If you haven't previously prepared the Active Directory Schema, the account must also be a member of the Schema Admins group. For information about preparing Active Directory for Exchange 2013, see [Prepare Active Directory and domains](prepare-active-directory-and-domains-exchange-2013-help.md). If you have already performed the Schema and Active Directory preparation steps, the account you use must be a member of the Delegated Setup management role group or the Organization Management role group.


> [!NOTE]
> To download the latest version of Exchange 2013, see <A href="updates-for-exchange-2013-exchange-2013-help.md">Updates for Exchange 2013</A>.



1.  Log on to the computer on which you want to install Exchange 2013.

2.  Navigate to the network location of the Exchange 2013 installation files.

3.  Start Exchange 2013 Setup by double-clicking `Setup.exe`
    

    > [!IMPORTANT]
    > If you have User Access Control (UAC) enabled, you must right-click <CODE>Setup.exe</CODE> and select <STRONG>Run as administrator</STRONG>.



4.  On the **Check for Updates?** page, choose whether you want Setup to connect to the Internet and download product and security updates for Exchange 2013. If you select **Connect to the Internet and check for updates**, Setup will download updates and apply them prior to continuing. If you select **Don't check for updates right now**, you can download and install updates manually later. We recommend that you download and install updates now. Click **Next** to continue.

5.  
    
    The **Introduction** page begins the process of installing Exchange into your organization. It will guide you through the installation. Several links to helpful deployment content are listed. We recommend that you visit these links prior to continuing setup. Click **Next** to continue.

6.  
    
    On the **License Agreement** page, review the software license terms. If you agree to the terms, select **I accept the terms in the license agreement**, and then click **Next**.

7.  
    
    On the **Recommended settings** page, select whether you want to use the recommended settings. If you select **Use recommended settings**, Exchange will automatically send error reports and information about your computer hardware and how you use Exchange to Microsoft. If you select **Don't use recommended settings**, these settings remain disabled but you can enable them at any time after Setup completes. For more information about these settings and how information sent to Microsoft is used, click **?**.

8.  
    
    On the **Server Role Selection** page, choose whether you want to install the **Mailbox role**, the **Client Access role**, both roles, or just the **Management Tools** on this computer. You can add additional server roles later if you choose not to install them during this installation. An organization must have at least one Mailbox role and at least one Client Access server role installed. They can be installed on the same computer or on separate computers. The management tools are installed automatically if you install any server role.
    
    Select **Automatically install Windows Server roles and features that are required to install Exchange Server** to have the Setup wizard install required Windows prerequisites. You may need to reboot the computer to complete the installation of some Windows features. If you don't select this option, you must install the Windows features manually.
    

    > [!NOTE]
    > This option installs only the Windows features required by Exchange. You must manually install other prerequisites manually. For more information, see <A href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 prerequisites</A>.

    
    Click **Next** to continue.

9.  On the **Installation Space and Location** page, either accept the default installation location or click **Browse** to choose a new location. Make sure that you have enough disk space available in the location where you want to install Exchange. Click **Next** to continue.

10. 
    
    If this is the first Exchange server in your organization, on the **Exchange Organization** page, type a name for your Exchange organization. The Exchange organization name can contain only the following characters:
    
      - A through Z
    
      - a through z
    
      - 0 through 9
    
      - Space (not leading or trailing)
    
      - Hyphen or dash
        

        > [!NOTE]
        > The organization name can't contain more than 64 characters. The organization name can't be blank.

    
    If you want to use the Active Directory split permissions model, select **Apply Active Directory split permission security model to the Exchange organization**.
    

    > [!WARNING]
    > Most organizations don't need to apply the Active Directory split permissions model. If you need to separate management of Active Directory security principals and Exchange configuration, Role Based Access Control (RBAC) split permissions might work for you. For more information, click <STRONG>?</STRONG>.

    
    Click **Next** to continue.

11. If you're installing the Mailbox role, on the **Malware Protection Settings** page, choose whether you want to enable or disable malware scanning. If you disable malware scanning, it can be enabled in the future. Click **Next** to continue.

12. 
    
    On the **Readiness Checks** page, view the status to determine if the organization and server role prerequisite checks completed successfully. If they haven't completed successfully, you must resolve any reported errors before you can install Exchange 2013. You don't need to exit Setup when resolving some of the prerequisite errors. After resolving a reported error, click **back** and then click **Next** to run the prerequisite check again. Be sure to also review any warnings that are reported. If all readiness checks have completed successfully, click **Next** to install Exchange 2013.

13. 
    
    On the **Completion** page, click **Finish**.

14. Restart the computer after Exchange 2013 has completed.

15. Complete your deployment by performing the tasks provided in [Exchange 2013 post-Installation tasks](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## How do you know this worked?

To verify that you've successfully installed Exchange 2013, see [Verify an Exchange 2013 installation](verify-an-exchange-2013-installation-exchange-2013-help.md).

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Did you find what you’re looking for? Please take a minute to [send us feedback](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) about the information you were hoping to find.

