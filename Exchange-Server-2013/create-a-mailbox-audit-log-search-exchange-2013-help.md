---
title: 'Create a mailbox audit log search: Exchange 2013 Help'
TOCTitle: Create a mailbox audit log search
ms:assetid: 48ba22cf-b1f2-4dbc-98fc-fed22d97db14
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ff461929(v=EXCHG.150)
ms:contentKeyID: 49300496
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Create a mailbox audit log search

 

_**Applies to:** Exchange Server 2013_


You can create a mailbox audit log search to asynchronously search one or more mailboxes and have the search results sent by email as an XML file to specified addresses.

To search mailbox audit logs for a single mailbox and have the results displayed in the Shell, see [Search the mailbox audit log for a mailbox](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md).

For additional management tasks related to mailbox audit logging, see [Mailbox audit logging procedures](mailbox-audit-logging-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 2 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox audit logging" entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

  - By default, mailbox audit logging is disabled for all mailboxes. For each mailbox you want to audit, you must enable audit logging and specify the mailbox owner, delegate, or administrator actions you want to audit. For more details, see [Enable or disable mailbox audit logging for a mailbox](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md).

  - You can’t use the EAC to search mailbox audit logs for owner access. The auditing section in EAC includes reports for non-owner mailbox access and also allows you to search for and export non-owner access events.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the EAC to create a mailbox audit log search

1.  Navigate to **Compliance management** \> **Auditing**.

2.  In the list view, select **Export mailbox audit logs**.

3.  In **Export Mailbox Audit Logs**, complete the following fields, and then click **Export**:
    
      - **Start date**
    
      - **End date**
    
      - **Search these mailboxes or leave blank to find all mailboxes accessed by non-owners**
        

        > [!WARNING]
        > Depending on the number of mailboxes in your organization and the amount of mailbox audit log data in each mailbox, searching all mailboxes may take a long time.

    
      - **Search for access by**
        
        Select from the following types of access events you want to search:
        
          - **All non-owners**
        
          - **External users**
        
          - **Administrators and delegated users**
        
          - **Administrators**
    
      - **Send the auditing report to**

## Use the Shell to create a mailbox audit log search

For an example of how to use the Shell to create a mailbox audit log search, see [Example 1](https://technet.microsoft.com/en-us/95365cab-bbb2-4a64-8e8f-1c89fa9e0352\(exchg.150\)#example1) in **New-MailboxAuditLogSearch**.

