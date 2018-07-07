---
title: 'Message properties and search operators for In-Place eDiscovery: Exchange 2013 Help'
TOCTitle: Message properties and search operators for In-Place eDiscovery
ms:assetid: 402b74e4-8853-4c51-9737-1a9c19f8e3dd
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn774955(v=EXCHG.150)
ms:contentKeyID: 62617673
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Message properties and search operators for In-Place eDiscovery

 

_**Applies to:** Exchange Online, Exchange Server 2013_


This topic describes the properties of Exchange email messages that you can search by using In-Place eDiscovery & Hold in Exchange Server 2013 and Exchange Online. The topic also describes Boolean search operators and other search query techniques that you can use to refine eDiscovery search results.

In-Place eDiscovery uses Keyword Query Language (KQL). For more details, see [Keyword Query Language syntax reference](https://go.microsoft.com/fwlink/?linkid=269603).

## Searchable properties in Exchange

The following table lists email message properties that can be searched using an In-Place eDiscovery search or by using the **New-MailboxSearch** or the **Set-MailboxSearch** cmdlet. The table includes an example of the *property:value* syntax for each property and a description of the search results returned by the examples.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>Property description</th>
<th>Examples</th>
<th>Search results returned by the examples</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Attachment</p></td>
<td><p>The names of files attached to an email message.</p></td>
<td><p>attachment:annualreport.ppt</p>
<p>attachment:annual*</p></td>
<td><p>Messages that have an attached file named annualreport.ppt.</p>
<p>In the second example, using the wildcard returns messages with the word &quot;annual&quot; in the file name of an attachment.</p></td>
</tr>
<tr class="even">
<td><p>Bcc</p></td>
<td><p>The BCC field of an email message.1</p></td>
<td><p>bcc:pilarp@contoso.com</p>
<p>bcc:pilarp</p>
<p>bcc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>All examples return messages with Pilar Pinilla included in the Bcc field.</p></td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>The categories to search. Categories can be defined by users by using Outlook or Outlook Web App. The possible values are:</p>
<ul>
<li><p>blue</p></li>
<li><p>green</p></li>
<li><p>orange</p></li>
<li><p>purple</p></li>
<li><p>red</p></li>
<li><p>yellow</p></li>
</ul></td>
<td><p>category:&quot;Red Category&quot;</p></td>
<td><p>Messages that have been assigned the red category in the source mailboxes.</p></td>
</tr>
<tr class="even">
<td><p>Cc</p></td>
<td><p>The CC field of an email message.1</p></td>
<td><p>cc:pilarp@contoso.com</p>
<p>cc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>In both examples, messages with Pilar Pinilla specified in the CC field.</p></td>
</tr>
<tr class="odd">
<td><p>From</p></td>
<td><p>The sender of an email message.1</p></td>
<td><p>from:pilarp@contoso.com</p>
<p>from:contoso.com</p></td>
<td><p>Messages sent by the specified user or sent from a specified domain.</p></td>
</tr>
<tr class="even">
<td><p>Importance</p></td>
<td><p>The importance of an email message, which a sender can specify when sending a message. By default, messages are sent with normal importance, unless the sender sets the importance as <strong>high</strong> or <strong>low</strong>.</p></td>
<td><p>importance:high</p>
<p>importance:medium</p>
<p>importance:low</p></td>
<td><p>Messages that are marked as high importance, medium importance, or low importance.</p></td>
</tr>
<tr class="odd">
<td><p>Kind</p></td>
<td><p>The message type to search. Possible values:</p>
<ul>
<li><p>contacts</p></li>
<li><p>docs</p></li>
<li><p>email</p></li>
<li><p>faxes</p></li>
<li><p>im</p></li>
<li><p>journals</p></li>
<li><p>meetings</p></li>
<li><p>notes</p></li>
<li><p>posts</p></li>
<li><p>rssfeeds</p></li>
<li><p>tasks</p></li>
<li><p>voicemail</p></li>
</ul></td>
<td><p>kind:email</p>
<p>kind:email OR kind:im OR kind:voicemail</p></td>
<td><p>Email messages that meet the search criteria. The second example returns email messages, instant messaging conversations, and voice messages that meet the search criteria.</p></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>All the people fields in an email message; these fields are From, To, CC, and BCC.1</p></td>
<td><p>participants:garthf@contoso.com</p>
<p>participants:contoso.com</p></td>
<td><p>Messages sent by or sent to garthf@contoso.com.</p>
<p>The second example returns all messages sent by or sent to a user in the contoso.com domain.</p></td>
</tr>
<tr class="odd">
<td><p>Received</p></td>
<td><p>The date that an email message was received by a recipient.</p></td>
<td><p>received:04/15/2014</p>
<p>received&gt;=01/01/2014 AND received&lt;=03/31/2014</p></td>
<td><p>Messages that were received on April 15, 2014. The second example returns all messages received between January 1, 2014 and March 31, 2014.</p></td>
</tr>
<tr class="even">
<td><p>Recipients</p></td>
<td><p>All recipient fields in an email message; these fields are To, CC, and BCC.1</p></td>
<td><p>recipients:garthf@contoso.com</p>
<p>recipients:contoso.com</p></td>
<td><p>Messages sent to garthf@contoso.com.</p>
<p>The second example returns messages sent to any recipient in the contoso.com domain.</p></td>
</tr>
<tr class="odd">
<td><p>Sent</p></td>
<td><p>The date that an email message was sent by the sender.</p></td>
<td><p>sent:07/01/2014</p>
<p>sent&gt;=06/01/2014 AND sent&lt;=07/01/2014</p></td>
<td><p>Messages that were sent on the specified date or sent within the specified date range.</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>The size of an item, in bytes.</p></td>
<td><p>size&gt;26214400</p>
<p>size:1..1048576</p></td>
<td><p>Messages larger than 25 MB.</p>
<p>The second example returns messages from 1 through 1,048,576 bytes (1 MB) in size.</p></td>
</tr>
<tr class="odd">
<td><p>Subject</p></td>
<td><p>The text in the subject line of an email message.</p></td>
<td><p>subject:&quot;Quarterly Financials&quot;</p>
<p>subject:northwind</p></td>
<td><p>Messages that contain the exact phrase &quot;Quarterly Financials&quot; anywhere in the text of the subject line.</p>
<p>The second example returns all messages that contain the word northwind in the subject line.</p></td>
</tr>
<tr class="even">
<td><p>To</p></td>
<td><p>The To field of an email message.1</p></td>
<td><p>to:annb@contoso.com</p>
<p>to:annb</p>
<p>to:&quot;Ann Beebe&quot;</p></td>
<td><p>All examples return messages where Ann Beebe is specified in the To: line.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1&nbsp;&nbsp;&nbsp;For the value of a recipient property, you can use the SMTP address, display name, or alias to specify a user. For example, you can use annb@contoso.com, annb, or "Ann Beebe" to specify the user Ann Beebe.



## Supported search operators

Boolean search operators, such as **AND**, **OR**, help you define more-precise mailbox searches by including or excluding specific words in the search query. Other techniques, such as using property operators (such as \>= or ..), quotation marks, parentheses, and wildcards, help you refine eDiscovery search queries. The following table lists the operators that you can use to narrow or broaden search results.


> [!IMPORTANT]
> You must use uppercase Boolean operators in a search query. For example, use <STRONG>AND</STRONG>; don't use <STRONG>and</STRONG>. Using lowercase operators in search queries will return an error.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Operator</th>
<th>Usage</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AND</p></td>
<td><p>keyword1 AND keyword2</p></td>
<td><p>Returns messages that include all of the specified keywords or <code>property:value</code> expressions.</p></td>
</tr>
<tr class="even">
<td><p>+</p></td>
<td><p>keyword1 +keyword2 +keyword3</p></td>
<td><p>Returns items that contain <em>either</em> <code>keyword2 </code>or <code>keyword3 </code><em>and</em> that also contain <code>keyword1</code>. Therefore, this example is equivalent to the query <code>(keyword2 OR keyword3) AND keyword1</code>.</p>
<p>Note that the query <code>keyword1 + keyword2</code> (with a space after the <strong>+</strong> symbol) isn't the same as using the <strong>AND</strong> operator. This query would be equivalent to <code>&quot;keyword1 + keyword2&quot;</code> and return items with the exact phase <code>&quot;keyword1 + keyword2&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p>OR</p></td>
<td><p>keyword1 OR keyword2</p></td>
<td><p>Returns messages that include one or more of the specified keywords or <code>property:value</code> expressions.</p></td>
</tr>
<tr class="even">
<td><p>NOT</p></td>
<td><p>keyword1 NOT keyword2</p>
<p>NOT from:&quot;Ann Beebe&quot;</p></td>
<td><p>Excludes messages specified by a keyword or a <code>property:value</code> expression. For example, <code>NOT from:&quot;Ann Beebe&quot;</code> excludes messages sent by Ann Beebe.</p></td>
</tr>
<tr class="odd">
<td><p>-</p></td>
<td><p>keyword1 -keyword2</p></td>
<td><p>The same as the <strong>NOT</strong> operator. This query returns items that contain <code>keyword1</code> and excludes items that contain <code>keyword2</code>.</p></td>
</tr>
<tr class="even">
<td><p>NEAR</p></td>
<td><p>keyword1 NEAR(n) keyword2</p></td>
<td><p>Returns messages with words that are near each other, where n equals the number of words apart. For example, <code>best NEAR(5) worst</code> returns messages where the word &quot;worst&quot; is within five words of &quot;best&quot;. If no number is specified, the default distance is eight words.</p></td>
</tr>
<tr class="odd">
<td><p>:</p></td>
<td><p>property:value</p></td>
<td><p>The colon (:) in the <code>property:value</code> syntax specifies that the property value being searched for equals the specified value. For example, <code>recipients:garthf@contoso.com</code> returns any message sent to garthf@contoso.com.</p></td>
</tr>
<tr class="even">
<td><p>&lt;</p></td>
<td><p>property&lt;value</p></td>
<td><p>Denotes that the property being searched is less than the specified value. 1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;</p></td>
<td><p>property&gt;value</p></td>
<td><p>Denotes that the property being searched is greater than the specified value.1</p></td>
</tr>
<tr class="even">
<td><p>&lt;=</p></td>
<td><p>property&lt;=value</p></td>
<td><p>Denotes that the property being searched is less than or equal to a specific value.1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;=</p></td>
<td><p>property&gt;=value</p></td>
<td><p>Denotes that the property being searched is greater than or equal to a specific value.1</p></td>
</tr>
<tr class="even">
<td><p>..</p></td>
<td><p>property:value1..value2</p></td>
<td><p>Denotes that the property being searched is greater than or equal to value1 and less than or equal to value2.1</p></td>
</tr>
<tr class="odd">
<td><p>&quot; &quot;</p></td>
<td><p>&quot;fair value&quot;</p>
<p>subject:&quot;Quarterly Financials&quot;</p></td>
<td><p>Use double quotation marks (&quot; &quot;) to search for an exact phrase or term in keyword and <code>property:value</code> search queries.</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>cat*</p>
<p>subject:set*</p></td>
<td><p>Prefix wildcard searches (where the asterisk is placed at the end of a word) match for zero or more characters in keywords or <code>property:value</code> queries. For example, <code>subject:set*</code> returns messages that contain the word set, setup, and setting (and other words that start with &quot;set&quot;) in the subject line.</p></td>
</tr>
<tr class="odd">
<td><p>( )</p></td>
<td><p>(fair OR free) AND from:contoso.com</p>
<p>(IPO OR initial) AND (stock OR shares)</p>
<p>(quarterly financials)</p></td>
<td><p>Parentheses group together Boolean phrases, <code>property:value</code> items, and keywords. For example, <code>(quarterly financials)</code> returns items that contain the words quarterly and financials.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1&nbsp;&nbsp;&nbsp;Use this operator for properties that have date or numeric values.



## Unsupported characters in search queries

Unsupported characters in a search query typically cause a search error or return unintended results. Unsupported characters are often hidden and they're typically added to a query when you copy the query or parts of the query from other applications (such as Microsoft Word or Microsoft Excel) and copy them to the keyword box on the query page of In-Place eDiscovery search.

Here's a list of the unsupported characters for an In-Place eDiscovery search query.

  - **Smart quotation marks**   Smart single and double quotation marks (also called *curly quotes*) aren't supported. Only straight quotation marks can be used in a search query.

  - **Non-printable and control characters**   Non-printable and control characters don't represent a written symbol, such as a alpha-numeric character. Examples of non-printable and control characters include characters that format text or separate lines of text.

  - **Left-to-right and right-to-left marks**   These are control characters used to indicate text direction for left-to-right languages (such as English and Spanish) and right-to-left languages (such as Arabic and Hebrew).

  - **Lowercase Boolean operators**   As previous explained, you have to use uppercase Boolean operators, such as **AND** and **OR**, in a search query. Note that the query syntax will often indicate that a Boolean operator is being used even though lowercase operators might be used; for example, `(WordA or WordB) and (WordC or WordD)`.

**How to prevent unsupported characters in your search queries?**The best way to prevent unsupported characters is to just type the query in the keyword box. Alternatively, you can copy a query from Word or Excel and then paste it to file in a plain text editor, such as Microsoft Notepad. Then save the text file and select **ANSI** in the **Encoding** drop-down list. This will remove any formatting and unsupported characters. Then you can copy and paste the query from the text file to the keyword query box.

## Search tips and tricks

  - Keyword searches are not case sensitive. For example, **cat** and **CAT** return the same results.

  - A space between two keywords or two `property:value` expressions is the same as using **AND**. For example, `from:"Sara Davis" subject:reorganization` returns all messages sent by Sara Davis that contain the word **reorganization** in the subject line.

  - Use syntax that matches the `property:value` format. Values are not case-sensitive, and they can’t have a space after the operator. If there is a space, your intended value will just be full-text searched. For example **to: pilarp** searches for "pilarp" as a keyword, rather than for messages that were sent to pilarp.

  - When searching a recipient property, such as To, From, Cc, or Recipients, you can use an SMTP address, alias, or display name to denote a recipient. For example, you can use pilarp@contoso.com, pilarp, or "Pilar Pinilla".

  - You can use only prefix wildcard searches—for example, **cat\*** or **set\***. Suffix wildcard searches (\*cat) or substring wildcard searches (\*cat\*) aren’t supported.

  - When searching a property, use double quotation marks (" ") if the search value consists of multiple words. For example **subject:budget Q1** returns messages that contain **budget** in the in the subject line and that contain **Q1** anywhere in the message or in any of the message properties. Using **subject:"budget Q1"** returns all messages that contain **budget Q1** anywhere in the subject line.

