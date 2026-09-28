---
layout: Conceptual
title: Sensitive data threat detection in Defender for Storage - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-storage-data-sensitivity
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
description: Understand how Microsoft Defender for Storage detects and protects sensitive data from exposure, enhancing your organization's data security.
ms.date: 2025-07-01T00:00:00.0000000Z
ms.topic: overview
ai-usage: ai-assisted
locale: en-us
document_id: c5eb68ab-7ad0-8cba-a060-64f143c396f4
document_version_independent_id: fd912924-b166-cc10-bc13-8480486b199e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-storage-data-sensitivity.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-storage-data-sensitivity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-storage-data-sensitivity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 714aefc5-c588-17b5-c828-41ae995261ef
---

# Sensitive data threat detection in Defender for Storage - Microsoft Defender for Cloud | Microsoft Learn

Sensitive data threat detection helps you prioritize and examine security alerts efficiently. It considers the sensitivity of the data at risk, leading to better detection and prevention of data breaches. This capability helps security teams reduce the likelihood of data breaches by quickly identifying and addressing the most significant risks. It also enhances sensitive data protection by detecting exposure events and suspicious activities on resources containing sensitive data.

This feature is configurable in the new Defender for Storage plan. You can choose to enable or disable it with no further cost.

Learn more about [scope and limitations of sensitive data scanning](concept-data-security-posture-prepare).

## Prerequisites

Sensitive data threat detection is available for the following Blob storage account types:

Standard general-purpose v1

Standard general-purpose v2

Azure Data Lake Storage Gen2

Premium block blobs

It is also available for Azure Files (over REST API and SMB), but currently only for customers who have Defender CSPM enabled:

- Files
- Files v2
- Premium Files

To enable sensitive data threat detection at subscription and storage account levels, you need to have the relevant data-related permissions from the **Subscription owner** or **Storage account owner** roles.

Learn more about the [roles and permissions required for sensitive data threat detection](support-matrix-defender-for-storage).

## How does sensitive data discovery work?

Sensitive data threat detection is powered by the sensitive data discovery engine, an agentless engine that uses a smart sampling method to find resources with sensitive data.

The service is integrated with Microsoft Purview's sensitive information types (SITs) and classification labels, allowing seamless inheritance of your organization's sensitivity settings. This ensures that the detection and protection of sensitive data aligns with your established policies and procedures.

![Diagram showing how Defender CSPM and Defender for Storage combine to provide data-aware security.](media/defender-for-storage-data-sensitivity/data-sensitivity-cspm-storage.png)

Upon enablement, the engine initiates an automatic scanning process across all supported storage accounts. Results are typically generated within 24 hours. Additionally, newly created storage accounts under protected subscriptions are scanned within six hours of their creation. Recurring scans are scheduled to occur weekly after the enablement date. This is the same engine that Defender CSPM uses to discover sensitive data.