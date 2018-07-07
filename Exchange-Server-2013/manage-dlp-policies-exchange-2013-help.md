---
title: 'Manage DLP policies: Exchange 2013 Help'
TOCTitle: Manage DLP policies
ms:assetid: ba81fabd-7f7f-4ef7-968f-ce851ada9d70
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673559(v=EXCHG.150)
ms:contentKeyID: 49315510
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Manage DLP policies

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can view, change, or remove existing data loss prevention (DLP) policies in Microsoft Exchange, using the Exchange Administration Center (EAC) or the Exchange Management Shell.

For additional management tasks related to DLP, see [DLP procedures](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013) or [DLP procedures](https://technet.microsoft.com/en-us/library/jj938003\(v=exchg.150\)) (Exchange Online).

For more information about the Exchange Management Shell, see [Using PowerShell with Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/en-us/library/bb123778\(v=exchg.150\)).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 15-60 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the “Data loss prevention (DLP)” entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

  - For any DLP policy, you can select one of three modes:
    
      -  
        **Enforce**   Rules within the policy are evaluated for all messages and supported file types. Mail flow can be disrupted if data is detected that meets the conditions of the policy. All actions described within the policy are taken.
    
      -  
        **Test DLP policy with Policy Tips**   Rules within the policy are evaluated for all messages and supported file types. Mail flow will not be disrupted if data is detected that meets the conditions of the policy. That is, messages are not blocked. If Policy Tips are configured, they are shown to users.
    
      -  
        **Test DLP policy without Policy Tips**   Rules within the policy are evaluated for all messages and supported file types. Mail flow will not be disrupted if data is detected that meets the conditions of the policy. That is, messages are not blocked. If Policy Tips are configured, they are not shown to users.

  - An individual rule within a DLP policy can have its own mode settings. When the mode of a policy is different than the mode of a rule within that policy, the rule setting has priority and will be evaluated according to its mode.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## What do you want to do?

## View the details of an existing DLP policy

You may need to view the rules and actions of an existing DLP policy that you have already established for your organization. This can be useful if you experience unexpected mail flow issues or if your organization changes the way sensitive information needs to be monitored.

## Use the EAC to view the details within an existing DLP policy

1.  In the EAC, navigate to **Compliance management** \> **Data loss prevention**.

2.  Double-click one of the policies that appear in your list of policies, or highlight one item and click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **Edit DLP policy** page, click **Rules**.


> [!TIP]
> You can create a DLP policy and leave it in a non-activated or disabled mode. In this mode, a policy is not enforced and you can change any predicates, actions, or values associated with its rules before you test or begin enforcing it.



## Use the Shell to view the details within an existing DLP policy

This example returns information about the fictitious DLP policy named Employee Numbers. The command is piped to the **Format-List** cmdlet to display the detailed configuration of the specified DLP policy.

    Get-DlpPolicy "Employee Numbers" | Format-List

For syntax and parameter information, see [Get-DlpPolicy](https://technet.microsoft.com/en-us/library/jj215752\(v=exchg.150\)).

## Change a DLP policy

You can change an existing DLP policy by modifying either the name of the policy or the rules that govern the effects of the policy. An example rule change might include adding custom disclaimer text to a message body and RMS protection for messages sent within a specific domain and that are detected to have sensitive information. If you are using DLP policy templates, keep in mind that these are only one of the features in Exchange 2013 that can help you design and apply a robust policy and compliance system for your messaging environment.

## Use the EAC to change an existing DLP policy

1.  In the EAC, navigate to **Compliance management** \> **Data loss prevention**.

2.  Double-click one of the template-based policies that appear in your list of policies or highlight one item and click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **Edit DLP policy** page, click **Rules**.

4.  To change an existing rule, highlight the rule and click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

5.  To add a new blank rule that you can fully customize, click **New** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon").

6.  To add a rule about sender notification, blocking messages, or allowing overrides, click the arrow next to the **New** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon") icon.

7.  To remove a rule, highlight the rule and click **Delete** ![Delete icon](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon").

8.  Click **Save** to finish modifying the policy and save your changes.

## Use the Shell to change an existing DLP policy

You can specify the action and notification level of a policy using the Exchange Management Shell. This example sets the mode for a fictitious DLP policy named Employee Numbers so that the actions are not enforced and notification messages are not displayed.

    Set-DlpPolicy "Employee Numbers" -Mode Audit

For syntax and parameter information, see [Set-DlpPolicy](https://technet.microsoft.com/en-us/library/jj215778\(v=exchg.150\)).

## Delete a DLP policy

You can permanently remove a DLP policy using the EAC. Once you’ve deleted a policy, it will no longer be enforced and none of the rules and actions will be saved.

Alternatively, you can set the operational state or mode of a policy to **Test DLP policy without Policy Tips**. This stops it from being enforced in your message environment, but preserves the detailed configuration settings of the policy itself. This can be useful if there is a possibility that you will need to enforce the policy again in the future.

## Use the EAC to delete an existing DLP policy

1.  In the EAC, navigate to **Compliance management** \> **Data loss prevention**.

2.  Select the policy you want to remove in your list of policies, and then click **Delete** ![Delete icon](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Delete icon").

## Use the Shell to delete an existing DLP policy

This example removes the fictitious DLP policy named Employee Numbers.

    Remove-DlpPolicy "Employee Numbers"

For syntax and parameter information, see [Remove-DlpPolicy](https://technet.microsoft.com/en-us/library/jj215677\(v=exchg.150\)).

## For more information

[Data loss prevention](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Policy Tips](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)

