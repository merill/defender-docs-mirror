---
layout: Conceptual
title: Resolve Agentless Scan Errors for GCP VMs in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/resolve-disk-scanning-error
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
description: Troubleshoot missing agentless scan results for GCP VMs in Microsoft Defender for Cloud when the Compute Storage resource use restrictions policy blocks access.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: d5a8d41f-71b8-b407-5e74-e7088bd79ba0
document_version_independent_id: 9fadaf94-41f1-ab37-27f4-98d1d9177237
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/resolve-disk-scanning-error.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/resolve-disk-scanning-error
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/resolve-disk-scanning-error.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: d4507244-c8c5-c4aa-400b-fbed0457b96f
---

# Resolve Agentless Scan Errors for GCP VMs in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

After you connect your Google Cloud Platform (GCP) project to Microsoft Defender for Cloud, Defender for Cloud uses agentless machine scanning to identify vulnerabilities in your virtual machines (VMs). Defender for Cloud then provides security recommendations and alerts, along with guidance for remediation.

If no agentless scan results appear within 24 hours after you connect your GCP project, the GCP organizational policy `Compute Storage resource use restrictions (Compute Engine disks, images, and snapshots)` might be preventing Defender for Cloud from accessing the necessary resources.

This article explains how to identify and resolve this issue so Defender for Cloud can successfully scan your VMs.

## Prerequisites

You must have:

- A [GCP project onboarded to Microsoft Defender for Cloud](quickstart-onboard-gcp)
- Access to a GCP project
- Contributor level permission for the relevant Azure subscription

## Manage your organization's policies

By configuring your organization policies, you can control the resources that Defender for Cloud can access in your GCP project.

1. Sign in to your GCP project.
2. Navigate to **your organization** &gt; **relevant GCP project**.
3. Navigate to **IAM & Admin** &gt; **Organization Policies**.
4. Search for the `Compute Storage resource use restrictions (Compute Engine disks, images, and snapshots)` policy.
5. Select **Manage policy**.
6. Change the policy type to **Allow**.
7. Add `under:organizations/517615557103` to the allow list.
8. Select **Save**.

Defender for Cloud triggers agentless disk scanning by using API calls. You know this policy change worked after the next scheduled scan API call, which can take up to 24 hours.