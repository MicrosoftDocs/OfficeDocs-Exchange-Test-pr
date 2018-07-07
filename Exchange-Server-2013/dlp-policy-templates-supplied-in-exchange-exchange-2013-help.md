---
title: 'DLP policy templates supplied in Exchange: Exchange 2013 Help'
TOCTitle: DLP policy templates supplied in Exchange
ms:assetid: 7e1917ab-1920-4a52-97d1-7dfe2add6198
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150530(v=EXCHG.150)
ms:contentKeyID: 47560043
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# DLP policy templates supplied in Exchange

 

_**Applies to:** Exchange Online, Exchange Server 2013_


In Microsoft Exchange Server 2013 and Exchange Online, you can use data loss prevention (DLP) policy templates as a starting point for building DLP policies that help you meet your specific regulatory and business policy needs. You can modify the templates to meet the specific needs of your organization.


> [!WARNING]
> You should enable your DLP policies in test mode before running them in your production environment. During such tests, it is recommended that you configure sample user mailboxes and send test messages that invoke your test policies in order to confirm the results.<BR>Use of these policies does not ensure compliance with any regulation. After your testing is complete, make the necessary configuration changes in Exchange so the transmission of information complies with your organization's policies. For example, you might need to configure TLS with known business partners or add more restrictive transport rule actions, such as adding rights protection to messages that contain a certain type of data.



## Templates available for DLP

