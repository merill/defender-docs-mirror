---
layout: Conceptual
title: Start using Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/get-started-exposure-management
author: dlanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to start using the Microsoft Security Exposure Management dashboard to resolve prioritized exposure risks and monitor internet-facing assets.
ms.topic: overview
ms.date: 2026-06-28T00:00:00.0000000Z
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 0dfbb923-2ac7-7b27-763a-b0e5aa1bf620
document_version_independent_id: 0dfbb923-2ac7-7b27-763a-b0e5aa1bf620
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/get-started-exposure-management.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: get-started-exposure-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/get-started-exposure-management.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 8859f048-bc15-90ae-a4c0-fb49c985167a
---

# Start using Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

The [Microsoft Security Exposure Management](microsoft-security-exposure-management) dashboard in the Microsoft Defender portal gives security teams a consolidated, action-oriented view of exposure risk. It consolidates signals from cloud resources and devices, combining internet exposure vulnerabilities, security misconfigurations, and broader risk factors into a single experience, and organizes work around two core actions: **Resolve Now** and **Monitor Exposure**.

## Access Microsoft Security Exposure Management

Microsoft Security Exposure Management is integrated into the Microsoft Defender portal at https://security.microsoft.com. Navigate to **Exposure Management** &gt; **Overview** to open the dashboard.

Before you start, review [Prerequisites and support](prerequisites) for licensing, permissions, and environment requirements.

[![Screenshot of the Exposure Management Overview dashboard showing Resolve Now and Monitor Exposure sections.](media/get-started-exposure-management/exposure-management-overview.png)](media/get-started-exposure-management/exposure-management-overview.png#lightbox)

## Resolve Now

The **Resolve Now** section surfaces prioritized, actionable items across three categories, focused on internet-exposed and business-critical assets:

- **Patch** — Software updates that address known vulnerabilities, prioritized by internet exposure and business criticality.
- **Mitigate** — Risks you can't immediately patch (primarily zero-day vulnerabilities) with suggested compensating controls.
- **Fix** — Misconfigurations and security weaknesses, particularly around internet-exposed cloud assets that increase your attack surface.

Select any item to drill into the details and follow the linked remediation workflows.

## Monitor Exposure

The **Monitor Exposure** section provides a real-time view of your organization's external attack surface and security posture across domains.

### Internet Exposed Resources

The **Internet Exposed Resources** table shows the breakdown of your internet-facing assets by type: cloud assets, devices, and shadow resources. Use this view to quickly understand the external attack surface where your assets are visible to the internet.

### Domain initiative scores

Domain initiative scores show your organization's current security posture as a percentage versus a target score, across five domains: Code, Endpoint, Cloud, Identity, and SaaS. Use these scores to track progress and identify which domains need the most attention to reach your target posture.