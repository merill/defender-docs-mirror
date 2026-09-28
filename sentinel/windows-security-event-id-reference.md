---
layout: Conceptual
title: Windows security event sets that can be sent to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/windows-security-event-id-reference
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
description: Learn about the pre-built sets of Windows security events that you can collect and stream from your Windows systems to your Microsoft Sentinel workspace. 
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: reference
ms.date: 2026-08-07T00:00:00.0000000Z
locale: en-us
document_id: 4eb77102-37af-a1dd-ddc6-58a9f2ed5a4e
document_version_independent_id: 4a1dff58-da2f-bf3b-a262-227c5c6edc8f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/windows-security-event-id-reference.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/windows-security-event-id-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/windows-security-event-id-reference.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/691e3042-55ad-4ce1-b5e9-649b1cc47b5c
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b7d11190-096c-4ddb-87db-63764f603aac
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: ba295673-6025-7001-306a-0c957f64a4e3
---

# Windows security event sets that can be sent to Microsoft Sentinel | Microsoft Learn

When ingesting security events from Windows devices using the [Windows Security Events data connector](data-connectors-reference#windows-security-events-via-ama) (including the legacy version), you can choose which events to collect from among the following sets:

The Windows Security Events via AMA connector writes these events to the `SecurityEvent` table, which is queried by many built-in Windows security analytics rules. The Windows Forwarded Events connector writes forwarded events to `WindowsEvent` instead. If forwarded events don't trigger a built-in rule, verify which table the rule queries, and either use the Windows Security Events via AMA connector or adapt the rule for `WindowsEvent`.

- **All events** - Collects the full, unfiltered set of events from the Windows Security event log and the AppLocker event log channels. The Security log (`Windows Logs > Security` in Event Viewer) records auditing events such as logons, privilege use, and policy changes. The AppLocker logs (`Application and Services Logs > Microsoft > Windows > AppLocker`) cover application execution and installation policies. This set does *not* include events from other Windows event logs such as Application, System, or Setup.
- **Common** - A standard set of events for auditing purposes. A full user audit trail is included in this set. For example, it contains both user sign-in and user sign-out events (event IDs 4624, 4634). There are also auditing actions such as security group changes, key domain controller Kerberos operations, and other types of events in line with accepted best practices.

    The **Common** event set may contain some types of events that aren't so common. This is because the main point of the **Common** set is to reduce the volume of events to a more manageable level, while still maintaining full audit trail capability.
- **Minimal** - A small set of events that might indicate potential threats. This set does not contain a full audit trail. It covers only events that might indicate a successful breach, and other important events that have very low rates of occurrence. For example, it contains successful and failed user logons (event IDs 4624, 4625), but it doesn't contain sign-out information (4634) which, while important for auditing, is not meaningful for breach detection and has relatively high volume. Most of the data volume of this set consists of sign-in events and process creation events (event ID 4688).
- **Custom** - A set of events determined by you, the user, and defined in a data collection rule using XPath queries. [Learn more about data collection rules](/en-us/azure/azure-monitor/agents/data-collection-windows-events#filter-events-using-xpath-queries).

## Event ID reference

The following list provides a complete breakdown of the Security and App Locker event IDs for each set:

| Event set | Collected event IDs |
| --- | --- |
| **Minimal** | 1102, 4624, 4625, 4657, 4663, 4688, 4700, 4702, 4719, 4720, 4722, 4723, 4724, 4727, 4728, 4732, 4735, 4737, 4739, 4740, 4754, 4755, 4756, 4767, 4799, 4825, 4946, 4948, 4956, 5024, 5033, 8001, 8002, 8003, 8004, 8005, 8006, 8007, 8222 |
| **Common** | 1, 299, 300, 324, 340, 403, 404, 410, 411, 412, 413, 431, 500, 501, 1100, 1102, 1107, 1108, 4608, 4610, 4611, 4614, 4622, 4624, 4625, 4634, 4647, 4648, 4649, 4657, 4661, 4662, 4663, 4665, 4666, 4667, 4688, 4670, 4672, 4673, 4674, 4675, 4689, 4697, 4700, 4702, 4704, 4705, 4716, 4717, 4718, 4719, 4720, 4722, 4723, 4724, 4725, 4726, 4727, 4728, 4729, 4733, 4732, 4735, 4737, 4738, 4739, 4740, 4742, 4744, 4745, 4746, 4750, 4751, 4752, 4754, 4755, 4756, 4757, 4760, 4761, 4762, 4764, 4767, 4768, 4771, 4774, 4778, 4779, 4781, 4793, 4797, 4798, 4799, 4800, 4801, 4802, 4803, 4825, 4826, 4870, 4886, 4887, 4888, 4893, 4898, 4902, 4904, 4905, 4907, 4931, 4932, 4933, 4946, 4948, 4956, 4985, 5024, 5033, 5059, 5136, 5137, 5140, 5145, 5632, 6144, 6145, 6272, 6273, 6278, 6416, 6423, 6424, 8001, 8002, 8003, 8004, 8005, 8006, 8007, 8222, 26401, 30004 |
|  |  |