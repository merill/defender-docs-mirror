---
layout: Conceptual
title: Gated deployment for Kubernetes container images - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/runtime-gated-overview
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
description: Learn how gated deployment in Microsoft Defender for Containers uses vulnerability findings to audit or deny Kubernetes deployments.
ms.date: 2026-06-01T00:00:00.0000000Z
ms.topic: overview
ai-usage: ai-assisted
locale: en-us
document_id: 5a632014-1aed-5d7e-cb82-00550d7f1dbf
document_version_independent_id: 77176bdc-ad22-6bdc-9941-0f42439a6691
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/runtime-gated-overview.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/runtime-gated-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/runtime-gated-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/cb49e66a-8528-497d-adaa-eade2d009d1b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/472c9d15-157b-443c-afa2-e209c8fecf58
platformId: bd3560dc-3200-ee75-861e-346303f8ffb0
---

# Gated deployment for Kubernetes container images - Microsoft Defender for Cloud | Microsoft Learn

Gated deployment is a Microsoft Defender for Containers capability that uses an admission controller to evaluate container images before they're admitted into a Kubernetes cluster. It uses vulnerability assessment findings from supported container registries to audit or deny deployments when container images don't meet your organization's vulnerability policy.

Use gated deployment to enforce vulnerability-based controls during Kubernetes deployment. For example, you can audit image deployments with high or critical vulnerabilities, deny deployments that match configured vulnerability conditions, apply rules to specific scopes such as clusters or namespaces, and create exemptions for specific vulnerabilities or resources.

## How gated deployment works

1. Defender for Containers scans supported container images.
2. Vulnerability findings are associated with the image.
3. A user or pipeline requests to deploy the image to a Kubernetes cluster.
4. The admission controller evaluates the image against gated deployment rules.
5. If a rule matches, gated deployment applies the configured action.

The rule action determines what happens to the deployment:

- **Audit** allows the deployment and creates an admission event for review.
- **Deny** blocks deployments that match the rule conditions.

If vulnerability findings artifacts aren't available for an image, gated deployment behavior depends on the rule configuration.

## Default and custom rules

After the required prerequisites are met, Defender for Containers creates a default audit rule that flags image deployments with high or critical vulnerabilities.

You can create custom rules to define:

- The cloud and resource scope of the rule.
- The vulnerability conditions that trigger the rule.
- Exemptions for specific vulnerabilities or resources.

## Monitoring

You can monitor gated deployment events to review rule evaluations, triggered actions, affected resources, and rule configuration details. Use these events to help refine rule scope, conditions, and exemptions.

Learn how to [monitor gated deployment events](enablement-guide-runtime-gated#monitor-gated-deployment-events).

## Supported environments and registries

Gated deployment is available for supported Kubernetes environments and container registries. For current support details, see the [Defender for Containers support matrix](support-matrix-defender-for-containers#containers-software-supply-chain-protection-features).