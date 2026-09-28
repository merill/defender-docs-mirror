---
layout: Conceptual
title: Defender for Cloud CLI Overview - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-cli-overview
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
description: 'Defender for Cloud CLI: Orchestrate security scans in CI/CD pipelines or locally with minimal setup. Upload results to Defender for Cloud for prioritization and tracking.'
ms.date: 2025-11-06T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: cf3d498c-9967-56af-594f-6639205c2910
document_version_independent_id: d89023f8-a85a-4296-b358-e70c43e32fec
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-cli-overview.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-cli-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-cli-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: c9fcb42d-eeb3-1fda-5bb1-532345cb1644
---

# Defender for Cloud CLI Overview - Microsoft Defender for Cloud | Microsoft Learn

The Defender for Cloud CLI is a developer‑first command‑line tool that orchestrates security scans in CI/CD pipelines and on developer terminals. It uploads results to Microsoft Defender for Cloud for posture management, code‑to‑runtime context, prioritization, and tracking. It accelerates secure delivery with minimal setup, easy-to-use command-line options, and actionable guidance that helps teams fix issues fast without breaking flow.

## What the Defender for Cloud CLI does

- **Run security scans anywhere:** You can initiate scans from your laptop or any CI/CD pipeline system (such as GitHub Actions, Azure DevOps, Jenkins, Bitbucket, and more). The tool requires minimal configuration—a single executable, sensible defaults, and streamlined authentication.
- **Unify scanners with one tool:** Orchestrate multiple security engines (for example, container image analysis and more as they become available) with consistent output and exit codes that optimize pipeline gating and automation.
- **Upload findings to Defender for Cloud:** Results land in a single place where security teams gain code‑to‑runtime visibility, attack‑path context, and standard recommendation content to target what matters first.
- **Built for developer experience:** Provides clear help, concise console output, and remediation guidance that align with how developers work (pipelines, terminals, and pull requests).

## How it fits into your workflow

1. You install and authenticate in your CI/CD pipeline or locally.
2. You scan the image you're working on.
3. You review results in the console, export if needed, and upload to Defender for Cloud.

## Authentication

Defender for Cloud CLI supports two authentication methods to align with enterprise security practices. The first and preferred method is connector‑based authentication, currently available for Azure DevOps and GitHub. By establishing a connector between these source control managers and Defender for Cloud, authentication is handled automatically, eliminating the need to add tokens to pipelines. The second method is token‑based authentication, where security admins create tokens in the Microsoft Defender for Cloud portal and configure them as environment variables in CI/CD pipelines or local terminals. This approach offers flexibility across build systems and enables targeted scoping by subscription. For detailed steps and examples, see [Authentication](defender-cli-authentication).

## CI/CD integration

The Defender for Cloud CLI is platform‑agnostic and works if you use a native connector or authentication tokens. Teams can adopt it progressively, optimize YAML with defaults, and rely on stable, consistent exit codes to wire in checks. Examples and marketplace entries (Azure DevOps Task) are part of the standard rollout to accelerate onboarding. For detailed steps and examples, see [CI/CD integration](ci-cd-pipeline-scanning-with-defender-cli).

## Command reference design

Defender for Cloud CLI syntax follows a simple reference `name` - `command` - `parameter` - `parameter value` pattern. For example, here's how to scan a container:

```bash
defender scan image myregistry.azurecr.io/app:build-123
```

For detailed reference, see [Syntax](defender-cli-syntax).

## Results and remediation

- Provides readable console output with issues and next steps for remediation.
- When invoked from CI/CD pipelines, it uploads results to Defender for Cloud, where findings appear in asset inventories, recommendations, and attack paths with runtime context (for example, internet exposure and affected workloads).

To review results, see [Reviewing Results](defender-cli-reviewing-results).

## Code‑to‑runtime visibility

When findings are uploaded, Defender for Cloud models repository, pipeline, image, and runtime resource relationships so security teams can target the right owners, understand blast radius, and align remediation with risk. For more details, see [Container Image Mapping](container-image-mapping).

## Migration from MSDO CLI

If you're using the legacy Microsoft Security DevOps (MSDO) CLI, consider moving to the Defender for Cloud CLI to get:

- Microsoft Container Security Scanner (MDVM‑backed) container scanning (replacing Trivy image scanning in pipelines).
- Enhanced user developer experience (run locally and in CI with command line options).
- A future‑proof path as new scanners are orchestrated by Defender for Cloud CLI. MSDO CLI remains in maintenance support.