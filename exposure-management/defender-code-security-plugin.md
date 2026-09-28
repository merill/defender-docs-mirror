---
layout: Conceptual
title: Defender Code Security skills overview - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/defender-code-security-plugin
author: dlanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how Defender Code Security skills bring agentic code scan results and local scanning into your coding agent, so you can find and fix vulnerabilities without leaving the terminal.
ms.topic: overview
ms.date: 2026-06-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 867f8207-26ec-a503-fa47-5339afb9574a
document_version_independent_id: 867f8207-26ec-a503-fa47-5339afb9574a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/defender-code-security-plugin.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-code-security-plugin
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/defender-code-security-plugin.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/341fdab2-4964-4759-8241-f5820b012a47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cc1f92bb-c0d6-4d40-99ce-dabea3161a84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: c6ea3fb2-1e4a-39b8-814e-0b00c02a895b
---

# Defender Code Security skills overview - Microsoft Security Exposure Management | Microsoft Learn

Defender Code Security skills extend your coding agent with capabilities that surface Microsoft Defender agentic (Codename MDASH) scan results and run local security scans inline in chat. Developers can fetch the latest scan findings for their repo, run SAST, SCA, IaC, and secrets scans on their working tree, and accept AI-generated fixes - all without leaving the terminal or opening the portal.

Supported coding agents:

- **GitHub Copilot CLI**
- **Claude**

## Skills

The following skills are available:

| Skill | What it does |
| --- | --- |
| `onboard-defender-cli` | Downloads the Defender CLI binary and completes tenant setup. |
| `run-security-scan` | Retrieves the latest MDASH AI scan results for the current repo, and runs SAST, SCA, IaC, and secrets scans against your working tree or the full repo using Defender CLI. |
| `fix-security-issues` | Generates a diff preview for a selected finding and applies the fix to your working tree on acceptance. |

## What you can do

### Fetch AI scan results for your repo

The `run-security-scan` skill resolves your repo from the `origin` remote and returns the latest MDASH findings in chat — no portal navigation required.

Results include a header with the branch, scan timestamp, and scan ID, followed by a severity breakdown and per-finding rows with severity, rule, file and line number, a short rationale, and a **Fix it** affordance.

### Scan locally and fix findings inline

The `run-security-scan` skill runs Defender CLI scans against your local working tree. Results show the exact scope scanned (changed files or full repo), findings with severity and file location, and a **Fix it** affordance for each finding.

Select **Fix it** to invoke `fix-security-issues`, which posts a diff preview. Accept or decline the proposed change - accepted diffs apply directly to your working tree. No source code leaves the local machine.

## Requirements

- GitHub Copilot CLI or Claude CLI installed. If you don't have GitHub Copilot CLI, install it from https://aka.ms/copilot.
- Agentic code security onboarded in your tenant. See [Set up agentic code security](ai-code-security-onboarding).
- The **Scan results** permission at the **Read** level in Microsoft Defender unified RBAC. See [Security posture – AI code scan](/en-us/defender-xdr/custom-permissions-details#security-posture--ai-code-scan).
- An active internet connection to download the Defender CLI binary during onboarding.

## Install and onboard

### Using GitHub Copilot CLI

Run this command in your terminal:

```bash
copilot plugin install microsoft/security-devops-common:plugin/defender-code-security
```

Note

You might see a warning. You can safely ignore it. The actual plugin install for customers will be through a public marketplace.

### Using Claude CLI

The plugin isn't published to a Claude marketplace yet. To use Claude CLI, install the skill manually from the GitHub source.

1. Install the `onboard-defender-cli` skill from `https://github.com/microsoft/security-devops-common/tree/main/plugin/defender-code-security/skills/onboard-defender-cli`.
2. Claude fetches the `SKILL.md` and supporting files from that path and adds the skill to your environment.
3. Ask your agent to onboard you.

    Open Copilot, Claude, or your CLI agent, and send:

    ```text
    Onboard me to Defender CLI
    ```

    Or, if you're on Copilot CLI, run this command from your terminal:

    ```bash
    copilot -i /defender-code-security:onboard-defender-cli
    ```
4. The agent downloads the binary to `~/.mdc`, verifies the Authenticode signature, and adds it to your PATH automatically. After it's done, you only need to confirm that onboarding is complete.
5. Choose your tenant ID if prompted. If you have more than one tenant, you can choose the tenant ID.
6. Verify that onboarding works.

    After onboarding finishes, restart your terminal, or open your VS Code in a folder that contains a Git repository that has been AI-scanned, and ask your agent:

    ```text
    Show me AI scan results for my repo
    ```

    You should see findings rendered inline with severity, file locations, and suggested fixes.