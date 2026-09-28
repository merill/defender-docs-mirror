---
layout: Conceptual
title: Microsoft Sentinel alert schema differences between standalone and XDR connectors | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/security-alert-schema-differences
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
description: Learn how alert schema, field mappings, and ingestion behavior differ between standalone connectors and the Microsoft Defender XDR connector in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: idpelleg
ms.topic: reference
ms.date: 2026-06-17T00:00:00.0000000Z
locale: en-us
document_id: a477d4a3-c519-1e8d-cf81-94b1d58fea85
document_version_independent_id: 824cdfe6-9836-d138-092f-4e6b24e10ac7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/security-alert-schema-differences.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/security-alert-schema-differences
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/security-alert-schema-differences.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: 155928e7-1e33-a64a-56e1-5a0361a44032
---

# Microsoft Sentinel alert schema differences between standalone and XDR connectors | Microsoft Learn

This article explains the differences between alerts ingested through standalone connectors and alerts ingested through the Microsoft Defender XDR connector in Microsoft Sentinel.

Standalone connectors ingest alerts directly from the original security products, whereas the Microsoft Defender XDR connector ingests alerts through the Microsoft Defender XDR pipeline. This includes connectors such as Microsoft Defender for Office 365, Microsoft Defender for Endpoint, Microsoft Defender for Identity, Information Risk Management (IRM), Data Loss Prevention (DLP), Microsoft Defender for Cloud (MDC), and Microsoft Defender for Cloud Apps (MDA).

These differences can affect field mappings, derived field behavior, schema structure, alert ingestion, and connector behavior, which might impact your existing queries, analytic rules, workbooks, and automation. Review these differences before migrating to the XDR connector or onboarding Microsoft Sentinel to the Defender portal with Microsoft Defender XDR.

For the full alert schema, see the [Security alert schema reference](security-alert-schema).

## Standalone connector behavior after onboarding to the Defender portal

After you onboard Microsoft Sentinel to the Defender portal with Microsoft Defender XDR, alerts from Microsoft security products are routed through the Microsoft Defender XDR connector instead of standalone Microsoft security product alert connectors.

In a single-workspace environment, alerts from Microsoft security products continue to be available in Microsoft Sentinel, but are ingested through the Microsoft Defender XDR connector. This change can affect source-related fields, field mappings, schema behavior, queries, analytic rules, workbooks, and automation.

In a multi-workspace environment, the Microsoft Defender XDR connector is connected to the primary workspace only. To prevent duplicate tenant-based alerts across workspaces, standalone data connectors for Microsoft Defender for Office 365, Microsoft Entra ID Protection, Microsoft Defender for Cloud Apps, Microsoft Defender for Endpoint, and Microsoft Defender for Identity are automatically disconnected in secondary workspaces during onboarding.

As a result, tenant-based alerts from these Microsoft security products are available only in the primary workspace. Any queries, analytic rules, workbooks, automation rules, or integrations that depend on alerts from standalone Microsoft security product connectors in secondary workspaces no longer function as expected after onboarding.

Non-Microsoft data connectors aren't affected by this behavior.

For more information, see [Multiple Microsoft Sentinel workspaces in the Defender portal](workspaces-defender-portal#primary-and-secondary-workspaces).

## CompromisedEntity behavior

The CompromisedEntity field is handled differently across products when alerts are ingested through the XDR connector.

| Product | CompromisedEntity equivalent value in XDR alerts |
| --- | --- |
| Microsoft Defender for Endpoint (MDE) | The device where `"LeadingHost": true` in the alert entities JSON |
| Microsoft Entra ID (Identity Protection) | Always set to the user’s UPN |
| Microsoft Defender for Identity (MDI) | Fixed string `"CompromisedEntity"` |

Note

In MDE alerts, CompromisedEntity is derived from the device where `"LeadingHost": true`. In some alerts, this field might not be populated.

In MDI alerts, CompromisedEntity doesn't represent a host or user and is always the literal string `"CompromisedEntity"`.

## Field mapping changes

Some fields are renamed or use different value sets in alerts from the XDR connector.

| Product | Legacy field/property | XDR behavior |
| --- | --- | --- |
| MDE | ExtendedProperties.MicrosoftDefenderAtp.Category | Mapped to `ExtendedProperties.Category` |
| Microsoft Defender for Office (MDO) | ExtendedProperties.Status | Uses a different value set from legacy |
| Microsoft Defender for Office (MDO) | ExtendedProperties.InvestigationName | Not available |

## Structural schema transformations (MDI)

The standalone Microsoft Defender for Identity (MDI) connector sometimes used placeholder entities to store additional information. In the XDR connector, this information is folded into properties under the `resourceAccessEvents` collection.

| Legacy entity/property | XDR representation |
| --- | --- |
| ResourceAccessInfo.Time | `resourceAccessEvents[].AccessDateTime` |
| ResourceAccessInfo.IpAddress | `resourceAccessEvents[].IpAddress` |
| ResourceAccessInfo.ResourceIdentifier.AccountId | `resourceAccessEvents[].AccountId` |
| ResourceAccessInfo.ResourceIdentifier.ResourceName | `resourceAccessEvents[].ResourceIdentifier` |
| DomainResourceIdentifier | `resourceAccessEvents[].ResourceIdentifier` |

ResourceAccessInfo.ComputerId is no longer required because it's identical to the Host entity that ResourceAccessInfo is defined in.

## Alert ingestion filtering

Some alerts available through standalone connectors aren't ingested through the XDR connector.

| Product | Filtering behavior |
| --- | --- |
| Microsoft Defender for Cloud (MDC) | Informational severity alerts aren't ingested |
| Microsoft Entra ID | By default, alerts below High severity aren't ingested; customers can configure ingestion to include all severities |

## Scoping behavior (Microsoft Defender for Cloud)

Microsoft Defender for Cloud alerts use different scoping when ingested through the XDR connector.

| Standalone connector scope | XDR connector scope |
| --- | --- |
| Subscription level | Tenant level |

Note

All MDC alerts are available in the primary workspace for the tenant. Alerts are scoped according to MDC subscription scopes within Defender XDR.