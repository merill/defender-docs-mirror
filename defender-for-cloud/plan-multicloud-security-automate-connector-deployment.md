---
layout: Conceptual
title: Automate Microsoft Defender for Cloud Connector Deployment - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-multicloud-security-automate-connector-deployment
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
description: Automate Defender for Cloud connector deployment to onboard AWS accounts and GCP projects at scale. Learn how to use the REST API to standardize workflows.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 4983fe40-0264-9034-4712-50dfa302cb61
document_version_independent_id: 0037dec7-dd5d-13a4-b558-7b9fb84b1437
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-multicloud-security-automate-connector-deployment.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-multicloud-security-automate-connector-deployment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-multicloud-security-automate-connector-deployment.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 76fa3fc4-7c9c-e66a-e29f-341d607afa78
---

# Automate Microsoft Defender for Cloud Connector Deployment - Microsoft Defender for Cloud | Microsoft Learn

This article is part of a series that provides guidance as you design a solution for cloud security posture management (CSPM) and cloud workload protection platform (CWPP) for multicloud resources with Microsoft Defender for Cloud. You can create Amazon Web Services (AWS) and Google Cloud Platform (GCP) connectors programmatically so you can standardize deployment workflows.

## Connector deployment automation goals

Connect AWS accounts or GCP projects programmatically.

## Set up automated connector deployment

You can connect AWS accounts and GCP projects to Microsoft Defender for Cloud programmatically by using the Defender for Cloud REST API. Review the [Security Connectors REST API](/en-us/rest/api/defenderforcloud-composite/security-connectors?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true).

[![Screenshot that shows a table of security connector operations.](media/planning-multicloud-security/security-connectors.png)](media/planning-multicloud-security/security-connectors.png#lightbox)

- When you use the REST API to create a connector, you also need the CloudFormation template or Azure Cloud Shell script, depending on the environment you want to onboard.
- The easiest way to get the template or script is to download it from the Defender for Cloud portal.
- The template or script changes depending on which Defender for Cloud protection plans you want to enable.