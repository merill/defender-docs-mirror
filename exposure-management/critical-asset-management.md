---
layout: Conceptual
title: Overview of critical asset management in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/critical-asset-management
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn about critical asset management in Microsoft Security Exposure Management.
ms.topic: overview
ms.date: 2025-07-30T00:00:00.0000000Z
locale: en-us
document_id: d88569ba-7000-dd85-087a-0bf10f29e678
document_version_independent_id: d88569ba-7000-dd85-087a-0bf10f29e678
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/critical-asset-management.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: critical-asset-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/critical-asset-management.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 9e7a5484-0cd5-6c4f-21a5-79265afe21d6
---

# Overview of critical asset management in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

[Microsoft Security Exposure Management](microsoft-security-exposure-management) streamlines the identification and prioritization of business-critical assets across all domains including devices, identities, and cloud resources, enabling risk-managers and SOC teams to focus efforts where they matter most and reduce overall attack surface risk. With the integration of Defender for Cloud in the Defender portal, asset classification now covers the unified inventory spanning endpoints, cloud environments, and external attack surfaces. Asset classification is driven by proprietary classifiers, which can be fine-tuned manually to reflect organizational context. This article details the underlying mechanisms used for identifying and classifying assets within the Critical Assets Protection framework.

- Microsoft Defender automatically detects and categorizes critical assets, streamlining identification and enabling immediate protection.
- Your security team can prioritize security investigations, posture recommendations, and remediation steps to focus on critical assets and systems first.

Tip

If you arrived here from an alert or incident investigation in Microsoft Defender XDR, critical asset information tells you whether the affected device, identity, or cloud resource is classified as business-critical. Assets marked as critical appear with a crown indicator in the Defender portal. To view or adjust classifications, go to **Exposure management** &gt; **Critical assets** in the [Microsoft Defender portal](https://security.microsoft.com). To manage classifications, see [Review and classify critical assets](classify-critical-assets). If you manage cloud assets in Microsoft Defender for Cloud, see [Critical assets protection in Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/critical-assets-protection).

## Predefined classifications

Security Exposure Management provides an out-of-the-box catalog of predefined critical asset classifications for assets that include devices, identities, and cloud resources across the unified inventory. Predefined classifications include:

- Critical cyber-security assets such as file servers and domain controllers
- Databases with sensitive data
- Identity groups such as Power Users
- User roles like Privileged Role Administrator
- Cloud resources from Azure, AWS, and GCP environments
- External assets discovered through third-party integrations

In addition, you can create custom critical assets to prioritize what your organization considers to be critical when assessing exposure and risk across all asset types in the unified inventory.

## Identifying critical assets

Critical assets can be identified in different ways:

- **Automatically:** The solution employs advanced analytics to automatically identify critical assets within your organization, in line with predefined classifications. This streamlines the identification process, enabling you to pinpoint assets that require heightened protection and immediate attention.
- **With custom queries:** Writing custom queries allows you to pinpoint your organization's "crown jewels" based on your unique criteria. With granular control, you can ensure that you can focus your security efforts precisely where they're needed.
- **Manually:**
    - Review assets in the [device inventory](/en-us/defender-endpoint/machines-view-overview) sorted by criticality level, and identify assets that require attention.
    - Review and approve assets classified automatically but with lower confidence.

## Classifying assets

After business critical assets are defined and identified, asset criticality appears with your asset information. Asset criticality is integrated into other experiences in the Defender portal, such as in advanced hunting, the device inventory, and in attack paths that involve critical assets.

For example, in the **Device Inventory**, a criticality level is shown.

[![Screenshot of the Device inventory window. The image includes an emphasis on the criticality level section.](media/critical-asset-management/device-inventory-criticality-level.png)](media/critical-asset-management/device-inventory-criticality-level.png#lightbox)

In another example, on the [**Attack surface map**](enterprise-exposure-map), as you look for exposure to threats and identify choke points, the halo color surrounding the asset icon, and the crown indicator, visually indicate the high criticality level.

[![Screenshot of an asset viewed in the exposure map in the context of other connections. Two devices on the map show high critical levels.](media/critical-asset-management/attack-surface-exposure-map.png)](media/critical-asset-management/attack-surface-exposure-map.png#lightbox)

## Working with asset classifications

You can create custom asset classifications, add assets manually, modify criticality levels, and edit or turn off custom classifications. Third-party connector data can also trigger automatic critical asset tagging. For step-by-step instructions, see [Review and classify critical assets](classify-critical-assets).

## Reviewing critical assets

The critical asset classification logic uses asset behavior from Microsoft Defender workloads, cloud environments (Azure, AWS, GCP), and third-party integrations. With the integration of Defender for Cloud in the Defender portal, this now includes assets from the unified inventory across all domains. To implement different logic, turn off the rule and create a custom rule suited to your scenarios.

Some assets that match a classification might not meet the criticality threshold. For example, an asset might be a domain controller or a cloud resource, but it might not be deemed critical for your business. Use the asset review feature to add these assets to your defined classification. This feature allows you to include assets based on your organization's specific criticality criteria across the entire unified asset inventory, ensuring all critical assets across devices, identities, and cloud resources are properly managed in one place.

## Critical Asset Protection initiative

The Critical Asset Protection initiative helps prioritize business-critical systems and assets, focusing SOC team efforts on enhancing resiliency, monitoring, and incident response. This initiative is available in the Initiatives section of Exposure Insights in the Microsoft Defender portal.

- The initiative continuously monitors the security resilience of your critical assets, providing real-time insights into the effectiveness of your protection measures. Use the initiative score to compare the security resilience of critical assets across different environments, helping you identify areas that require more focus and improvement.
- The initiative provides visibility into all critical assets within your organization, identifies potential gaps in critical asset discovery, and fine-tunes your classifications accordingly. The initiative consolidates information about critical assets and their security resilience into a single view. This comprehensive report enables you to make informed decisions and take proactive measures to safeguard your critical assets.