---
title: 'Add or remove email addresses for a mailbox: Exchange 2013 Help'
TOCTitle: Add or remove email addresses for a mailbox
ms:assetid: 93e2d9a4-7558-4509-8641-8381a7eb674f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb123794(v=EXCHG.150)
ms:contentKeyID: 49315465
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Add or remove email addresses for a mailbox

 

_**Applies to:** Exchange Online, Exchange Server 2013_


You can configure more than one email address for the same mailbox. The additional addresses are called *proxy addresses*. A proxy address lets a user receive email that’s sent to a different email address. Any email message sent to the user's proxy address is delivered to their primary email address, which is also known as the *primary SMTP address* or the *default reply address*.


> [!IMPORTANT]
> If you're using Office 365 for business, you should add or remove email addresses for user mailboxes in the <A href="https://go.microsoft.com/fwlink/p/?linkid=8347775">Office 365 admin center: Add additional email aliases to a user in Office 365</A>



For additional management tasks related to managing recipients, see the "Recipients documentation" table in [Recipients](recipients-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: 2 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipient Provisioning Permissions" section in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

The procedures in this topic show how to add or remove email addresses for a user mailbox. You can use similar procedures to add or remove email addresses for other recipient types.

## What do you want to do?

## Add an email address to a user mailbox

## Use the EAC to add an email address

1.  In the EAC, navigate to **Recipients** \> **Mailboxes**.

2.  In the list of user mailboxes, click the mailbox that you want to add an email address to, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the mailbox properties page, click **Email Address**.
    

    > [!NOTE]
    > On the <STRONG>Email Address</STRONG> page, the primary SMTP address is displayed in bold text in the address list, with the uppercase <STRONG>SMTP</STRONG> value in the <STRONG>Type</STRONG> column.



4.  Click **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Add Icon"), and then click **SMTP** to add an SMTP email address to this mailbox.
    

    > [!NOTE]
    > SMTP is the default email address type. You can also add Exchange Unified Messaging (EUM) addresses or custom addresses to a mailbox. For more information, see "Change user mailbox properties" in the <A href="manage-user-mailboxes-exchange-2013-help.md">Manage user mailboxes</A> topic.



5.  Type the new SMTP address in the **Email address** box, and then click **OK**.
    
    The new address is displayed in the list of email addresses for the selected mailbox.

6.  Click **Save** to save the change.

## Use the Shell to add an email address

The email addresses associated with a mailbox are contained in the *EmailAddresses* property for the mailbox. Because it can contain more than one email address, the *EmailAddresses* property is known as a *multivalued* property. The following examples show different ways to modify a multivalued property.

This example shows how to add an SMTP address to the mailbox of Dan Jump.

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com"}

This example shows how to add multiple SMTP addresses to a mailbox.

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com","danj@tailspintoys.com"}

For more information about how to use this method of adding and removing values for multivalued properties, see [Modifying multivalued properties](modifying-multivalued-properties-exchange-2013-help.md).

This example shows another way to add email addresses to a mailbox by specifying all addresses associated with the mailbox. In this example, danj@tailspintoys.com is the new email address that you want to add. The other two email addresses are existing addresses. The address with the case-sensitive qualifier `SMTP` is the primary SMTP address. You have to include all email addresses for the mailbox when you use this command syntax. If you don't, the addresses specified in the command will overwrite the existing addresses.

    Set-Mailbox "Dan Jump" -EmailAddresses SMTP:dan.jump@contoso.com,dan.jump@northamerica.contoso.com,danj@tailspintoys.com

For detailed syntax and parameter information, see [Set-Mailbox](https://technet.microsoft.com/en-us/library/bb123981\(v=exchg.150\)).

## How do you know this worked?

To verify that you’ve successfully added an email address to a mailbox, do one of the following:

  - In the EAC, navigate to **Recipients** \> **Mailboxes**, click the mailbox, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

  - On the mailbox properties page, click **Email Address**.

  - In the list of email addresses for the mailbox, verify that the new email address is included.

Or

  - Run the following command in the Shell.
    
        Get-Mailbox <identity> | fl EmailAddresses

  - Verify that the new email address is included in the results.

## Remove an email address from a user mailbox

## Use the EAC to remove an email address

1.  In the EAC, navigate to **Recipients** \> **Mailboxes**.

2.  In the list of user mailboxes, click the mailbox that you want to remove an email address from, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

3.  On the mailbox properties page, click **Email Address**.

4.  In the list of email addresses, select the address you want to remove, and then click **Remove** ![Remove icon](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Remove icon").

5.  Click **Save** to save the change.

## Use the Shell to remove an email address

This example shows how to remove an email address from the mailbox of Janet Schorr.

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janets@corp.contoso.com"}

This example shows how to remove multiple addresses from a mailbox.

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janet.schorr@corp.contoso.com","janets@tailspintoys.com"}

For more information about how to use this method of adding and removing values for multivalued properties, see [Modifying multivalued properties](modifying-multivalued-properties-exchange-2013-help.md).

You can also remove an email address by omitting it from the command to set email addresses for a mailbox. For example, let's say Janet Schorr's mailbox has three email addresses: janets@contoso.com (the primary SMTP address), janets@corp.contoso.com, and janets@tailspintoys.com. To remove the address janets@corp.contoso.com, you would run the following command.

    Set-Mailbox "Janet Schorr" -EmailAddresses SMTP:janets@contoso.com,janets@tailspintoys.com

Because janets@corp.contoso.com was omitted in the previous command, it’s removed from the mailbox.

For detailed syntax and parameter information, see [Set-Mailbox](https://technet.microsoft.com/en-us/library/bb123981\(v=exchg.150\)).

## How do you know this worked?

To verify that you’ve successfully removed an email address from a mailbox, do one of the following:

  - In the EAC, navigate to **Recipients** \> **Mailboxes**, click the mailbox, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

  - On the mailbox properties page, click **Email Address**.

  - In the list of email addresses for the mailbox, verify that the email address isn't included.

Or

  - Run the following command in the Shell.
    
        Get-Mailbox <identity> | fl EmailAddresses

  - Verify that the email address isn't included in the results.

## Use the Shell to add email addresses to multiple mailboxes

You can add a new email address to multiple mailboxes at one time by using the Shell and a comma separated values (CSV) file.

This example imports data from C:\\Users\\Administrator\\Desktop\\AddEmailAddress.csv, which has the following format.

    Mailbox,NewEmailAddress
    Dan Jump,danj@northamerica.contoso.com
    David Pelton,davidp@northamerica.contoso.com
    Kim Akers,kima@northamerica.contoso.com
    Janet Schorr,janets@northamerica.contoso.com
    Jeffrey Zeng,jeffreyz@northamerica.contoso.com
    Spencer Low,spencerl@northamerica.contoso.com
    Toni Poe,tonip@northamerica.contoso.com
    ...

Run the following command to use the data in the CSV file to add the email address to each mailbox specified in the CSV file.

    Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Set-Mailbox $_.Mailbox -EmailAddresses @{add=$_.NewEmailAddress}}


> [!NOTE]
> The column names in the first row of this CSV file (<CODE>Mailbox,NewEmailAddress</CODE>) are arbitrary. Whatever you use for column names, make sure you use the same column names in the Shell command.



## How do you know this worked?

To verify that you’ve successfully added an email address to multiple mailboxes, do one of the following:

  - In the EAC, navigate to **Recipients** \> **Mailboxes**, click a mailbox that you added the address to, and then click **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Edit icon").

  - On the mailbox properties page, click **Email Address**.

  - In the list of email addresses for the mailbox, verify that the new email address is included.

Or

  - Run the following command in the Shell, using the same CSV file that you used to add the new email address.
    
        Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Get-Mailbox $_.Mailbox | fl Name,EmailAddresses}

  - Verify that the new email address is included in the results for each mailbox.


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..


