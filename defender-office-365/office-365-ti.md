---
layout: Conceptual
title: Threat investigation & response capabilities in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/office-365-ti
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.date: 2023-10-10T00:00:00.0000000Z
ms.topic: overview
ms.localizationpriority: medium
ms.assetid: 32405da5-bee1-4a4b-82e5-8399df94c512
ms.collection:
- m365-security
- tier1
ms.custom:
- seo-marvel-apr2020
- sfi-ga-nochange
description: Learn about threat investigation and response capabilities in Microsoft Defender for Office 365 Plan.
ms.service: defender-office-365
locale: en-us
document_id: d378cf18-974e-77c5-4ba9-ad16c05a1cf3
document_version_independent_id: d378cf18-974e-77c5-4ba9-ad16c05a1cf3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/office-365-ti.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: office-365-ti
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/office-365-ti.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 39d1dc51-52fa-0a08-dbe2-58c8476f06da
---

# Threat investigation & response capabilities in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Threat investigation and response capabilities in [Microsoft Defender for Office 365](mdo-about) help security analysts and administrators protect their organization's Microsoft 365 for business users by:

- Making it easy to identify, monitor, and understand cyberattacks.
- Helping to quickly address threats in Exchange Online, SharePoint, OneDrive and Microsoft Teams.
- Providing insights and knowledge to help security operations prevent cyberattacks against their organization.
- Employing [automated investigation and response in Office 365](air-about) for critical email-based threats.

Threat investigation and response capabilities provide insights into threats and related response actions that are available in the Microsoft Defender portal. These insights can help your organization's security team protect users from email- or file-based attacks. The capabilities help monitor signals and gather data from multiple sources, such as user activity, authentication, email, compromised PCs, and security incidents. Business decision makers and your security operations team can use this information to understand and respond to threats against your organization and protect your intellectual property.

## Get acquainted with threat investigation and response tools

Threat investigation and response capabilities in the Microsoft Defender portal at https://security.microsoft.com are a set of tools and response workflows that include:

- Explorer
- Incidents
- [Attack simulation training](attack-simulation-training-simulations)
- [Automated investigation and response](air-about)

### Explorer

Use [Explorer (and real-time detections)](threat-explorer-real-time-detections-about) to analyze threats, see the volume of attacks over time, and analyze data by threat families, attacker infrastructure, and more. Explorer (also referred to as Threat Explorer) is the starting place for any security analyst's investigation workflow.

