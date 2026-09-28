---
layout: Conceptual
title: Support and prerequisites for deploying the Defender for APIs plan - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-apis-prepare
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn about the requirements for Defender for APIs deployment in Microsoft Defender for Cloud
ms.topic: checklist
ms.date: 2026-06-29T00:00:00.0000000Z
ms.custom: references_regions
ai-usage: ai-assisted
locale: en-us
document_id: 1d655f74-812d-214d-4d2c-ec088ee06cad
document_version_independent_id: eebae882-aa29-ed02-24fe-91c163afdf0f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-apis-prepare.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-apis-prepare
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-apis-prepare.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/bf4dbf7f-261c-4ae9-9fee-5989668a780a
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/1c4b5d48-3f26-4bd8-9592-816d9c1a3420
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 416dfe17-4971-0ee7-1550-f8ca6e832448
---

# Support and prerequisites for deploying the Defender for APIs plan - Microsoft Defender for Cloud | Microsoft Learn

Review the onboarding requirements on this page before setting up [Microsoft Defender for APIs](defender-for-apis-introduction).

## Cloud and region support

Defender for APIs is available in the Azure commercial cloud, in these regions:

- Asia (Southeast Asia, East Asia)
- Australia (Australia East, Australia Southeast, Australia Central, Australia Central 2)
- Brazil (Brazil South, Brazil Southeast)
- Canada (Canada Central, Canada East)
- Europe (West Europe, North Europe)
- France (France Central, France South)
- Germany (Germany West Central, Germany North)
- India (Central India, South India, West India)
- Italy (Italy North)
- Japan (Japan East, Japan West)
- Korea (Korea Central, Korea South)
- Norway (Norway East, Norway West)
- South Africa (South Africa North, South Africa West)
- Sweden (Sweden Central, Sweden South)
- Switzerland (Switzerland North, Switzerland West)
- UAE (UAE Central, UAE North)
- UK (UK South, UK West)
- US (East US, East US 2, West US, West US 2, West US 3, Central US, North Central US, South Central US, West Central US, East US 2 EUAP, Central US EUAP)

Review the latest cloud support information for Defender for Cloud plans and features in the [cloud support matrix](support-matrix-defender-for-cloud).

## API support

| **Feature** | **Supported** |
| --- | --- |
| Availability | This feature is available in the Premium, Standard, Basic, and Developer tiers of Azure API Management. |
| API gateways | Azure API Management Defender for APIs currently doesn't onboard APIs that are exposed using the API Management [self-hosted gateway](/en-us/azure/api-management/self-hosted-gateway-overview), or managed using API Management [workspaces](/en-us/azure/api-management/workspaces-overview). |
| API types | Currently, Defender for APIs discovers and analyzes REST APIs. |

## Defender CSPM integration

To explore API security risks using Cloud Security Explorer, the Defender Cloud Security Posture Management (CSPM) plan must be enabled. [Learn more](concept-cloud-security-posture-management).

## Onboarding requirements

Onboarding requirements for Defender for APIs are as follows.

| **Requirement** | **Details** |
| --- | --- |
| API Management instance | At least one API Management instance in an Azure subscription. Defender for APIs is enabled at the level of a subscription. One or more supported APIs must be imported to the API Management instance. |
| Azure account | You need an Azure account to sign in to the Azure portal. |
| Onboarding permissions | To enable and onboard Defender for APIs, you'll need [API Management Service Contributor](/en-us/azure/api-management/api-management-role-based-access-control#built-in-service-roles) role access, along with the permissions outlined in the [User roles and permissions](permissions#roles-and-allowed-actions) for enabling Microsoft Defender plans. |
| Onboarding location | You can [enable Defender for APIs in the Defender for Cloud portal](defender-for-apis-deploy), or in the [Azure API Management portal](/en-us/azure/api-management/protect-with-defender-for-apis). |