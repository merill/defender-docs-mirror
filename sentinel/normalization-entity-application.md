---
layout: Conceptual
title: The Advanced Security Information Model (ASIM) Application Entity reference - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-entity-application
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
ms.reviewer: ofshezaf
description: This article displays the Microsoft Sentinel Application Entity schema.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2025-12-29T00:00:00.0000000Z
locale: en-us
document_id: 141d39cc-ff31-dd1b-a7a6-72687d8d0849
document_version_independent_id: 9596c3c2-9927-a8b5-f090-09c08499e4f1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-entity-application.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-entity-application
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-entity-application.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: f60a8b0e-86b2-a5a9-b7a5-e71ba680d87c
---

# The Advanced Security Information Model (ASIM) Application Entity reference - Microsoft Sentinel | Microsoft Learn

## Prefixes

Different ASIM schemas prefix the entity fields by the following prefixes:

- `Src` is typically used to designate a client application.
- `Dst` or `Target` is commonly used to designate a remote application, typically on a server.

## Fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **AppName** | Optional | String | The name of the application.Example: `Facebook` |
| **AppId** | Optional | String | The ID of the application, as reported by the reporting device. If AppType is `Process`, `DstAppId` and `DstProcessId` should have the same value.Example: `124` |
| **AppType** | Optional | AppType | The type of the application. Supported values include: `Process`, `Service`, `Resource`, `URL`, `SaaS application`, `CSP`, and `Other`.This field is mandatory if DstAppName or DstAppId are used. |
| **ProcessName** | Optional | String | The file name of the process used by the application. Example: `C:\Windows\explorer.exe` |
| **Process** | Alias |  | Alias to the ProcessNameExample: `C:\Windows\System32\rundll32.exe` |
| **ProcessId** | Optional | String | The process ID (PID) of the process the application is using.Example: `48610176`**Note**: The type is defined as *string* to support varying systems, but on Windows and Linux this value must be numeric. If you are using a Windows or Linux machine and used a different type, make sure to convert the values. For example, if you used a hexadecimal value, convert it to a decimal value. |
| **ProcessGuid** | Optional | String | A generated unique identifier (GUID) of the process used by the application.  Example: `01234567-89AB-CDEF-0123-456789ABCDEF` |