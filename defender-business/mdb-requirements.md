---
layout: Conceptual
title: Requirements for Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-requirements
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Microsoft Defender for Business license, hardware, and software requirements
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2025-09-11T00:00:00.0000000Z
ms.reviewer: nehabha
ms.collection:
- SMB
- m365-security
- m365solution-mdb-setup
- highpri
- tier1
locale: en-us
document_id: 68a0527e-4627-39c1-2859-713e250d07a7
document_version_independent_id: 68a0527e-4627-39c1-2859-713e250d07a7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-requirements.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-requirements
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-requirements.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/82f69bd7-5cb0-4163-9fd6-9103bb1a8352
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/f003597a-dab2-429a-8639-1d2acd9c0371
platformId: 57fb0a7b-91ee-c3ba-941a-2856314cb60c
---

# Requirements for Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

This article describes the requirements for Defender for Business.

## What to do

1. Review the requirements and make sure you meet them.
2. Proceed to your next steps.

## Review the requirements

The following table lists the basic requirements you need to configure and use Defender for Business.

| Requirement | Description |
| --- | --- |
| Subscription | Microsoft 365 Business Premium or Defender for Business (standalone).  For more information, see [How to get Defender for Business](get-defender-business). |
| Datacenter | One of the following datacenter locations: <br>- European Union<br>- United Kingdom<br>- United States<br>- Australia |
| User accounts | - User accounts are created in the Microsoft 365 admin center (https://admin.microsoft.com).<br>- Licenses for Defender for Business (or Microsoft 365 Business Premium) are assigned in the Microsoft 365 admin center.<br><br> To get help with this task, see [Add users and assign licenses](mdb-add-users). |
| Permissions | To use the Microsoft Defender portal to view or manage devices and security policies, users must have an appropriate [role assigned in Microsoft Entra ID](mdb-roles-permissions): <br>- Security Reader - Security Administrator<br><br> To learn more, see [Roles and permissions in Defender for Business](mdb-roles-permissions). |
| Browser | Microsoft Edge or Google Chrome |
| Client computer operating system | To manage devices in the Microsoft Defender portal, your devices must be running one of the following operating systems: <br>- Windows 10 or 11 Business<br>- Windows 10 or 11 Professional<br>- Windows 10 or 11 Enterprise<br>- Mac (the three most-current releases are supported)<br><br> Make sure that [KB5006738](https://support.microsoft.com/topic/october-26-2021-kb5006738-os-builds-19041-1320-19042-1320-and-19043-1320-preview-ccbce6bf-ae00-4e66-9789-ce8e7ea35541) is installed on the Windows devices. |
| Mobile devices | To onboard mobile devices, such as iOS or Android OS, you can use [Mobile threat defense capabilities](mdb-mtd) or Microsoft Intune.  For more information about onboarding devices, including requirements for mobile threat defense, see [Onboard devices to Microsoft Defender for Business](mdb-onboard-devices). |
| Server license | To onboard a device running Windows Server or Linux Server, you need another license, such as [Microsoft Defender for Business servers](get-defender-business#how-to-get-microsoft-defender-for-business-servers) (see note 1 below). |
| Server requirements | Windows Server endpoints must meet the [requirements for Defender for Endpoint](/en-us/defender-endpoint/minimum-requirements#hardware-and-software-requirements), and enforcement scope must be turned on. <br>1. In the Microsoft Defender portal, go to **Settings** &gt; **Endpoints** &gt; **Configuration management** &gt; **Enforcement scope**.<br>2. Select **Use MDE to enforce security configuration settings from MEM**, select **Windows Server**.<br>3. Select **Save**.<br><br> Linux Server endpoints must meet the [prerequisites for Microsoft Defender for Endpoint on Linux](/en-us/defender-endpoint/microsoft-defender-endpoint-linux#prerequisites). |

Note

1. To onboard servers, we recommend using [Microsoft Defender for Business servers](get-defender-business#how-to-get-microsoft-defender-for-business-servers). Alternately, you could use [Microsoft Defender for Servers Plan 1 or Plan 2](/en-us/azure/defender-for-cloud/plan-defender-for-servers). For more information, see [Onboard devices to Microsoft Defender for Business](mdb-onboard-devices).
2. [Microsoft Entra ID](/en-us/entra/fundamentals/what-is-entra) is used to manage user permissions and device groups. Microsoft Entra ID is included in your Defender for Business subscription.

    - If you don't have a Microsoft 365 subscription before you start your trial, Microsoft Entra ID is provisioned for you during the activation process.
    - If you do have another Microsoft 365 subscription when you start your Defender for Business trial, you can use your existing Microsoft Entra service.
3. Security defaults are included in Defender for Business. If you prefer to use Conditional Access policies instead, you need Microsoft Entra ID P1 or P2 (P1 is included in [Microsoft 365 Business Premium](/en-us/microsoft-365/business-premium/m365bp-overview)). For more information, see [Multifactor authentication in Microsoft 365](/en-us/microsoft-365/admin/security-and-compliance/multi-factor-authentication-microsoft-365).