---
layout: Conceptual
title: Operational guide - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/ops-guide/ops-guide
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn about the Microsoft Defender for Identity activities that we recommend for your team on a daily, weekly, and monthly basis.
ms.date: 2024-01-29T00:00:00.0000000Z
ms.topic: article
ms.reviewer: martin77s
locale: en-us
document_id: aaf278c4-83bb-8628-e27c-f8c82e71d781
document_version_independent_id: aaf278c4-83bb-8628-e27c-f8c82e71d781
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/ops-guide/ops-guide.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ops-guide/ops-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/ops-guide/ops-guide.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 2a1d4950-de59-ae70-7060-8f6ec03791db
---

# Operational guide - Microsoft Defender for Identity | Microsoft Learn

This article summarizes the Microsoft Defender for Identity activities we recommend for your team on a daily, weekly, and monthly basis.

| Cadence | Tasks |
| --- | --- |
| **Daily** | - [Triage incidents by priority](ops-guide-daily#triage-incidents-by-priority)- [Configure tuning rules for benign true positives / false positive alerts](ops-guide-daily#configure-tuning-rules-for-benign-true-positives--false-positive-alerts) - [Review the Identity Security dashboard](ops-guide-daily#review-the-identity-security-dashboard)- [Proactively hunt](ops-guide-daily#proactively-hunt) - [Review Defender for Identity health issues](ops-guide-daily#review-defender-for-identity-health-issues) |
| **Weekly** | - [Review Secure score recommendations](ops-guide-weekly#review-secure-score-recommendations) - [Review and respond to emerging threats](ops-guide-weekly#review-and-respond-to-emerging-threats)- [Proactively hunt](ops-guide-weekly#proactively-hunt) |
| **Monthly** | - [Review tuned alerts and adjust tuning if needed](ops-guide-monthly#review-tuned-alerts-and-adjust-tuning-if-needed) - [Track new changes in Microsoft Defender XDR and Defender for Identity](ops-guide-monthly#track-new-changes-in-microsoft-defender-xdr-and-defender-for-identity) |
| **Quarterly / Ad hoc**Depending on your organization's needs and processes | - [Review Microsoft service health](ops-guide-quarterly#review-microsoft-service-health) - [Review server setup process to include sensors](ops-guide-quarterly#review-server-setup-process-to-include-sensors)- [Check domain configuration via PowerShell](ops-guide-quarterly#check-domain-configuration-via-powershell) |

You might want to proactively hunt on a daily or weekly basis, depending on your level as a SOC analyst.