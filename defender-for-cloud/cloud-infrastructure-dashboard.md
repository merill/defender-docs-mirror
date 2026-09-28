---
layout: Conceptual
title: Cloud overview dashboard in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/cloud-infrastructure-dashboard
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
zone_pivot_group_filename: defender-for-cloud/zone-pivots/zone-pivot-groups.json
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to use the Cloud overview dashboard to monitor security posture, threat protection, and exposure management across your multicloud environment.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
zone_pivot_groups: defender-portal-experience
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 8f07f14d-be90-441e-aa0b-e5de8ad33b6e
document_version_independent_id: 5b5c3553-fb94-6aa3-5147-ab115cb18cb1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/cloud-infrastructure-dashboard.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/cloud-infrastructure-dashboard
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/cloud-infrastructure-dashboard.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 5e72b1fd-e972-1bbd-df02-f4c5d319e5e6
---

# Cloud overview dashboard in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

::: zone pivot="defender-portal"

## Cloud overview dashboard in the Defender portal

The Cloud Overview dashboard is the landing page for Microsoft Defender for Cloud in the unified security portal (Defender portal). It gives security teams a clear view of cloud security status before and after a breach. Use it to prioritize work, track progress over time, and take action quickly. You can review data at tenant level or by selected scope.

Important

Microsoft Defender for Cloud is expanding to the Defender portal to provide a unified security experience across cloud and code environments. As part of this expansion, some features are now available in the Microsoft Defender Portal, and additional capabilities will be added to the Defender portal over time.

This change is designed to:

- Unlock new cloud and posture management experiences.
- Provide deep integration with other Microsoft security services.
- Empower security teams with streamlined workflows by bringing all tools together in one portal.

To identify documentation specific for the Defender Portal, look for the portal entry point at the top of the article. This pivot indicates whether the content applies to the Defender portal or the Azure portal.

Our documentation will be continuously updated to reflect these changes, so check back regularly for the latest guidance and feature availability.

## Who is this for?

- Cloud Security Admins & Architects: Monitor posture, threats, and trends across environments.
- Workload Owners (DevOps, Developers): Track scoped issues and act to resolve them.

## Access the dashboard

You can access the Cloud Overview dashboard from the navigation bar in the Microsoft Defender portal:

