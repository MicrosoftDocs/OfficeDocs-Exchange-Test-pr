---
title: 'Account setup in Outlook for iOS and Android using Basic authentication: Exchange 2013 Help'
TOCTitle: Account setup in Outlook for iOS and Android using Basic authentication
ms:assetid: 013dbe8c-30de-4c9c-baa9-75081b9229e8
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Mt829322(v=EXCHG.150)
ms:contentKeyID: 74518349
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
---

# Account setup in Outlook for iOS and Android using Basic authentication

 

_**Applies to:** Exchange Server 2013_


**Summary:** How users in your Exchange 2013 organization can quickly set up their Outlook for iOS and Android accounts using Basic authentication.

Outlook for iOS and Android offers Exchange administrators the ability to "push" account configurations to their on-premises users who use basic authentication via the ActiveSync protocol. This capability works with any Mobile Device Management (MDM) provider who uses the [Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/introduction/intro.html) channel for iOS or the [Android in the Enterprise](https://developer.android.com/samples/apprestrictions/index.html) channel for Android.

For on-premises users enrolled in Microsoft Intune, you can deploy the account configuration settings using Intune in the Azure Portal.

Once an account configuration has been created and the user enrolls their device, Outlook for iOS and Android will detect that an account is "Found" and will then prompt the user to add the account. The only information the user needs to enter to complete the setup process is their password. Then, the user's mailbox content will load and the user can begin using the app.

The following images show an example of the end-user setup process after Outlook for iOS and Android has been configured in Intune in the Azure Portal.

![Account setup for Outlook for iOS and Android on-premises](images/Mt829322.04bd56f2-5c45-4268-8762-436994acd656(EXCHG.150).png "Account setup for Outlook for iOS and Android on-premises")

## Create an app configuration policy for Outlook for iOS and Android using Microsoft Intune

If you are using Microsoft Intune as your mobile device management provider, the following steps will allow you to deploy account configuration settings for your on-premises mailboxes that leverage basic authentication with the ActiveSync protocol. Once the configuration is created, you can assign the settings to groups of users, as detailed in the next section, Assign configuration settings.


> [!NOTE]
> If users in your organization use both iOS and Android for Work devices, you'll need to create a separate app configuration policy for each platform.



1.  Sign in to the Azure portal.

2.  Select **More Services \> Monitoring + Management \> Intune**.

3.  On the **Mobile apps** blade of the Manage list, select **App configuration policies**.

4.  On the **App configuration policies** blade, choose **Add**.

5.  On the **Add app configuration** blade, enter a **Name**, and optional **Description** for the app configuration settings.

6.  For **Device enrollment** type, choose **Managed devices**.

7.  For **Platform**, choose **iOS** or **Android for Work**.

8.  Choose **Associated apps**, and then, on the **Targeted apps** blade, choose **Microsoft Outlook**.

9.  Click **OK** to return to the **Add app configuration** blade.

10. Choose **Configuration settings**. On the **Configuration settings** blade, define the key value pairs that will supply configurations for Outlook for iOS and Android. The key value pairs you enter are defined later in this article, in the section Key value pairs.
    

    > [!NOTE]
    > To enter the key value pairs, you have a choice between using the configuration designer or entering an XML property list.



11. When you are done, choose **OK**.

12. On the **Add app configuration** blade, choose **Create**.

The newly created configuration policy will be displayed on the **App configuration policies** blade.

## Assign configuration settings

You assign the settings you created in the previous section to groups of users in Azure Active Directory. When a user has the Microsoft Outlook app installed, the app will be managed by the settings you have specified. To do this:

1.  On the **Mobile apps** blade of the Intune mobile application management dashboard, choose **App configuration policies**.

2.  From the list of app configuration policies, select the one you want to assign, and then choose **Assignments**.

3.  On the **Assignments** blade, choose **Select groups**.

4.  On the **Select groups** blade, select the Azure AD group to which you want to assign the app configuration policy, then choose **Select**, and then **Save**.

## Key value pairs

When you create an app configuration policy in the Azure Portal or through your MDM provider, you will need the following key value pairs:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Key</th>
<th>Values</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailAccountName</p></td>
<td><p>This value specifies the display name email account as it will appear to users on their devices .</p>
<p><strong>Value type</strong>: String</p>
<p><strong>Accepted values</strong>: Display Name</p>
<p><strong>Default if not specified</strong>: &lt;blank&gt;</p>
<p><strong>Example</strong>: user</p>
<p><strong>Intune Token*</strong>: {{username}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.EmailAddress</p></td>
<td><p>This value specifies the email address to be used for sending and receiving mail.</p>
<p><strong>Value type</strong>: String</p>
<p><strong>Accepted values</strong>: Email address</p>
<p><strong>Default if not specified</strong>: &lt;blank&gt;</p>
<p><strong>Example</strong>: user@companyname.com</p>
<p><strong>Intune Token*</strong>: {{mail}}</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailUPN</p></td>
<td><p>This value specifies the User Principal Name or username for the email profile that will be used to authenticate the account.</p>
<p><strong>Value type</strong>: String</p>
<p><strong>Accepted values</strong>: UPN Address or username</p>
<p><strong>Default if not specified</strong>: &lt;blank&gt;</p>
<p><strong>Example</strong>: userupn@companyname.com</p>
<p><strong>Intune Token*</strong>: {{userprincipalname}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.ServerAuthentication</p></td>
<td><p>This value specifies the authentication method for the user.</p>
<p><strong>Value type</strong>: String</p>
<p><strong>Accepted values</strong>: 'Username and Password'; 'Certificates'</p>
<p><strong>Default if not specified</strong>: 'Username and Password'</p>
<p><strong>Example</strong>: 'Username and Password'</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.ServerHostName</p></td>
<td><p>This value specifies the host name of your Exchange server.</p>
<p><strong>Value type</strong>: String</p>
<p><strong>Accepted values</strong>: ActiveSync FQDN</p>
<p><strong>Default if not specified</strong>: &lt;blank&gt;</p>
<p><strong>Example</strong>: mail.companyname.com</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.AccountDomain</p></td>
<td><p>This value specifies the user’s account domain.</p>
<p><strong>Value type</strong>: String</p>
<p><strong>Accepted values</strong>: Domain</p>
<p><strong>Default if not specified</strong>: &lt;blank&gt;</p>
<p><strong>Example</strong>: companyname</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.AccountType</p></td>
<td><p>This value specifies the account type being configured based on the authentication model.</p>
<p><strong>Value type</strong>: String</p>
<p><strong>Accepted values</strong>: BasicAuth</p>
<p><strong>Default if not specified</strong>: BasicAuth</p>
<p><strong>Example</strong>: BasicAuth</p></td>
</tr>
</tbody>
</table>


**\*** Microsoft Intune users can use tokens that will expand to the correct value according to the MDM enrolled user. See [Add app configuration policies for managed iOS devices](https://docs.microsoft.com/en-us/intune/app-configuration-policies-use-ios) for more information.

