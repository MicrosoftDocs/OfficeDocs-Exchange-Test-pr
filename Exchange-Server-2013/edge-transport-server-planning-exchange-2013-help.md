---
title: 'Edge Transport server planning: Exchange 2013 Help'
TOCTitle: Edge Transport server planning
ms:assetid: 3d34de82-58a5-4b30-9978-7d330102eb92
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn641596(v=EXCHG.150)
ms:contentKeyID: 62221565
ms.date: 07/14/2016
mtps_version: v=EXCHG.150
---

# Edge Transport server planning

 

_**Applies to:** Exchange Server 2013_


The Edge Transport server role has been re-introduced in Exchange Service Pack 1. Edge Transport provides improved anti-spam protection for the Exchange organization. The Edge Transport server also applies policies to messages in transport between organizations. This server role is deployed in the perimeter network and outside the Active Directory forest. Edge Transport servers don't have direct access to Active Directory for configuration and recipient information in the way Client Access or Mailbox servers do. The Edge Transport server uses the Active Directory Lightweight Directory Service (AD LDS) to store configuration and recipient information locally.

You can add an Edge Transport server to an existing Exchange 2013 organization. You don't have to perform any additional Active Directory preparation steps when you install the Edge Transport server.


> [!NOTE]
> If you are adding Edge Transport to an existing Exchange 2010 or Exchange 2007 organization, you will need to install specific rollup updates on your legacy servers before installing Exchange 2013 Edge Transport. For details, see <A href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 system requirements</A>.



When you're planning to deploy Edge Transport servers, you should consider the following issues:

  - **Server Capacity**   Planning for server capacity includes planning to conduct performance monitoring of the Edge Transport server. Performance monitoring will help you understand how hard the server is working. This information will determine the capacity of your current hardware configuration.

  - **Transport Features**   The Edge Transport server can provide anti-spam protection at the edge of the network. As part of your planning process, you should determine the anti-spam features that you will enable at the Edge Transport server and how they will be configured.

  - **Security**   The Edge Transport server role is designed to have a minimal attack surface. Therefore, it's important to correctly secure and manage both the physical access and network access to the server. Planning for security will help you make sure that IP connections are only enabled from authorized servers and from authorized users. For more information, see the [Deployment security checklist](deployment-security-checklist-exchange-2013-help.md).
    
    The recommended practice is to put the Edge Transport server within a perimeter network. To make sure that the server can send and receive e-mail and receive recipient and configuration data updates from the Microsoft Exchange EdgeSync service, you must allow communication through the ports that are listed in the following table.
    
    ### Communication port settings for Edge Transport servers
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Network interface</th>
    <th>Open port</th>
    <th>Protocol</th>
    <th>Note</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Inbound from and outbound to the Internet</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>This port is required for mail flow to and from the Internet.</p></td>
    </tr>
    <tr class="even">
    <td><p>Inbound from and outbound to the internal network</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>This port is required for mail flow to and from the Exchange organization.</p></td>
    </tr>
    <tr class="odd">
    <td><p>Local only</p></td>
    <td><p>50389/TCP</p></td>
    <td><p>LDAP</p></td>
    <td><p>This port is used to make a local connection to AD LDS.</p></td>
    </tr>
    <tr class="even">
    <td><p>Inbound from the internal network</p></td>
    <td><p>50636/TCP</p></td>
    <td><p>Secure LDAP</p></td>
    <td><p>This port is required for EdgeSync synchronization.</p></td>
    </tr>
    <tr class="odd">
    <td><p>Inbound from the internal network</p></td>
    <td><p>3389/TCP</p></td>
    <td><p>RDP</p></td>
    <td><p>Opening this port is optional. It provides more flexibility in managing the Edge Transport servers from inside the internal network by letting you use a remote desktop connection to manage the Edge Transport server.</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!NOTE]
    > The Edge Transport server role uses non-standard LDAP ports. The ports specified in this topic are the LDAP communication ports configured when the Edge Transport server role is installed.



  - **EdgeSync**   The recommended deployment process is to create an Edge Subscription to subscribe the Edge Transport server to the Exchange organization. When you create an Edge Subscription, recipient and configuration data is replicated from Active Directory to AD LDS. You subscribe an Edge Transport server to an Active Directory site. Then the Microsoft Exchange EdgeSync service that is running on the Mailbox servers in that site periodically updates AD LDS by synchronizing data from Active Directory. The Edge Subscription process automatically provisions the Send connectors that are required to enable mail flow from the Exchange organization to the Internet through an Edge Transport server. If you're using the recipient lookup or safelist aggregation features on the Edge Transport server, you must subscribe the Edge Transport server to the organization.

## Configure DNS settings for the Edge Transport server role

The Edge Transport server is deployed outside the Exchange organization as a stand-alone server in the perimeter network or as a member of a perimeter network Active Directory domain. You need to manually configure the correct DNS suffix for the Edge Transport server role before you install Exchange 2013. If a DNS suffix isn't configured, setup will fail.

Because the Edge Transport server is deployed in the perimeter network, it has network interfaces that are connected to multiple network segments. Each of these network segments has a unique IP configuration. The network interface that is connected to the external, or public, network segment should be configured to use a public DNS server for name resolution. This enables the server to resolve SMTP domain names to MX resource records and route mail to the Internet.

The network interface that is connected to the internal, or private, network segment should be configured to use a DNS server that can resolve the names of the Mailbox servers in your organization, or should have a Hosts file available. The Edge Transport servers and the Mailbox servers must be able to use DNS host resolution to locate each other.

To enable name resolution of Mailbox servers by Edge Transport servers, use one of the following methods:

  - Manually create resource records for Mailbox servers in a forward lookup zone on the DNS server that's configured on the internal network adapter of the Edge Transport server.

  - Edit the Hosts file on the Edge Transport server to include the Host records for the Mailbox servers. The Hosts file is a local text file in the same format as the 4.3 Berkeley Software Distribution (BSD) UNIX /etc/hosts file. This file maps host names to IP addresses, and the file is stored in the \\%Systemroot%\\System32\\Drivers\\Etc folder.

To enable name resolution of Edge Transport servers by Mailbox servers, use one of the following methods:

  - Manually create resource records for Edge Transport servers in a forward lookup zone on the DNS server that's configured on the Mailbox server.

  - To include the Host records for the Edge Transport servers, edit the Hosts file on the Mailbox servers that are located in the subscribed Active Directory site.

Follow these steps to configure DNS settings for the Edge Transport server:

1.  Verify that the DNS server settings for each network interface are correct for the network segment.

2.  Configure the DNS suffix for the Edge Transport server name using the following steps:
    
    1.  Open Control Panel, and then choose **System Properties**.
    
    2.  Choose the **Computer Name** tab.
    
    3.  Choose **Change**.
    
    4.  On the **Computer Name Changes** page, click **More**.
    
    5.  In the **Primary DNS suffix of this computer** field, type a DNS domain name and suffix for the Edge Transport server.
    
    This name can't be changed after the Edge Transport server role is installed.

## Override DNS settings

You might need to override the default DNS settings on the Exchange server so mail can be routed and delivered correctly. To do this, modify the **Internal DNS Lookups** and **External DNS Lookups** settings of the transport server's properties. These settings override the settings on the network adapter to route e-mail messages.

