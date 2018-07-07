---
title: 'Import address rewrite entries on Edge Transport servers: Exchange 2013 Help'
TOCTitle: Import address rewrite entries on Edge Transport servers
ms:assetid: bd0942c6-9c66-4b4c-b9bc-2f5f783def76
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb331966(v=EXCHG.150)
ms:contentKeyID: 61200296
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Import address rewrite entries on Edge Transport servers

 

_**Applies to:** Exchange Server 2013_


You can bulk-create or import address rewriting information into an Edge Transport server by using a comma-separated value (CSV) file. The following list describes common scenarios that require you to do this:

  - You are replacing an address rewriting solution with an Edge Transport server.

  - You enter into an agreement with a third-party solution provider that requires you to rewrite their email addresses.

  - You acquire another organization, and you need to temporarily rewrite the email addresses in the acquired organization.

You can use any text editor, like Notepad, or an application like Microsoft Excel, to create the CSV file. Format the file as described in this topic and save it as a .csv file.

The first row, or *header row*, of the CSV file lists the names of the parameters. Each parameter is separated by a comma. The required and optional parameters are described in the following table.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Required or optional</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Required</p></td>
<td><p>A unique, descriptive name for the address rewrites entry.</p></td>
</tr>
<tr class="even">
<td><p><em>InternalAddress</em></p></td>
<td><p>Required</p></td>
<td><p>The address you want to change. You can use the following values:</p>
<ul>
<li><p>A single email address (chris@contoso.com)</p></li>
<li><p>A single domain or subdomain (contoso.com or sales.contoso.com)</p></li>
<li><p>A domain and all subdomains (*.contoso.com)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>ExternalAddress</em></p></td>
<td><p>Required</p></td>
<td><p>The final email address you want. You can use the following values:</p>
<ul>
<li><p>A single email address if you specified a single email address for <em>InternalAddress</em></p></li>
<li><p>A single domain or subdomain for all other values of <em>InternalAddress</em></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ExceptionList</em></p></td>
<td><p>Optional</p></td>
<td><p>Available only when you are rewriting email addresses in a domain and all subdomains (*.contoso.com). Specifies one or more subdomains you want to exclude from address rewriting. Enclose the value in double quotation marks, and separate multiple values by commas. For example, <code>&quot;marketing.contoso.com&quot;</code> or <code>&quot;marketing.contoso.com,legal.contoso.com&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundOnly</em></p></td>
<td><p>Optional</p></td>
<td><p><code>False</code> means that addresses are written on inbound and outbound mail. <code>True</code> means that addresses are rewritten on outbound mail only, and you need to manually configure the rewritten email address as a proxy address on the affected recipients.</p>
<p>The default value is <code>False</code>, but you must set it to <code>True</code> if <em>InternalAddress</em> contains the wildcard character (*.contoso.com).</p>
<p>The <em>OutboundOnly</em> parameter value in the CSV file is <code>True</code> or <code>False</code>, not <code>$True</code> or <code>$False</code>.</p></td>
</tr>
</tbody>
</table>


Each row under the header row represents an individual address rewrite entry. The values in each row must be in the same order as the parameter names in the header row. Each value is separated by a comma.

## What do you need to know before you begin?

  - Estimated time to complete this task: 30 minutes

  - Make sure you understand the ramifications of address rewriting. For example, the rewritten email address must be unique in your Exchange organization, and you might need to configure proxy addresses on the affected recipients. For more information, see [Address rewriting on Edge Transport servers](address-rewriting-on-edge-transport-servers-exchange-2013-help.md) and [Manage address rewriting on Edge Transport servers](manage-address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Address Rewriting agent" entry in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - If you have more than one Edge Transport server, we recommend that you use the procedures in this topic to import the address rewrite entries into a single Edge Transport server and then clone the configuration of that Edge Transport server to the other Edge Transport servers in your organization. For more information about how to clone an Edge Transport server, see [Edge Transport server cloned configuration](edge-transport-server-cloned-configuration-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## How do you do this?

## Step 1: Create the CSV file

When you create the CSV file, consider the following items:

  - If you specify values for optional parameters in the CSV file, every row must include a value in that column. If you want to create multiple address rewrite entries where some entries have optional parameters and some entries do not, you need to separate those address rewrite entries into two separate CSV files and then import each CSV file separately.

  - If the CSV file contains non-ASCII characters, be sure to save the CSV file with UTF-8 encoding or other Unicode encoding. Depending on the application, saving the CSV file with UTF-8 encoding or other Unicode encoding might be easier when the system locale of the computer matches the language used in the CSV file.

The following example shows how a CSV file can be populated with the optional *ExceptionList* and *OutboundOnly* parameters included:

    Name,InternalAddress,ExternalAddress,ExceptionList,OutboundOnly
    "Wingtip UK",*.wingtiptoys.co.uk,tailspintoys.com,"legal.wingtiptoys.co.uk,finance.wingtiptoys.co.uk,support.wingtiptoys.co.uk",True
    "Wingtip USA",*.wingtiptoys.com,tailspintoys.com,"legal.wingtiptoys.com,finance.wingtiptoys.com,support.wingtiptoys.com,corp.wingtiptoys.com",True
    "Wingtip Canada",*.wingtiptoys.ca,tailspintoys.com,"legal.wingtiptoys.ca,finance.wingtiptoys.ca,support.wingtiptoys.ca",True

## Step 2: Import the CSV file

To import the CSV file, use the following syntax:

    Import-Csv <FileNameAndPath> | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

This example imports the address rewrite entries from C:\\My Documents\\ImportAddressRewriteEntries.csv.

    Import-Csv "C:\My Documents\ImportAddressRewriteEntries.csv" | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

## How do you know this step worked?

To verify that you have successfully imported address rewrite entries from a CSV file, do the following:

1.  To see all address rewrite entries, run the command `Get-AddressRewriteEntry`.

2.  To see details about a specific address rewrite entry, run the command `Get-AddressRewriteEntry <AddressRewriteIdentity> | Format-List`