[![The Threat explorer page](media/7a7cecee-17f0-4134-bcb8-7cee3f3c3890.png)](media/7a7cecee-17f0-4134-bcb8-7cee3f3c3890.png#lightbox)

To view and use this report in the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Explorer**. Or, to go directly to the **Explorer** page, use https://security.microsoft.com/threatexplorer.

#### Office 365 Threat Intelligence connection

This feature is only available if you have an active Office 365 E5 or G5 or Microsoft 365 E5 or G5 subscription or the Threat Intelligence add-on. For more information, see the Office 365 Enterprise E5 product page.

Data from Microsoft Defender for Office 365 is incorporated into Microsoft Defender to conduct a comprehensive security investigation in Office 365 mailboxes and Windows devices.

### Incidents

Use the Incidents list (this is also called Investigations) to see a list of in flight security incidents. Incidents are used to track threats such as suspicious email messages, and to conduct further investigation and remediation.

[![The list of current Threat Incidents in Office 365](media/acadd4c7-d2de-4146-aeb8-90cfad805a9c.png)](media/acadd4c7-d2de-4146-aeb8-90cfad805a9c.png#lightbox)

To view the list of current incidents for your organization in the Microsoft Defender portal at https://security.microsoft.com, go to **Incidents & alerts** &gt; **Incidents**. Or, to go directly to the **Incidents** page, use https://security.microsoft.com/incidents.

### Attack simulation training

Use Attack simulation training to set up and run realistic cyberattacks in your organization, and identify vulnerable people before a real cyberattack affects your business. To learn more, see [Simulate a phishing attack](attack-simulation-training-simulations).

To view and use this feature in the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Attack simulation training**. Or, to go directly to the **Attack simulation training** page, use https://security.microsoft.com/attacksimulator?viewid=overview.

### Automated investigation and response

Use automated investigation and response (AIR) capabilities to save time and effort correlating content, devices, and people at risk from threats in your organization. AIR processes can begin whenever certain alerts are triggered, or when started by your security operations team. To learn more, see [Automated investigation and response (AIR) examples in Microsoft Defender for Office 365 Plan 2](air-examples).

## Threat intelligence widgets

As part of the Microsoft Defender for Office 365 Plan 2 offering, security analysts can review details about a known threat. This is useful to determine whether there are additional preventative measures/steps that can be taken to keep users safe.

[![The Security trends pane showing information about recent threats](media/11e7d40d-139b-4c56-8d52-c091c8654151.png)](media/11e7d40d-139b-4c56-8d52-c091c8654151.png#lightbox)

## How do we get these capabilities?

Microsoft 365 threat investigation and response capabilities are included in Microsoft Defender for Office 365 Plan 2, which is included in Enterprise E5 or as an add-on to certain subscriptions. To learn more, see [Defender for Office 365 Plan 1 vs. Plan 2 cheat sheet](mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet).

## Required roles and permissions

Microsoft Defender for Office 365 uses role-based access control. Permissions are assigned through certain roles in Microsoft Entra ID, the Microsoft 365 admin center, or the Microsoft Defender portal.

Tip

Although some roles, such as Security Administrator, can be assigned in the Microsoft Defender portal, consider using either the Microsoft 365 admin center or Microsoft Entra ID instead. For information about roles, role groups, and permissions, see the following resources:

- [Permissions in the Microsoft Defender portal](mdo-portal-permissions)
- [Microsoft Entra built-in roles](/en-us/entra/identity/role-based-access-control/permissions-reference)
- [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac)

| Activity | Roles and permissions |
| --- | --- |
| Use the Microsoft Defender Vulnerability Management dashboard  View information about recent or current threats | One of the following: <br>- **Global Administrator**^\*^<br>- **Security Administrator**<br>- **Security Reader**<br><br> These roles can be assigned in either Microsoft Entra ID (https://portal.azure.com) or the Microsoft 365 admin center (https://admin.microsoft.com). |
| Use [Explorer (and real-time detections)](threat-explorer-real-time-detections-about) to analyze threats | One of the following: <br>- **Global Administrator**^\*^<br>- **Security Administrator**<br>- **Security Reader**<br><br> These roles can be assigned in either Microsoft Entra ID (https://portal.azure.com) or the Microsoft 365 admin center (https://admin.microsoft.com). |
| View Incidents (also referred to as Investigations)  Add email messages to an incident | One of the following: <br>- **Global Administrator**^\*^<br>- **Security Administrator**<br>- **Security Reader**<br><br> These roles can be assigned in either Microsoft Entra ID (https://portal.azure.com) or the Microsoft 365 admin center (https://admin.microsoft.com). |
| Trigger email actions in an incident  Find and delete suspicious email messages | One of the following: <br>- **Global Administrator**^\*^<br>- **Security Administrator** plus the **Search and Purge** role<br><br> The **Global Administrator**^\*^ and **Security Administrator** roles can be assigned in either Microsoft Entra ID (https://portal.azure.com) or the Microsoft 365 admin center (https://admin.microsoft.com).  The **Search and Purge** role must be assigned in the **Email & collaboration roles** in the Microsoft 365 Defender portal (https://security.microsoft.com). |
| Integrate Microsoft Defender for Office 365 Plan 2 with Microsoft Defender for Endpoint  Integrate Microsoft Defender for Office 365 Plan 2 with a SIEM server | Either the **Global Administrator**^\*^ or the **Security Administrator** role assigned in either Microsoft Entra ID (https://portal.azure.com) or the Microsoft 365 admin center (https://admin.microsoft.com).  --- **plus** ---  An appropriate role assigned in additional applications (such as [Microsoft Defender Security Center](/en-us/windows/security/threat-protection/microsoft-defender-atp/user-roles) or your SIEM server). |
| View email preview/download .eml of Quarantined emails (view/download only Quarantined emails) | One of the following: <br>- **Global Administrator**^\*^<br>- **Security Administrator**<br>- **Security Reader**<br><br> These roles can be assigned in either Microsoft Entra ID (https://portal.azure.com) or the Microsoft 365 admin center (https://admin.microsoft.com). |
| View email preview/download .eml of ANY email in Explorer | One of the following: <br>- **Security Administrator**<br>- **Security Reader**<br><br> These roles can be assigned in either Microsoft Entra ID (https://portal.azure.com) or the Microsoft 365 admin center (https://admin.microsoft.com). |

Important

^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.