---
layout: Conceptual
title: Troubleshooting policies - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/troubleshoot-policies
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article describes the process for troubleshooting policy creation in Defender for Cloud Apps.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: troubleshooting-general
locale: en-us
document_id: 96404e03-dac0-0a66-e937-eed9ab1ef270
document_version_independent_id: 96404e03-dac0-0a66-e937-eed9ab1ef270
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/troubleshoot-policies.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/troubleshoot-policies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 0ae393e0-91ae-ebe5-c717-0b30cabe6868
---

# Troubleshooting policies - Microsoft Defender for Cloud Apps | Microsoft Learn

This article describes the process for troubleshooting policy creation in Defender for Cloud Apps.

## Troubleshooting

The following chart has the description and resolution for errors you might see for policies.

| Error | Description | Resolution |
| --- | --- | --- |
| **The policy &lt;*name*&gt; was automatically disabled due to a configuration error** | If you get this error in Microsoft Defender for Cloud Apps, it means that you need to fix the configuration of the indicated policy. When you create a Microsoft Defender for Cloud Apps policy, you often make use of other objects created within Defender for Cloud Apps or the Security and Compliance Center such as IP tags or custom sensitive types. If the IP tag or custom sensitive type you used in the policy is deleted, the policy will automatically be disabled, and you'll receive this error. This message might also indicate a more general configuration error such as a filter that is too complex. | To restore the policy, edit the policy and fix every configuration error mentioned. This error usually means you need to remove any deleted objects from the policy filters and save the policy. |