---
title: 'Multi-tenancy in Exchange 2013: Exchange 2013 Help'
TOCTitle: Multi-tenancy in Exchange 2013
ms:assetid: df09257d-dd98-4f59-b830-1818cedda15c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ862352(v=EXCHG.150)
ms:contentKeyID: 50182057
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Multi-tenancy in Exchange 2013

 

_**Applies to:** Exchange Online, Exchange Server, Exchange Server 2013_


A multi-tenant (hosted) Exchange 2013 deployment is defined as one where the Exchange organization is configured to host multiple and discrete organizations or business units (the tenants) that ordinarily don’t share email, data, users, global address lists (GALs), or other commonly used Exchange objects. This sharing of hardware, software and resources (all while maintaining a logical separation between tenants), allows organizations to leverage the simplicity of a standard Exchange deployment while providing multi-tenant functionality and services to meet their hosting needs.

## Multi-tenancy in Exchange 2013 organizations

In Exchange 2013, we continue to support hosting by using a standard, on-premises Exchange installation similar to the approach used in Exchange 2010 Service Pack 2 (SP2). We discontinued the `/hosting` mode switch and are emphasizing the use of address book policies (ABPs) in combination with hosting management solutions and automation tools provided by approved Independent Software Vendors (ISVs). These solutions are built on a framework of Microsoft-approved configuration guidelines and practices and will offer Exchange organizations an easier, more robust way to provide hosting services and features.

Exchange 2013 supports multi-tenancy by leveraging the following primary components and features:

  - **Active Directory**   Instead of having separate *ExchangeOrganization* Active Directory containers for each business unit in a multi-tenant Exchange organization, Exchange 2013 multi-tenancy is supported by using a single *ExchangeOrganization* Active Directory container. This allows for a simpler Active Directory structure and reduces the likelihood of Active Directory-related permission problems.
    
    To learn more about Active Directory changes in Exchange 2013, see [Active Directory](active-directory-exchange-2013-help.md).

  - **Address book policies (ABPs)**   Introduced in Exchange 2010 SP2, ABPs are used in Exchange 2013 to control user access to an address list, the global address list (GAL), and an offline address books (OABs) in the Exchange organization. ABPs group these different Active Directory objects into a single, virtual object that can be assigned to individual users and to create a logical grouping of these resources along a multi-tenant organizational structure. ABP functionality in Exchange 2013 is similar to what it was in Exchange 2010 SP2.
    
    To learn more about ABPs in Exchange 2013, see [Address book policies](address-book-policies-exchange-2013-help.md).

  - **Hosting management solutions**   Some administrators using Exchange 2013 to provide a hosted Exchange solution will benefit from using a customized hosting management approach. Due to some limitations of the Exchange Administration Center (EAC), Microsoft works with third-party vendors to assist them in the development of control panel and automation solutions that are in compliance with the guidelines and approved framework for hosted Exchange 2013 organizations. We recommend that organizations configuring a hosted Exchange solution leverage these tools to manage their hosted organizations where circumstances require it.
    
    To learn more about hosted management solutions, including validated solution vendors, see [Exchange Server 2013 hosting and multi-tenancy solutions and guidance](https://go.microsoft.com/fwlink/?linkid=275036)

