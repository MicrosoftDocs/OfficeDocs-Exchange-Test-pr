---
title: 'Content conversion: Exchange 2013 Help'
TOCTitle: Content conversion
ms:assetid: bc367eb3-0306-4da9-9a84-4341caef77af
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb232174(v=EXCHG.150)
ms:contentKeyID: 49318585
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Content conversion

 

_**Applies to:** Exchange Server 2013_


*Content conversion* is the process of correctly formatting a message for each recipient. The decision to perform content conversion on a message depends on the destination and format of the message being processed. In Microsoft Exchange Server 2013, there are two different kinds of content conversion:

  - **Message conversion for external recipients**   This type of content conversion includes the Transport Neutral Encapsulation Format (TNEF) conversion options and message encoding options for external recipients. Messages sent to recipients inside the Exchange organization don't require this type of content conversion. This type of content conversion is handled by the categorizer in the Transport service on Mailbox server. Categorization on each message happens after a newly arrived message is put in the Submission queue. In addition to recipient resolution and routing resolution, content conversion is performed on the message before the message is put in a delivery queue. If a single message contains multiple recipients, the categorizer determines the appropriate encoding for each message recipient. Content conversion tracing doesn't capture any content conversion failures that the categorizer encounters as it converts messages sent to external recipients.

  - **MAPI conversion for internal recipients**   This type of content conversion is handled by the Mailbox Transport service. The Mailbox Transport service exists on Mailbox servers to transmit messages between mailbox databases on the local server, and the Transport service on Mailbox servers. Specifically, the Mailbox Transport Submission service transmits messages from the sender's Outbox to the Transport service on a Mailbox server. The Mailbox Transport Delivery service transmits messages from the Transport service on a Mailbox server to the recipient's Inbox. The Mailbox Transport Submission service converts all outgoing messages from MAPI and the Mailbox Transport Delivery service converts all incoming messages to MAPI. Content conversion tracing captures these MAPI conversion failures. For more information, see [Content conversion tracing](content-conversion-tracing-exchange-2013-help.md).

This topic explains the message conversion options for external recipients.

**Contents**

Exchange and Outlook message formats

Content conversion options for external recipients

Understanding the structure of email messages

## Exchange and Outlook message formats

The following list describes the basic message formats available in Exchange and Microsoft Outlook:

  - **Plain text**   A plain text message uses only US-ASCII text as described in RFC 2822. The message can't contain different fonts or other text formatting. The following two formats can be used for a plain text message:
    
      - The message headers and the message body are composed of US-ASCII text. Attachments must be encoded by using *Uuencode*. Uuencode represents Unix-to-Unix encoding and defines an encoding algorithm to store binary attachments in the body of an email message by using US-ASCII text characters.
    
      - The message is MIME-encoded with a Content-Type value of text/plain, and a Content-Transfer-Encoding value of 7bit for the text parts of a multipart message. Any message attachments are encoded by using Quoted-printable or Base64 encoding. By default, when you compose and send a plain text message in Outlook, the message is MIME-encoded with a Content-Type value of text/plain.

  - **HTML**   An HTML message supports text formatting, background images, tables, bullet points, and other graphical elements. By definition, an HTML-formatted message must be MIME-encoded to preserve these formatting elements.

  - **Rich text format (RTF)**   RTF supports text formatting and other graphical elements. RTF is synonymous with TNEF. TNEF and RTF can be used interchangeably. The rich text message format is completely different from the rich text document format available in Microsoft Word.
    
    Only Outlook and a few other MAPI email clients understand RTF messages.

  - **TNEF**   The Transport Neutral Encapsulation Format is a Microsoft-specific format for encapsulating MAPI message properties. A TNEF message contains a plain text version of the message and an attachment that packages the original formatted version of the message. Typically, this attachment is named Winmail.dat. The Winmail.dat attachment includes the following information:
    
      - Original formatted version of the message, including, for example, fonts, text sizes, and text colors
    
      - OLE objects, including, for example, embedded pictures or embedded Microsoft Office documents
    
      - Special Outlook features, including, for example, custom forms, voting buttons, or meeting requests
    
      - Regular message attachments that were in the original message
    
    The resulting plain text message can be represented in the following formats:
    
      - RFC 2822-compliant message composed of only US-ASCII text with a Winmail.dat attachment encoded in Uuencode
    
      - Multipart MIME-encoded message that has a Winmail.dat attachment
    
    A MAPI-compliant email client that fully understands TNEF, such as Outlook, processes the Winmail.dat attachment and displays the original message content without ever displaying the Winmail.dat attachment. An email client that doesn't understand TNEF may present a TNEF message in any of the following ways:
    
      - The plain text version of the message is displayed, and the message contains an attachment named Winmail.dat, Win.dat, or some other generic name such as Att*nnnnn*.dat or Att*nnnnn*.eml where the *nnnnn* placeholder represents a random number.
    
      - The plain text version of the message is displayed. The TNEF attachment is ignored or removed. The result is a plain text message.
    
      - Messaging servers that understand TNEF can be configured to remove TNEF attachments from incoming messages. The result is a plain text message. Moreover, some email clients such as Microsoft Outlook Express may not understand TNEF, but recognize and ignore TNEF attachments. The result is a plain text message.
    
    There are third-party utilities that can help convert Winmail.dat attachments.
    
    TNEF is understood by all versions of Exchange since Exchange Server version 5.5.

  - **Summary Transport Neutral Encapsulation Format (STNEF)**   STNEF is equivalent to TNEF. However, STNEF messages are encoded differently than TNEF messages. Specifically, STNEF messages are always MIME-encoded and always have a Content-Transfer-Encoding value of Binary. Therefore, there's no plain text representation of the message, and there's no distinct Winmail.dat attachment contained in the body of the message. The whole message is represented by using only binary data. Messages that have a Content-Transfer-Encoding value of Binary can only be transferred between SMTP messaging servers that support and advertise the BINARYMIME and CHUNKING SMTP extensions as defined in RFC 3030. The messages are always transferred between SMTP messaging by using the BDAT command, instead of the standard DATA command.
    
    STNEF is understood by all versions of Exchange since Exchange 2000. STNEF is automatically used for all messages transferred between Exchange servers in the organization since native mode Exchange Server 2003.
    
    Exchange never sends STNEF messages to external recipients. Only TNEF messages can be sent to recipients outside the Exchange organization.

