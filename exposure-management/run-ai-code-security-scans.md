---
layout: Conceptual
title: Run agentic code scans - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/run-ai-code-security-scans
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to submit agentic code scans, check job status, view results, and manage jobs using the Defender CLI.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5f03d9eb-5841-1fa2-015f-8dbf13e5bea6
document_version_independent_id: 5f03d9eb-5841-1fa2-015f-8dbf13e5bea6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/run-ai-code-security-scans.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: run-ai-code-security-scans
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/run-ai-code-security-scans.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a79d38a8-e34d-1832-5452-0de3fbf99dca
---

# Run agentic code scans - Microsoft Security Exposure Management | Microsoft Learn

Use the Defender CLI to submit agentic code scans, monitor job status, and view results.

## Prerequisites

Before you start:

- Defender CLI is installed. See, [Set up the Defender CLI](defender-cli).
- Authenticate with your credentials.
- Navigate to your repository:

    ```bash
    cd /path/to/your/repo
    ```

## Run your first scan

Submit a scan and wait for results in a single command:

```bash
defender scan ai-scan submit .
```

This command archives your repository code, submits it to the agentic code security service for analysis, and waits for the scan to complete.

## Async workflow

For long-running scans, use the async workflow to submit a job and check status independently.

```bash
# Step 1: Submit and get a job ID
defender scan ai-scan submit .
# Output: Job submitted: <JOB_ID>

# Step 2: Check job status
defender status ai-scan <JOB_ID>

# Step 3: (Optional) Wait for completion and download results
defender status wait <JOB_ID> -o results.sarif
```

## Set severity thresholds

To limit results to high and critical findings only:

```bash
defender scan ai-scan submit . --severity high
```

## View results in the portal

After a scan finishes, the Microsoft Defender portal publishes the results. To view the results:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Exposure Management** &gt; **Initiatives** &gt; **Codename MDASH - Agentic code scanner (preview)**.

## Manage jobs

Use the following commands to list and cancel scan jobs:

```bash
defender status                         # List all tracked jobs
defender status cancel <JOB_ID>         # Cancel a running job
```