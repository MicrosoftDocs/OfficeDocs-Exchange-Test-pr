---
title: 'Create a Send connector to send email to a partner, with Transport Layer Security (TLS) applied: Exchange 2013 Help'
TOCTitle: Create a Send connector to send email to a partner, with Transport Layer Security (TLS) applied
ms:assetid: ff2abefc-dd3e-4431-b947-df942fbf82d9
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ657514(v=EXCHG.150)
ms:contentKeyID: 49289478
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Create a Send connector to send email to a partner, with Transport Layer Security (TLS) applied

 

_**Applies to:** Exchange Server 2013_


If you want to ensure secure, encrypted communication with a partner, you can create a Send connector that is configured to enforce Transport Layer Security (TLS) for messages sent to a partner domain. TLS provides secure communication over the Internet.

Interested in scenarios where this procedure is used? See the following topics:

  - [Configure mail flow and client access](configure-mail-flow-and-client-access-exchange-2013-help.md)

## What do you need to know before you begin?

  - Estimated time to complete: 10 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Send connectors" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - See [Deploy a new installation of Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) if you are beginning your installation. After the installation you can use the steps in this topic to create your outbound connector.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the EAC to create a Send connector to send email to a partner, with TLS applied

To create a Send connector for this scenario, log in to the EAC and perform the following steps:

1.  In the EAC, navigate to **Mail flow** \> **Send connectors**, and then click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

2.  In the **New send connector** wizard, specify a name for the send connector and then select **Partner** for the **Type**. When you select **Partner**, the connector is configured to allow connections only to servers that authenticate with TLS certificates. Click **Next**.

3.  Verify that **MX record associated with recipient domain** is selected, which specifies that the connector uses the domain name system (DNS) to route mail. Click **Next**.

4.  Under **Address space**, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"). In the **Add domain** window, make sure SMTP is listed as the **Type**. For **Fully Qualified Domain Name (FQDN)**, enter the name of your partner domain. Click **Save**.

5.  For **Source server**, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"). In the **Select a server** window, select a Mailbox server that will be used to send mail to the Internet via the Client Access server and click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"). After you've selected the server, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"). Click **OK**.

6.  Click **Finish**.

Once you have created the Send connector, it appears in the Send connector list.

## How do you know this worked?

To verify that you have successfully created a Send connector to send email to a partner, with TLS applied, send a message from a user in your organization to a recipient at the partner organization. If the recipient receives the message, the connector was created successfully.

## For more information

[Create a Send connector for email sent to the Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Create a Send connector to route outbound email through a smart host](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

