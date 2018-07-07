---
title: 'Enable or disable hierarchical address books: Exchange 2013 Help'
TOCTitle: Enable or disable hierarchical address books
ms:assetid: b4c3a175-ce5e-4bfb-a4a0-92d25f3644b3
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ff607473(v=EXCHG.150)
ms:contentKeyID: 49289382
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Enable or disable hierarchical address books

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can configure a hierarchical address book (HAB), which is a feature available to end users in Microsoft Outlook 2010 or later. With an HAB, users can look for recipients in their Exchange organization by using an organizational hierarchy based on seniority or management structure. To learn more about HABs, see [Hierarchical address books](hierarchical-address-books-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 1 hour.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Distribution groups" entry in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - You can’t use the Exchange Administration Center (EAC) to perform this procedure. You must use the Shell.

  - Before you get started, read the topic [Hierarchical address books](hierarchical-address-books-exchange-2013-help.md). You should understand if a HAB is appropriate for your Exchange organization.

  - Understand how organizational units (OUs), groups, users, and contacts are currently configured in your Exchange organization.

  - Understand the cmdlets and associated parameters in the following table, which are required to configure a HAB.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Cmdlet</th>
    <th>Parameter</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/en-us/library/aa997443(v=exchg.150)">Set-OrganizationConfig</a></p></td>
    <td><p><em>HierarchicalAddressBookRoot</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/en-us/library/bb123770(v=exchg.150)">Set-Group</a></p></td>
    <td><p><em>IsHierarchicalGroup</em></p>
    <p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/en-us/library/aa998221(v=exchg.150)">Set-User</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/en-us/library/bb124535(v=exchg.150)">Set-Contact</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    </tbody>
    </table>


  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## Use the Shell to enable a HAB


> [!NOTE]
> Although you can't use the EAC to enable a HAB, after it’s enabled you can use the EAC to manage the membership of the groups in the organizational hierarchy.



For this example, an OU called HAB will be created for the HAB. The name of the domain for the organization is Contoso-dom, and Contoso,Ltd will be the name of the top-level organization in the hierarchy (the *root organization*). Subordinate groups named Corporate Office, Product Support Organization, and Sales & Marketing Organization will be created as child organizations under Contoso,Ltd. Additionally, the groups Human Resources, Accounting Group, and Administration Group will be created as child organizations under Corporate Office.

For detailed information about creating distribution groups, see [Create and manage distribution groups](create-and-manage-distribution-groups-exchange-2013-help.md).

1.  Create an OU named HAB in the Contoso organization. You can use Active Directory Users and Computers or type the following at a command prompt.
    

    > [!NOTE]
    > Alternatively, you can use an existing OU in your Exchange forest.

    
        dsadd ou "OU=HAB,DC=Contoso-dom,DC=Contoso,DC=com"
    

    > [!NOTE]
    > For details, see <A href="https://go.microsoft.com/fwlink/p/?linkid=198986">Create a New Organizational Unit</A>.



2.  Create the root distribution group Contoso,Ltd for the HAB.
    

    > [!NOTE]
    > For the purposes of this topic, the Shell example is provided. However, you can also use the EAC to create a distribution group. For details, see <A href="create-and-manage-distribution-groups-exchange-2013-help.md">Create and manage distribution groups</A>.

    
        New-DistributionGroup -Name "Contoso,Ltd" -DisplayName "Contoso,Ltd" -Alias "ContosoRoot" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "ContosoRoot" -Type "Distribution"

3.  Designate Contoso,Ltd as the root organization for the HAB.
    
        Set-OrganizationConfig -HierarchicalAddressBookRoot "Contoso,Ltd"

4.  Create distribution groups for the other tiers in the HAB. For this example, you would create the following groups: Corporate Office, Product Support Organization, Sales & Marketing Organization, Human Resources, Accounting Group, and Administration Group. This example creates the distribution group Corporate Office.
    

    > [!NOTE]
    > For the purposes of this topic, the Shell example is provided. However, you can also use the EAC to create distribution groups. For details, see <A href="create-and-manage-distribution-groups-exchange-2013-help.md">Create and manage distribution groups</A>.

    
        New-DistributionGroup -Name "Corporate Office" -DisplayName "Corporate Office" -Alias "CorporateOffice" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "CorporateOffice" -Type "Distribution"

5.  Designate each of the groups as members of the HAB. For this example, you would designate the following groups as being hierarchical groups: Contoso,Ltd, Corporate Office, Product Support Organization, Sales & Marketing Organization, Human Resources, Accounting Group, and Administration Group. This example designates the distribution group Contoso,Ltd as a member of the HAB.
    
        Set-Group -Identity "Contoso,Ltd" -IsHierarchicalGroup $true

6.  Add each of the subordinate groups as members of the root organization. For this example, distribution groups Corporate Office, Product Support Organization, and Sales & Marketing Organization, are added as members of the root organization Contoso,Ltd in the HAB. This example adds the Corporate Office distribution group as a member of the Contoso,Ltd root distribution group.
    

    > [!NOTE]
    > This example uses the alias of the distribution groups.

    
        Add-DistributionGroupMember -Identity "ContosoRoot" -Member "CorporateOffice"

7.  Add each of the groups that are subordinate to the distribution group Corporate Office as members of the group. For this example, distribution groups Human Resources, Accounting Group, and Administration Group, are added as members of the distribution group Corporate Office. This example adds the Human Resources distribution group as a member of the Corporate Office distribution group.
    

    > [!NOTE]
    > This example uses the alias of the distribution groups and assumes the Human Resources distribution group alias is HumanResources.

    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "HumanResources"

8.  Add users to the groups in the HAB. For this example, David Hamilton (SMTP address DHamilton@contoso.com) is an existing user in the OU Contoso-dom.Contoso.com/Users and will be added to the group Corporate Office. Repeat this step to add other users to groups in the HAB.
    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "DHamilton"

9.  Set the *SeniorityIndex* parameter for groups in the HAB. For this example, the Corporate Office group contains three child groups: Human Resources, Accounting Group, and Administration Group. Instead of having the groups listed in ascending alphabetical order, which is the default, the preferred sorting will be Human Resources (*SeniorityIndex* = 100), Accounting Group (*SeniorityIndex* = 50), and then Administration Group (*SeniorityIndex* = 25). This example sets the *SeniorityIndex* parameter for the Human Resources group to 100.
    
        Set-Group -Identity "Human Resources" -SeniorityIndex 100
    

    > [!NOTE]
    > The <EM>SeniorityIndex</EM> parameter is a numerical value used to sort groups or users in descending numerical order in a HAB. If the <EM>SeniorityIndex</EM> parameter isn't set or is equal for two or more users, the HAB sorting order uses the <EM>PhoneticDisplayName</EM> parameter value to list the users in ascending alphabetical order. If the <EM>PhoneticDisplayName</EM> value isn't set, the HAB sorting order defaults to the <EM>DisplayName</EM> parameter value and lists the users in ascending alphabetical order.



10. Set the *SeniorityIndex* parameter for users in the HAB groups. For this example, the Corporate Office group contains three users: Amy Alberts, David Hamilton, and Rajesh M. Patel. Instead of having the users listed in ascending alphabetical order by default, the preferred sorting will be David Hamilton (*SeniorityIndex* = 100), Rajesh M. Patel (*SeniorityIndex* = 50), and then Amy Alberts (*SeniorityIndex* = 25). This example sets the *SeniorityIndex* parameter for the user David Hamilton to 100.
    
        Set-User -Identity "DHamilton@contoso.com" -SeniorityIndex 100

After completing the preceding steps, the HAB will be visible in Outlook. To view the HAB, open Outlook and click **Address Book**. The HAB is displayed on the **Organization** tab, similar to the following figure.

**Example HAB for Contoso,Ltd**

![Hierarchical Address Book dialog](images/Ff629379.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "Hierarchical Address Book dialog")

After the HAB is created, you can use the EAC to manage the membership of the groups in the organizational hierarchy. However, you must use the Shell to modify the *SeniorityIndex* parameter for any new groups or users.

For detailed syntax and parameter information, see the following:

  - [New-DistributionGroup](https://technet.microsoft.com/en-us/library/aa998856\(v=exchg.150\))

  - [Set-OrganizationConfig](https://technet.microsoft.com/en-us/library/aa997443\(v=exchg.150\))

  - [Set-Group](https://technet.microsoft.com/en-us/library/bb123770\(v=exchg.150\))

  - [Add-DistributionGroupMember](https://technet.microsoft.com/en-us/library/bb124340\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/en-us/library/aa998221\(v=exchg.150\))

## Use the Shell to disable a hierarchical address book

This example disables the root organization used for the HAB.

    Set-OrganizationConfig -HierarchicalAddressBookRoot $null


> [!NOTE]
> This command doesn't delete the root organization or child groups used in the HAB structure or reset the <EM>SeniorityIndex</EM> values for groups or users. It only prevents the HAB from being displayed in Outlook. To enable the HAB with the same configuration settings again, you only need to enable the root organization again.



For detailed syntax and parameter information, see [Set-OrganizationConfig](https://technet.microsoft.com/en-us/library/aa997443\(v=exchg.150\)).

