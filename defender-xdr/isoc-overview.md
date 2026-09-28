---
layout: Conceptual
title: Integrated Security Operations Center (ISOC) in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/isoc-overview
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how Integrated Security Operations Center (ISOC) in Microsoft Defender brings XDR, SIEM, threat intelligence, automation, and AI together, including eligibility and workspace requirements.
ms.service: defender-xdr
author: mberdugo
ms.author: monaberdugo
ms.localizationpriority: high
ms.collection:
- m365-security
- m365solution-getstarted
- highpri
- tier1
- usx-security
- zerotrust-solution
- msftsolution-secops
ms.topic: overview
ai-usage: ai-assisted
ms.date: 2026-09-14T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 0bd08118-cd70-ac39-7608-d197e3b92c08
document_version_independent_id: 0bd08118-cd70-ac39-7608-d197e3b92c08
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/isoc-overview.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: isoc-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/isoc-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: bb66c1b2-59a5-a1a6-e6db-71f616ada2ba
---

# Integrated Security Operations Center (ISOC) in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Integrated Security Operations Center (ISOC) in Microsoft Defender brings leading XDR and SIEM capabilities, threat intelligence, automation, and AI together in the Microsoft Defender portal. ISOC gives security teams shared security signals, context, and workflows to detect, investigate, and respond to threats faster from one integrated experience.

Note

ISOC is in preview. Capabilities and availability might change during the preview period.

[![Screenshot of the Microsoft Defender home page showing the Integrated Security Operations Center capabilities banner.](media/isoc-overview/integrated-security-operations-defender-home.png)](media/isoc-overview/integrated-security-operations-defender-home.png#lightbox)

## ISOC advantages

ISOC helps security teams:

- **Integrated security operations** - Leading SIEM capabilities are available out of the box in Microsoft Defender, delivering immediate security operations value from day one without requiring a traditional SIEM deployment as a starting point.
- **Value from Microsoft 365 investments** - Eligible customers receive 30 days of included retention for Defender data during this phase of the preview. For broader visibility, bring in additional Microsoft and non-Microsoft data through more than 500 data connectors. Additional ingestion charges might apply depending on the data you ingest.
- **Path for agentic security** - Security teams and Perception agents work together on a common set of signals, context, and workflows, enabling faster investigations, coordinated response, and improved security outcomes.

## Who can use ISOC?

During this phase of the preview, ISOC is available to eligible customers with Microsoft Defender Suite, Microsoft 365 E5, or Microsoft 365 E7 that don't have an active Microsoft Sentinel workspace.

If your organization has an active Microsoft Sentinel workspace, continue using your existing Microsoft Sentinel experience during this phase. Don't disconnect a production Microsoft Sentinel workspace only to qualify for the ISOC preview.

## Prerequisites

To use ISOC, you need an active, eligible Microsoft Defender Suite, Microsoft 365 E5, or Microsoft 365 E7 license.

To create an ISOC workspace and use workspace-dependent capabilities, you also need an Azure subscription with [the required permissions](onboard-isoc-workspace).

## Licensing and pricing

For Microsoft 365 E5 plan details and pricing, see [Microsoft 365 E5 for Enterprise](https://www.microsoft.com/microsoft-365/enterprise/e5#Pricing).

To compare the security capabilities included with Microsoft 365 enterprise plans, see [Microsoft 365 Security Enterprise Plans](https://www.microsoft.com/security/pricing/enterprise-plans).

## ISOC capabilities

ISOC lets eligible customers start with security operations capabilities built into Microsoft Defender and expand with additional data and capabilities when needed.

- Start immediately with case management, workbooks, and natural-language playbook generation.
- Add an ISOC workspace when you need additional Microsoft and non-Microsoft data ingestion, UEBA, Content hub connectors, repositories (CI/CD), threat intelligence, and other workspace-dependent capabilities.

The following table summarizes the workspace requirements for the capabilities covered in this preview.

| Capability | ISOC workspace required | Learn more |
| --- | --- | --- |
| Case management | No | [Case management in the Microsoft Defender portal](siem-defender-case-management) |
| Natural-language playbook generation | No | [Generate playbooks using AI with ISOC](siem-defender-generate-playbooks) |
| Enhanced automation rule | No | [Create automation rules with ISOC in Microsoft Defender](siem-defender-create-automation-rules) |
| Workbooks | No | [Create and manage workbooks with ISOC in Microsoft Defender](siem-defender-workbooks) |
| User and Entity Behavior Analytics (UEBA) | Yes | [Add UEBA to Microsoft 365 E5 data](extend-ueba) |
| Content hub | Yes | [Use Content hub with ISOC in Microsoft Defender](content-hub-defender) |
| CI/CD | Yes | [Deploy content as code from your repository for an ISOC workspace](deploy-content-integrated-security-operations) |
| Threat intelligence | Yes | [Threat intelligence in Microsoft Defender](defender-threat-intelligence) |
| Azure and third-party security data | Yes | [Data ingestion and billing for ISOC](integrated-security-operations-data-billing-retention) |

Note

This table shows whether an ISOC workspace is required for each capability during this preview. It doesn't indicate licensing or availability for the same capabilities in other Microsoft security experiences.

## Get started

If the capabilities you want to use require an ISOC workspace, see [Create an ISOC workspace in the Microsoft Defender portal](onboard-isoc-workspace).

For information about ingesting additional security data and understanding billing, see [Data ingestion and billing for ISOC](integrated-security-operations-data-billing-retention).