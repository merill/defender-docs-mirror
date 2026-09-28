---
layout: Conceptual
title: Review Workload Protection in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/workload-protections-dashboard
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
description: Review workload protection in the Workload protections dashboard in Microsoft Defender for Cloud to detect threats and protect your resources.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 11d4d765-67e5-5973-bd60-8e792bac4805
document_version_independent_id: 299dd79f-8c38-a8bd-fff5-9615a43b82bf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/workload-protections-dashboard.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/workload-protections-dashboard
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/workload-protections-dashboard.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 519983ea-d0c8-45d9-1e0e-9696692d28aa
---

# Review Workload Protection in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud helps you detect threats and protect your resources. Use the **Workload protections** dashboard to review this information.

[![An example of Defender for Cloud's workload protections dashboard.](../../reusable-content/ce-skilling/azure/media/defender-for-cloud/sample-defender-dashboard-numbered.png)](../../reusable-content/ce-skilling/azure/media/defender-for-cloud/sample-defender-dashboard-numbered.png#lightbox)

## Review Defender for Cloud coverage

In the **Defender for Cloud coverage** section of the dashboard, you can see the resources types in your subscription that are eligible for protection by Defender for Cloud. Where relevant, you can upgrade resources from this section. If you want to upgrade all possible eligible resources, select **Upgrade all**.

## Review security alerts

The **Security alerts** section shows alerts. When Defender for Cloud detects a threat in any area of your environment, it generates an alert. These alerts describe details of the affected resources, suggested remediation steps, and in some cases an option to trigger a logic app in response. Selecting anywhere in this graph opens the **Security alerts page**.

## Review advanced workload protection features

Defender for Cloud offers advanced threat protection for virtual machines, SQL databases, containers, web applications, your network, and more. This section shows the status of resources in your selected subscriptions for each protection. Select any protection type to go to its configuration area.

## Review workload protection insights

Insights provide you with news, suggested reading, and high priority alerts that are relevant in your environment.

## Prerequisites

The plan must be enabled at the subscription level to ensure proper functionality. Resources onboarded to Defender for Cloud at the resource level won't be eligible for the capabilities available through the Workload protection area.