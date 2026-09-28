---
layout: Conceptual
title: Risk evaluation framework changelog - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/risk-evaluation-changelog
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Track MSEM-initiated changes to the Risk Evaluation Framework that affect Secure Score and recommendation risk level calculations in Microsoft Security Exposure Management.
ms.topic: reference
ms.date: 2026-07-01T00:00:00.0000000Z
locale: en-us
document_id: db590731-5fba-e915-74cf-c00c4dbae344
document_version_independent_id: db590731-5fba-e915-74cf-c00c4dbae344
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/risk-evaluation-changelog.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: risk-evaluation-changelog
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/risk-evaluation-changelog.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: 2439e53c-d5f3-22ff-f085-27f4efc777fc
---

# Risk evaluation framework changelog - Microsoft Security Exposure Management | Microsoft Learn

The Risk Evaluation Framework (REF) changelog documents MSEM-initiated changes that affect how security risk is evaluated in your environment. Changes reflect updates to **inputs and components** of the REF - such as scope, weights, and coverage - not the underlying scoring formula.

Review this changelog if you notice unexpected changes to:

- Your risk-based secure score
- Recommendation risk levels

## Understanding REF updates

MSEM initiates REF changes, not customer actions. They might include:

- **New recommendations introduced to the framework** to expand risk visibility across emerging security scenarios
- **New asset risk factors added to evaluations** to improve attack surface coverage and strengthen risk assessment depth
- **Risk weighting updates** to improve evaluation accuracy and better reflect relative security impact
- **Evaluation scope or domain definition changes** to provide more granular and context-aware risk evaluation metrics

Note

These changes reflect updates to risk evaluation inputs and components. The core scoring formula remains stable.

## Changelog

Note

This changelog includes publicly available changes only. Private preview updates are communicated separately through preview communications and in-app experiences.

| Date | Change type | Description | More information |
| --- | --- | --- | --- |
| 30 June 2026 | New recommendations added | 200+ multi-cloud recommendations are now generally available. | [What's new in Defender for Cloud](/en-us/azure/defender-for-cloud/release-notes#expanded-multicloud-security-coverage-is-now-generally-available) |
| 26 July 2026 | New recommendations added | 80+ Defender for SQL Vulnerability Assessment recommendations are now generally available | [Database-level recommendations experience for SQL Vulnerability Assessment](https://aka.ms/SQLVARecommendations) |