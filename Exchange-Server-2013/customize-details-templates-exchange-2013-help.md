---
title: 'Customize details templates: Exchange 2013 Help'
TOCTitle: Customize details templates
ms:assetid: b4beeedd-e46f-442e-844a-e8575f95dca0
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.toolbox.detailstemplate(v=EXCHG.150)
ms:contentKeyID: 49090993
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Customize details templates

 

_**Applies to:** Exchange Server 2013_


Use the Details Templates Editor to customize the client-side graphical user interface (GUI) presentation of object properties that are accessed by using address lists in Microsoft Outlook. For example, when a user opens an address list in Outlook, the properties of a particular object are presented as defined by the details template in the Exchange organization. The objects can be customized by changing field sizes, adding or removing fields, adding or removing tabs, and rearranging fields. The layout of these templates may vary by language.

## What do you need to know before you begin?

  - There is no undo option in the details template editor. If you make a mistake, you will need to revert back to the previous version. For more information, see [Restore a details template to the default configuration](restore-a-details-template-to-the-default-configuration-exchange-2013-help.md).

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Details templates" entry in the [Email address and address book permissions](email-address-and-address-book-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Customize the details template

1.  In the **Exchange Toolbox**, click **Details Templates Editor**, and then in the action pane, click **Open Tool**.

2.  In the console tree of the Details Templates Editor, click **Details Templates**.
    
    In the details pane, the following columns are displayed:
    
      - **Language**   This column lists the language in which the template was created.
    
      - **Template Type**   This column lists the type of template that you can customize.
    
      - **Identity**   This column lists the unique identity of the template.
    
      - **Created**   This column lists the date and time that the template was created.
    
      - **Modified**   This column lists the date and time that the template was last modified.

3.  To edit a template, click the template you want, and then, in the action pane, click **Edit**. For example, the **English (United States)** contacts details template is shown in the following figure.
    
    **Default details template as viewed from Outlook 2013**
    
    ![Default details template in Outlook 2007](images/JJ673049.a0af8aca-663d-4702-ab2f-9a342f481cdf(EXCHG.150).gif "Default details template in Outlook 2007")  

4.  After you click **Edit**, there are several tasks you can perform to customize a details template:
    
      - To move an object in the designer pane, select the object, and then drag it to its new location on the template. As you move the object, you are provided with alignment lines.
    
      - To change a label's text, select the label in the design pane. In the properties pane, type the new text in the **Text** box. To create keyboard shortcuts, you can use the ampersand (&) symbol. Place the ampersand (&) before the letter that you want to use as the shortcut.
    
      - To change the size of an object, select the object, and then drag the sizing handles until the object is the shape and size you want.
    
      - To delete an object, select the object, and then press the DELETE key.
        

        > [!NOTE]
        > The Details Templates Editor doesn't contain an <STRONG>Undo</STRONG> button, nor can you use a keyboard shortcut to undo an action. To undo an addition you made to the template, you must use the DELETE key. To undo a deletion, you must reapply the setting. You can also revert to the original settings by exiting the Details Templates Editor without saving your changes. If you want to undo changes after you have saved, you can restore the template. When you restore a template, all customization is lost, and the template is restored to its original configuration. For more information about how to restore the details template, see <A href="restore-a-details-template-to-the-default-configuration-exchange-2013-help.md">Restore a details template to the default configuration</A>.

    
      - To add an "Edit" text boxes, list boxes, multi-valued drop-down boxes, or multi-valued list boxes, in the toolbox pane, drag the object to the design pane. Set the attribute of the object by clicking the attribute drop-down box in the properties pane and then selecting the attribute that will be used by Exchange.
        

        > [!NOTE]
        > You must link the object to an attribute for it to be used by Exchange. In addition, the attribute determines the content that is displayed to the end user in Outlook. If you don't select an attribute, a random attribute is selected automatically.

    
      - To add a group box, drag the object to the design pane. Then, in the properties pane, type a name in the **Text** box. Use group boxes to group similar objects.
    
      - To add a tab to the template, right-click an existing tab, and then click **Add Tab**. A blank tab appears. To name the tab, type the name in the **Text** box in the properties pane.
    
      - To remove a tab from the template, right-click the tab, and then click **Remove Tab**. A warning appears. Click **OK** to confirm that you want to remove the tab.
    
      - To change the tabbing order of the objects on a tab so that users can use the TAB key to navigate the objects in the order you want, select the object in the design pane. Then, in the properties pane, use the **TabIndex** box to change the order.
        

        > [!NOTE]
        > To make sure that users cannot use the TAB key to access the labels of an object (for example <STRONG>Name</STRONG> or <STRONG>Alias</STRONG>), change the order of the labels so that they are last in the tabbing order.



5.  To save changes to the details template, on the **File** menu, click **Save**.

6.  To close the template, on the **File** menu, click **Exit**.

