---
title: 'Create incident reports for DLP policy detections: Exchange 2013 Help'
TOCTitle: Create incident reports for DLP policy detections
ms:assetid: 8e807f94-384c-43f5-be6f-06c5587175a0
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150534(v=EXCHG.150)
ms:contentKeyID: 47560050
ms.date: 06/13/2017
mtps_version: v=EXCHG.150
---

# Create incident reports for DLP policy detections

 

_**Applies to:** Exchange Online, Exchange Server 2013_


In Exchange Server 2013, you can establish an action to create an incident report within a DLP policy rule set. Additionally, you can indicate to whom the report should be sent and what to do with the original message. The incident report can contain any of the following information.

## Content of an incident management report

The **Generate Incident Report** action enables users to send incident reports to an incident management mailbox. A single incident report will be generated for each message only if the **Generate Incident Report** action is applied within a policy.

The following is a complete list of the line names in the incident report template. The format column describes how to recognize each field in the report. The optional field column specifies what fields might not be in the Report for each rule match. The DLP specific column shows what fields exist as a result of the DLP feature.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Line</strong> <strong>name</strong></p></td>
<td><p><strong>Description</strong></p></td>
<td><p><strong>Format</strong></p></td>
<td><p><strong>Optional field</strong></p></td>
<td><p><strong>DLP specific</strong></p></td>
</tr>
<tr class="even">
<td><p>Message-Id</p></td>
<td><p>ID of the original sent message</p></td>
<td><p>Message-Id: ID of message</p></td>
<td><p>Mandatory</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Sender</p></td>
<td><p>True sender of the original message</p></td>
<td><p>Sender: Email address of sender</p></td>
<td><p>Mandatory</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Subject</p></td>
<td><p>Subject of the original message</p></td>
<td><p>Subject: end-user input subject string</p></td>
<td><p>Mandatory</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>To</p></td>
<td><p>Recipient or recipients of the original message</p>
<p>Each To line will only contain a single recipient, and there can be up to 10 recipients displayed in the Incident Report. If there are additional recipients, the next To line will display the remaining number of recipients.</p></td>
<td><p>To: Email address of recipient</p></td>
<td><p>Mandatory</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>CC email address of the original message; the line is optional</p>
<p>Each CC line will only contain a single CC email address, and there can only be up to 10 CC email addresses that are displayed in the Incident Report. If there are additional CC addresses, the next CC line will display the remaining number of CC email addresses.</p></td>
<td><p>CC: Email address of CC recipient</p></td>
<td><p>Optional</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>BCC</p></td>
<td><p>BCC email address of the original message; the line is optional</p>
<p>Each BCC line will only contain a single BCC email address, and there can only be up to 10 BCC addresses that are displayed in the Incident Report. If there are additional BCC email addresses, the following BCC line will display the remaining number of BCC email addresses.</p></td>
<td><p>BCC: Email address of BCC recipient</p></td>
<td><p>Optional</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Severity</p></td>
<td><p>Audit severity of the rule hit; displays the highest severity if multiple rules were hit.</p></td>
<td><p>Severity: Low, Medium, or High</p></td>
<td><p>Optional</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Override</p></td>
<td><p>Displays if an override was reported for the message, and the justification of the override if provided.</p></td>
<td><p>Override: Yes, Justification: IW input justification string</p></td>
<td><p>Optional</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="even">
<td><p>False Positive</p></td>
<td><p>Displays if a false positive was reported for the message.</p></td>
<td><p>False Positive: Yes</p></td>
<td><p>Optional</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="odd">
<td><p>Data Classification</p></td>
<td><p>Detected data classifications found in the original message; the line is optional.</p>
<p>Each data classification line will only contain a single detected classification along with its count, confidence, and recommended minimum confidence level. Up to 5 detected classifications will be displayed in the Incident Report. If the detected classification was an affinity, the count value does not apply and will not be shown.</p></td>
<td><p>Data Classification: sensitive information type, Count: instances of the sensitive information found in the message, Confidence: percent value, Recommended Minimum Confidence: percent value</p></td>
<td><p>Optional</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="even">
<td><p>Rule Hit</p></td>
<td><p>Displays all the rules that hit the original message.</p>
<p>Includes the name of the rule that was hit, the DLP Policy (optional) that the rule resides in, action(s) that were taken on the message because of the rule, data classification(s) in the rule that caused the rule to hit, and the definition of the rule.</p></td>
<td><p>Rule Hit: rule name, DLP Policy: DLP Policy name if applicable, Action: single action, Data Classification: sensitive information type, Definition: rule definition if applicable</p></td>
<td><p>Mandatory</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>ID Match</p></td>
<td><p>Displays the matched data classification, the exact matched content from the message, and the primary evidence of the data classification match; the line is optional.</p></td>
<td><p>ID Match: sensitive information type, Value: actual value of the sensitive data, Context: text around the sensitive data in the message</p></td>
<td><p>Optional</p></td>
<td><p>Yes</p></td>
</tr>
</tbody>
</table>


## For more information

[View DLP policy detection reports](view-dlp-policy-detection-reports-exchange-2013-help.md)

[Data loss prevention](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

