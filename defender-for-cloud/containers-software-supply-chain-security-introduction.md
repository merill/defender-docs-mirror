---
layout: Conceptual
title: Container software supply chain security with Defender for Containers - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/containers-software-supply-chain-security-introduction
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
description: Learn how Defender for Containers helps assess container images, associate vulnerability findings with images, and enforce deployment controls for Kubernetes workloads.
ms.topic: concept-article
ms.date: 2026-05-31T00:00:00.0000000Z
locale: en-us
document_id: 26372bcb-7127-d613-40b3-fd6dadc059f5
document_version_independent_id: 0a33d29f-3269-102d-d003-c35c87f6594d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/containers-software-supply-chain-security-introduction.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/containers-software-supply-chain-security-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/containers-software-supply-chain-security-introduction.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: e096fdff-7f1a-e6bf-c8c1-61342cc542ba
---

# Container software supply chain security with Defender for Containers - Microsoft Defender for Cloud | Microsoft Learn

Container software supply chain security helps reduce the risk of deploying vulnerable or untrusted container images into production environments.

Microsoft Defender for Containers supports the [Microsoft Containers Secure Supply Chain (CSSC) framework](/en-us/azure/security/container-secure-supply-chain) with capabilities that help you assess container images, associate vulnerability findings with images, and enforce deployment controls for Kubernetes workloads.

Defender for Containers helps you:

- Scan supported container images for vulnerabilities.
- Scan container images in CI/CD pipelines or local development environments before images are pushed to a registry.
- Associate vulnerability findings with container images by signing the vulnerability findings artifact with a Microsoft certificate.
- Create gated deployment security rules that evaluate container images before they're admitted into a Kubernetes cluster.
- Audit or block deployments when container images don't meet the vulnerability conditions defined in your security rules.
- Review container vulnerability findings and security posture recommendations in Defender for Cloud.

## Scan images earlier in the development lifecycle

You can use the [Microsoft Defender for Cloud CLI](/en-us/azure/defender-for-cloud/defender-cli-overview) to scan container images for vulnerabilities and misconfigurations in CI/CD pipelines or local development environments.

Scanning images before they're pushed to a registry helps developers identify and remediate issues earlier in the development lifecycle.

## Validate vulnerability findings

Defender for Containers signs the vulnerability findings artifact with a Microsoft certificate for integrity and authenticity. The signed artifact is associated with the container image in the registry for validation.

The signed artifact doesn't sign the container image itself. It signs the vulnerability findings associated with the image, so the findings can be validated and used by other Defender for Containers capabilities.

## Enforce deployment controls

Gated deployment uses vulnerability scan results to evaluate container images before they're admitted into a Kubernetes cluster.

You can create security rules that audit or deny deployments when images don't meet your organization's vulnerability policy. Use audit mode to monitor the effect of rules before enforcement. Use deny mode when you're ready to block deployments that violate configured rules.

Learn more about [gated deployment for Kubernetes container images](runtime-gated-overview).