Return to top

## Content conversion options for external recipients

The content conversion options that you can set in an Exchange organization for external recipients can be described in the following categories:

  - **TNEF conversion options**   These conversion options specify whether TNEF should be preserved or removed from messages that leave the Exchange organization.

  - **Message encoding options**   These options specify message encoding options, such as MIME and non-MIME character sets, message encoding, and attachment formats.

These conversion and encoding options are independent of one another. For example, whether TNEF messages can leave the Exchange organization isn't related to the MIME encoding settings or plain text encoding settings of those messages.

You can specify the content conversion at various levels of the Exchange organization as described in the following list:

  - **Remote domain settings**   Remote domains define the settings for outgoing message transfers between the Exchange organization and external domains.. Even if you don't create remote domain entries for specific domains, there's a predefined remote domain named Default that applies to all remote address spaces (\*).

  - **Mail user and mail contact settings**   Mail users and mail contacts are similar because both have external email addresses and contain information about people outside the Exchange organization. The main difference is mail users have accounts that can be used to log on to the Active Directory domain and access resources in the organization.

  - **Outlook settings**   In Outlook, you can set the message formatting and encoding options described in the following list:
    
      - **Message format**   You can set the default message format for all messages. You can override the default message format as you compose a specific message.
    
      - **Internet message format**   You can control whether TNEF messages are sent to remote recipients or whether they are first converted to a more compatible format. You can also specify various message encoding options for messages sent to remote recipients. These settings don't apply to messages sent to recipients in the Exchange organization.
    
      - **Internet recipient message format**   You can control whether TNEF messages are sent to specific recipients or whether they are first converted to a more compatible format. You can set the conversion options for specific contacts in your Contacts folder, and you can override the conversion options for a specific recipient in the To, Cc, or Bcc fields as you compose a message. These conversion options aren't available for recipients in the Exchange organization.
    
      - **Internet recipient message encoding options**   You can control the MIME or plain text encoding options for specific contacts in your Contacts folder, and you can override the conversion options for a specific recipient in the To, Cc, or Bcc fields as you compose a message. These conversion options aren't available for recipients in the Exchange organization.
    
      - **International options**   You can control the character sets used in messages.

## TNEF conversion options

You can specify the TNEF conversion options at the following levels:

  - Remote domain settings

  - Mail user and mail contact settings

  - Outlook settings, including:
    
      - Message format
    
      - Internet message format
    
      - Internet recipient message format

## Message encoding options

You can specify the message encoding options at the following levels:

  - Remote domain settings

  - Mail user and mail contact settings

  - Outlook settings, including:
    
      - Message format
    
      - Internet message
    
      - Internet recipient message format
    
      - Message character set encoding options

For detailed information, see [Message encoding options](message-encoding-options-exchange-2013-help.md).

Return to top

## Understanding the structure of email messages

