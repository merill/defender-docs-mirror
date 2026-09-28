---
layout: Conceptual
title: Autofix agentic code vulnerabilities - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/auto-fix-ai-vulnerabilities
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to use the Defender CLI to generate AI-powered code fixes from your agentic code scan results.
ms.topic: how-to
ms.date: 2026-05-27T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 3f6e00e7-b1bb-a3b2-1173-d0a1c795e8f4
document_version_independent_id: 3f6e00e7-b1bb-a3b2-1173-d0a1c795e8f4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/auto-fix-ai-vulnerabilities.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: auto-fix-ai-vulnerabilities
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/auto-fix-ai-vulnerabilities.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/341fdab2-4964-4759-8241-f5820b012a47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cc1f92bb-c0d6-4d40-99ce-dabea3161a84
platformId: 3b8760e3-b3b9-cd3d-369a-9c4b23cf3a2a
---

# Autofix agentic code vulnerabilities - Microsoft Security Exposure Management | Microsoft Learn

After running an agentic code scan, use `defender fix` to generate AI-powered code fixes from your scan results.

## Prerequisites

Before you start:

- Install Defender CLI. See [Set up the Defender CLI](defender-cli).
- Install GitHub Copilot CLI. See [Installing GitHub Copilot in the CLI](https://docs.github.com/en/copilot/github-copilot-in-the-cli/installing-github-copilot-in-the-cli).
- Complete at least one scan and have a SARIF results file. See [Run agentic code scans](run-ai-code-security-scans).

## Apply fixes

To fix findings, run the following command with your SARIF results file:

```bash
defender fix ./defender-aiscan-<JOB_ID>.sarif
```

To fix findings at all severity levels, specify a severity threshold. Findings at or above the severity threshold are included.

```bash
defender fix ./results.sarif --severity low
```