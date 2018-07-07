---
title: 'Set the default language on a dial plan: Exchange 2013 Help'
TOCTitle: Set the default language on a dial plan
ms:assetid: 7a1d2e7e-4053-40af-9ec1-ec714df12ad4
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998914(v=EXCHG.150)
ms:contentKeyID: 49315447
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Set the default language on a dial plan

 

_**Applies to:** Exchange Server 2013, Exchange Server 2016_


You can set the default language for a Unified Messaging (UM) dial plan. Each dial plan you create will initially use English (en-US) as the default language. The English (en-US) language pack is installed on all versions of Microsoft Exchange Server 2013 and can't be removed.

If you want to select another language as the default language, for example, German (de-DE), you must first download the German UM language pack .exe file from [Exchange Server 2013 UM Language Packs](https://go.microsoft.com/fwlink/p/?linkid=266542) and install that language pack on the Mailbox server by using the UMLanguagePack.de-de.exe installation file. After you've installed the language pack, you can set the default language to a language other than English (en-US) on your UM dial plans.

For additional tasks related to UM languages, see [UM languages, prompts, and greetings procedures](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 1 minute.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM dial plans" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the EAC to set the default language on a UM dial plan

1.  In the EAC, navigate to **Unified Messaging** \> **UM dial plans**.

2.  In the list view, select the UM dial plan that you want to modify, and then, on the toolbar, click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the **UM dial plan** page, click **Configure**.

4.  On the **Settings** page, under **Audio language**, select the language you want to set from the drop-down list.

5.  Click **Save** to accept your changes.

## Use the Shell to set the default language on a UM dial plan

This example sets the default language on a UM dial plan named `MyUMDialPlan` to German.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage de-DE

This example sets the default language on a UM dial plan named `MyUMDialPlan` to Japanese.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage ja-JP

This example sets the default language on a UM dial plan named `MyUMDialPlan` to Australian English.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage en-AU

