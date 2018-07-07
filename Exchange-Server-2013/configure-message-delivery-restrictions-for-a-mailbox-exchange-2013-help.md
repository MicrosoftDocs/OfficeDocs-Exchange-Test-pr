---
title: 'Configure message delivery restrictions for a mailbox: Exchange 2013 Help'
TOCTitle: Configure message delivery restrictions for a mailbox
ms:assetid: c4b8b89f-3dbe-4cb8-8839-9a4e8067e00c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb397214(v=EXCHG.150)
ms:contentKeyID: 50396328
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Configure message delivery restrictions for a mailbox

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can use the EAC or the Shell to place restrictions on whether messages are delivered to individual recipients. Message delivery restrictions are useful to control who can send messages to users in your organization. For example, you can configure a mailbox to accept or reject messages sent by specific users or to accept messages only from users in your Exchange organization.

The message delivery restrictions covered in this topic apply to all recipient types. To learn more about the different recipient types, see [Recipients](recipients-exchange-2013-help.md).

For additional management tasks related to recipients, see the following topics:

  - [Manage user mailboxes](manage-user-mailboxes-exchange-2013-help.md)

  - [Create and manage distribution groups](create-and-manage-distribution-groups-exchange-2013-help.md)

  - [Manage dynamic distribution groups](manage-dynamic-distribution-groups-exchange-2013-help.md)

  - [Manage mail users](manage-mail-users-exchange-2013-help.md)

  - [Manage mail contacts](manage-mail-contacts-exchange-2013-help.md)

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipient Provisioning Permissions" section in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to configure message delivery restrictions

1.  In the EAC, navigate to **Recipients** \> **Mailboxes**.

2.  In the list of user mailboxes, click the mailbox that you want to configure message delivery restrictions for, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the mailbox properties page, click **Mailbox Features**.

4.  Under **Message Delivery Restrictions**, click **View details** to view and change the following delivery restrictions:
    
      - **Accept messages from**   Use this section to specify who can send messages to this user.
        
          - **All senders**   This option specifies that the user can accept messages from all senders. This includes both senders in your Exchange organization and external senders. This is the default option. It includes external users only if you clear the **Require that all senders are authenticated** check box. If you select this check box, messages from external users will be rejected.
        
          - **Only senders in the following list**   This option specifies that the user can accept messages only from a specified set of senders in your Exchange organization. Click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") to display a list of all recipients in your Exchange organization. Select the recipients you want, add them to the list, and then click **OK**. You can also search for a specific recipient by typing the recipient’s name in the search box and then clicking **Search** ![Search icon](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Search icon").
        
          - **Require that all senders are authenticated**   This option prevents anonymous users from sending messages to the user. This includes external users that are outside of your Exchange organization.
    
      - **Reject messages from**   Use this section to block people from sending messages to this user.
        
          - **No senders**   This option specifies that the mailbox won’t reject messages from any senders in the Exchange organization. This is the default option.
        
          - **Senders in the following list**   This option specifies that the mailbox will reject messages from a specified set of senders in your Exchange organization. Click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") to display a list of all recipients in your Exchange organization. Select the recipients you want, add them to the list, and then click **OK**. You can also search for a specific recipient by typing the recipient’s name in the search box and then clicking **Search** ![Search icon](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Search icon").

5.  Click **OK** to close the **Message Delivery Restrictions** page, and then click **Save** to save your changes.

## Use the Shell to configure message delivery restrictions

The following examples show how to use the Shell to configure message delivery restrictions for a mailbox. For other recipient types, use the corresponding **Set-** cmdlet with the same parameters.

This example configures the mailbox of Robin Wood to accept messages only from the users Lori Penor, Jeff Phillips, and members of the distribution group Legal Team 1.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom "Lori Penor","Jeff Phillips" -AcceptMessagesOnlyFromDLMembers "Legal Team 1"


> [!NOTE]
> If you're configuring a mailbox to accept messages only from individual senders, you have to use the <EM>AcceptMessagesOnlyFrom</EM> parameter. If you're configuring a mailbox to accept messages only from senders that are members of a specific distribution group, use the <EM>AcceptMessagesOnlyFromDLMembers</EM> parameter.



This example adds the user named David Pelton to the list of users whose messages will be accepted by the mailbox of Robin Wood.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom @{add="David Pelton"}

This example configures the mailbox of Robin Wood to require all senders to be authenticated. This means the mailbox will only accept messages sent by other users in your Exchange organization.

    Set-Mailbox -Identity "Robin Wood" -RequireSenderAuthenticationEnabled $true

This example configures the mailbox of Robin Wood to reject messages from the users Joe Healy, Terry Adams, and members of the distribution group Legal Team 2.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFrom "Joe Healy","Terry Adams" -RejectMessagesFromDLMembers "Legal Team 2"

This example configures the mailbox of Robin Wood to also reject messages sent by members of the group Legal Team 3.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFromDLMembers @{add="Legal Team 3"}


> [!NOTE]
> If you're configuring a mailbox to reject messages from individual senders, you have to use the <EM>RejectMessagesFrom</EM> parameter. If you're configuring a mailbox to reject messages from senders that are members of a specific distribution group, use the <EM>RejectMessagesFromDLMembers</EM> parameter.



For detailed syntax and parameter information related to configuring delivery restrictions for different types of recipients, see the following topics:

  - [Set-DistributionGroup](https://technet.microsoft.com/en-us/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/en-us/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/en-us/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/en-us/library/aa995950\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/en-us/library/aa995971\(v=exchg.150\))

## How do you know this worked?

To verify that you've successfully configured message delivery restrictions for a user mailbox, do one the following:

1.  In the EAC, navigate to **Recipients** \> **Mailboxes**.

2.  In the list of user mailboxes, click the mailbox that you want to verify the message delivery restrictions for, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the mailbox properties page, click **Mailbox Features**.

4.  Under **Message Delivery Restrictions**, click **View details** to verify the delivery restrictions for the mailbox.

Or

Run the following command in the Shell.

    Get-Mailbox <identity> | fl AcceptMessagesOnlyFrom,AcceptMessagesOnlyFromDLMembers,RejectMessagesFrom,RejectMessagesFromDLMembers,RequireSenderAuthenticationEnabled

