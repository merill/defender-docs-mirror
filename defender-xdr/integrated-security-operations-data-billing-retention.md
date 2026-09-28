---
layout: Conceptual
title: Data ingestion and billing for ISOC in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/integrated-security-operations-data-billing-retention
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how Microsoft security data and additional Microsoft and non-Microsoft security data are handled and billed with ISOC in Microsoft Defender.
author: mberdugo
ms.author: monaberdugo
ms.localizationpriority: high
ms.collection:
- m365-security
- m365solution-getstarted
- highpri
- tier1
- usx-security
- msftsolution-secops
ms.topic: concept-article
ms.service: microsoft-sentinel
ai-usage: ai-assisted
ms.date: 2026-09-17T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: a3018aa1-e3e0-007c-d45a-e48fa92f6945
document_version_independent_id: a3018aa1-e3e0-007c-d45a-e48fa92f6945
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/integrated-security-operations-data-billing-retention.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: integrated-security-operations-data-billing-retention
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/integrated-security-operations-data-billing-retention.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: e0abdc18-4f42-d5b3-4f53-0202e91916db
---

# Data ingestion and billing for ISOC in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Integrated Security Operations Center (ISOC) in Microsoft Defender supports Microsoft security data and additional Microsoft and non-Microsoft security data.

Note

ISOC is in preview. Capabilities and availability might change during the preview period.

## How data is handled

Native Microsoft Defender data is available directly in the Microsoft Defender experience and doesn't need to be separately ingested into an ISOC workspace.

Other supported Microsoft and non-Microsoft data can be connected through an ISOC workspace by using data connectors.

## Microsoft security data

ISOC supports Microsoft security data from the following sources:

- Microsoft Defender for Endpoint
- Microsoft Defender for Office 365
- Microsoft Defender for Identity
- Microsoft Defender for Cloud Apps
- Microsoft Defender for Cloud
- Microsoft Entra Identity Protection logs
- Azure Activity and audit logs through a connector
- Office 365 Activity and audit logs through a connector

Eligible customers with Microsoft Defender Suite, Microsoft 365 E5, or Microsoft 365 E7 can use supported Microsoft Defender security data as part of the ISOC experience.

Note

During this phase of the preview, eligible customers receive 30 days of included retention for Defender data.

For Microsoft 365 E5 plan details and pricing, see [Microsoft 365 E5 for Enterprise](https://www.microsoft.com/microsoft-365/enterprise/e5#Pricing).

To compare the security capabilities included with Microsoft 365 enterprise plans, see [Microsoft 365 Security Enterprise Plans](https://www.microsoft.com/security/pricing/enterprise-plans).

## Additional Microsoft and non-Microsoft security data

An ISOC workspace is required to ingest additional Microsoft and non-Microsoft security data through more than 500 data connectors.

Additional ingestion charges might apply depending on the data you ingest.