To better understand the content conversion options for external recipients, you need to understand the structure of email messages. An SMTP message is based on plain 7-bit US-ASCII text to compose and send email messages. A standard SMTP message consists of the following elements:

  - **Message envelope**   The message envelope is defined in RFC 2821. The message envelope contains information required to transmit and deliver the message. Recipients never see the message envelope, because it's generated by the message transmission process and isn't actually part of the message contents.

  - **Message contents**   The message contents are defined in RFC 2822. The message contents consist of the following elements:
    
      - **Message header**   The message header is a collection of header fields. Header fields consist of a field name, followed by a colon (:) character, followed by a field body, and ended by a carriage return/line feed (CR/LF) character combination.
        
        A field name must be composed of printable US-ASCII text characters except the colon (:) character. Specifically, ASCII characters that have values from 33 through 57 and 59 through 126 are permitted.
        
        A field body may be composed of any US-ASCII characters, except for the carriage return (CR) character and the line feed (LF) character. However, a field body may contain the CR/LF character combination when used in *header folding*. Header folding is the separation of a single header field body into multiple lines as described in section 2.2.3 of RFC 2822. Other field body syntax requirements are described in sections 3 and 4 of RFC 2822.
    
      - **Message body**   The message body is a collection of lines of US-ASCII text characters that appears after the message header. The message header and the message body are separated by a blank line that ends with the CR/LF character combination. The message body is optional. Any line of text in the message body must be less than 998 characters. The CR and LF characters can only appear together to indicate the end of a line.

When SMTP messages contain elements that aren't plain US-ASCII text, the message must be encoded to preserve those elements. The MIME standard defines a method of encoding content in messages that isn't text. MIME allows for text in other character sets, attachments without text, multipart message bodies, and header fields in other character sets. MIME is defined in RFC 2045, RFC 2046, RFC 2047, RFC 2048, and RFC 2077. MIME defines a collection of header fields that specifies additional message attributes. The following table describes some important MIME header fields.

