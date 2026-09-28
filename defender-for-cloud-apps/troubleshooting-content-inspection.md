---
layout: Conceptual
title: Troubleshooting content inspection errors - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/troubleshooting-content-inspection
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
description: This article provides a list of content inspection statuses and their meanings.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: troubleshooting-general
locale: en-us
document_id: 78b4e4b0-0c7a-54c2-88d9-82cf8dd818cf
document_version_independent_id: 78b4e4b0-0c7a-54c2-88d9-82cf8dd818cf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/troubleshooting-content-inspection.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshooting-content-inspection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/troubleshooting-content-inspection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
platformId: 3ee565ce-d52c-83e8-9a70-fd6df8abb3a1
---

# Troubleshooting content inspection errors - Microsoft Defender for Cloud Apps | Microsoft Learn

Important

File policies retire on January 6, 2027. To maintain file-based data protection, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

This article provides a list of content inspection statuses and their meanings.

## Content inspection status

The table lists each content inspection status and its description.

| Content inspection status | Description |
| --- | --- |
| Completed | The content inspection completed successfully. |
| Not applicable | Content inspection wasn't applicable for this file. This status might appear because no policy requires content inspection of this file or because the file type isn't supported. |
| Pending | The file is currently in the content inspection queue. |
| Failed: Download error | Microsoft Defender for Cloud Apps couldn't download the file for inspection. |
| Failed: File is encrypted | The file couldn't be decrypted. If the [Inspect protected files](content-inspection#content-inspection-for-protected-files) setting is active and the file policy has the **Inspect protected files** checkbox selected, this status is expected and can be safely disregarded. |
| Failed: File is corrupted | The file is corrupted in some way and couldn't be inspected. |
| Failed: Internal error | Something undetermined went wrong when trying to inspect the file. |
| Failed: File size exceeded | The file exceeded the maximum file size of 30 MB. |
| Failed: File is too long and was partially scanned | The file exceeded the maximum of 1 million characters. For the part of the content that was scanned, relevant policy matches were applied. |
| Failed: File access denied | The file is external to your cloud and couldn't be accessed by Defender for Cloud Apps. |
| Failed: File was deleted | The file no longer exists in your cloud and couldn't be inspected. |
| Failed: Unsupported file type | Defender for Cloud Apps can't perform content inspection on this file type. This status may appear because the file type isn't supported or because the file isn't actually in the format of the expected file type. |

Note

If you see a dash in the scan status, this means that the file is not queued to be scanned. See [File policies](data-protection-policies) for information on setting content inspection policies.