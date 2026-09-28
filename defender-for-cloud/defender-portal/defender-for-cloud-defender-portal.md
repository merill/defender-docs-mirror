---
layout: Conceptual
title: Overview of Defender for Cloud in Defender Portal - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-portal/defender-for-cloud-defender-portal
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Comprehensive overview of Microsoft Defender for Cloud in the Defender portal, including navigation hub, dashboard features, and unified security management capabilities.
ms.topic: overview
ms.date: 2026-04-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 97ec41ae-46fa-6726-04f0-7e8e3ae26734
document_version_independent_id: de601629-1ec7-3a96-d9de-3bb1fd2fe3c1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-portal/defender-for-cloud-defender-portal.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: ../toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-portal/defender-for-cloud-defender-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-portal/defender-for-cloud-defender-portal.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: aa9aa5e3-3250-972f-7524-2bf860c6002b
---

# Overview of Defender for Cloud in Defender Portal - Microsoft Defender for Cloud | Microsoft Learn

Important

Microsoft Defender for Cloud is expanding to the Defender portal to provide a unified security experience across cloud and code environments. As part of this expansion, some features are now available in the Microsoft Defender Portal, and additional capabilities will be added to the Defender portal over time.

This change is designed to:

- Unlock new cloud and posture management experiences.
- Provide deep integration with other Microsoft security services.
- Empower security teams with streamlined workflows by bringing all tools together in one portal.

To identify documentation specific for the Defender Portal, look for the portal entry point at the top of the article. This pivot indicates whether the content applies to the Defender portal or the Azure portal.

Our documentation will be continuously updated to reflect these changes, so check back regularly for the latest guidance and feature availability.

This article provides a comprehensive overview of Microsoft Defender for Cloud's integration with the Defender portal, covering key features, benefits, and capabilities available in this unified security experience.

## Overview

Microsoft Defender for Cloud (MDC) is now deeply integrated into the Defender portal at security.microsoft.com and part of the broader Microsoft Security eco-system. With threat protection already deeply embedded into the Defender portal, this integration adds posture management—bringing together a complete cloud-native application protection platform (CNAPP) solution in one unified experience. This native-integration eliminates silos so security teams can see and act on threats across all cloud, hybrid, and code environments - all from one place and eliminates the need to switch between tools and portals.

[![Screenshot of the Defender for Cloud overview dashboard in the Defender portal.](../media/defender-portal-dashboard/overview-dashboard.png)](../media/defender-portal-dashboard/overview-dashboard.png#lightbox)

The cloud-agnostic expansion supports Azure, AWS, GCP, and other platforms in a single interface, making it ideal for hybrid and multicloud organizations seeking comprehensive exposure management too. In the first phase, the journey for new customers still starts in the Azure portal for initial onboarding, connecting environments for protection, and setting policies and configurations. Once this is complete, users can consume the data in the Defender portal. In a later phase, users will also be able to manage and configure settings directly in Defender, enabling them to perform all MDC end-to-end use cases within a single portal.

## Supported experiences in the Defender portal

Cloud security data and signals can be accessed through several experiences. Some are exclusive to the cloud, while others are incorporated into broader Defender experiences like XDR and Exposure Management.

#### Cloud security

- [Cloud Overview dashboard](../cloud-infrastructure-dashboard?pivots=defender-portal)
- [Cloud inventory](../asset-inventory?pivots=defender-portal)

#### Posture Management

- [Cloud Secure Score](../secure-score-access-and-track?pivots=defender-portal)
- [Recommendations](../review-security-recommendations?pivots=defender-portal)
- [Attack paths](../how-to-manage-attack-path?pivots=defender-portal)
- [Cloud vulnerabilities](/en-us/security-exposure-management/vulnerability-management-integration)

#### Threat Detection & Response

- [Incidents and alerts](../concept-integration-365)
- [Response actions](../continuous-export)
- [Advanced hunting](../concept-integration-365#advanced-hunting-in-xdr)

#### Configurations

- [Cloud Scopes & RBAC](../cloud-scopes-unified-rbac?pivots=defender-portal)

## Key values and benefits

**[Cloud overview dashboard](../cloud-infrastructure-dashboard?pivots=defender-portal)**: The Cloud overview dashboard centralizes both posture management and threat protection, giving security personas an overview of their environment. It also highlights the top improvement actions for risk reduction, workload-specific views with security insights and track security progress over time out of the box.

**[Cloud asset inventory](../asset-inventory?pivots=defender-portal)**: A complete inventory offers a comprehensive view of cloud and code assets across Azure, AWS, and GCP. Assets are categorized by workload, criticality, and coverage, with integrated health data, asset actions, and risk signals. Information security and SOC teams can easily access resource-specific views, exposure map, and metadata to address security recommendations and respond quickly to threats.

**[Unified cloud security posture capabilities](/en-us/security-exposure-management/microsoft-security-exposure-management)**: All the cloud security posture management (CSPM) capabilities unified into Microsoft Security Exposure Management (MSEM). Security personas can view secure scores, prioritized recommendations, attack paths and vulnerabilities, all in a single pane of glass, empowering them to reduce risk and get a holistic view of all their posture end-to-end including devices, identities, SaaS apps and data. For more information, see [What's new in Microsoft Security Exposure Management](/en-us/security-exposure-management/whats-new).

**[Granular access management](../cloud-scopes-unified-rbac?pivots=defender-portal)**: Security teams can now provide targeted access to security content, so only relevant users see necessary information. This allows users to view security insights without direct resource permissions, enhancing operational security and compliance. Using a new cloud scopes capability, cloud accounts like Azure subscriptions, AWS accounts, and GCP projects can be organized into logical groups for improved data pivoting and RBAC, supporting segmentation by business unit, region, or workload with persistent filtering across dashboards and workflows.

## Why integrate into the Defender portal?

The Microsoft Defender portal delivers a unified security operations experience across endpoints, identities, email, and cloud resources. By integrating Defender solutions, such as Defender for Cloud, Defender for Endpoint, and others, it provides comprehensive protection, detection, investigation, and response capabilities in one place. This unified approach streamlines threat detection, correlates insights, and strengthens your organization’s security posture. Powered by advanced AI and Microsoft’s global threat intelligence, it helps identify emerging risks faster and enables proactive defense against sophisticated attacks.

### How to get started?

Defender for Cloud customers with at any paid plan can access the consumption experiences in the Defender portal.

To get started, go to **Defender portal** → **Cloud security** → **Overview**, and select **Prepare my tenant**.

Note

Data might take up to 24 hours to appear.

- Read the [known limitations](known-limitations)
- Read the [FAQ](integration-faq)