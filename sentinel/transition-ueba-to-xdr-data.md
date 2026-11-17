---
layout: Conceptual
title: Update UEBA to use Microsoft Defender XDR data | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/transition-ueba-to-xdr-data
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Learn how User and Entity Behavior Analytics (UEBA) uses supported Microsoft Defender XDR data when transitioning an existing Microsoft Sentinel deployment.
author: mberdugo
ms.author: monaberdugo
ms.topic: how-to
ms.date: 2026-11-15T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1032
locale: en-us
document_id: b0a46fc7-af63-5f88-ec2e-2261cb9ef139
document_version_independent_id: d3444d29-4b61-db35-6500-8080c7cb5d3c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/transition-ueba-to-xdr-data.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/transition-ueba-to-xdr-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/transition-ueba-to-xdr-data.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: c097e366-d51d-ff94-8bdb-e5a5a9f202c1
---

# Update UEBA to use Microsoft Defender XDR data | Microsoft Learn

When you transition an existing Microsoft Sentinel deployment, User and Entity Behavior Analytics (UEBA) uses supported Microsoft Defender XDR data directly instead of relying on the same first-party data being ingested into a Microsoft Sentinel workspace.

UEBA outputs continue to be stored in Microsoft Sentinel workspaces. Output from data processed from XDR is sent to the primary workspace. You can select the XDR source tables in the primary workspace's UEBA settings. For data processed from Log Analytics tables, whether ingested through connectors or other means, output is sent to the workspace where UEBA is enabled, which can be a primary or secondary workspace. You can change the Log Analytics source tables selected in UEBA settings.

For customers with a single workspace, the change to Microsoft Defender XDR-backed UEBA is seamless. If you use multiple workspaces or Data Collection Rules (DCRs), review the changes that might affect your existing UEBA configuration before you onboard.

## Prerequisites

- If you use multiple workspaces, review workspace-specific content that depends on UEBA output.
- If you have UEBA-enabled Microsoft Sentinel workspaces that aren't connected to the Microsoft Defender portal, connect them before the transition and wait 30 days so that UEBA baselines can be reaccumulated.

The table UEBA supports for this process is `DeviceLogonEvents`. Data from this table transitions seamlessly to the Defender tables, subject to the DCR behavior described in the following sections. The list of supported tables will be updated based on the sources UEBA supports.

## Transition UEBA for a single workspace

### Existing UEBA customers

For existing UEBA deployments with a single Microsoft Sentinel workspace, the change to Microsoft Defender XDR-backed UEBA happens seamlessly if there are no DCRs in place for the originating table.

If your environment has an existing DCR configured for the supported tables, UEBA continues to process the data from Log Analytics. If you stop the DCR on the table, UEBA transitions to the XDR table within 24 hours.

Important

During this window, UEBA still processes events from the XDR table, and DCR filtering doesn't apply to the UEBA output in the workspace. To mitigate this window, you can apply the same DCR to the UEBA tables (`behaviorAnalytics` and `Anomalies`) to avoid data exposure.

Important

If you stop ingestion to the Log Analytics tables, you need to stop the DCRs on those tables for UEBA to transition to the XDR table. This transition takes up to 24 hours.

UEBA output derived from supported Microsoft Defender XDR, Log Analytics, and third-party data continues to be available in the UEBA tables in your Microsoft Sentinel workspace.

Third-party data continues to reach UEBA through Microsoft Sentinel data connectors.

Don't disable and re-enable UEBA as part of the transition. Doing so deletes existing UEBA profiles and baselines. No separate UEBA transition is required.

### Customers without UEBA

If UEBA isn't currently enabled:

1. Complete the required Microsoft Sentinel workspace onboarding.
2. Open the UEBA settings experience.
3. Enable UEBA and any required directory synchronization.
4. In your primary workspace, connect your supported Microsoft Defender XDR data sources to UEBA. You can connect them individually or use the recommended bulk option. In your secondary workspaces, you can connect only Log Analytics tables.
5. Connect any third-party data sources that you want UEBA to process.

UEBA uses supported Microsoft Defender XDR data as its first-party input. You don't need to separately ingest the same supported first-party data into Microsoft Sentinel for UEBA.

## Transition UEBA for multiple workspaces

UEBA output derived from supported Microsoft Defender XDR data is written to your primary workspace and can only be configured in the primary workspace's UEBA settings. UEBA output derived from third-party and other non-XDR data remains associated with the workspace where the source data is ingested.

There isn't an option to ingest Microsoft Defender XDR-derived UEBA output in a non-primary workspace. However, you can connect Log Analytics tables to UEBA in secondary workspaces, and UEBA reads from the Log Analytics table.

## Review DCR behavior

If you use Data Collection Rules (DCRs) to filter first-party data used by UEBA, the existing filtering doesn't apply when UEBA processes the corresponding Microsoft Defender XDR data directly.

Review the implications of the following configurations:

- When you enable a DCR on an XDR source, UEBA stops processing that source within 24 hours. During this window, you can also apply a DCR to the UEBA table to avoid data exposure.
- When a DCR is enabled for a supported UEBA table and you stop ingestion to that table as part of ISOC recommendations, UEBA continues to process that table until you stop the DCR. If ingestion stops, UEBA processes a stale table and doesn't generate new outputs or update baselines.

DCR filtering for third-party data continues to work as before.

There isn't a DCR workaround for Microsoft Defender XDR data used directly by UEBA. Review the impact before onboarding. To continue onboarding with the affected data sources, acknowledge the change or turn off UEBA for those data sources.

## Where UEBA output goes

After the transition, UEBA processes supported Microsoft Defender XDR data at the tenant level. Microsoft Defender XDR-derived UEBA output is mapped to the primary Microsoft Sentinel workspace, while other UEBA output remains in the workspace where its source data is ingested.