---
title: 'Modify the SMTP banner on a Receive connector: Exchange 2013 Help'
TOCTitle: Modify the SMTP banner on a Receive connector
ms:assetid: d667704e-fd69-4aca-9c35-eef7006944b2
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124740(v=EXCHG.150)
ms:contentKeyID: 50934226
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Modify the SMTP banner on a Receive connector

 

_**Applies to:** Exchange Server 2013_


The *SMTP banner* is the SMTP connection response that a remote SMTP messaging server receives after it connects to a Receive connector that's configured on a computer running Microsoft Exchange Server 2013.

This is the default response received by a remote SMTP messaging server after it connects to the Receive connector:

    220 <Servername> Microsoft ESMTP MAIL service ready at <RegionalDay-Date-24HourTimeFormat> <RegionalTimeZoneOffset>

When you specify a custom value for SMTP banner on a Receive connector, a remote SMTP messaging server that connects to that SMTP Receive connector receives the following response.

    220 <Banner Text>

You may want to modify the SMTP banner for Internet-facing SMTP Receive connectors so the server name and messaging server software aren't disclosed by the SMTP banner.

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Receive connectors" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - You can only use the Shell to perform this procedure.

  - The replacement SMTP banner text string must always start with `220`. As defined in RFC 2821, the default service ready SMTP response code is 220.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to modify the SMTP banner on a Receive connector

Run the following command:

    Set-ReceiveConnector <ConnectorIdentity> -Banner "220 <Banner Text>"

This example modifies the SMTP banner on the existing Receive connector named From the Internet so the SMTP banner displays `220 Contoso Corporation`.

    Set-ReceiveConnector "From the Internet" -Banner "220 Contoso Corporation"

This example removes the custom SMTP banner on the Receive connector named From the Internet, which returns the SMTP banner to the default value.

    Set-ReceiveConnector "From the Internet" -Banner $null

## How do you know this worked?

To verify that you have successfully modified the SMTP banner on a Receive connector, do the following:

1.  Open a telnet client on a computer that can access the Receive connector, and run the following command:
    
        open <Connector FQDN or IP address> <Port>

2.  Verify the response from the Receive connector contains the SMTP banner you configured.

Note that this procedure only works on Receive connectors that allow anonymous or Basic authentication. For more information, see [Use Telnet to test SMTP communication](use-telnet-to-test-smtp-communication-exchange-2013-help.md).