1. Sign in to the [Defender portal](https://security.microsoft.com).
2. Go to **Cloud security** &gt; **Overview**

## Filter the dashboard with top controls

At the top of the dashboard, you find key filters:

- **Scope Filter**: Narrow the dashboard view to a specific scope you’re authorized to access, based on [unified scopes](cloud-scopes-unified-rbac).
- **Environment Filter**: Pivot the dashboard by the cloud environment you want to view, such as Azure, Amazon Web Services (AWS), or Google Cloud Platform (GCP).
- **Time Range**: Select 30 days, 3 months, or 6 months to view trends over time. This applies to all historical graphs and trend indicators.

![Screenshot of filters on cloud overview dashboard.](media/defender-portal-dashboard/top-controls.png)

## Understand the dashboard sections

The dashboard is organized into the following sections, each highlighting a different aspect of your security posture.

### Security at a glance

The **Security at a glance** section gives you a quick snapshot of your current security status:

- **Cloud Secure Score** (preview): Your overall cloud security risk score with a trend indicator.
- **Threat Protection**: Number of alerts by severity.
- **Assets Coverage**: Number of protected assets by Defender for Cloud plans and their coverage status.
    - **Full** - assets covered by posture and protection plans
    - **Partial** - assets protected by posture or protection plans
    - **None** - unprotected assets

In addition, all cloud and code environments that are currently connected to Defender for Cloud are presented.

![Screenshot of cloud overview dashboard highlights.](media/defender-portal-dashboard/overview-highlights.png)

### Top Actions

The **Top Actions** section helps you decide where to start. The Top Actions section guides next steps that reduce attack surface efficiently. The Top Actions section highlights:

**Critical Recommendations**: Help you focus on the most critical recommendations found in your environment. **High-Severity Incidents**: Investigate active alerts. **Attack Paths**: Understand potential lateral movement.

![Screenshot of cloud overview dashboard top actions.](media/defender-portal-dashboard/top-actions.png)

### Trends over time

Track how your security posture and threat detection evolve.

**Security Posture**: View over time of the new Cloud Secure Score in addition to recommendations by severity.

![Screenshot of cloud overview dashboard security posture trends.](media/defender-portal-dashboard/security-posture.png)

**Threat Detection**: View security alert trends by severity.

![Screenshot of cloud overview dashboard threat detection trends.](media/defender-portal-dashboard/threat-detection.png)

The Security Posture and Threat Detection graphs update daily and reflect the selected time range. Hover over data points to see daily breakdowns.

### Workload Insights

Each tile in the **Workload Insights** section surfaces insights from Microsoft Cloud-native application protection platform (CNAPP).

Workloads include:

- Compute (including virtual machines)
- Data
- Containers
- AI
- APIs
- DevOps
- CIEM

Each tile acts as a mini dashboard, showing top issues, protection coverage, and links to detailed views. This helps teams focus on what matters most for each workload.

[![Screenshot of cloud overview dashboard workload insights.](media/defender-portal-dashboard/workloads.png)](media/defender-portal-dashboard/workloads.png#lightbox)

::: zone-end

::: zone pivot="azure-portal"

## Overview dashboard in the Azure portal

Microsoft Defender for Cloud gives a unified view of the security posture of hybrid cloud workloads with the interactive **Overview** dashboard. Select any element on the dashboard to get more information.

[![Screenshot of Defender for Cloud's overview page.](media/overview-page/overview-07-2023.png)](media/overview-page/overview-07-2023.png#lightbox)

## View metrics on the dashboard

The **top menu bar** offers:

- **Subscriptions** - View and filter the list of subscriptions by selecting this button. Defender for Cloud adjusts the display to reflect the security posture of the selected subscriptions.
- **What's new** - Opens the [release notes](release-notes) to stay updated with new features, bug fixes, and deprecated functionality.
- **High-level numbers** for the connected cloud accounts, showing the context of the information in the main tiles, and the number of assessed resources, active recommendations, and security alerts. Select the assessed resources number to access [Asset inventory](asset-inventory). For onboarding guidance, see [Connect Amazon Web Services (AWS) accounts](quickstart-onboard-aws) and [Connect Google Cloud Platform (GCP) projects](quickstart-onboard-gcp).

[![Screenshot of Defender for Cloud's overview page's top bar.](media/overview-page/top-bar-of-overview-new.png)](media/overview-page/top-bar-of-overview-new.png#lightbox)

## Explore the feature tiles

The center of the page shows the feature tiles. Each tile links to a key feature or a dedicated dashboard:

- **Security posture** - Defender for Cloud continually assesses your resources, subscriptions, and organization for security issues. It aggregates findings into one score so you can quickly evaluate current risk: the higher the score, the lower the identified risk level. For details, see [Secure Score and security controls](secure-score-security-controls).
- **Workload protections** - The cloud workload protection platform (CWPP) in Defender for Cloud provides advanced protection for workloads on Azure, on-premises machines, and other cloud providers. Each resource type has a related Microsoft Defender plan. The tile shows coverage for connected resources in selected subscriptions and recent alerts by severity. For plan details, see [Defender plans and CWPP coverage](defender-for-cloud-introduction#cloud-workload-protection-platform-cwpp).
- **Regulatory compliance** - Defender for Cloud continuously assesses hybrid and multicloud resources and maps findings to supported compliance standards. This mapping helps you track compliance status against the standards that matter to your organization. For guidance, see [Regulatory compliance dashboard](regulatory-compliance-dashboard).
- **Inventory** - Asset inventory gives you a unified view of the security posture for connected resources. It includes resources with unresolved recommendations. If you enable integration with Microsoft Defender for Endpoint and Microsoft Defender for Servers, you also get software inventory. The overview tile shows healthy and unhealthy resource counts for selected subscriptions. To explore this view, see [Asset inventory in Defender for Cloud](asset-inventory).

## Review dashboard insights

The Insights pane offers customized items for your environment including:

- **Actionable items to enhance your security.**
- **Tips to handle alerts and recommendations.**
- **Recommendations on how to upgrade your service to enhance your environment's protections.**
- **Recent blog posts by Microsoft Defender for Cloud experts.**

## Next steps

For related tasks and follow-up guidance, see the following articles:

- [Explore attack paths and security insights](concept-attack-path)
- [Review cloud infrastructure assets](asset-inventory?pivots=azure-portal)
- [Configure cloud scopes for filtering](cloud-scopes-unified-rbac?pivots=azure-portal)
- [Set up vulnerability management](auto-deploy-vulnerability-assessment?pivots=azure-portal)
- [Configure email notifications](configure-email-notifications)

::: zone-end