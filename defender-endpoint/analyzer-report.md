---
layout: Conceptual
title: Understand the client analyzer HTML report - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/analyzer-report
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to analyze the Microsoft Defender for Endpoint Client Analyzer HTML report
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: concept-article
ms.subservice: onboard
ms.date: 2025-03-27T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 6668a110-67e6-f392-4caf-b3ec80e48454
document_version_independent_id: 6668a110-67e6-f392-4caf-b3ec80e48454
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/analyzer-report.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: analyzer-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/analyzer-report.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 23625b40-ef1d-a769-7b5a-965148f7c3ff
---

# Understand the client analyzer HTML report - Microsoft Defender for Endpoint | Microsoft Learn

The client analyzer produces a report in HTML format. Learn how to review the report to identify potential sensor issues so that you can troubleshoot them.

Use the following example to understand the report.

## Example output

In this example, the [Defender for Endpoint Client Analyzer](overview-client-analyzer) produced information about a device that was onboarded to an expired Org ID and failed to reach a required Defender for Endpoint URL:

[![The MDE Client Analyzer Results page](media/147cbcf0f7b6f0ff65d200bf3e4674cb.png)](media/147cbcf0f7b6f0ff65d200bf3e4674cb.png#lightbox)

- On top, the script version and script runtime are listed for reference
- The **Device Information** section provides basic OS and device identifiers to uniquely identify the device on which the analyzer has run.
- The **Endpoint Security Details** provides general information about Microsoft Defender for Endpoint-related processes including Microsoft Defender Antivirus and the sensor process. If important processes aren't online as expected, the color changes to red.

    [![The Check Results Summary page](media/85f56004dc6bd1679c3d2c063e36cb80.png)](media/85f56004dc6bd1679c3d2c063e36cb80.png#lightbox)
- On **Check Results Summary**, you'll have an aggregated count for error, warning, or informational events detected by the analyzer.
- On **Detailed Results**, you'll see a list (sorted by severity) with the results and the guidance based on the observations made by the analyzer.

## Open a support ticket to Microsoft and include the Analyzer results

To include analyzer result files [when opening a support ticket](contact-support#open-a-service-request), make sure you use the **Attachments** section and include the `MDEClientAnalyzerResult.zip` file:

[![An attachment prompt](media/508c189656c3deb3b239daf811e33741.png)](media/508c189656c3deb3b239daf811e33741.png#lightbox)

Note

If the file size is larger than 25 MB, the support engineer assigned to your case will provide a dedicated secure workspace to upload large files for analysis.