---
layout: Conceptual
title: Overview of Endor Labs integration - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/integration-endor-labs
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
description: Learn how integrating Endor Labs with Microsoft Defender for Cloud enhances vulnerability analysis by identifying exploitable open-source vulnerabilities from code to runtime.
ms.topic: overview
ms.date: 2025-12-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 8d6c98be-cc73-6271-af93-cdfacf5fc351
document_version_independent_id: b7de1869-c293-0016-ab8c-ceb854da9f13
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/integration-endor-labs.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/integration-endor-labs
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/integration-endor-labs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: f683dc5c-6e56-4294-38b5-ea4a77032beb
---

# Overview of Endor Labs integration - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud integrates with Endor Labs to enhance vulnerability analysis by adding reachability-based Software Composition Analysis (SCA), helping security teams focus on open-source vulnerabilities that are exploitable within an application’s execution flow.

By correlating signals from source code repositories, build pipelines, and deployed workloads, Defender for Cloud provides visibility into exploitable vulnerabilities across the application lifecycle—from code development to runtime environments.

## Reachable vulnerabilities and risk prioritization

Reachable vulnerabilities are security flaws in open-source packages that have a confirmed execution path within an application. Unlike vulnerabilities that exist in unused or inactive code paths, reachable vulnerabilities can be actively triggered and exploited, making them higher risk.

The Endor Labs integration identifies vulnerable security combinations, such as exploitable open-source dependencies used by internet-exposed workloads. This reachability context enables Defender for Cloud to prioritize vulnerabilities based on exploitability rather than severity alone.

## Unified visibility across code and runtime

With this integration, Defender for Cloud correlates vulnerabilities identified in source repositories—such as Azure DevOps, GitHub, and GitLab—with workloads running across Azure, Amazon Web Services (AWS), and Google Cloud Platform (GCP). Security teams can trace attack paths from a vulnerable code commit through build and deployment pipelines to affected runtime resources.

Reachability analysis findings from Endor Labs surface directly in Defender for Cloud experiences, including:

- Security recommendations
- Attack path analysis
- Security explorer

This unified view helps central security teams understand how open-source risks propagate through their environments and where remediation efforts will have the greatest impact.

## Benefits of integrating Endor Labs

Integrating Endor Labs with Microsoft Defender for Cloud enables you to:

- Prioritize remediation by focusing on vulnerabilities that are actively exploitable.
- Reduce noise from vulnerabilities that don’t pose immediate risk.
- Gain code-to-runtime visibility into how open-source dependencies affect deployed workloads.
- Identify high-risk vulnerabilities earlier in the development lifecycle.