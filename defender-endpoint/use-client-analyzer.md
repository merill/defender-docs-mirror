---
layout: Conceptual
title: Diagnose Defender for Endpoint issues with Client Analyzer - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/use-client-analyzer
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.topic: article
description: Understand how to Diagnose Defender for Endpoint issues with Client Analyzer so that you can send the right data to Microsoft support for troubleshooting.
ms.service: defender-endpoint
author: chrisda
ms.author: chrisda
ms.collection:
- m365-security
- tier1
- mde-ngp
ms.subservice: ngp
ms.date: 2025-10-28T00:00:00.0000000Z
locale: en-us
document_id: acb9609a-7965-88f5-e066-3b4eef60c630
document_version_independent_id: acb9609a-7965-88f5-e066-3b4eef60c630
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/use-client-analyzer.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: use-client-analyzer
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/use-client-analyzer.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 7164ad66-8818-40ca-a064-6bb01f9a6b2b
---

# Diagnose Defender for Endpoint issues with Client Analyzer - Microsoft Defender for Endpoint | Microsoft Learn

When you troubleshoot Microsoft Defender for Endpoint, collecting diagnostic data is crucial for problem resolution. Different issues such as performance, connectivity and detection-related concerns, require different telemetry. As a security expert investigating these issues, you can use the [Client Analyzer](overview-client-analyzer) tool to gather data about your organization's Defender for Endpoint issues. With this data, you can troubleshoot your organization's Defender for Endpoint issues, and if needed [work with Microsoft support](contact-support) to resolve them

This article lists different types of issues and how to collect data for them using the Client Analyzer tool. The tool's flags are listed in [Data collection for advanced troubleshooting on Windows](data-collection-analyzer).

## Categorize your issue

Use the categories listed in the table to identify the type of issue you're experiencing. Run the Client Analyzer tool with the appropriate flags when collecting data.

| Issue | Description and examples | Flags |
| --- | --- | --- |
| Issues that can't be reproduced | Issues that occur sporadically or are triggered by automated processes and can't be reproduced. This includes problems related to scheduled tasks such as automatic updates and scans, and Attack Surface Reduction (ASR) rules triggered unpredictably. | Run without flags |
| Performance issues that can be reproduced | Includes high CPU usage, memory consumption problems, and slow response times. | `-a` and `-v` |
| General | On-demand scans, manual updates, sense portal and alert issues, Attack Surface Reduction (ASR) issues that can be triggered on command, and app compatibility problems. | `-e` and `-v` |
| Hanging systems | Unresponsive systems and freezes. Require advanced debugging techniques including memory dumps and crash analysis. | `-z` |
| Compatibility | Issues with third-party applications, other security solutions, system software, performance problems, and functional issues. | `-c`, `-e` and `-v` |
| Controlled Folder Access (CFA) | Include blocked applications, unexpected access permissions, and issues related to protected folders configuration. | Reproducible: `-cfa`, `-e` and `-v`Nonreproducible: `-cfa` |
| Data Loss Prevention (DLP) | Include policy enforcement problems, content detection false positives and negatives, and DLP client health and connectivity issues. | Reproducible: `-e`, `-t` and `-v`Nonreproducible: `-t` |
| Indicator | Include problems with URLs, domains, IP addresses, files, and certificates that aren't enforced as expected. | URL, IP, domain in first-party browser: `-a`, `-i` and `-v`File indicator: `-v` |
| Web Content Filtering (WCF) | Unenforced WCF policy when accessing web content using first and third party browsers. | `-a`, `-i` and `-v` |
| Network protection | Network protection doesn't trigger configured policies when URLs, domains, and IPs are accessed through third-party browsers. | `-i` and `-v` |

## Run the Client Analyzer tool

Follow the steps in this section to collect data for the issues you've identified. Use the appropriate flags when needed. If you have scenarios that involve both working and nonworking conditions, collect separate log packages for each scenario and clearly label each collection. The comparison helps identify the differences that cause the performance issue.

1. Start log collection running:

    ```powershell
    
    MDEClientAnalyzer.cmd
    
    ```

    If you used a flag that includes a timespan, such as `-a`, `-e`, or `-v`, you're asked to specify the duration of the log collection.
2. Once the log collection starts, reproduce the issue so that the issue's data is captured while the logs are being collected.
3. To stop the log collection press Press `q`.