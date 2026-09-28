---
layout: Conceptual
title: Monitor ASR rule activity - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/attack-surface-reduction-rules-monitor
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to monitor attack surface reduction (ASR) rule events using advanced hunting, the device timeline, and Windows Event Viewer in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.subservice: asr
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.reviewer: sugamar, yongrhee
ms.custom: asr, msecd-doc-authoring-1016
ms.topic: how-to
ms.collection:
- m365-security
- m365solution-asr-rules
- highpri
- tier1
- mde-asr
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: da14dc3b-fea9-6894-7d73-c7f2ddf530cc
document_version_independent_id: da14dc3b-fea9-6894-7d73-c7f2ddf530cc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/attack-surface-reduction-rules-monitor.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-surface-reduction-rules-monitor
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/attack-surface-reduction-rules-monitor.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: c4e1fdb7-4b98-47c0-d1ae-b0f039839540
---

# Monitor ASR rule activity - Microsoft Defender for Endpoint | Microsoft Learn

A critical part of any deployment of attack surface reduction (ASR) rules is monitoring the effect of rules on devices. You can view ASR rule events in your Microsoft Defender for Endpoint organization by using the ASR rules report, Advanced Hunting queries, the device timeline, or Windows Event Viewer. For more information about ASR rules, see [Attack surface reduction (ASR) rules overview](attack-surface-reduction-rules-overview).

## View the ASR rules report

Note

This feature requires Microsoft Defender for Endpoint Plan 2 or Microsoft Defender for Business.

For complete information, see [Attack surface reduction rules report in the Microsoft Defender portal](attack-surface-reduction-rules-report).

## Query ASR rule events in Advanced Hunting

Note

This feature requires Microsoft Defender for Endpoint Plan 2.

One of the most powerful features of [Microsoft Defender XDR](https://security.microsoft.com) is advanced hunting. If you're not familiar with advanced hunting, see [Proactively hunt for threats with advanced hunting](/en-us/defender-xdr/advanced-hunting-overview).

Advanced hunting is a Kusto Query Language (KQL) threat-hunting tool in the Microsoft Defender portal that lets you explore up to 30 days of the captured (raw) data from devices. You can proactively inspect events to find interesting indicators and entities for both known and potential threats.

Through advanced hunting, you can extract ASR rule information, create reports, and get detailed context on a specific audit or block event from ASR rules.

ASR rule events are available in the `DeviceEvents` table on the **Advanced hunting** page of the Defender portal at https://security.microsoft.com/v2/advanced-hunting.

Attack surface reduction events shown in advanced hunting are throttled to unique processes seen every hour. The time of the attack surface reduction event is the first time the event is seen within that hour.

The following sample query reports all events from the last 30 days with ASR rules as the data source. The query summarizes by `ActionType` count, which is the ASR rule.

```kusto
DeviceEvents
| where Timestamp > ago(30d)
| where ActionType startswith "Asr"
| summarize EventCount=count() by ActionType
```

[![Screenshot of the Advanced hunting page in the Microsoft Defender portal with the example DeviceEvents query results.](media/advanced-hunting-attack-surface-reduction-rules-query.png)](media/advanced-hunting-attack-surface-reduction-rules-query.png#lightbox)

To focus on a specific rule and get details on the actual files and processes involved, change the filter for `ActionType` and replace the `summarize` line with a `project` line that contains the fields you want to see. The following query filters for Office child-process ASR events and extracts the corresponding `RuleId` from `AdditionalFields` to help troubleshoot rule behavior:

```kusto
DeviceEvents
| where (ActionType startswith "AsrOfficechild")
| extend RuleId=extractjson("$Ruleid", AdditionalFields, typeof(string))
| project DeviceName, FileName, FolderPath, ProcessCommandLine, InitiatingProcessFileName, InitiatingProcessCommandLine
```

Advanced hunting lets you customize queries to target individual devices or extract insights from your entire environment.

For more information about hunting options, see [Demystifying attack surface reduction rules - Part 3](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/demystifying-attack-surface-reduction-rules-part-3/ba-p/1360968).

## View ASR events in the device timeline

Note

This feature requires Microsoft Defender for Endpoint Plan 2 or Microsoft Defender for Business.

A narrower scoped alternative to advanced hunting is the Defender for Endpoint device timeline. For more information, see [Microsoft Defender for Endpoint device timeline](investigate-machines#investigate-device-timeline).

To open the device timeline of a device in the Microsoft Defender portal, complete the following steps:

1. Open the **Device Inventory** page at https://security.microsoft.com/machines.
2. On the appropriate tab of the **Device Inventory** page (for example, **All devices** or **Computers & mobile**), select a device by selecting the device name link.
3. In the details page that opens, select the **Timeline** tab.
4. On the **Timeline** tab, select **Filter**. In the **Filter** flyout that opens, select **ASR events** from the **Event group** section, and then select **Apply**.

    The default timeframe is **1 week**, but you can also select **1 day**, **3 days**, **30 days**, or a custom date range within 30 days.

[![Screenshot of the Timeline tab of the device details page of a device selected from the Device Inventory page of the Microsoft Defender portal. The results are filtered by the Event group value ASR events.](media/device-inventory-timeline.png)](media/device-inventory-timeline.png#lightbox)

## View ASR events in Windows Event Viewer

For complete information, see [Attack surface reduction events in Windows Event Viewer](attack-surface-reduction-windows-events).

## Troubleshoot ASR rules

To troubleshoot ASR rules, see [Troubleshoot attack surface reduction rules](troubleshoot-asr).