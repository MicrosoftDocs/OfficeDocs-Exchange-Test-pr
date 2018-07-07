---
title: 'Use mail flow rules to route email based on a list of words, phrases, or patterns: Exchange 2013 Help'
TOCTitle: Use mail flow rules to route email based on a list of words, phrases, or patterns
ms:assetid: 4c5bee1b-58b5-4152-baef-86fa103050ae
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn951131(v=EXCHG.150)
ms:contentKeyID: 65236533
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Use mail flow rules to route email based on a list of words, phrases, or patterns

 

_**Applies to:** Exchange Online, Exchange Online Protection, Exchange Server 2013_


To help your users comply with your organization's email policies, you can use Exchange transport rules to determine how email containing specific words or patterns is routed. For a short list of words or phrases, you can use the Exchange admin center. For a longer list, you might want to use the Exchange Module for Windows PowerShell to read the list from a text file.

  - Example 1: Use a short list of unacceptable words

  - Example 2: Use a long list of unacceptable words

If your organization uses Data Loss Prevention (DLP), see [Data loss prevention](technical-overview-of-dlp-data-loss-prevention-in-exchange.md) for additional options for identifying and routing email that contains sensitive information.

## Example 1: Use a short list of unacceptable words

If your list of words or phrases is short, you can create a rule using the Exchange admin center. For example, if you want to make sure no one sends email with bad words or with misspellings of your company name, internal acronyms or product names, you could create a rule to block the message and tell the sender. Note that words, phrases, and patterns are not case sensitive.

This example blocks messages with common typos.

![Rule showing blocking a message based on text patterns](images/Dn951131.a8489cbb-be59-4890-ae30-1431703eeb88(EXCHG.150).png "Rule showing blocking a message based on text patterns")

## Example 2: Use a long list of unacceptable words

If your list of words, phrases, or patterns is long, you can put them in a text file with each word, phrase, or pattern on its own line. Use the Exchange Module for Windows PowerShell to read in the list of keywords into a variable, create a transport rule, and assign the variable with the keywords to the transport rule condition. For example, the following script takes a list of misspellings from a file called misspelled\_companyname.txt.

    $keywords=Import-Content  .\misspelled_companyname.txt
    New-TransportRule -Name "Block messages with unacceptable words" -SubjectOrBodyContainsWords $keywords -SentToScope "NotInOrganization" -RejectMessageReasonText "Do not use internal acronyms, product names, or misspellings in external communications."

## Using phrases and patterns in the text file

The text file can contain regular expressions for patterns. These expressions are not case-sensitive. Common regular expressions include:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Expression</strong></p></td>
<td><p><strong>Matches</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>.</strong></p></td>
<td><p>Any single character</p></td>
</tr>
<tr class="odd">
<td><p><strong>*</strong></p></td>
<td><p>Any additional characters</p></td>
</tr>
<tr class="even">
<td><p><strong>\d</strong></p></td>
<td><p>Any decimal digit</p></td>
</tr>
<tr class="odd">
<td><p>[<em>character_group</em>]</p></td>
<td><p>Any single character in <em>character_group</em>.</p></td>
</tr>
</tbody>
</table>


For example, this text file contains common misspellings of Microsoft.

    [mn]sft
    [mn]icrosft
    [mn]icro soft
    [mn].crosoft

To learn how to specify patterns using regular expressions, see [Regular Expression Reference](https://go.microsoft.com/fwlink/p/?linkid=532394).

