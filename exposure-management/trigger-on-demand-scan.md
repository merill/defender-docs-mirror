---
layout: Conceptual
title: Trigger an on-demand agentic scan - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/trigger-on-demand-scan
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Trigger a remote on-demand agentic code scan for a GitHub repository that you've onboarded through the GitHub connector in Microsoft Defender.
ms.topic: how-to
ms.date: 2026-07-06T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 18077ac3-fc2b-2770-9069-503aa57324f1
document_version_independent_id: 18077ac3-fc2b-2770-9069-503aa57324f1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/trigger-on-demand-scan.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: trigger-on-demand-scan
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/trigger-on-demand-scan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
platformId: 14f49abe-def4-5c04-db51-7ebd0c94f9fa
---

# Trigger an on-demand agentic scan - Microsoft Security Exposure Management | Microsoft Learn

After activating the SCM connector, the ability to trigger an on-demand agentic code scan for onboarded repositories.

Important

Onboarded repositories become available within up to one hour.

## Prerequisites

- A SCM connector created and activated. See [Create a GitHub connector](create-github-connector) or [Create an Azure DevOps connector](create-azure-devops-connector)

## Step 1: Open Manage scans

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Exposure management** &gt; **Initiatives**.
2. Open the **Codename MDASH - Agentic code scanner (preview)** initiative, and then select **Open initiative page**.
3. Select the **Manage scans** button (next to the **Settings** button).

## Step 2: View the list of repositories

The side panel lists every repository discovered through the SCM connectors activated in your tenant.

For each repository, you can see:

- Repository name
- Repository size
- Organization name
- SCM type
- Scan status — last scan
- Tokens consumed in the last scan

The repository size and tokens consumed signals can help your security team predict the impact of a rescan.

## Step 3: Select a repository and run a scan

1. Select the repository you want to scan.
2. Select **Start scan**.
3. In the confirmation dialog, choose the scan configuration to use **for this scan only** — **Standard**, or select **MAI Cyber** **(Preview)** — then select **Scan repo**. The selection applies to this scan only. A scan configuration whose required models aren't deployed shows an inline error and can't be selected. For the models required by each configuration, see [Deploy the required models](/en-us/security-exposure-management/mdash-foundry-integration).

*If your tenant already has 10 queued scans from the portal and the CLI combined, a warning appears. You can still submit the scan. Queued scans that don't start running within 72 hours of submission are automatically cleaned up, so some queued scans might not run.*

A notification appears confirming the scan was started. The new scan appears in the **Scans** tab and progresses through its lifecycle.