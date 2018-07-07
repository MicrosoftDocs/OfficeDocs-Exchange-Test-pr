---
title: 'Content conversion tracing: Exchange 2013 Help'
TOCTitle: Content conversion tracing
ms:assetid: eb9c7df2-9093-49f9-aa4f-044909bd2225
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb397226(v=EXCHG.150)
ms:contentKeyID: 49345062
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Content conversion tracing

 

_**Applies to:** Exchange Server 2013_


Content conversion tracing captures failures in the MAPI content conversion that's performed by the Mailbox Transport service on inbound and outbound messages on a Microsoft Exchange Server 2013 Mailbox server.

The Mailbox Transport service on a Mailbox server is responsible for the content conversion of messages sent to and from mailbox recipients. Specifically, the Mailbox Transport Submission service converts outbound messages from mailbox users from MAPI to MIME. The Mailbox Transport Delivery service converts inbound messages for mailbox users from MIME to MAPI. Content conversion tracing is responsible for capturing these MAPI conversion failures.

The categorizer in the Transport service on a Mailbox server is responsible for the content conversion of all messages sent to external recipients. Content conversion tracing doesn't capture any content conversion failures that the categorizer in the Transport service encounters as it converts messages sent to external recipients.

**Contents**

Configure content conversion tracing

How content conversion tracing works

Considerations for content conversion tracing

## Configure content conversion tracing

Content conversion tracing is controlled by the following parameters in the **Set-TransportService** and **Set-MailboxTransportService** cmdlets in the Exchange Management Shell:

  - *ContentConversionTracingEnabled*   This parameter enables or disables content conversion tracing in the Transport service on the Mailbox server, or in the Mailbox Transport service on the Mailbox server. Valid values for this parameter are `$true` and `$false`. The default value is `$false`. If your Exchange organization contains multiple Mailbox servers, you must enable content conversion tracing on each Mailbox server.

  - *PipelineTracingPath*   Although this parameter is associated with pipeline tracing, it also specifies the root location of the content conversion tracing files. The default location in the Transport service is `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`. The default location in the Mailbox Transport service is `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`.The path must be local to the Exchange computer.

Content conversion creates a folder named `ContentConversionTracing` in the path specified by the *PipelineTracingPath* parameter. In the `ContentConversionTracing` folder, content conversion creates two subfolders: `InboundFailures` and `OutboundFailures`. The `InboundFailures` folder contains the information from inbound message content conversion failures. The `OutboundFailures` folder contains the information from outbound message content conversion failures.

The maximum size for all the files in the `InboundFailures` folder or the `OutboundFailures` folder is 128 megabytes (MB). Content conversion tracing doesn't use circular logging to remove old files based on the age or size of the files. As soon as the maximum size for a folder is reached, content conversion tracing stops writing information to the folder. If you want to make sure that the maximum folder size limits aren't exceeded, you can create a scheduled task that periodically moves the content conversion tracing files to a different location.

The permissions required on the folders and subfolders used in content conversion tracing are as follows:

  - Administrators: Full Control

  - Network Service: Full Control

  - System: Full Control


> [!WARNING]
> Content conversion tracing copies the complete contents of email messages. To avoid the unwanted disclosure of confidential information, you need to set appropriate security permissions on the location of the content conversion tracing files.



Return to top

## How content conversion tracing works

When the content conversion of an inbound message fails, a delivery status notification (DSN) that has the status code 5.6.0 is sent to the message sender. If content conversion tracing is enabled, the failure information is recorded at the time that the 5.6.0 DSN message is generated. Each content conversion error generates two separate files.

A content conversion error that occurs when an inbound message is converted from MIME to MAPI generates the following two files in the InboundFailures folder:

  - **\<GUID\>.eml**   This file contains the failed message in text format.

  - **\<GUID\>.txt**   This file contains the exception description, conversion results, conversion options, and message size limits imposed on all messages by the Mailbox Transport service.

A content conversion error that occurs when an outbound message is converted from MAPI to MIME generates the following two files in the OutboundFailures folder:

  - **\<GUID\>.msg**   This file contains the failed message in the Microsoft Outlook message format.

  - **\<GUID\>.txt**   This file contains the exception description, conversion results, conversion options, and message size limits imposed on all messages by the store driver.

The placeholder \<*GUID*\> is the same in both file names. Each content conversion error generates a different GUID that's used in the file names of the corresponding message and text files. An example of a GUID that's used in the file names is `038b930e-61fd-4bfd-b9b4-0374c18b73f7`.

Return to top

## Considerations for content conversion tracing

You can leave content conversion tracing enabled for proactive monitoring. Or, you can enable content conversion tracing to troubleshoot a specific failure event. You can usually reproduce inbound content conversion failures by asking the recipient of the 5.6.0 DSN message to resend the original message.

Inbound content conversion failures are the most common. Some of the reasons for inbound content conversion errors include the following:

  - **Violations of message size limits**   These message size limits are imposed by the Mailbox Transport service to help prevent denial of service attacks (DoS). These message limits are listed in the \<*GUID*\>.txt file. These message limits include the following:
    
      - **MaxMimeTextHeaderLength**   This limit specifies the maximum number of text characters that can be used in a MIME header. The value is 2000.
    
      - **MaxMimeSubjectLength**   This limit specifies the maximum number of text characters that can be used in the subject line. The value is 255.
    
      - **MSize**   This limit specifies the maximum message size. The value is 2147483647 bytes.
    
      - **MaxMimeRecipients**   This limit specifies the total number of recipients allowed in the To, Cc, and Bcc fields. The value is 12288.
    
      - **MaxRecipientPropertyLength**   This limit specifies the maximum number of text characters that can be used in a recipient description. The value is 1000.
    
      - **MaxBodyPartsTotal**   This limit specifies the maximum number of message parts that can be used in a MIME multipart message. The value is 250.
    
      - **MaxEmbeddedMessageDepth**   This limit specifies the maximum number of forwarded messages that can exist in a message. The value is 30.
    
    For more information about configurable message size limits used in the Transport service on Mailbox servers or on Edge Transport servers, see [Message size limits](message-size-limits-exchange-2013-help.md).

  - **Failure to convert an inbound iCalendar message to a meeting request**   RFC 2445 defines iCalendar as a standard for calendar data exchange. Specific causes of the conversion failure include the following:
    
      - Incorrect use of iCalendar by the sending agent.
    
      - Constructs of iCalendar that can't be supported by the Outlook or Exchange calendar schema.
    
    Conversion failures of iCalendar don't result in the sender receiving a 5.6.0 DSN message. Instead, the message is delivered with an attached .ics file that contains the iCalendar message body.

  - **Failures caused by badly formatted MIME messages**   Unsolicited commercial email or spam messages may have formatting errors in the message header, such as unmatched quotation marks in recipient descriptions. A much smaller number of failures caused by badly formatted MIME messages are considered bugs.

Outbound content conversion failures are much less common than inbound failures. When outbound failures occur, they are usually caused by Exchange code bugs or corrupted message content.

Return to top

