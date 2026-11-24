---
layout: Conceptual
title: Data ingestion, retention, and billing for ISOC in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/integrated-security-operations-data-billing-retention
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how Microsoft security data and additional Microsoft and non-Microsoft security data are handled, retained, and billed with ISOC in Microsoft Defender.
author: mberdugo
ms.author: kschwabacher
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
ms.date: 2026-11-24T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1032
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
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: e0abdc18-4f42-d5b3-4f53-0202e91916db
---

# Data ingestion, retention, and billing for ISOC in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Integrated Security Operations Center (ISOC) in Microsoft Defender supports Microsoft security data and additional Microsoft and non-Microsoft security data.

## How data is handled

Native Microsoft Defender data is available directly in the Microsoft Defender experience and doesn't need to be separately ingested into an ISOC workspace.

Other supported Microsoft and non-Microsoft data can be connected through an ISOC workspace by using [data connectors](/en-us/azure/sentinel/connect-data-sources?tabs=defender-portal).

## Microsoft security data

ISOC supports Microsoft security data from the following sources:

- Microsoft Defender for Endpoint
- Microsoft Defender for Office 365
- Microsoft Defender for Identity
- Microsoft Defender for Cloud Apps
- Microsoft Defender for Cloud
- Microsoft Entra

Eligible customers with Microsoft Defender Suite, Microsoft 365 E5, or Microsoft 365 E7 can use supported Microsoft Defender security data as part of the ISOC experience.

For Microsoft 365 E5 plan details and pricing, see [Microsoft 365 E5 for Enterprise](https://www.microsoft.com/microsoft-365/enterprise/e5#Pricing).

To compare the security capabilities included with Microsoft 365 enterprise plans, see [Microsoft 365 Security Enterprise Plans](https://www.microsoft.com/security/pricing/enterprise-plans).

### 90-day retention

Starting November 15, 2026, eligible customers receive up to 90 days of included retention for supported Microsoft Defender data.

The retention benefit applies at the workload level, except for the tables listed in Retention exceptions. As additional supported tables become available for an included workload, they're also included in the retention benefit unless otherwise noted.

The following tables and data sources are currently included:

- **Alerts**

    - `AlertEvidence`
    - `AlertInfo`
- **Behaviors**

    Retention varies by underlying source; 90-day retention applies only to supported, enabled sources.

    - `BehaviorEntities` (Preview)
    - `BehaviorInfo` (Preview)
- **Microsoft Defender for Cloud**

    A full 90-day history is expected by January 3, 2027 for data covered by the current rollout.

    - `CloudPolicyEnforcementEvents`
    - `CloudKeyVaultEvents` (Preview)
    - `CloudProcessEvents`
    - `CloudStorageAggregatedEvents` (Preview)
    - `CloudAuditEvents`
    - `CloudDnsEvents`
- **Microsoft Defender for Cloud Apps**

    - `CloudAppEvents`
    - `OAuthAppInfo` (Preview)
- **Microsoft Defender for Endpoint**

    - `DeviceEvents`
    - `DeviceFileEvents`
    - `DeviceImageLoadEvents`
    - `DeviceLogonEvents`
    - `DeviceNetworkEvents`
    - `DeviceProcessEvents`
    - `DeviceRegistryEvents`
    - `DisruptionAndResponseEvents`
- **Microsoft Defender for Identity**

    - `IdentityDirectoryEvents`
    - `IdentityEvents` (Preview)
    - `IdentityLogonEvents`
    - `IdentityQueryEvents`
- **Microsoft Defender for Office 365**

    - `CallActivityEvents`
    - `CampaignInfo` (Preview)
    - `EmailAttachmentInfo`
    - `EmailEvents`
    - `EmailPostDeliveryEvents`
    - `EmailUrlInfo`
    - `FileMaliciousContentInfo` (Preview)
    - `MessageEvents`
    - `MessagePostDeliveryEvents`
    - `MessageUrlInfo`
    - `UrlClickEvents`
- **Microsoft Entra**

    - `EntraIdSignInEvents`
    - `EntraIdSpnSignInEvents`
    - `GraphAPIAuditEvents`

### Extend Microsoft Defender data retention

When you enable streaming for supported Microsoft Defender data, the retention period starts at 180 days.

Extended retention applies to new data after you enable it. Data that was collected before you enabled extended retention isn't backfilled.

Additional charges apply when you extend retention beyond the retention included with ISOC.

### Retention exceptions

The following tables don't receive the 90-day included retention benefit. They're stored in XDR for 30 days. As with other supported tables, extended retention starts at 180 days.

| Table | Retention in XDR | Extended retention starts at |
| --- | --- | --- |
| `AgentsInfo` | 30 days. | 180 days. |
| `IdentityAccountInfo` | 30 days. | 180 days. |

## Additional Microsoft and non-Microsoft security data

An ISOC workspace is required to ingest additional Microsoft and non-Microsoft security data through [more than 500 data connectors](/en-us/azure/sentinel/data-connectors-reference).

Except for threat intelligence ingestion, additional Microsoft and non-Microsoft security data is billed separately from the Microsoft security data included with the ISOC benefit. Ingested data can be retained for up to 90 days as part of the ISOC ingestion experience.

Additional ingestion and retention charges will apply depending on the data you ingest and how long you retain it.

## Threat intelligence ingestion

Threat intelligence ingestion is free for ISOC customers through all ingestion methods, including TAXII, upload APIs, STIX APIs, and threat intelligence vendor connectors.

## Choose a retention option

Use the retention option that matches how you plan to use the data:

- Use interactive retention for data that analysts need for investigations, hunting, and ongoing security operations.
- Use data lake retention for data that you keep primarily for longer-term analysis, audit, or compliance scenarios.

Additional charges apply when you extend retention beyond the retention included with ISOC.