---
title: 'Create a custom DLP policy: Exchange 2013 Help'
TOCTitle: Create a custom DLP policy
ms:assetid: b3299a39-9663-41e4-b76e-9d2f7879d486
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150550(v=EXCHG.150)
ms:contentKeyID: 47560077
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Create a custom DLP policy

 

_**Applies to:** Exchange Online, Exchange Server 2013_


A custom data loss prevention (DLP) policy allows you to establish conditions, rules, and actions that can help meet the specific needs of your organization, and which may not be covered in one of the pre-existing DLP templates.

The rule conditions that are available to you in a single policy include all the traditional transport rules in addition to the sensitive information types presented in [What the sensitive information types in Exchange look for](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md). For more information about transport rules, see [Mail flow rules (transport rules) in Exchange 2013](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) or [Mail flow rules (transport rules) in Exchange Online](https://technet.microsoft.com/en-us/library/jj919238\(v=exchg.150\)) (Exchange Online).


> [!WARNING]
> You should enable your DLP policies in test mode before running them in your production environment. During such tests, it is recommended that you configure sample user mailboxes and send test messages that invoke your test policies in order to confirm the results. for more information about testing, see <A href="test-a-mail-flow-rule-exchange-2013-help.md">Test a mail flow rule</A>.



For additional management tasks related to creating a custom DLP policy, see [DLP procedures](dlp-procedures-exchange-2013-help.md)(Exchange 2013) or [DLP procedures](https://technet.microsoft.com/en-us/library/jj938003\(v=exchg.150\)) (Exchange Online).

## What do you need to know before you begin?

  - Estimated time to complete: 60 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the “Data loss prevention (DLP)” entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

  - In order to create a new custom DLP policy, you must follow the installation instructions for Exchange 2013. For more information about deployment, see [Planning and deployment](planning-and-deployment-for-exchange-2013-installation-instructions.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!NOTE]
> Due to the variances in customer environments, Microsoft Customer Support Services (CSS) cannot participate in the development or testing of custom Regular Expression scripts (“RegEx scripts”). For RegEX custom script development, testing and debugging, Office 365 customers will need to rely upon internal IT resources. Alternatively, Office 365 customers may choose to use an external consulting resource such as Microsoft Consulting Services (MCS). Regardless of the script development resource, CSS EXO and EOP support engineers are not available to assist customers with custom RegEx script inquiries.




> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the EAC to create a custom DLP policy without any existing rules

1.  In the EAC, navigate to **Compliance management** \> **Data loss prevention**. Any existing policies that you have configured are shown in a list.

2.  Click the arrow that is beside the **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") icon, and select **New custom policy**.
    

    > [!IMPORTANT]
    > If you click <STRONG>Add</STRONG> <IMG title="Add Icon" alt="Add Icon" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif"> icon instead of the arrow, you will create a new policy based on a template. For more information about using templates, see <A href="how-to-new-dlp-data-loss-prevention-policy-template.md">Create a DLP policy from a template</A>.



3.  On the **New custom policy** page, complete the following fields:
    
    1.  **Name**   Add a name that will distinguish this policy from others.
    
    2.  **Description**   Add an optional description that summarizes this policy.
    
    3.  **Choose a state**   Select the mode or state for this policy. The new policy is not fully enabled until you specify that it should be. The default mode for a policy is test without notifications.

4.  Click **Save** to finish creating the new policy reference information. The policy is added to the list of all policies that you have configured, although there are not yet any rules or actions associated with this new custom policy.

5.  Double-click the policy that you just created or select it and click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

6.  On the **Edit DLP policy** page, click **Rules**.
    
    Click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") to add a new blank rule. You can establish conditions using all the traditional transport rules in addition to the sensitive information types.
    
    In order to avoid confusion, supply a unique name for each part of your policy or rule when you have the option to provide your own character string. There are several options additional options available to you:
    
    1.  Click the arrow that is beside the **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") icon to add a rule about sender notification or allowing overrides.
    
    2.  To remove a rule, highlight the rule and click **Delete** ![Delete icon](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon").
    
    3.  Click **More options** ![More Options Icon](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "More Options Icon") to add additional conditions and actions for this rule including time-bound limits of enforcement or effects on other rules in this policy.

7.  Click **Save** to finish modifying the policy and save your changes.

DLP policy templates are one type of feature Microsoft Exchange that can help you design and apply a robust policy and compliance system for your messaging environment. For more information about compliance features, see [Messaging policy and compliance](messaging-policy-and-compliance-exchange-2013-help.md) (Exchange 2013) or [Security and compliance for Exchange Online](https://technet.microsoft.com/en-us/library/jj200706\(v=exchg.150\)).

## For more information

[Data loss prevention](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Mail flow rules (transport rules) in Exchange 2013](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange 2013

[Mail flow rules (transport rules) in Exchange Online](https://technet.microsoft.com/en-us/library/jj919238\(v=exchg.150\)) Exchange Online

[Integrating sensitive information rules with transport rules](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

