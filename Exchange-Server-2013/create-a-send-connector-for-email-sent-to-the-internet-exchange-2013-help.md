---
title: 'Create a Send connector for email sent to the Internet: Exchange 2013 Help'
TOCTitle: Create a Send connector for email sent to the Internet
ms:assetid: 6deaefa8-1152-40d9-b1ba-9c19bdf8a928
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ657457(v=EXCHG.150)
ms:contentKeyID: 49289297
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Create a Send connector for email sent to the Internet

 

_**Applies to:** Exchange Server 2013_


By default, Microsoft Exchange Server 2013 doesn’t allow you to send mail outside of your domain. To send mail outside your domain, you need to create a Send connector. The following graphic illustrates mail flow when you create a Send connector to send mail to the Internet.

![connector\_send\_onprem\_internet](images/JJ657457.e8963e4f-7dce-461f-bbcf-660278cefa35(EXCHG.150).gif "connector_send_onprem_internet")

Interested in scenarios where this procedure is used? See the following topics:

  - [Configure mail flow and client access](configure-mail-flow-and-client-access-exchange-2013-help.md)

## What do you need to know before you begin?

  - Estimated time to complete: 15 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Send connectors" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - See [Deploy a new installation of Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) if you are beginning your installation. After the installation you can use the steps in this topic to create your outbound connector.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the EAC to create a send connector for email sent to the Internet

1.  In the EAC, navigate to **Mail flow** \> **Send connectors**, and then click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

2.  In the **New send connector** wizard, specify a name for the send connector and then select **Internet** for the **Type**. Click **Next**.

3.  Verify that **MX record associated with recipient domain** is selected, which specifies that the connector uses the domain name system (DNS) to route mail. Click **Next**.

4.  Under **Address space**, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"). In the **Add domain** window, make sure SMTP is listed as the **Type**. For **Fully Qualified Domain Name (FQDN)**, enter \*, which indicates that this send connector applies to messages addressed to any domain. Click **Save**.

5.  Make sure **Scoped send connector** is not selected and then click **Next**.

6.  For **Source server**, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"). In the **Select a server** window, select a Mailbox server that will be used to send mail to the Internet via the Client Access server and click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"). After you've selected the server, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"). Click **OK**.

7.  Click **Finish**.

Once you have created the Send connector, it appears in the Send connector list.

## Use the Shell to route mail through the Client Access server

In Exchange 2013 you can use the *FrontendProxyEnabled* parameter of the **Set-SendConnector** cmdlet to route outbound messages through the Client Access server. This parameter is not set to `$true` by default, but in many cases it can consolidate and simplify mail flow, especially if you are working with an environment with a large number of messaging servers.

This example sets the *FrontendProxyEnabled* parameter to `$true` on a Send connector.

    Set-SendConnector "Contoso.com Send Connector" -FrontendProxyEnabled $true

## How do you know this worked?

To verify that you have successfully created a Send Connector for email sent to the Internet, send mail from one of your users to an outside recipient and verify that the message arrives successfully.

## For more information

[Send connectors](send-connectors-exchange-2013-help.md)

[Create a Send connector to route outbound email through a smart host](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

