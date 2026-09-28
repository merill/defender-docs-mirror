---
layout: Conceptual
title: Assign regulatory compliance standards in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/assign-regulatory-compliance-standards
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
description: Assign regulatory compliance standards to Azure subscriptions, AWS accounts, and GCP projects in Defender for Cloud, and track compliance results in the Regulatory compliance dashboard.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 1ae00694-6b31-f35f-69b8-8cf183e92a4f
document_version_independent_id: fb37a202-0c01-02d6-0b54-ccb039b3ee6f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/assign-regulatory-compliance-standards.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/assign-regulatory-compliance-standards
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/assign-regulatory-compliance-standards.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: e81b3db6-f72c-0bc4-00a7-3927609737a3
---

# Assign regulatory compliance standards in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

This article shows how to assign regulatory compliance standards to supported scopes in Microsoft Defender for Cloud and review the resulting compliance assessments.

In Defender for Cloud, regulatory compliance standards use Azure Policy initiatives. Defender for Cloud evaluates these standards in the Regulatory compliance dashboard.

You can assign regulatory compliance standards to specific scopes such as Azure subscriptions, Amazon Web Services (AWS) accounts, and Google Cloud Platform (GCP) projects.

Defender for Cloud continually assesses the selected scope against each standard. It then shows whether resources are compliant or noncompliant and provides remediation recommendations.

## Prerequisites

Before you assign a standard, make sure you meet the following prerequisites:

- To access compliance standards in Defender for Cloud, onboard any Defender for Cloud plan, except Defender for Servers Plan 1 or Defender for API Plan 1.
- You need `Owner` or `Policy Contributor` permissions to add a standard.

## Assign a standard

If you assign a regulatory standard but have no relevant assessed resources, the standard doesn't appear on your regulatory compliance dashboard.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Regulatory compliance**. For each standard, you can see the applied subscription.
3. Select **Manage compliance policies**.

    [![Screenshot of the regulatory compliance page that shows you where to select the manage compliance policy button.](media/update-regulatory-compliance-packages/manage-compliance.png)](media/update-regulatory-compliance-packages/manage-compliance.png#lightbox)
4. Select an account or management account (Azure subscription or management group, AWS account or management account, GCP project or organization) to assign the regulatory compliance standard.

    Note

    We recommend selecting the highest scope applicable to the standard so that compliance data is aggregated and tracked for all nested resources.
5. Select **Security policies**.
6. Locate the standard you want to enable and toggle the status to **On**.

    [![Screenshot showing regulatory compliance dashboard options.](media/update-regulatory-compliance-packages/turn-standard-on.png)](media/update-regulatory-compliance-packages/turn-standard-on.png#lightbox)

    If any information is needed to enable the standard, the **Set parameters** page appears for you to type in the information.

    The selected standard appears in the **Regulatory compliance** dashboard as enabled for the subscription where the standard was enabled.