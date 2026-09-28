---
layout: Conceptual
title: Step 6. Identify SOC maintenance tasks - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/integrate-microsoft-365-defender-secops-tasks
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Identify SOC maintenance tasks when integrating Microsoft Defender XDR into your security operations.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- msftsolution-secops
- tier2
ms.topic: how-to
ms.date: 2026-06-15T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 73dbea1e-6c65-aedf-f90c-df4ff55f34bd
document_version_independent_id: 73dbea1e-6c65-aedf-f90c-df4ff55f34bd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/integrate-microsoft-365-defender-secops-tasks.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: integrate-microsoft-365-defender-secops-tasks
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/integrate-microsoft-365-defender-secops-tasks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: ad2947b4-393c-0eac-9f7d-c3cb2e1145f8
---

# Step 6. Identify SOC maintenance tasks - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- Microsoft Defender XDR

## Maintain your SOC for Microsoft Defender XDR

Here are the periodic or as-needed tasks to maintain your SOC for Microsoft Defender XDR. The following table outlines each recurring activity, its recommended cadence, and the team typically responsible for it. Use these tasks to ensure your security operations center stays aligned with Microsoft Defender XDR capabilities.

| Activity | Description | Cadence | Team assigned |
| --- | --- | --- | --- |
| Service administration collaboration with SOC Teams | Administration of peripheral services such as asset tracking (CMDB), application licensing (new SaaS licenses), device purchases (upgrades or renew device deployments), and other Microsoft 365 tenant-wide changes (Intune, Microsoft 365, and others) that may affect deployment of Microsoft Defender XDR products. | Weekly and as needed | Engineering & SecOps |
| Update anti-phishing and data loss prevention campaigns | Incorporate SOC use case and lessons learned with extended organization (HR, legal, training, and others). | Monthly and as needed | SOC Oversight |
| Deploy automation scripts and services where appropriate | Download and test automation scripts and configuration files from approved Microsoft sites to improve Microsoft Defender XDR operations. | Weekly and as needed | Engineering and SecOps |
| Portal or license management | Check announcements and the Microsoft Messaging Center for Microsoft Defender portal or licensing needs based on Microsoft updates and new features. | Weekly | SOC Oversight |
| Update SOC escalation tickets | All SOC teams update escalation tickets (such as Sentinel, ServiceNow tickets) assigned to them. | Daily | All SOC teams |
| Track Microsoft Defender Vulnerability Management (MDVM) remediation activity | Generate MDVM Secure Score remediation activity and report to asset owners through an intranet portal. | Daily | Monitoring |
| Generate Secure Score report | Monitoring team tracks and reports Secure Score improvements. | Weekly SOC | Monitoring |
| Run IR tabletop exercise | Test SOC team playbooks in tabletop exercise. | As needed | All SOC teams |

Integrate these tasks into your current SOC processes.