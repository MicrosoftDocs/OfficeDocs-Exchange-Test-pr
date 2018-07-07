---
title: 'Define your own DLP templates and information types: Exchange 2013 Help'
TOCTitle: Define your own DLP templates and information types
ms:assetid: f4622dba-3347-4758-b4a2-f01b043c908c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ674310(v=EXCHG.150)
ms:contentKeyID: 49319939
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Define your own DLP templates and information types

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can develop data loss prevention (DLP) policy templates as XML files independent of Microsoft Exchange Server 2013 and then import them using the Exchange Administration Center or the Exchange management shell. This section describes the process and details of authoring and tuning DLP XML files for use within a DLP solution. You are not required to develop your own DLP XML files because the Exchange Administration Center provides a way for you to get started quickly with existing DLP policy templates and transport rules in order to scan messages.

Looking for management tasks related to DLP policy templates? See [DLP procedures](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013) or [DLP procedures](https://technet.microsoft.com/en-us/library/jj938003\(v=exchg.150\)) (Exchange Online).


> [!NOTE]
> Exchange 2013: DLP is a premium feature that requires an Exchange Enterprise Client Access License (CAL). For more information about CALs and server licensing, see <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server Licensing</A>.<BR>Exchange Online: DLP is a premium feature that requires an Exchange Online Plan 2 subscription. For more information, see <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Exchange Online Licensing</A>.




> [!IMPORTANT]
> It’s beyond the scope of this documentation to recommend a business model or information about file packaging or deployment guidelines for the sensitive information rules or to discuss how such rules would be distributed. Furthermore, this documentation does not discuss protection mechanisms, such as encryption, for custom developed rules, nor does it discuss how such mechanism would be employed.



## Extend the information types to meet your needs

The following sections describe concepts and the XML schema definition that you must understand in order to begin creating your own XML files for both DLP policy templates and sensitive information rule packages that can be imported into Exchange 2013 and used as DLP policies.

DLP in Microsoft Exchange helps you to apply organizational-specific policy to sensitive information. A key factor in the strength of a DLP solution is the ability to correctly identify confidential or sensitive information that may be unique to the organization, regulatory needs, geography, or other aspects of business. Although Microsoft has provided policy templates and sensitive information types within the product for you to get started, your unique business needs can require a custom data loss prevention solution. For this reason, Microsoft provides a way for you to create and import your own DLP policy templates or your own sensitive information definitions within classification rule packages. An accurate DLP solution relies on configuring the correct set of rules for the sensitive information detection engine that provide high degree of protection while minimizing false positives and negatives.

## Develop your own DLP policy templates

You can write your own DLP policy template XML file and import it. This approach to extending the DLP solution provided in Exchange will allow you to build DLP policies that closely match your DLP requirements.

Managing custom templates and their related policies is similar to managing the DLP policies that you create based on Microsoft-supplied templates. In a typical DLP policy lifecycle, you would do the following:

1.  Create your own DLP policy template, a custom XML file. To learn more, see [Developing DLP policy template files](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md).

2.  Import your custom template. To learn more, see [Import a custom DLP policy template from a file](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md).

3.  Create a DLP Policy based on your custom template. To learn more, see [Create a DLP policy from a template](how-to-new-dlp-data-loss-prevention-policy-template.md).

4.  Update your custom template by repeating steps 1 and 2.

5.  Remove your custom template. To learn more, see [Remove-DlpPolicyTemplate](https://technet.microsoft.com/en-us/library/jj215739\(v=exchg.150\)).

For more information about the XML schema definition and concepts related to developing your own templates, see [Developing DLP policy template files](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md).

## Develop your own sensitive information types and matching logic in classification rule packages

You can write your own sensitive information definitions in a classification rule package, which is an XML file, and import it as part of your DLP solution. The sensitive information detection engine provides the deep content analysis capabilities for identifying sensitive information like credit card numbers, social security numbers, and company intellectual property. The engine is controlled by a configurable set of instructions, or rules, for scanning and analyzing the content. The rules are combined together into a classification rule package, an XML document that adheres to a standardized rules package XML schema definition. Here’s how you can develop your own.

1.  Create your own sensitive information types, a custom XML file. To learn more, see [Developing sensitive information rule packages](technical-description-of-xml-schema-for-dlp-rule-packages.md).

2.  Import your sensitive information type. To learn more, see [New-ClassificationRuleCollection](https://technet.microsoft.com/en-us/library/jj218619\(v=exchg.150\)).

3.  Create custom template based on your information types. To learn more, see [Developing sensitive information rule packages](technical-description-of-xml-schema-for-dlp-rule-packages.md)

4.  Update your custom template by repeating steps 1 and 2.

5.  Remove your custom template. To learn more, see [Remove-ClassificationRuleCollection](https://technet.microsoft.com/en-us/library/jj218670\(v=exchg.150\))

For more information about the rule packages, see [Developing sensitive information rule packages](technical-description-of-xml-schema-for-dlp-rule-packages.md) and [Matching methods and techniques for rule packages](technical-description-of-xsd-rule-matching-for-dlp-rule-packages.md).

## Understanding rule types in rule packages

The rules within a rule package configure the process for detecting well-defined content characteristics; for example, rules for finding a driver’s license number. Two main rule types are available: Entity and Affinity.

*Entity* rules are targeted toward well-defined (and oftentimes regulated) identifiers such as U.S. social security numbers. An Entity is represented by a collection of countable patterns. A pattern defines a collection of matches with an explicit primary match identifier. An example Entity is a driver’s license.

*Affinity* rules are targeted toward a certain type of document such as a corporate financial statement. An Affinity is represented as a collection of independent evidences. Evidence is an aggregation of required matches within certain proximity. An example of an Affinity is the U.S. Sarbanes-Oxley Act.

## For more information

[Data loss prevention](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Import a custom DLP policy template from a file](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

[New-ClassificationRuleCollection](https://technet.microsoft.com/en-us/library/jj218619\(v=exchg.150\))

[Mail flow rules (transport rules) in Exchange 2013](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange Server 2013

[Mail flow rules (transport rules) in Exchange Online](https://technet.microsoft.com/en-us/library/jj919238\(v=exchg.150\)) Exchange Online

[What the sensitive information types in Exchange look for](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