### Important MIME header fields

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Header field name</th>
<th>Default value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MIME-Version</p></td>
<td><p>1.0</p></td>
<td><p>This header field is the first MIME header field that appears in a MIME-formatted message. This header field appears after the other standard RFC 2822 header fields, but before any other MIME header fields. MIME-aware email clients use this header field to identify a MIME-encoded message. When this header field is absent, MIME-aware email clients identify the message as plain text.</p></td>
</tr>
<tr class="even">
<td><p>Content-Type</p></td>
<td><p>text/plain</p></td>
<td><p>This header field identifies the media type of the message content as described in RFC 2046. A media type consists of a type, a subtype, and one or more optional parameters, such as a <em>charset=</em> parameter that defines the MIME character encoding. Types that begin with &quot;x-&quot; aren't standard. Subtypes that begin with &quot;vnd.&quot; are vendor-specific. The Internet Assigned Numbers Authority (IANA) maintains a list of registered media types. For more information, see <a href="https://www.iana.org/assignments/media-types/">MIME Media Types</a>.</p>
<p>The <em>multipart</em> media type allows for multiple message parts in the same message by using sections defined by different media types. Some Content-Type field values include text/plain, text/html, multipart/mixed, and multipart/alternative.</p></td>
</tr>
<tr class="odd">
<td><p>Content-Transfer-Encoding</p></td>
<td><p>7bit</p></td>
<td><p>This header field can describe the following information about a message:</p>
<ul>
<li><p>The encoding algorithm used to transform any non-US-ASCII text or binary data that exists in the message body.</p></li>
<li><p>An indicator that describes the current condition of the message body.</p></li>
</ul>
<p>There can be multiple values of the Content-Transfer-Encoding header field in a MIME message. When the Content-Transfer-Encoding header field appears in the message header, it applies to the whole body of the message. When the Content-Transfer-Encoding header field appears in one of the parts of a multipart message, it applies only to that part of the message.</p>
<p>When an encoding algorithm is applied to the message body data, the message body data is transformed into plain US-ASCII text. This transformation allows the message to travel through older SMTP messaging servers that only support messages in US-ASCII text. The values of the Content-Transfer-Encoding header field that indicate an encoding algorithm was used on the message body are as follows:</p>
<ul>
<li><p><strong>Quoted-printable</strong>   This encoding algorithm uses printable US-ASCII characters to encode the message body data. If the original message text is mostly US-ASCII text, Quoted-printable encoding gives somewhat readable and compact results. All printable US-ASCII text characters except the equal sign (=) character can be represented without encoding.</p></li>
<li><p><strong>Base64</strong>   This encoding algorithm is based primarily on the privacy-enhanced mail (PEM) standard defined in RFC 1421. Base64 encoding uses the 64-character alphabet encoding algorithm and output padding characters defined by PEM to encode the message body data. A Base64 encoded message is typically 33 percent larger than the original message. Base64 encoding creates a predictable increase in message size and is optimal for binary data and non-US-ASCII text.</p></li>
</ul>
<p>Typically, you won't see multiple encoding algorithms used in the same message.</p>
<p>When no encoding algorithm has been used on the message body, the Content-Transfer-Encoding header field merely identifies the current condition of the message body data. The following values of the Content-Transfer-Encoding header field indicate that no encoding algorithms were used on the message body:</p>
<ul>
<li><p><strong>7bit</strong>   This value indicates that the message body data is already in the RFC 2822 format. Specifically, this means that the following conditions must be true:</p>
<ul>
<li><p>All lines of text must be less than 998 characters long.</p></li>
<li><p>All characters must be US-ASCII text that have character values from 1 through 127.</p></li>
<li><p>The CR and LF characters can only be used together to indicate the end of a line of text.</p></li>
</ul>
<p>The whole message body may be 7bit, or part of the message body in a multipart message may be 7bit. If the multipart message contains other parts that have any binary data or non-US-ASCII text, that part of the message must be encoded using the Quoted-printable or Base64 encoding algorithms.</p>
<p>Messages that have 7bit bodies can travel between SMTP messaging servers by using the standard DATA command.</p></li>
<li><p><strong>8bit</strong>   This value indicates that the message body data contains non-US-ASCII characters. Specifically, this means that the following conditions must be true:</p>
<ul>
<li><p>All lines of text must be less than 998 characters long.</p></li>
<li><p>One or more characters in the message body have values larger than 127.</p></li>
<li><p>The CR and LF characters can only be used together to indicate the end of a line of text.</p></li>
</ul>
<p>The whole message body may be 8bit, or part of the message body in a multipart message may be 8bit. If the multipart message contains other parts that have binary data, that part of the message must be encoded using the Quoted-printable or Base64 encoding algorithms.</p>
<p>Messages that have 8bit bodies can only travel between SMTP messaging servers that support the 8BITMIME SMTP extension as defined in RFC 1652, such as servers running Exchange 2000 Server or newer versions. Specifically, this means that the following conditions must be true:</p>
<ul>
<li><p>The 8BITMIME keyword must be advertised in the server's EHLO response.</p></li>
<li><p>Messages are still transferred by using the SMTP standard DATA command. However, the BODY=8BITMIME parameter must be added to the end of the MAIL FROM command.</p></li>
</ul></li>
<li><p><strong>Binary</strong>   This value indicates that the message body contains non-US-ASCII text or binary data. Specifically, this means that the following conditions are true:</p>
<ul>
<li><p>Any sequence of characters is allowed.</p></li>
<li><p>There is no line length limitation.</p></li>
<li><p>Binary message elements don't require encoding.</p></li>
</ul>
<p>Messages that have Binary bodies can only travel between SMTP messaging servers that support the BINARYMIME SMTP extension as defined in RFC 3030, such as servers running Exchange 2000 Server or newer versions. Specifically, this means that the following conditions must be true:</p>
<ul>
<li><p>The BINARYMIME keyword must be advertised in the server's EHLO response.</p></li>
<li><p>The BINARYMIME SMTP extension can only be used with the CHUNKING SMTP extension. <em>Chunking</em> enables large message bodies to be sent in multiple, smaller chunks. Chunking is also defined in RFC 3030. The CHUNKING keyword must also be advertised in the server's EHLO response.</p></li>
<li><p>Messages are transferred using the BDAT command instead of the standard DATA command.</p></li>
<li><p>The <em>BODY=BINARYMIME</em> parameter must be added to the end of the MAIL FROM command when the message has a message body.</p></li>
</ul></li>
</ul>
<p>The values 7bit, 8bit, and Binary never exist together in the same multipart message. The values are mutually exclusive. The Quoted-printable or Base64 values may appear in a 7bit or 8bit multipart message body, but never in a Binary message body. If a multipart message body contains different parts composed of 7bit and 8bit content, the whole message is classified as 8bit. If a multipart message body contains different parts composed of 7bit, 8bit, and Binary content, the whole message is classified as Binary.</p></td>
</tr>
<tr class="even">
<td><p>Content-Disposition</p></td>
<td><p>Attachment</p></td>
<td><p>This header field instructs a MIME-enabled email client on how it should display an attached file, and is described in RFC 2183. The values of this field may be Inline or Attachment. When the value of this field is Inline, the attachment is displayed in the message body. When the value of this field is Attachment, the attached file appears as a regular attachment separate from the message body. Other parameters are available when the value is Attachment, such as Filename, Creation-date, and Size.</p></td>
</tr>
</tbody>
</table>


Return to top

