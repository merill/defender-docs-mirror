---
layout: Conceptual
title: What changes when managing cloud security plans in the Defender portal - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-portal/plan-management-changes-defender-portal
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
description: Understand how billing, configuration scope, and cloud security plans change when you manage plans in the Microsoft Defender portal.
ms.topic: concept-article
ms.date: 2026-07-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 6bbdef1a-16bd-baa5-124e-d3d4dd3a658e
document_version_independent_id: 231176ed-e608-c735-011a-63279dd26ad8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-portal/plan-management-changes-defender-portal.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: ../toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-portal/plan-management-changes-defender-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-portal/plan-management-changes-defender-portal.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 987fefc1-754a-3e91-4dfc-bec0a0e69be9
---

# What changes when managing cloud security plans in the Defender portal - Microsoft Defender for Cloud | Microsoft Learn

Important

This feature is in preview. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

When you move Defender for Cloud plan management from the Azure portal to the Microsoft Defender portal, the way that plans are billed, configured, and applied changes.

Before moving an Azure environment, review the following changes:

- Billing moves to the Defender Workload Unit model.
- Plan configuration moves from resource-level settings to tenant-level, management-group, and subscription settings.
- Some existing plans are replaced, consolidated, or measured differently.

## Defender Workload Unit billing

After an Azure subscription moves to Defender portal plan management, billing is based on Defender Workload Units (DWUs).

Each supported protected workload maps to a defined number of DWUs. The same unit model is used for:

- Cost estimation
- Usage reporting
- Billing

For more information about estimating and reviewing DWU usage, see [Estimate and track Cloud security cost](estimate-track-costs).

## Scope-based plan management

The Defender portal uses a top-down plan-management model.

Plans and their settings are configured at the tenant, management-group, or subscription level. Resource-level plan configuration isn't supported.

When a plan is enabled for a subscription, either directly or through an inherited configuration:

- All supported resources in the subscription receive protection.
- New supported resources created in the subscription inherit protection automatically.
- Plan coverage is applied consistently across the subscription.

When a plan is disabled for a subscription, protection is removed from all supported resources in that subscription.

Important

Existing resource-level configurations aren't preserved when plan management moves from the Azure portal to the Defender portal. They are replaced by the configuration applied at the management-group or subscription scope.

After an environment moves to Defender portal management:

- Plan configuration is managed in the Defender portal.
- Plan configuration appears as view-only in the Azure portal.
- Billing for migrated subscriptions uses DWUs.
- Cost becomes available in the Cloud Security Cost & usage report.

## Security plan changes

Some existing plans are replaced, consolidated, or measured differently when they move to the Defender portal.

| Current plan | Updated plan or behavior |
| --- | --- |
| Defender for Key Vault billed by transaction | Defender for Key Vault billed per resource |
| Defender for Storage V1 billed by transaction | Defender for Storage V2 billed per resource |
| Defender for Resource Manager billed by transaction | Defender for Resource Manager billed per resource |
| Defender for Containers billed by vCPU | Defender for Containers billed by protected node |
| Defender for Azure SQL Databases, Defender for SQL Servers on Machines, and Defender for Open-Source Relational Databases | Consolidated Defender for Databases plan |
| Defender for DNS | Continue without DNS protection, or enable Defender for Servers Plan 2 |

Most supported plans are mapped automatically to the new model.

Defender for DNS isn't carried forward automatically. During migration, choose whether to:

- Continue without DNS protection.
- Enable Defender for Servers Plan 2, which includes DNS protection and might result in additional charges.

Review the changes shown in the Defender portal before confirming the migration.