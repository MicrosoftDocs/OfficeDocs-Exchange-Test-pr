---
title: 'Manage address rewriting on Edge Transport servers: Exchange 2013 Help'
TOCTitle: Manage address rewriting on Edge Transport servers
ms:assetid: 323a0b55-f921-425d-b1b0-18ad0fac315c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa997185(v=EXCHG.150)
ms:contentKeyID: 61200282
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Manage address rewriting on Edge Transport servers

 

_**Applies to:** Exchange Server 2013_


You use the Exchange Management Shell on an Edge Transport server for all management tasks related to address rewriting and the address rewriting agents. For more information about address rewriting, see [Address rewriting on Edge Transport servers](address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

You can create address rewrite entries that apply to a single recipient, to all recipients in a specific domain or subdomain, or all recipients in multiple subdomains. Address rewriting can be outbound only, or inbound and outbound (bidirectional). When you create address rewrite entries, remember the following:

  - Verify that the resulting email addresses are unique in your organization.

  - Only literal strings are supported in the email address values.

  - The wildcard character (\*) is supported only in the internal address (the addresses you want to change). Valid syntax for using the wildcard character is **\*.contoso.com**. The values **\*contoso.com** or **sales.\*.com** are not allowed.

  - When you use the wildcard character, you need to configure the address rewriting as outbound only (you need to set the *OutboundOnly* parameter to the value `$true`).

  - When you configure outbound-only address rewriting (by setting the *OutboundOnly* parameter to the value `$true`), you need to configure proxy addresses on the affected recipients. This allows mail that is sent to the rewritten address to be delivered correctly.

  - By default, address rewriting is bidirectional for single recipients or all recipients in a specific domain or subdomain (the default value for the *OutboundOnly* parameter is `$false`).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 10 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Edge Transport servers" section in the [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md) topic.

  - You can only use the Shell to perform this procedure.

  - Be careful when you configure address rewriting. Any changes that you make are immediately applied when you run the command. Consider running the command with the *WhatIf* parameter. For more information about the *WhatIf* parameter, see [WhatIf, Confirm, and ValidateOnly switches](whatif-confirm-and-validateonly-switches-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to enable or disable address rewriting

To completely enable or disable address rewriting, you enable or disable the address rewriting agents. By default, the address rewriting agents on an Edge Transport server are enabled.

To disable address rewriting, run the following commands:

    Disable-TransportAgent "Address Rewriting Inbound Agent"
    Disable-TransportAgent "Address Rewriting Outbound Agent"

To enable address rewriting, run the following commands:

    Enable-TransportAgent "Address Rewriting Inbound Agent"
    Enable-TransportAgent "Address Rewriting Outbound Agent"

## How do you know this worked?

To verify that you have successfully enabled or disabled address rewriting, do the following:

1.  Run the following command:
    
        Get-TransportAgent

2.  Verify the values of the **Enabled** property for the Address Rewriting Inbound Agent and the Address Rewriting Outbound Agent are the values you configured.

## Use the Shell to view address rewrite entries

To view a summary list of all address rewrite entries, run the following command.

    Get-AddressRewriteEntry

To view details of an address rewrite entry, use the following syntax.

    Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List

The following example displays the details of the address rewrite entry named Rewrite Contoso.com to Northwindtraders.com:

    Get-AddressRewriteEntry "Rewrite Contoso.com to Northwindtraders.com" | Format-List

## Use the Shell to create address rewrite entries

## Rewrite the email addresses of single recipients

To rewrite the email address for a single recipient, use the following syntax:

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> [-OutboundOnly <$true | $false>]

The following example rewrites the email address of all messages entering and leaving the Exchange organization for the recipient joe@contoso.com. Outbound messages are rewritten so they appear to come from support@nortwindtraders.com. Inbound messages sent to support@northwindtraders.com are rewritten to joe@contoso.com for delivery to the recipient (the *OutboundOnly* parameter is `$false` by default).

    New-AddressRewriteEntry -Name "joe@contoso.com to support@northwindtraders.com" -InternalAddress joe@contoso.com -ExternalAddress support@northwindtraders.com

## Rewrite email addresses for recipients in a single domain or subdomain

To rewrite the email addresses for recipients in a single domain or subdomain, use the following syntax:

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> [-OutboundOnly <$true | $false>]

The following example rewrites the email addresses of all messages entering and leaving the Exchange organization for recipients in the contoso.com domain. Outbound messages are rewritten so they appear to come from the fabrikam.com domain. Inbound messages sent to fabrikam.com email addresses are rewritten to contoso.com for delivery to the recipients (the *OutboundOnly* parameter is `$false` by default).

    New-AddressRewriteEntry -Name "Contoso to Fabrikam" -InternalAddress contoso.com -ExternalAddress fabrikam.com

The following example rewrites the email addresses of all messages leaving the Exchange organization that are sent by recipients in the sales.contoso.com subdomain. Outbound messages are rewritten so they appear to come from the contoso.com domain. Inbound messages sent to contoso.com email addresses aren't rewritten.

    New-AddressRewriteEntry -Name "sales.contoso.com to contoso.com" -InternalAddress sales.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

## Rewrite email addresses for recipients in multiple subdomains

To rewrite the email addresses for recipients in a domain and all subdomains, use the following syntax.

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -OutboundOnly $true [-ExceptionList <domain1,domain2...>]

The following example rewrites the email addresses of all messages leaving the Exchange organization that are sent by recipients in the contoso.com domain and all subdomains. Outbound messages are rewritten so they appear to come from the contoso.com domain. Inbound messages sent to contoso.com recipients can't be rewritten because a wildcard is used in the *InternalAddress* parameter.

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

The following example is just like the previous example, except now messages sent by recipients in the legal.contoso.com and corp.contoso.com subdomains are never rewritten:

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains except legal.contoso.com and corp.contoso.com" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true -ExceptionList legal.contoso.com,corp.contoso.com

## How do you know this worked?

To verify that you have successfully created address rewrite entries, do the following:

1.  Run the command `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` and verify the settings displayed are the settings you configured.

2.  From a mailbox that's affected by an address rewrite entry, send a test message to an external mailbox. Verify the test message appears to originate from the rewritten email address.

3.  Reply to the test message from the external mailbox. Verify the original mailbox receives the reply.

## Use the Shell to modify address rewrite entries

The configuration options that are available when you modify an existing address rewrite entry are identical to the configuration options when you create a new address rewrite entry.

## Modify address rewrite entries for single recipients

To modify an address rewrite entry that rewrites the email address of a single recipient, use the following syntax:

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> -OutboundOnly <$true | $false>

The following example modifies the following properties of the single recipient address rewrite entry named "joe@contoso.com to support@nortwindtraders.com":

  - Changes the external address to support@northwindtraders.net.

  - Changes the name of the address rewrite entry to "joe@contoso.com to support@northwindtraders.net".

  - Changes the value of *OutboundOnly* to `$true`. Note that this change requires you to configure support@northwindtraders.net as a proxy address on Joe's mailbox.

<!-- end list -->

    Set-AddressRewriteEntry "joe@contoso.com to support@nortwindtraders.com" -Name "joe@contoso.com to support@northwindtraders.net" -ExternalAddress support@northwindtraders.net -OutboundOnly $true

## Modify address rewrite entries for recipients in single domains or subdomains

To modify an address rewrite entry that rewrites the email addresses of recipients from a single domain or subdomain, use the following syntax.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> -OutboundOnly <$true | $false>

The following example changes the internal address value of the single domain address rewrite entry named "Northwind Traders to Contoso".

    Set-AddressRewriteEntry "Northwindtraders to Contoso" -InternalAddress northwindtraders.net

## Modify address rewrite entries for recipients in multiple subdomains

To modify an address rewrite entry that rewrites the email address of recipients in a domain and all subdomains, use the following syntax.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -ExceptionList <list of domains>

To replace the existing exception list values of a multiple subdomain address rewrite entry, use the following syntax:

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList <domain1,domain2,...>

The following example replaces the existing exception list for the multiple subdomain address rewrite entry named Contoso to Northwind Traders with the values marketing.contoso.com and legal.contoso.com:

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList sales.contoso.com,legal.contoso.com

To selectively add or remove exception list values from a multiple subdomain address rewrite entry without modifying any existing exception list values, use the following syntax:

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

The following example adds finanace.contoso.com and removes marketing.contoso.com from the exception list of the multiple subdomain address rewrite entry named Contoso to Northwind Traders:

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList @{Add="finanace.contoso.com"; Remove="marketing.contoso.com"}

## How do you know this worked?

To verify that you have successfully modified an address rewrite entry, do the following:

1.  Run the command `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` and verify the settings displayed are the settings you configured.

2.  From a mailbox that's affected by an address rewrite entry, send a test message to an external mailbox. Verify the test message appears to originate from the rewritten email address.

3.  From the external mailbox, reply to the test message. Verify the original mailbox receives the reply.

## Use the Shell to remove address rewrite entries

To remove a single address rewrite entry, use the following syntax:

    Remove-AddressRewriteEntry <AddressRewriteEntryIdentity>

The following example removes the address rewrite entry named "Contoso.com to Northwindtraders.com":

    Remove-AddressRewriteEntry "Contoso.com to Northwindtraders.com"

To remove multiple address rewrite entries, use the following syntax:

    Get-AddressRewriteEntry [<search criteria>] | Remove-AddressRewriteEntry [-WhatIf]

The following example removes all address rewrite entries:

    Get-AddressRewriteEntry | Remove-AddressRewriteEntry

The following example simulates the removal of address rewrite entries that contain the text "to contoso.com" in the name. The *WhatIf* switch allows you to preview the result without committing any changes.

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry -WhatIf

If you are satisfied with the result, run the command again without the *WhatIf* switch to remove the address rewrite entries.

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry

## How do you know this worked?

To verify that you have successfully removed an address rewrite entry, do the following:

1.  Run the command `Get-AddressRewriteEntry`, and verify that the address rewrite entries you removed aren't listed.

2.  From a mailbox that's affected by an address rewrite entry, send a test message to an external mailbox. Verify the test message is no longer affected by the removed address rewrite entry.

3.  From the external mailbox, reply to the test message. Verify the original mailbox receives the reply and that the message is unaffected by the removed address rewrite entry.

