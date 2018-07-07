---
title: 'Hierarchical address books: Exchange 2013 Help'
TOCTitle: Hierarchical address books
ms:assetid: a1d277a0-5437-40af-aade-e4730a0d1308
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ff629379(v=EXCHG.150)
ms:contentKeyID: 49289358
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Hierarchical address books

 

_**Applies to:** Exchange Server 2013_


The hierarchical address book (HAB) allows end users to look for recipients in their address book using an organizational hierarchy. Normally, users are limited to the default global address list (GAL) and its recipient properties and the structure of the GAL often doesn't reflect the management or seniority relationships of recipients in your organization. Being able to customize an HAB that maps to your organization's unique business structure provides your users with an efficient method for locating internal recipients.

## Using hierarchical address books

In an HAB, your root organization (for example, Contoso, Ltd) is used as the top-level tier. Under this top-level tier, you can add several child tiers to create a customized HAB that's segmented by division, department, or any other organizational tier you want to specify. The following figure illustrates an HAB for Contoso, Ltd with the following structure:

  - The top-level tier represents the root organization Contoso, Ltd.

  - The second-level child tiers represent the business divisions within Contoso, Ltd: Corporate Office, Product Support Organization, and Sales & Marketing Organization.

  - The third-level child tiers represent departments within the Corporate Office division: Human Resources, Accounting Group, and Administration Group.

**Example HAB for Contoso, Ltd**

![Hierarchical Address Book dialog](images/Ff629379.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "Hierarchical Address Book dialog")

You can provide an additional level of hierarchical structure by using the *SeniorityIndex* parameter. When creating an HAB, use the *SeniorityIndex* parameter to rank individual recipients or organizational groups by seniority within these organizational tiers. This ranking specifies the order in which the recipients or groups are displayed in the HAB. For example, in the preceding example, the *SeniorityIndex* parameter for the recipients in the Corporate Office division is set to the following:

  - `100` for David Hamilton

  - `50` for Rajesh M. Patel

  - `25` for Amy Alberts


> [!NOTE]
> If the <EM>SeniorityIndex</EM> parameter isn't set or is equal for two or more users, the HAB sorting order uses the <EM>PhoneticDisplayName</EM> parameter value to list the users in ascending alphabetical order. If the <EM>PhoneticDisplayName</EM> parameter value isn't set, the HAB sorting order defaults to the <EM>DisplayName</EM> parameter value and lists the users in ascending alphabetical order.



## Configuring hierarchical address books

Detailed instructions for creating HABs are included in the topic [Enable or disable hierarchical address books](enable-or-disable-hierarchical-address-books-exchange-2013-help.md). The general steps are as follows:

1.  Create a distribution group that will be used for the root organization (top-level tier). If desired, you can use an existing organizational unit in your Exchange forest for the distribution group.

2.  Create distribution groups for the child tiers and designate them as members of the HAB. Modify the *SeniorityIndex* parameter of these groups so they're listed in the proper hierarchical order within the root organization.

3.  Add organization members. Modify the *SeniorityIndex* parameter of the members so they're listed in the proper hierarchical order within the child tiers.

4.  For accessibility purposes, you can use the *PhoneticDisplayName* parameter, which specifies a phonetic pronunciation of the *DisplayName* parameter.

