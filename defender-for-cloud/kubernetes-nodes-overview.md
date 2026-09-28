---
layout: Conceptual
title: Overview of Kubernetes Nodes Protection - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/kubernetes-nodes-overview
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
description: Learn about Defender for Containers vulnerability assessment and malware detection for Kubernetes nodes.
ms.date: 2026-05-26T00:00:00.0000000Z
ms.topic: overview
ai-usage: ai-assisted
locale: en-us
document_id: 830982d8-84ca-cca0-ac63-763f451dfb28
document_version_independent_id: c499d950-6805-0e64-93e5-7f47e6bee8c4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/kubernetes-nodes-overview.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/kubernetes-nodes-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/kubernetes-nodes-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
platformId: 2afb726b-5073-5de7-0a19-4dfc0c17158c
---

# Overview of Kubernetes Nodes Protection - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud helps protect supported Kubernetes nodes by providing vulnerability assessment and malware detection for the virtual machines (VMs) that run your cluster workloads.

Vulnerability assessment is available for supported Azure Kubernetes Service (AKS) nodes. Malware detection is available for AKS nodes and in preview for Amazon Elastic Kubernetes Service (EKS) and Google Kubernetes Engine (GKE) nodes.

These protections help you identify vulnerabilities and detect malware on the nodes that support your cluster.

## Protections for Kubernetes nodes

Defender for Cloud provides the following protections for supported Kubernetes nodes:

- [Vulnerability assessment](kubernetes-nodes-va) identifies known vulnerabilities on node software and surfaces recommendations to help you remediate them.
- [Malware detection](kubernetes-nodes-malware) scans nodes for malware and generates security alerts when malware is detected.

For support details, view the [support matrix for Defender for Containers](support-matrix-defender-for-containers).

## How Kubernetes node protection works

Kubernetes node protection uses agentless, snapshot-based scanning of node pool disks.

This capability relies on **Agentless scanning for machines**. When that feature is enabled in a supported plan, Defender for Cloud can scan supported Kubernetes nodes and surface findings in recommendations and alerts.

For more information about the underlying architecture, see [Agentless scanning architecture](concept-agentless-data-collection).

## Shared responsibility

Responsibility for Kubernetes nodes is shared between the managed Kubernetes service and your organization.

- The managed Kubernetes service provides supported node VM images and updated versions.
- You configure node pools based on your workload requirements.
- You are responsible for upgrading node pool VM versions to adopt newer images and improve your security posture.