The following table lists the DLP policy templates in Exchange. To learn more about customizing these templates to create DLP policies, see [Manage DLP policies](manage-dlp-policies-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Template</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Australia Financial Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be financial data in Australia, including credit cards, and SWIFT codes.</p></td>
</tr>
<tr class="even">
<td><p>Australia Health Records Act (HRIP Act)</p></td>
<td><p>Helps detect the presence of information commonly considered to be subject to the Health Records and Information Privacy (HRIP) act in Australia, like medical account number and tax file number.</p></td>
</tr>
<tr class="odd">
<td><p>Australia Personally Identifiable Information (PII) Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be personally identifiable information (PII) in Australia, like tax file number and driver's license.</p></td>
</tr>
<tr class="even">
<td><p>Australia Privacy Act</p></td>
<td><p>Helps detect the presence of information commonly considered to be subject to the privacy act in Australia, like driver's license and passport number.</p></td>
</tr>
<tr class="odd">
<td><p>Canada Financial Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be financial data in Canada, including bank account numbers and credit cards.</p></td>
</tr>
<tr class="even">
<td><p>Canada Health Information Act (HIA)</p></td>
<td><p>Helps detect the presence of information subject to Canada Health Information Act (HIA) for Alberta, including data like passport numbers and health information.</p></td>
</tr>
<tr class="odd">
<td><p>Canada Personal Health Act (PHIPA) - Ontario</p></td>
<td><p>Helps detect the presence of information subject to Canada Personal Health Information Protection Act (PHIPA) for Ontario, including data like passport numbers and health information.</p></td>
</tr>
<tr class="even">
<td><p>Canada Personal Health Information Act (PHIA) - Manitoba</p></td>
<td><p>Helps detect the presence of information subject to Canada Personal Health Information Act (PHIA) for Manitoba, including data like health information.</p></td>
</tr>
<tr class="odd">
<td><p>Canada Personal Information Protection Act (PIPA)</p></td>
<td><p>Helps detect the presence of information subject to Canada Personal Information Protection Act (PIPA) for British Columbia, including data like passport numbers and health information.</p></td>
</tr>
<tr class="even">
<td><p>Canada Personal Information Protection Act (PIPEDA)</p></td>
<td><p>Helps detect the presence of information subject to Canada Personal Information Protection and Electronic Documents Act (PIPEDA), including data like passport numbers and health information.</p></td>
</tr>
<tr class="odd">
<td><p>Canada Personally Identifiable Information (PII) Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be personally identifiable information (PII) in Canada, like health ID number and social insurance number.</p></td>
</tr>
<tr class="even">
<td><p>France Data Protection Act</p></td>
<td><p>Helps detect the presence of information commonly considered to be subject to the Data Protection Act in France, like the health insurance card number.</p></td>
</tr>
<tr class="odd">
<td><p>France Financial Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be financial information in France, including information like credit card, account information, and debit card numbers.</p></td>
</tr>
<tr class="even">
<td><p>France Personally Identifiable Information (PII) Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be personally identifiable information (PII) in France, including information like passport numbers.</p></td>
</tr>
<tr class="odd">
<td><p>Germany Financial Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be financial data in Germany like EU debit card numbers.</p></td>
</tr>
<tr class="even">
<td><p>Germany Personally Identifiable Information (PII) Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be personally identifiable information (PII) in Germany, including information like driver's license and passport numbers.</p></td>
</tr>
<tr class="odd">
<td><p>Israel Financial Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be financial data in Israel, including bank account numbers and SWIFT codes.</p></td>
</tr>
<tr class="even">
<td><p>Israel Personally Identifiable Information (PII) Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be personally identifiable information (PII) in Israel, like national ID number.</p></td>
</tr>
<tr class="odd">
<td><p>Israel Protection of Privacy</p></td>
<td><p>Helps detect the presence of information commonly considered to be subject to the Protection of Privacy in Israel, including information like bank account numbers or national ID.</p></td>
</tr>
<tr class="even">
<td><p>Japan Financial Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be financial information in Japan, including information like credit card, account information, and debit card numbers.</p></td>
</tr>
<tr class="odd">
<td><p>Japan Personally Identifiable Information (PII) Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be personally identifiable information (PII) in Japan, including information like driver's license and passport numbers.</p></td>
</tr>
<tr class="even">
<td><p>Japan Protection of Personal Information</p></td>
<td><p>Helps detect the presence of information subject to Japan Protection of Personal Information, including data like resident registration numbers.</p></td>
</tr>
<tr class="odd">
<td><p>PCI Data Security Standard (PCI DSS)</p></td>
<td><p>Helps detect the presence of information subject to PCI Data Security Standard (PCI DSS), including information like credit card or debit card numbers.</p></td>
</tr>
<tr class="even">
<td><p>Saudi Arabia - Anti-Cyber Crime Law</p></td>
<td><p>Helps detect the presence of information commonly considered to be subject to the Anti-Cyber Crime Law in Saudi Arabia, including international bank account numbers and SWIFT codes.</p></td>
</tr>
<tr class="odd">
<td><p>Saudi Arabia Financial Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be financial data in Saudi Arabia, including international bank account numbers and SWIFT codes.</p></td>
</tr>
<tr class="even">
<td><p>Saudi Arabia Personally Identifiable Information (PII) Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be personally identifiable information (PII) in Saudi Arabia, like national ID number.</p></td>
</tr>
<tr class="odd">
<td><p>U.K. Access to Medical Reports Act</p></td>
<td><p>Helps detect the presence of information subject to United Kingdom Access to Medical Reports Act, including data like National Health Service numbers.</p></td>
</tr>
<tr class="even">
<td><p>U.K. Data Protection Act</p></td>
<td><p>Helps detect the presence of information subject to United Kingdom Data Protection Act, including data like national insurance numbers.</p></td>
</tr>
<tr class="odd">
<td><p>U.K. Financial Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be financial information in United Kingdom, including information like credit card, account information, and debit card numbers.</p></td>
</tr>
<tr class="even">
<td><p>U.K. Personal Information Online Code of Practice (PIOCP)</p></td>
<td><p>Helps detect the presence of information subject to United Kingdom Personal Information Online Code of Practice, including data like health information.</p></td>
</tr>
<tr class="odd">
<td><p>U.K. Personally Identifiable Information (PII) Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be personally identifiable information (PII) in United Kingdom, including information like driver's license and passport numbers.</p></td>
</tr>
<tr class="even">
<td><p>U.K. Privacy and Electronic Communications Regulations</p></td>
<td><p>Helps detect the presence of information subject to United Kingdom Privacy and Electronic Communications Regulations, including data like financial information.</p></td>
</tr>
<tr class="odd">
<td><p>U.S. Federal Trade Commission (FTC) Consumer Rules</p></td>
<td><p>Helps detect the presence of information subject to U.S. Federal Trade Commission (FTC) Consumer Rules, including data like credit card numbers.</p></td>
</tr>
<tr class="even">
<td><p>U.S. Financial Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be financial information in United States, including information like credit card, account information, and debit card numbers.</p></td>
</tr>
<tr class="odd">
<td><p>U.S. Gramm-Leach-Bliley Act (GLBA)</p></td>
<td><p>Helps detect the presence of information subject to Gramm-Leach-Bliley Act (GLBA), including information like social security numbers or credit card numbers.</p></td>
</tr>
<tr class="even">
<td><p>U.S. Health Insurance Act (HIPAA)</p></td>
<td><p>Helps detect the presence of information subject to United States Health Insurance Portability and Accountability Act (HIPAA),including data like social security numbers and health information.</p></td>
</tr>
<tr class="odd">
<td><p>U.S. Patriot Act</p></td>
<td><p>Helps detect the presence of information commonly subject to U.S. Patriot Act, including information like credit card numbers or tax identification numbers.</p></td>
</tr>
<tr class="even">
<td><p>U.S. Personally Identifiable Information (PII) Data</p></td>
<td><p>Helps detect the presence of information commonly considered to be personally identifiable information (PII) in the United States, including information like social security numbers or driver's license numbers.</p></td>
</tr>
<tr class="odd">
<td><p>U.S. State Breach Notification Laws</p></td>
<td><p>Helps detect the presence of information subject to U.S. State Breach Notification Laws, including data like social security and credit card numbers.</p></td>
</tr>
<tr class="even">
<td><p>U.S. State Social Security Number Confidentiality Laws</p></td>
<td><p>Helps detect the presence of information subject to U.S. State Social Security Number Confidentiality Laws, including data like social security numbers.</p></td>
</tr>
</tbody>
</table>


## For more information

[Data loss prevention](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Create a DLP policy from a template](how-to-new-dlp-data-loss-prevention-policy-template.md)

[What the sensitive information types in Exchange look for](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

