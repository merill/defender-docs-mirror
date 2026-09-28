---
layout: Conceptual
title: Prioritize, investigate and remediate vulnerabilities with Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/prioritize-vulnerabilities
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to review OT vulnerabilities, investigate affected devices, and take recommended remediation actions in Microsoft Defender for IoT in the Defender portal.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 6a560bc9-1845-fc82-2df4-b001f93ac976
document_version_independent_id: 6a560bc9-1845-fc82-2df4-b001f93ac976
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/prioritize-vulnerabilities.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: prioritize-vulnerabilities
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/prioritize-vulnerabilities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 2695b07d-ec92-b1aa-2d25-3f3f1fdca0d9
---

# Prioritize, investigate and remediate vulnerabilities with Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

With vulnerability management, Microsoft Defender for IoT in the Defender portal provides extended coverage for operational technology (OT) networks, gathers OT device data into one place, and displays the data with the other devices on your network.

In this article, you learn how to investigate vulnerabilities and take recommended remediation actions. Learn more about how Defender for IoT discovers vulnerabilities in the [vulnerability discovery overview](discover-vulnerabilities-overview).

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Investigate vulnerabilities

To investigate vulnerabilities and review recommended remediation actions, follow these steps:

1. In the Defender portal, select **Endpoints &gt; Vulnerability management &gt; Weaknesses**.
2. Set the filter settings as needed. If device groups are created for your sites, you can use them filter the weaknesses page.

    1. Select **Filter by device groups**.
    2. Select a device group.
    3. Select **Apply**.
3. Select a Common Vulnerabilities and Exposures (CVE) ID.

    A side panel opens with the CVE ID as the title, and the **Vulnerability details** tab visible. You can also select the **Exposed devices** and **Affected software** tabs.
4. Select **Go to related security recommendation**.

    The **Security recommendations** page opens, filtered to show the CVE you're investigating.
5. Select a recommendation. A side panel opens. Do one of the following:

    - Select **Request remediation** and follow the [Request remediation instructions](/en-us/defender-vulnerability-management/tvm-remediation#request-remediation). This sends a request to the relevant team to perform the remediation.
    - Select **Exception options** and fill in the details. For more information, see [justification for an exception](/en-us/defender-vulnerability-management/tvm-security-recommendation#explore-security-recommendation-options). To complete, select **Submit**.