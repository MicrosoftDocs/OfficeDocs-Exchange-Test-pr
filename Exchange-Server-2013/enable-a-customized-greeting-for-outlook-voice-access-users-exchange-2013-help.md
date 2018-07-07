---
title: 'Enable a customized greeting for Outlook Voice Access users: Exchange 2013 Help'
TOCTitle: Enable a customized greeting for Outlook Voice Access users
ms:assetid: abd418ec-2c65-4720-859d-c11a2698dc06
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124125(v=EXCHG.150)
ms:contentKeyID: 50067633
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Enable a customized greeting for Outlook Voice Access users

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


By default, each Unified Messaging (UM) dial plan uses a standard .wav file for the welcome greeting that’s played to callers, including Outlook Voice Access users who dial in to an Outlook Voice Access number that’s been configured. However, you can create a .wav or .wma file for the welcome greeting, and then enable it on the UM dial plan.

For example, you might want to change the default welcome greeting and instead provide a welcome greeting that's specific to your company, such as "Welcome to Outlook Voice Access for Woodgrove Bank." To do this, you record the customized welcome greeting and save it as a .wav or .wma file. Then you configure the dial plan to use the customized welcome greeting.

For more information about the menu options available for Outlook Voice Access users, see the Quick Reference Guide for Outlook Voice Access, which is available from the [Microsoft Download Center](https://go.microsoft.com/fwlink/p/?linkid=272767).

For additional management tasks related to UM dial plans, see [UM dial plan procedures](um-dial-plan-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM dial plans" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to enable a customized welcome greeting

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**.

2.  In the list view, select the UM dial plan that you want to modify, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM dial plan** page, click **Configure**.

4.  In **Outlook Voice Access**, under **Welcome greeting**, click **Change**, and then click **Browse** to locate the greeting file.
    

    > [!IMPORTANT]
    > The file you use for the welcome greeting must be a .wav or .wma file.



5.  After you've located the file, click **Open**, and then click **Save**.

## Use the Shell to enable a customized welcome greeting

This example enables a welcome greeting that uses the C:\\UMPrompts\\welcome.wav file on a UM dial plan named `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename c:\UMPrompts\welcome.wav

