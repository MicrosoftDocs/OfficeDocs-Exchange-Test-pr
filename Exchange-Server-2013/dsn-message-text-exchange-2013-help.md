---
title: 'DSN message text: Exchange 2013 Help'
TOCTitle: DSN message text
ms:assetid: eae4a050-5ecb-4c87-b377-74edb93a5995
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb125135(v=EXCHG.150)
ms:contentKeyID: 49286855
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# DSN message text

 

_**Applies to:** Exchange Server 2013_


You can include text in a customized delivery status notification (DSN) message in Microsoft Exchange Server 2013, and you can format that text in HTML.

You can include any information that you want to display to the recipient of the DSN message. For example, you can include a detailed description of the DSN, contact information for your help desk, and a link to your support department's Web site. Each DSN message can contain a maximum of 512 characters.

Because DSN messages can be displayed in HTML, you can embed HTML formatting tags in the DSN text. For example, if you want to make some text in your DSN message bold, enclose the text in \<B\> and \</B\> HTML tags. The following table provides some examples of valid HTML tags that can be used in DSN message text.

### Valid HTML tags for use in DSN messages

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>HTML tag</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt;B&gt;</p></td>
<td><p>Bold begin</p></td>
</tr>
<tr class="even">
<td><p>&lt;/B&gt;</p></td>
<td><p>Bold end</p></td>
</tr>
<tr class="odd">
<td><p>&lt;A HREF=&quot;url&quot;&gt;</p></td>
<td><p>Hyperlink begin</p></td>
</tr>
<tr class="even">
<td><p>&lt;/A&gt;</p></td>
<td><p>Hyperlink end</p></td>
</tr>
<tr class="odd">
<td><p>&lt;BR&gt;</p></td>
<td><p>Link break</p></td>
</tr>
<tr class="even">
<td><p>&lt;EM&gt;</p></td>
<td><p>Italic begin</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/EM&gt;</p></td>
<td><p>Italic end</p></td>
</tr>
<tr class="even">
<td><p>&lt;P&gt;</p></td>
<td><p>Paragraph begin</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/P&gt;</p></td>
<td><p>Paragraph end</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> By default, Exchange sends HTML DSN messages, but you can configure whether Exchange sends HTML DSN messages to internal senders, external senders, or both. To configure this behavior, modify the <EM>InternalDsnSendHtml</EM> parameter and the <EM>ExternalDsnSendHtml</EM> parameter with the <STRONG>Set-TransportService</STRONG> command.<BR>If the <EM>InternalDsnSendHtml</EM> parameter is set to <CODE>$false</CODE>, Exchange suppresses HTML tags in DSN messages sent to internal senders. If the <EM>ExternalDsnSendHtml</EM> parameter is set to <CODE>$false</CODE>, Exchange suppresses HTML tags in DSN messages sent to external senders.



The following characters that Exchange uses in DSN message text have special meanings:

  - Greater than sign (\>)

  - Less than sign (\<)

  - Ampersand (&)

  - Quotation marks (")

These characters are used to determine where HTML tags begin and end, and where text that should be displayed to senders starts and stops. If you want to display these characters in your DSN messages, you must use the escape codes in the following table.

For example, if you want to display the message `"Please contact the Help Desk at <1234>."`, you must add `"Please contact the Help Desk at &lt;1234&gt;." `to the DSN message text.

### DSN message character escape codes

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Escape code</th>
<th>Character</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&amp;lt;</p></td>
<td><p>&lt;</p></td>
</tr>
<tr class="even">
<td><p>&amp;gt;</p></td>
<td><p>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;</p></td>
<td><p>&quot;</p></td>
</tr>
<tr class="even">
<td><p>&amp;amp;</p></td>
<td><p>&amp;</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> If you include an HTML tag in your DSN message text that contains quotation marks ("), such as <CODE>&lt;A HREF="url"&gt;</CODE>, you must use single quotation marks (') around the whole DSN message text. You will receive an error message if you use double quotation marks around the whole DSN message text and around an HTML tag.


