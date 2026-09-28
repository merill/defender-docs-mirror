---
layout: Conceptual
title: Operational guide - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/ops-guide/ops-guide
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article provides operational recommendations to help security operations teams to plan and run security activities.
ms.date: 2023-12-13T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: fd83402a-6bfa-0062-a81f-028a83a95a25
document_version_independent_id: fd83402a-6bfa-0062-a81f-028a83a95a25
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/ops-guide/ops-guide.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ops-guide/ops-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/ops-guide/ops-guide.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 1eaf0c2b-c58c-8d9e-1e47-df27bb70411d
---

# Operational guide - Microsoft Defender for Cloud Apps | Microsoft Learn

This section of the Microsoft Defender for Cloud Apps documentation helps security operations (SOC) teams and security administrators to plan and run regular security activities with Microsoft Defender for Cloud Apps.

## Prerequisites

The activities in this article assume that you deployed Defender for Cloud Apps. For more information, see [Basic setup for Defender for Cloud Apps](../general-setup) and the [Defender for Cloud Apps Ninja training](https://aka.ms/MDCANinjaTraining).

## Activity reference

The following table lists activities that we recommend you perform regularly with Defender for Cloud Apps:

| Frequency | Activities |
| --- | --- |
| **Daily** | - [Review alerts and incidents](ops-guide-daily#review-alerts-and-incidents) - [Review threat detection data](ops-guide-daily#review-threat-detection-data) - [Review application governance](ops-guide-daily#review-application-governance) - [Review Conditional Access app control](ops-guide-daily#review-conditional-access-app-control) - [Review shadow IT - cloud discovery](ops-guide-daily#review-shadow-it---cloud-discovery) - [Review the cloud discovery dashboard](ops-guide-daily#review-the-cloud-discovery-dashboard) - [Review information protection](ops-guide-daily#review-information-protection) |
| **Weekly** | - [Review SaaS security posture management](ops-guide-weekly#review-saas-security-posture-management) - [Check app connectors, log collectors, and SIEM agent health](ops-guide-weekly#check-app-connectors-log-collectors-and-siem-agent-health) - [Track new changes in Microsoft Defender XDR](ops-guide-weekly#track-new-changes-in-microsoft-defender-xdr) - [Review the governance log](ops-guide-weekly#review-the-governance-log) |
| **Monthly** | - [Review policy assessments](ops-guide-monthly#review-policy-assessments) - [Review activity logs](ops-guide-monthly#review-activity-logs) |
| **Ad-hoc** | - [Review Microsoft service health](ops-guide-ad-hoc#review-microsoft-service-health) - [Run advanced hunting queries](ops-guide-ad-hoc#run-advanced-hunting-queries) - [Review file quarantines](ops-guide-ad-hoc#review-file-quarantines) - [Review app risk scores](ops-guide-ad-hoc#review-app-risk-scores) - [Delete cloud discovery data](ops-guide-ad-hoc#delete-cloud-discovery-data) - [Generate a cloud discovery executive report](ops-guide-ad-hoc#generate-a-cloud-discovery-executive-report) - [Generate a cloud discovery snapshot report](ops-guide-ad-hoc#generate-a-cloud-discovery-snapshot-report) |