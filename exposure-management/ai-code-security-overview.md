---
layout: Conceptual
title: Codename MDASH Overview - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/ai-code-security-overview
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how Codename MDASH - Agentic code scanner uses a multi-model agentic AI system to detect code vulnerabilities with depth and accuracy beyond traditional static analysis.
ms.topic: overview
ms.date: 2026-08-26T00:00:00.0000000Z
ms.custom: references_regions
ai-usage: ai-assisted
locale: en-us
document_id: ee356523-3eea-a8c5-0f64-8d29c4dc3c7d
document_version_independent_id: ee356523-3eea-a8c5-0f64-8d29c4dc3c7d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/ai-code-security-overview.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ai-code-security-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/ai-code-security-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 6d5f27a3-33e0-add4-6dcb-2be45daa36f6
---

# Codename MDASH Overview - Microsoft Security Exposure Management | Microsoft Learn

Codename MDASH is an agentic code scanner within Microsoft Defender that uses a multi-model agentic AI system to assist security and engineering teams detect and fix code vulnerabilities with unprecedented depth and accuracy.

## How it works

This service uses a multistage agentic pipeline where specialized AI agents collaborate to find, validate, and prove vulnerabilities:

- **Prepare** — The system ranks files by risk using call-graph analysis and code complexity metrics, prioritizing functions most likely to contain vulnerabilities.
- **Scan** — More than 100 specialized AI agents (for example, injection-auditor, memory-safety-auditor, auth-bypass-auditor) analyze the ranked code using multiple LLMs. Each agent targets a specific vulnerability class.
- **Validate** — The system uses taint analysis and type resolution through Language Server Protocol (LSP) servers. A multi-model agentic debate refines confidence and eliminates false positives.
- **Dedup** — The system consolidates duplicate findings, producing a final set of unique, actionable vulnerabilities.

## Key features & capabilities

| Capability | Description |
| --- | --- |
| AI-powered vulnerability detection | Submits code repositories to a multi-model agentic pipeline that identifies vulnerabilities with greater depth than traditional, pattern-matching static analysis. |
| Granular confidence scoring | Rates each finding with a confidence score so teams can prioritize with precision. |
| AI-generated code fixes | Uses the `defender fix` command in the Defender CLI to generate and apply code fixes directly from scan results. |
| Centralized results in Defender portal | Publishes findings to Microsoft Security Exposure Management for organization-wide tracking and triage. |
| Deployment and developer integration | Connects directly to GitHub and Azure DevOps using connecters, triggers on-demand scans locally or in the CI/CD via Defender CLI and integrates with AI coding environments using a dedicated agentic SKILL. |

## Language support

MDASH detects your project's language(s) automatically based on file extensions, and will use specialized language-specific sub agents to detect vulnerabilities in the following languages:

| Language | File Extension(s) |
| --- | --- |
| Java | `.java` |
| C/C++ | `.c`, `.h`, `.c.in`, `.cc`, `.cpp`, `.cxx`, `.hh`, `.hpp` |
| C# | `.cs` |
| JavaScript\*\* / TypeScript | `.js`, `.mjs`, `.cjs`, `.ts`, `.tsx`, `.mts` \*\*Minified Javascipt is currently excluded from the languages MDASH supports. |
| Python | `.py`, `.pyw` |

## Additional Languages Supported by Generalist Sub-Agents

If your repository contains additional common file types, MDASH will use general purpose vulnerability discovery sub-agents to scan these files, and scan quality will vary.

| Language | File Extension(s) |
| --- | --- |
| Objective-C | `.m` |
| Objective-C++ | `.mm` |
| Go | `.go` |
| Kotlin | `.kt`, `.k`, `.kts` |
| PHP | `.php`, `.phtml`, `.inc`, `.module`, `.install`, `.theme` |
| Ruby | `.rb` |
| Rust | `.rs` |
| Swift | `.swift` |
| Zig | `.zig` |

## Requirements

- For prerequisites, see [Set up agentic code security](ai-code-security-onboarding).
- For permissions, see [Security posture – AI code scan](/en-us/defender-xdr/custom-permissions-details#security-posture--ai-code-scan).

## Allow list

The following domains must be reachable from the machine or pipeline running the CLI.

**Required for `defender scan ai-scan`**

- `*.cli.dfd.security.azure.com`
- `*.blob.core.windows.net`
- `*.azurefd.net`
- `*.login.microsoftonline.com`
- `*.graph.microsoft.com`

**Required for GitHub Actions (OIDC)**

- `*.token.actions.githubusercontent.com`

**Required for Azure Pipelines (OIDC)**

- `*.dev.azure.com`

**Recommended for telemetry**

- `*.in.applicationinsights.azure.com`
- `*.dc.services.visualstudio.com`

**Optional**

- `*.aka.ms`

**Required for `scan fs`**

- `*.ghcr.io`
- `*.public.ecr.aws`
- `*.registry-1.docker.io`
- `*.auth.docker.io`

## Cloud and region support

Codename MDASH - Agentic code scanner is available in the Azure commercial cloud in the following regions:

- US (United States)
- EU (Europe)
- UK (United Kingdom)
- AUS (Australia)
- IND (India)
- CH (Switzerland)
- UAE (United Arab Emirates)
    - UAE currently supports MDASH CLI scans only.