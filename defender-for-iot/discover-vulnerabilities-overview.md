---
layout: Conceptual
title: Overview of vulnerability management and weaknesses with Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/discover-vulnerabilities-overview
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: This article describes the vulnerability management and weaknesses features of Microsoft Defender for IoT in the Defender portal.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2024-06-24T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: 5d10ebe9-7e19-ea64-b9d0-95c47e04ddf0
document_version_independent_id: 5d10ebe9-7e19-ea64-b9d0-95c47e04ddf0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/discover-vulnerabilities-overview.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: discover-vulnerabilities-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/discover-vulnerabilities-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 178aa451-ad07-e001-cfb6-32eb5398ba46
---

# Overview of vulnerability management and weaknesses with Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

With vulnerability management, Microsoft Defender for IoT in the Defender portal provides extended coverage for OT networks, gathers OT device data into one place, and displays the data with the other devices on your network.

The OT security administrator proactively manages network exposure based on the vulnerability details and recommended remediation actions.

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Vulnerability management capabilities

The key vulnerability management capabilities are:

| Capability | Description |
| --- | --- |
| Extended vulnerability coverage | Defender for IoT uses detailed OT device firmware information and discovers the device vendor, model, and version to identify known vulnerabilities. |
| [Security recommendations page](/en-us/defender-vulnerability-management/tvm-security-recommendation) | Offers actionable steps to update and mitigate vulnerable products. |
| [Weaknesses page](/en-us/defender-vulnerability-management/tvm-weaknesses) | Includes a detailed list of vulnerabilities like zero-days and known exploits. |
| [Management](/en-us/defender-vulnerability-management/tvm-weaknesses#view-common-vulnerabilities-and-exposures-cve-entries-in-other-places) | You can manage and control the vulnerabilities globally, per tenant or device group, per device from the device page, or per vulnerable product through the Inventory page. |
| [Exception handling](/en-us/defender-vulnerability-management/tvm-security-recommendation#file-for-exception) | Create exceptions for recommendations that can't be patched. |
| [Customizable Vulnerability Notifications](/en-us/defender-endpoint/configure-vulnerability-email-notifications) | Alert key stakeholders with customizable notifications. |
| [Reporting Inaccuracies](/en-us/defender-vulnerability-management/tvm-weaknesses#report-inaccuracy) | Users can report inaccuracies on discovered CVEs or request support for new vulnerabilities. |

## Weaknesses page

The Microsoft Defender portal displays Microsoft Defender for IoT security vulnerabilities in the **Endpoints &gt; Weaknesses** page.

Vulnerabilities are listed based on their publicly registered Common Vulnerability and Exposures(CVEs) ID.

The **Weaknesses** page lists the detected security vulnerabilities across all devices, endpoints, applications and other sources on your network. The data can be filtered according to device groups based on the created sites.

The OT security administrator uses the list of detected vulnerabilities in the **Weaknesses** page to send a remediation request for the relevant team to handle.

Learn more about the [Weaknesses page in the Microsoft Defender Vulnerability Management](/en-us/defender-vulnerability-management/tvm-weaknesses).