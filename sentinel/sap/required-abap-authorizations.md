---
layout: Conceptual
title: Required ABAP authorizations for the Microsoft Sentinel solution for SAP applications | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/required-abap-authorizations
breadcrumb_path: ../breadcrumb/toc.json
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
ms.reviewer: mapankra
description: Understand the ABAP authorizations required for the SAP user account used by the Microsoft Sentinel agentless data connector.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: c28f8cf6-03c6-9eeb-2095-794c26a8a121
document_version_independent_id: 42a0c856-19d8-05bf-729f-932879a09ede
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/required-abap-authorizations.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/required-abap-authorizations
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/required-abap-authorizations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 6ef5c2d1-c9be-9f0e-8fd8-22c12b794953
---

# Required ABAP authorizations for the Microsoft Sentinel solution for SAP applications | Microsoft Learn

This article lists the ABAP authorizations required for the SAP user account used by the Microsoft Sentinel agentless data connector.

To create a role with the required authorizations, load the authorizations from the [**MSFTSEN\_SENTINEL\_READER**](https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/Solutions/SAP/Sample%20Authorizations%20Role%20File/MSFTSEN_SENTINEL_READER.SAP) file.

The following table lists the authorizations in the reader role. If you manually define a role, include all the listed authorizations.

## Agentless data collection

The following authorization objects are required for agentless data collection.

| Authorization object | Field | Value |
| --- | --- | --- |
| S\_ADMI\_FCD | S\_ADMI\_FCD | AUDD |
| S\_RFC | ACTVT | Execute |
| S\_RFC | RFC\_NAME | /OSP/SYSTEM\_TIMEZONE |
| S\_RFC | RFC\_NAME | BAPI\_USER\_GET\_DETAIL |
| S\_RFC | RFC\_NAME | RFCPING |
| S\_RFC | RFC\_NAME | RFC\_METADATA\_GET |
| S\_RFC | RFC\_NAME | RFC\_READ\_TABLE |
| S\_RFC | RFC\_NAME | RSAU\_API\_GET\_LOG\_DATA |
| S\_RFC | RFC\_NAME | SIAG\_ROLE\_GET\_AUTH |
| S\_RFC | RFC\_TYPE | Function group |
| S\_RFC | RFC\_TYPE | Function module |
| S\_SAL | SAL\_ACTVT | SHOW\_LOG |
| S\_TABU\_NAM | ACTVT | Display |
| S\_TABU\_NAM | TABLE | AGR\_1251 |
| S\_TABU\_NAM | TABLE | AGR\_DEFINE |
| S\_TABU\_NAM | TABLE | AGR\_USERS |
| S\_TABU\_NAM | TABLE | CDHDR |
| S\_TABU\_NAM | TABLE | CDPOS |
| S\_TABU\_NAM | TABLE | PAHI |
| S\_TABU\_NAM | TABLE | T000 |
| S\_TABU\_NAM | TABLE | USR02 |
| S\_TABU\_NAM | TABLE | USRSTAMP |
| S\_TCODE | TCD | SUIM |
| S\_USER\_GRP | ACTVT | Display |
| S\_USER\_GRP | ACTVT | Lock |
| S\_USER\_GRP | CLASS | SUPER |
| S\_USER\_UID | ACTVT | Display |
| S\_USER\_UID | CLASS | SUPER |
| S\_USER\_UID | EXTUID\_TYPGU | \* |