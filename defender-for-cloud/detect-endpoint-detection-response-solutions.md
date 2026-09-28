---
layout: Conceptual
title: Detecting Endpoint Detection and Response Solutions - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/detect-endpoint-detection-response-solutions
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
description: Check whether your machines are connected to a supported endpoint detection and response (EDR) solution in Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 48b34a99-0ade-03aa-6a84-d480475b5cfc
document_version_independent_id: 4a197488-a48d-ba34-ffc6-16f045307d41
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/detect-endpoint-detection-response-solutions.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/detect-endpoint-detection-response-solutions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/detect-endpoint-detection-response-solutions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 6a40efc5-4dd1-bfda-182e-0d14c92ba4fd
---

# Detecting Endpoint Detection and Response Solutions - Microsoft Defender for Cloud | Microsoft Learn

This article explains how to check whether machines use a supported endpoint detection and response (EDR) solution.

Defender for Cloud includes EDR features for supported machines. It can:

- Detect whether a machine connects to a supported EDR solution.
- [Integrate natively with Microsoft Defender for Endpoint as an EDR solution](integration-defender-for-endpoint).

## Check for an EDR solution

Defender for Cloud uses [agentless scanning](concept-agentless-data-collection) to check whether Azure virtual machines (VMs), Amazon Web Services (AWS) machines, and Google Cloud Platform (GCP) machines connect to an EDR solution.

Agentless scanning for EDR settings is available when you enable [Defender for Servers Plan 2](tutorial-enable-servers-plan) or the [Defender CSPM plan](tutorial-enable-cspm-plan) in your Azure subscription.

Based on the findings, Defender for Cloud provides recommendations to help you find and fix machines that don't have an EDR solution running:

- `EDR solution should be installed on virtual machines`
- `EDR solution should be installed on EC2 instances`
- `EDR solution should be installed on virtual machines in GCP`

## Supported EDR solutions

The following table lists the EDR solutions that Defender for Cloud supports:

| Solution | Supported platform |
| --- | --- |
| Microsoft Defender for Endpoint | Windows |
| Microsoft Defender for Endpoint | Linux |
| Microsoft Defender for Endpoint Unified Solution | Windows Server 2012/2012 R2 |
| CrowdStrike (Falcon) | Windows and Linux |
| Trellix | Windows and Linux |
| Symantec | Windows and Linux |
| Sophos | Windows and Linux |
| Singularity Platform by SentinelOne | Windows and Linux |
| Cortex XDR | Windows and Linux (Supported only when installed via package manager on Linux) |