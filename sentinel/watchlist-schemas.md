---
layout: Conceptual
title: Schemas for Microsoft Sentinel watchlist templates | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/watchlist-schemas
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
description: Learn about the schemas used in each built-in watchlist template in Microsoft Sentinel.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: reference
ms.date: 2023-12-15T00:00:00.0000000Z
locale: en-us
document_id: d371b2f2-4f20-5edb-e0a9-1bf034e9ad3b
document_version_independent_id: 1da0dbb0-7828-3afd-d1e4-649e683a2f69
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/watchlist-schemas.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/watchlist-schemas
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/watchlist-schemas.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 81b7d099-ea2e-a319-86fa-9d605a94a4bc
---

# Schemas for Microsoft Sentinel watchlist templates | Microsoft Learn

This article details the schemas used in each built-in watchlist template provided by Microsoft Sentinel. For more information, see [Create watchlists in Microsoft Sentinel](watchlists-create).

The Microsoft Sentinel watchlist templates are currently in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## High Value Assets

The High Value Assets watchlist lists devices, resources, and other assets that have critical value in the organization, and includes the following fields:

| Field name | Format | Example | Mandatory/Optional |
| --- | --- | --- | --- |
| **Asset Type** | String | `Device`, `Azure resource`, `AWS resource`, `URL`, `SPO`, `File share`, `Other` | Mandatory |
| **Asset Id** | String, depending on asset type | `/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/SOC-Purview/providers/Microsoft.Storage/storageAccounts/purviewadls` | Mandatory |
| **Asset Name** | String | `Microsoft.Storage/storageAccounts/purviewadls` | Optional |
| **Asset FQDN** | FQDN | `Finance-SRv.local.microsoft.com` | Mandatory |
| **IP Address** | IP | `1.1.1.1` | Optional |
| **Tags** | List | `["SAW user","Blue Ocean team"] ` for CSV files created in Microsoft Excel or `[""SAW user"",""Blue Ocean team""] ` for CSV files created in a text editor | Optional |

## VIP Users

The VIP Users watchlist lists user accounts of employees that have high impact value in the organization, and includes the following values:

| Field name | Format | Example | Mandatory/Optional |
| --- | --- | --- | --- |
| **User Identifier** | UID | `52322ec8-6ebf-11eb-9439-0242ac130002` | Optional |
| **User AAD Object Id** | SID | `aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb` | Optional |
| **User On-Prem Sid** | SID | `S-1-12-1-4141952679-1282074057-627758481-2916039507` | Optional |
| **User Principal Name** | UPN | `JeffL@seccxp.ninja` | Mandatory |
| **Tags** | List | `["SAW user","Blue Ocean team"]` for CSV files created in Microsoft Excel or `[""SAW user"",""Blue Ocean team""]` for CSV files created in a text editor | Optional |

## Network Addresses

The Network Addresses watchlist lists IP subnets and their respective organizational contexts, and includes the following fields:

| Field name | Format | Example | Mandatory/Optional |
| --- | --- | --- | --- |
| **IP Subnet** | Subnet range | `198.51.100.0/24` | Mandatory |
| **Range Name** | String | `DMZ` | Optional |
| **Tags** | List | `["Example","Example"]` for CSV files created in Microsoft Excel or `[""Example"",""Example""]` for CSV files created in a text editor | Optional |

## Terminated Employees

The Terminated Employees watchlist lists user accounts of employees that have been, or are about to be, terminated, and includes the following fields:

| Field name | Format | Example | Mandatory/Optional |
| --- | --- | --- | --- |
| **User Identifier** | UID | `52322ec8-6ebf-11eb-9439-0242ac130002` | Optional |
| **User AAD Object Id** | SID | `aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb` | Optional |
| **User On-Prem Sid** | SID | `S-1-12-1-4141952679-1282074057-123` | Optional |
| **User Principal Name** | UPN | `JeffL@seccxp.ninja` | Mandatory |
| **UserState** | String We recommend using either `Notified` or `Terminated` | `Terminated` | Mandatory |
| **Notification date** | Timestamp - day We recommend using the UTC format | `2020-12-1` | Optional |
| **Termination date** | Timestamp - day We recommend using the UTC format | `2021-01-01` | Mandatory |
| **Tags** | List | `["SAW user","Amba Wolfs team"]` for CSV files created in Microsoft Excel or `[""SAW user"",""Amba Wolfs team""]` for CSV files created in a text editor | Optional |

## Identity Correlation

The Identity Correlation watchlist lists related user accounts that belong to the same person, and includes the following fields:

| Field name | Format | Example | Mandatory/Optional |
| --- | --- | --- | --- |
| **User Identifier** | UID | `52322ec8-6ebf-11eb-9439-0242ac130002` | Optional |
| **User AAD Object Id** | SID | `aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb` | Optional |
| **User On-Prem Sid** | SID | `S-1-12-1-4141952679-1282074057-627758481-2916039507` | Optional |
| **User Principal Name** | UPN | `JeffL@seccxp.ninja` | Mandatory |
| **Employee Id** | String | `8234123` | Optional |
| **Email** | Email | `JeffL@seccxp.ninja` | Optional |
| **Associated Privileged Account ID** | UID/SID | `S-1-12-1-4141952679-1282074057-627758481-2916039507` | Optional |
| **Associated Privileged Account** | UPN | `Admin@seccxp.ninja` | Optional |
| **Tags** | List | `["SAW user","Amba Wolfs team"]` for CSV files created in Microsoft Excel or `[""SAW user"",""Amba Wolfs team""]`for CSV files created in a text editor | Optional |

## Service Accounts

The Service Accounts watchlist lists service accounts and their owners, and includes the following fields:

| Field name | Format | Example | Mandatory/Optional |
| --- | --- | --- | --- |
| **Service Identifier** | UID | `1111-112123-12312312-123123123` | Optional |
| **Service AAD Object Id** | SID | `11123-123123-123123-123123` | Optional |
| **Service On-Prem Sid** | SID | `S-1-12-1-3123123-123213123-12312312-2916039507` | Optional |
| **Service Principal Name** | UPN | `myserviceprin@contoso.com` | Mandatory |
| **Owner User Identifier** | UID | `52322ec8-6ebf-11eb-9439-0242ac130002` | Optional |
| **Owner User AAD Object Id** | SID | `aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb` | Optional |
| **Owner User On-Prem Sid** | SID | `S-1-12-1-4141952679-1282074057-627758481-2916039507` | Optional |
| **Owner User Principal Name** | UPN | `JeffL@seccxp.ninja` | Mandatory |
| **Tags** | List | `["Automation Account","GitHub Account"]` for CSV files created in Microsoft Excel or `[""Automation Account"",""GitHub Account""]`for CSV files created in a text editor | Optional |