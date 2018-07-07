---
title: 'Email address policies: Exchange 2013 Help'
TOCTitle: Email address policies
ms:assetid: b63b63bb-6faf-4337-8441-50bc64b49bb8
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb232171(v=EXCHG.150)
ms:contentKeyID: 49289383
ms.date: 07/21/2016
mtps_version: v=EXCHG.150
---

# Email address policies

 

_**Applies to:** Exchange Server 2013_


Recipients (which include users, resources, contacts, and groups) are any mail-enabled object in Active Directory to which Microsoft Exchange can deliver or route messages. For a recipient to send or receive email messages, the recipient must have an email address. Email address policies generate the primary and secondary email addresses for your recipients so they can receive and send email.

By default, Exchange contains an email address policy for every mail-enabled user. This default policy specifies the recipient's alias as the local part of the email address and uses the default accepted domain. The local part of an email address is the name that appears before the at sign (@). However, you can change how your recipients' email addresses will display. For example, you can specify that the addresses display as *firstname*.*lastname*@contoso.com.

Furthermore, if you want to specify additional email addresses for all recipients or just a subset, you can modify the default policy or create additional policies. For example, the user mailbox for David Hamilton can receive email messages addressed to hdavid@mail.contoso.com and hamilton.david@mail.contoso.com.

Looking for management tasks related to email address policies? See [Email address policy procedures](email-address-policy-procedures-exchange-2013-help.md).

## Behaviors of recipient policies

Exchange applies a policy to all recipients that match the recipient filtering criteria:

  - Recipient policies are applied in order from the highest priority to lowest priority. In the event of a conflict between two or more policies, the policy with the highest priority will be applied. The default recipient policy is always has the lowest priority and will be applied if no other policies are matched.
    
    When you create a recipient policy but don't explicitly specify a priority, it will be added as the highest priority. If you specify a priority that's already associated with an existing policy, the existing policy and all policies with a lower priority will be moved down by one. The new policy will be inserted at the priority you specified.
    
    The recipient policy functionality is divided into two features: email address policies and accepted domains. For more information about accepted domains, see [Accepted domains](accepted-domains-exchange-2013-help.md).

  - When you run the **Update-EmailAddressPolicy** cmdlet in the Exchange Management Shell, the recipient object is updated with the email address policy.

  - Each time a recipient object is modified and saved, Exchange enforces the correct application of the email address criteria and settings. When an email address policy is modified and saved, all associated recipients are updated with the change. In addition, if a recipient object is modified, that recipient's email address policy membership is reevaluated and enforced.

## Creating email address policies

When creating an email address policy, you can use the following email address types:

  - **Precanned SMTP email address**. *Precanned* SMTP email addresses are commonly used email address types that are provided for you.

  - **Custom SMTP email address**. If you don't want to use one of the precanned SMTP email addresses, you can specify a custom SMTP email address.
    
    When creating a custom SMTP email address, you can use the variables in the following table to specify alternate values for the local part of the email address.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Variable</th>
    <th>Value</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%g</p></td>
    <td><p>Given name (first name)</p></td>
    </tr>
    <tr class="even">
    <td><p>%i</p></td>
    <td><p>Middle initial</p></td>
    </tr>
    <tr class="odd">
    <td><p>%s</p></td>
    <td><p>Surname (last name)</p></td>
    </tr>
    <tr class="even">
    <td><p>%d</p></td>
    <td><p>Display name</p></td>
    </tr>
    <tr class="odd">
    <td><p>%m</p></td>
    <td><p>Exchange alias</p></td>
    </tr>
    <tr class="even">
    <td><p>%<em>x</em>s</p></td>
    <td><p>Uses the first <em>x</em> letters of the surname. For example, if <em>x</em> = 2, the first two letters of the surname are used.</p></td>
    </tr>
    <tr class="odd">
    <td><p>%<em>x</em>g</p></td>
    <td><p>Uses the first <em>x</em> letters of the given name. For example, if <em>x</em> = 2, the first two letters of the given name are used.</p></td>
    </tr>
    </tbody>
    </table>


  - **Non-SMTP email address**. The following types of non-SMTP email addresses are supported:
    
      - EX (Legacy DN Proxy Address Prefix DisplayName)
    
      - X.500
    
      - X.400
    
      - MSMail
    
      - CcMail
    
      - Lotus Notes
    
      - Novell GroupWise
    
      - Exchange Unified Messaging proxy address (EUM proxy address)
    

    > [!IMPORTANT]
    > In Exchange, all non-SMTP email addresses are considered custom addresses. Exchange doesn't provide unique dialog boxes or property pages for X.400, GroupWise, or Lotus Notes email address types. If you add a non-SMTP custom email address, you must have the appropriate dynamic-link library (DLL) files. If you don't provide the appropriate DLL files, you won't be able to create a customized email address policy. The following error will be logged in Event Viewer: "The email address description object in the Microsoft Exchange directory for the 'SADF' address type on 'i386' machines are missing."



For detailed instructions about how to create an email address policy, see the following topics:

[Create an Email Address Policy](create-an-email-address-policy-exchange-2013-help.md)

[Create an email address policy by using recipient filters](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)

