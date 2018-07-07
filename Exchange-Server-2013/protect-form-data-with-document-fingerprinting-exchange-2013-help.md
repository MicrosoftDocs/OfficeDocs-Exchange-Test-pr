---
title: 'Protect form data with document fingerprinting: Exchange 2013 Help'
TOCTitle: Protect form data with document fingerprinting
ms:assetid: 110c839b-7693-42f6-aa5d-58ce64f4c357
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn635175(v=EXCHG.150)
ms:contentKeyID: 61218307
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Protect form data with document fingerprinting

 

_**Applies to:** Exchange Online, Exchange Server 2013_


If your organization uses forms to collect sensitive information, users might try emailing those forms to outside contacts, which creates a security risk. Data loss prevention (DLP) in Exchange helps you protect that information by detecting it with [Document Fingerprinting](overview-of-document-fingerprinting-in-exchange.md). To use document fingerprinting, simply upload a blank form, such as an intellectual property document, government form, or other standard form used in your organization. Then, add the resulting document fingerprint to a DLP policy or transport rule. Here’s how.

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/0f803e16-397a-4b83-8a85-06cd4264aaca]

## Use the EAC to create a document fingerprint

![Path to Document Fingerprinting in EAC highlighted](images/Dn635175.e8562ea7-40ba-4feb-adde-2e81f029fcda(EXCHG.150).png "Path to Document Fingerprinting in EAC highlighted")

1.  In the Exchange Administration Center EAC, go to **compliance management** \> **data loss prevention**.

2.  Click **Manage document fingerprints**.

3.  On the document fingerprints page, click **New** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") to create a new document fingerprint.

4.  Give the document fingerprint a **Name** and **Description**. (The name you choose will appear in the sensitive information types list.)

5.  To upload a form, click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

6.  Choose a form, and click **Open**. (Make sure that the file you upload contains text, isn’t password protected, and is in one of the file types that are supported in transport rules. For a list of supported file types, see [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/en-us/library/jj919236\(v=exchg.150\)). Otherwise, you’ll get an error when you try creating the fingerprint.) Repeat for any additional files you want to add to the document list for this document fingerprint. You can also add or remove files from this document fingerprint later if you want.

7.  Click **Save**.

The document fingerprint is now part of your sensitive information types, and you can add it to a DLP policy or add it to a transport rule via the **The message contains sensitive information…** condition.

!["Apply this rule if" condition highlighted](images/Dn635175.9355a513-a790-48eb-a61b-575ba2ecdfa6(EXCHG.150).png "\"Apply this rule if\" condition highlighted")

For more information about adding rules to a DLP policy, see the “Change a DLP policy” section of [Manage DLP policies](manage-dlp-policies-exchange-2013-help.md), and for more information about modifying transport rules, see [Integrating sensitive information rules with transport rules](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md). If you want to create a new policy, see [Create a DLP policy from a template](how-to-new-dlp-data-loss-prevention-policy-template.md).

## Use the Shell to create a classification rule package based on document fingerprinting


> [!TIP]
> Even though you can create and modify classification rule packages in the Shell, you might find that creating document fingerprints is a little simpler in the EAC. We recommend you try it there before trying this procedure in the Shell.



DLP uses classification rule packages to detect sensitive content in messages. To create a classification rule package based on a document fingerprint, use the **New-Fingerprint** and **New-DataClassification** cmdlets. Because the results of **New-Fingerprint** aren’t stored outside the data classification rule, you always run **New-Fingerprint** and **New-DataClassification** or **Set-DataClassification** in the same PowerShell session. The following example creates a new document fingerprint based on the file C:\\My Documents\\Contoso Employee Template.docx. You store the new fingerprint as a variable so you can use it with the **New-DataClassification** cmdlet in the same PowerShell session.

    $Employee_Template = Get-Content "C:\My Documents\Contoso Employee Template.docx" -Encoding byte
    $Employee_Fingerprint = New-Fingerprint -FileData $Employee_Template -Description "Contoso Employee Template"

Now, let’s create a new data classification rule named "Contoso Employee Confidential" that uses the document fingerprint of the file C:\\My Documents\\Contoso Customer Information Form.docx.

    $Employee_Template = Get-Content "C:\My Documents\Contoso Customer Information Form.docx" -Encoding byte
    $Customer_Fingerprint = New-Fingerprint -FileData $Customer_Form -Description "Contoso Customer Information Form"
    New-DataClassification -Name "Contoso Customer Confidential" -Fingerprints $Customer_Fingerprint -Description "Message contains Contoso customer information." 

You can now use the **Get-DataClassification** cmdlet to find all DLP data classification rule packages, and in this example, “Contoso Customer Confidential” is part of the data classification rule packages list.

Finally, add the “Contoso Customer Confidential” data classification rule package to a DLP policy.

    New-TransportRule -Name "Notify :External Recipient Contoso confidential" -NotifySender NotifyOnly -Mode Enforce -SentToScope NotInOrganization -MessageContainsDataClassification @{Name=" Contoso Customer Confidential"}

The DLP agent now detects documents that match the Contoso Customer Form.docx document fingerprint.

For syntax and parameter information, see [New-Fingerprint](https://technet.microsoft.com/en-us/library/dn584142\(v=exchg.150\)), [New-DataClassification](https://technet.microsoft.com/en-us/library/dn584139\(v=exchg.150\)), [Set-DataClassification](https://technet.microsoft.com/en-us/library/dn584141\(v=exchg.150\)), and [Get-DataClassification](https://technet.microsoft.com/en-us/library/jj215720\(v=exchg.150\)).

## For more information

[Document Fingerprinting](overview-of-document-fingerprinting-in-exchange.md)

[Manage DLP policies](manage-dlp-policies-exchange-2013-help.md)

[Integrating sensitive information rules with transport rules](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

