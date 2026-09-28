---
layout: Conceptual
title: Configure automated investigation and remediation capabilities - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-automated-investigations-remediation
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Set up your automated investigation and remediation capabilities in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.subservice: edr
author: paulinbar
ms.author: painbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-edr
ms.topic: how-to
ms.reviewer: ramarom, evaldm, isco, mabraitm, chriggs
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 3554c317-1a30-5ab4-6208-4d24d16645ff
document_version_independent_id: 3554c317-1a30-5ab4-6208-4d24d16645ff
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-automated-investigations-remediation.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-automated-investigations-remediation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-automated-investigations-remediation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 61dae4d3-11de-fe63-d6f5-41edf2e672c0
---

# Configure automated investigation and remediation capabilities - Microsoft Defender for Endpoint | Microsoft Learn

If your organization is using [Defender for Endpoint](microsoft-defender-endpoint) (or [Defender for Business](/en-us/defender-business/mdb-overview)), [automated investigation and remediation capabilities](automated-investigations) can save your security operations team time and effort. As outlined in [Enhance your SOC with Microsoft Defender for Endpoint automatic investigation and remediation](https://techcommunity.microsoft.com/t5/microsoft-defender-atp/enhance-your-soc-with-microsoft-defender-atp-automatic/ba-p/848946), these capabilities mimic the ideal steps that a security analyst takes to investigate and remediate threats. For more information, see [Automated investigation and remediation](automated-investigations).

Important

As of September 1, 2026, Automated Investigation and Response (AIR) will no longer run as a separate investigation experience or be available for manual triggering in Microsoft Defender.

AIR detection and response capabilities are already included in Microsoft Defender's default antivirus protection stack and run automatically. For on-demand investigations, run a full antivirus scan as needed.

If you're using Defender for Endpoint, you can specify an automation level so that when a threat is detected on a device, the detected threat can be remediated automatically or only upon approval by your security team. You can configure automated investigation and remediation with device groups.

Note

In Defender for Business, automated investigation is configured automatically. See [Review settings for advanced features in Defender for Business](/en-us/defender-business/mdb-configure-security-settings#review-settings-for-advanced-features).

## Set up device groups

To create device groups and configure automation levels in the Microsoft Defender portal, follow these steps:

1. In the [Microsoft Defender portal](https://security.microsoft.com), on the **Settings** page, under **Permissions**, select **Device groups**.
2. Select **+ Add device group**.
3. Create at least one device group, as follows:

    - Specify a name and description for the device group.
    - In the **Automation level list**, select a level, such as **Full - remediate threats automatically**. The automation level determines whether remediation actions are taken automatically, or only upon approval. To learn more, see [Automation levels in automated investigation and remediation](automation-levels).
    - In the **Members** section, use one or more conditions to identify and include devices.
4. Select **Done** when you're finished setting up your device group.

Note

The **Automated Investigation** option has been removed from the advanced features setting in Defender for Endpoint. Automated investigation is now enabled by default.