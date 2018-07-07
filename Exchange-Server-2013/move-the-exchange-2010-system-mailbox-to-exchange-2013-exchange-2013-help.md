---
title: 'Move the Exchange 2010 system mailbox to Exchange 2013: Exchange 2013 Help'
TOCTitle: Move the Exchange 2010 system mailbox to Exchange 2013
ms:assetid: a3b03c4e-0bc7-41a2-885c-e9cac37566c8
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn249849(v=EXCHG.150)
ms:contentKeyID: 54770204
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Move the Exchange 2010 system mailbox to Exchange 2013

 

_**Applies to:** Exchange Server 2013_


In Exchange 2010, the Microsoft Exchange system mailbox is an arbitration mailbox used to store organization-wide data such as administrator audit logs, metadata for eDiscovery searches, and Unified Messaging data, such as menus, dial plans, and custom greetings. The Microsoft Exchange system mailbox is named **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}**; the display name is **Microsoft Exchange**.

When you upgrade your existing Exchange 2010 organization to Exchange 2013, you have to move the Microsoft Exchange system mailbox to a mailbox database on an Exchange 2013 Mailbox server. You should move this mailbox after you’ve installed and verified Exchange 2013. If you don’t move this system mailbox to Exchange 2013, the following issues will occur when Exchange 2010 and Exchange 2013 coexist in your Exchange organization:

  - Exchange 2013 tasks aren’t saved to the administrator audit log. When you run the **Search-AdminAuditLog** cmdlet or try to export the administrator audit log in the EAC, you’ll receive an error that says you can’t create an administrator audit log search because the system mailbox, SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}, is located on a server that isn’t running Exchange 2013. A Microsoft Exchange error with an Event ID of 5000 is also logged in the Windows Application log each time a command is run.

  - You can’t run eDiscovery searches using the EAC or the Shell in Exchange 2013. Mailbox searches can be created and queued, but they can’t be started. An error with an Event ID of 6 is logged in the MsExchange Management log, stating that the **Start-MailboxSearch** cmdlet failed. However, you can search mailboxes using the Shell and the Exchange Control Panel (ECP) in Exchange 2010.

You also have to move the Microsoft Exchange system mailbox to Exchange 2013 as part of upgrading Exchange 2010 Unified Messaging to Exchange 2013.

For more information about upgrading to Exchange 2013, see the following topics:

  - [Upgrade from Exchange 2010 to Exchange 2013](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)

  - [Upgrade Exchange 2010 UM to Exchange 2013 UM](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md)

## What do you need to know before you begin?

  - Estimated time to complete: 20 minutes. The actual time may vary depending on the size of the system mailbox.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox Move and Migration Permissions" entry in [Recipients Permissions](recipients-permissions-exchange-2013-help.md).

  - Run the following command in Exchange 2013 to obtain the identity and version of the Exchange servers and mailbox databases that contain the system mailboxes in your organization.
    
        Get-Mailbox -Arbitration | FL Name,DisplayName,ServerName,Database,AdminDisplayVersion
    
    The **AdminDisplayVersion** property indicates the version of Exchange that the server is running. The value `Version 14.x` indicates Exchange 2010; the value `Version 15.x` indicates Exchange 2013.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to move the system mailbox

1.  In the EAC, go to **Recipients** \> **Migration**.

2.  Click **New** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"), and then click **Move to a different database**.

3.  On the **New local mailbox move** page, click **Select the users that you want to move**, and then click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

4.  On the **Select Mailbox** page, add the mailbox that has the following properties:
    
      - The display name is **Microsoft Exchange**.
    
      - The alias of the mailbox’s email address is **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}**.

5.  Click **OK**, and then click **Next**.

6.  On the **Move configuration** page, type the name of the migration batch, and then click **Browse** next to the **Target database** box.

7.  On the **Select Mailbox Database** page, add the mailbox database to move the system mailbox to. Verify that the version of the mailbox database that you select is Version 15. x, which indicates that the database is located on an Exchange 2013 server.

8.  Click **OK**, and then click **Next**.

9.  On the **Start the batch** page, select the options to automatically start and complete the migration request, and then click **New**.

## Use the Shell to move the system mailbox

First, run the following command in Exchange 2013 to obtain the names and versions of all mailbox databases in your organization.

    Get-MailboxDatabase -IncludePreExchange2013 | FL Name,Server,AdminDisplayVersion

After you identify the name of the mailbox databases in your organization, run the following command in Exchange 2013 to move the Microsoft Exchange system mailbox to a mailbox database located on an Exchange 2013 server.

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | New-MoveRequest -TargetDatabase <name of Exchange 2013 database>

## How do you know this worked?

To verify that you’ve successfully moved the Microsoft Exchange system mailbox to a mailbox database located on an Exchange 2013 server, run the following command in the Shell.

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | FL Database,ServerName,AdminDisplayVersion

If the value of the **AdminDisplayVersion** property is **Version 15.x (Build xxx.x)**, this verifies that the system mailbox resides on a mailbox database that is located on an Exchange 2013 server.

After you move the Microsoft Exchange system mailbox to Exchange 2013, you’ll also be able to successfully perform the following administrative tasks:

  - Run the **Search-AdminAuditLog** cmdlet.

  - Export the administrator audit log in the EAC.

  - Successfully create and start eDiscovery searches using the EAC or the Shell in Exchange 2013.

