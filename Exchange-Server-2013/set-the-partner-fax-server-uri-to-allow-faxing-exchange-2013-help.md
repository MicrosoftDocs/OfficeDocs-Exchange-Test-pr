---
title: 'Set the partner fax server URI to allow faxing: Exchange 2013 Help'
TOCTitle: Set the partner fax server URI to allow faxing
ms:assetid: 77a9013b-d76b-4af2-8b2c-cef435cf67af
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ650873(v=EXCHG.150)
ms:contentKeyID: 49352374
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Set the partner fax server URI to allow faxing

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


You can enable and disable inbound faxes for users associated with a Unified Messaging (UM) mailbox policy. By default, when you enable users for UM, users can't receive fax messages until you enable inbound faxing on the UM mailbox policy and specify the URI for the partner fax server. If the URIs are configured on the UM mailbox policy but the option to allow incoming faxes is disabled on the UM dial plan or for an individual user, UM-enabled users linked to the UM mailbox policy still won't be able to receive faxes.

For more information about fax partners, see [Microsoft PinPoint for Fax Partners](https://go.microsoft.com/fwlink/?linkid=190238).

For additional management tasks related to faxing, see [Faxing procedures](faxing-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM mailbox policies" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM mailbox policy has been created. For detailed steps, see [Create a UM mailbox policy](create-a-um-mailbox-policy-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to set the fax partner URI

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**. In the list view, select the UM dial plan you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

2.  On the **UM dial plan** page, under **UM Mailbox Policies**, select the policy you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM mailbox policy** page \> **General**, in the **Partner fax server URI** box, enter the TCP or TLS URI. For example: *sip:faxserver1.contoso.com:5060;transport=tcp* or *sip:faxserver2.contoso.com:5061;transport=tls*
    

    > [!NOTE]
    > Although the box can contain more than one fax server URI, only one will be used. If you enter two URIs, only the first will be used.



4.  Click **Save** to save your changes.

## Use the Shell to set the fax partner URI

This example allows users who are linked with the UM mailbox policy `UMDialPlan Default Policy` to use TCP with port 5060 for the partner fax server `faxserver1`.

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver1.contoso.com:5060;transport=tcp

This example allows users who are linked with the UM mailbox policy `UMDialPlan Default Policy` to use TLS with port 5061 for the partner fax server `faxserver2`.

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver2.contoso.com:5061;transport=tls

