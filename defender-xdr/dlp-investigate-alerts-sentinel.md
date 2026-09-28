---
layout: Conceptual
title: Investigate data loss prevention alerts with Microsoft Sentinel - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/dlp-investigate-alerts-sentinel
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use the Microsoft Defender XDR connector in Microsoft Sentinel to import, correlate, and investigate data loss prevention (DLP) alerts across data sources.
ms.service: defender-xdr
ms.author: monaberdugo
author: mberdugo
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 538ec90d-ea7a-30e9-131a-52b3b8e5b5a1
document_version_independent_id: 538ec90d-ea7a-30e9-131a-52b3b8e5b5a1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/dlp-investigate-alerts-sentinel.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: dlp-investigate-alerts-sentinel
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/dlp-investigate-alerts-sentinel.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: c81ccf9c-bca7-2d91-e306-427793ad9eba
---

# Investigate data loss prevention alerts with Microsoft Sentinel - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- Microsoft Defender
- Microsoft Sentinel

This article explains how to use the Microsoft Defender XDR connector in Microsoft Sentinel to import, correlate, and investigate data loss prevention (DLP) alerts alongside other data sources. You learn how to set up the connector, view DLP incidents in Sentinel, and query user activities related to specific alerts.

## Prepare to investigate DLP alerts in Microsoft Sentinel

See, [Investigate data loss prevention alerts with Microsoft Defender](dlp-investigate-alerts-defender) for more details.

## DLP investigation experience in Microsoft Sentinel

You can use the Microsoft Defender XDR connector in Microsoft Sentinel to import all DLP incidents into Sentinel to extend your correlation, detection, and investigation across other data sources and extend your automated orchestration flows using Sentinel's native security orchestration, automation, and response (SOAR) capabilities.

1. Follow the instructions in [Connect data from Microsoft Defender XDR to Microsoft Sentinel](/en-us/azure/sentinel/connect-microsoft-365-defender) to import all incidents including DLP incidents and alerts into Sentinel. Enable the `CloudAppEvents` event connector, which imports Office 365 audit log events into Microsoft Sentinel, to pull all Office 365 audit logs into Sentinel.

    You should be able to see your DLP incidents in Sentinel once the Microsoft Defender XDR connector and the `CloudAppEvents` event connector are set up.
2. Select **Alerts** to view the alert page.
3. You can use **AlertType**, **startTime**, and **endTime** to query the **CloudAppEvents** table to get all the user activities that contributed to the alert. Use this query to identify the underlying activities. The query retrieves a specific security alert by its `SystemAlertId`, then correlates it with `CloudAppEvents` to return the user activities that occurred within the alert time window. Replace the empty `SystemAlertId` value with the ID of the alert you want to investigate.

    Use the following KQL query to locate a specific alert from the last 30 days by its `SystemAlertId` and correlate it with user activities in `CloudAppEvents`:

```kusto
let Alert = SecurityAlert
| where TimeGenerated > ago(30d)
| where SystemAlertId == ""; // insert the systemAlertID here
CloudAppEvents
| extend correlationId1 = parse_json(tostring(RawEventData.Data)).cid
| extend correlationId = tostring(correlationId1)
| join kind=inner Alert on $left.correlationId == $right.AlertType
| where RawEventData.CreationTime > StartTime and RawEventData.CreationTime < EndTime
```