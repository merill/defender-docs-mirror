---
layout: Conceptual
title: GitHub Advanced Security Integration with Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/github-advanced-security-overview
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
description: Learn how GitHub Advanced Security integrates with Microsoft Defender for Cloud to provide unified code-to-runtime security from development to production.
ms.date: 2026-04-30T00:00:00.0000000Z
ms.topic: overview
ai-usage: ai-assisted
locale: en-us
document_id: ea99f91a-5e66-3468-9e19-e1a8164461a1
document_version_independent_id: 01e551ae-81df-6c55-6a33-aab9f9a70c4d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/github-advanced-security-overview.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/github-advanced-security-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/github-advanced-security-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 3cb3ddb7-4112-6344-baa2-05b192441c7f
---

# GitHub Advanced Security Integration with Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

GitHub Advanced Security (GHAS) integration with Microsoft Defender for Cloud links your source code to your running cloud workloads and vice versa —so security teams can prioritize the vulnerabilities that actually reach production, and engineering teams can fix them without leaving GitHub.

Use this integration to:

- Trace runtime vulnerabilities back to the originating repository and code owner.
- Prioritize fixes based on code deployment, production exposure and runtime risk.
- Coordinate remediation across GitHub code repositories and Cloud environments with shared context and status.
- Accelerate fixes with AI-powered (Copilot) remediation.

This overview explains how the integration works and helps you understand its core capabilities before deployment.

## Availability and prerequisites

Confirm the following before you onboard:

| **Category** | **Details** |
| --- | --- |
| Environmental requirements | - GitHub account with a connector created in Defender for Cloud  - GHAS license  - Defender Cloud Security Posture Management (DCSPM) enabled on the subscription  - Microsoft Security Copilot (optional for automated remediation) |
| Roles and permissions | - Security Admin permissions  - Security Admin on the Azure subscription (to view findings in Defender for Cloud)  - GitHub organization owner |
| Cloud environments | - Available in commercial clouds only (not in Azure Government, Azure operated by 21Vianet, or other sovereign clouds) |

## Personas and pain points

[![Screenshot of personas and pain points for Cloud Security, AppSec, and Developer teams, with columns listing challenges and solutions.](media/github-advanced-security-overview/personas.png)](media/github-advanced-security-overview/personas.png#lightbox)

## Main flows

[![Diagram of onboarding, cloud security, AppSec, and developer flows showing step-by-step GitHub security integration processes.](media/github-advanced-security-overview/main-flows.png)](media/github-advanced-security-overview/main-flows.png#lightbox)

## Main capabilities

### Automatic code-to-runtime mapping

When you connect your GitHub organization or repository to Microsoft Defender for Cloud via [GitHub connector](/en-us/azure/defender-for-cloud/quickstart-onboard-github), the system automatically maps source repositories to running cloud workloads. It uses Defender for Cloud proprietary code-to-runtime methods to ensure that every workload is tracked to its repository of origin (and vice versa).

This capability gives you instant end-to-end visibility, so you know which code powers each deployed application and which running containerized workloads mapped to which source code repo without time-consuming manual mapping.

[![Screenshot of development phases on the remediation insights tab.](media/github-advanced-security/development-phase.png)](media/github-advanced-security/development-phase.png#lightbox)

### Production-aware alert prioritization

Cut through noisy security alerts and focus on vulnerabilities that truly matter.

GHAS security findings in GitHub are prioritized by real runtime context from Defender for Cloud. They highlight **Runtime Risk Factors** like **Internet Exposure**, **Sensitive Data**, **Critical Resources**, and **Lateral Movement**. These risk factors come from Defender CSPM’s attack-path analysis:

- **Internet Exposure** - workload reachable from the public internet
- **Sensitive Data** - workload handles regulated or confidential data
- **Critical Resources** - workload tagged or classified as business-critical
- **Lateral Movement** - workload sits on a path that an attacker could pivot through

These risks, identified in runtime workloads, are dynamically linked to those workloads’ code repositories of origin and the specific build artifacts in GitHub.

You can filter, triage, and act on only security issues that have actual production impact in both Defender for Cloud and GitHub . This ability helps your team stay efficient and keep your most important applications secure.

### In practice

A container image built from the contoso/payments-api repository is deployed to AKS. Defender for Cloud detects internet exposure plus sensitive-data handling on the workload. The CVE inside the image is automatically elevated to Critical in GitHub’s security tab, and a one-click GitHub issue is assigned to the repository’s CODEOWNERS with full runtime and SDLC context attached.

### Unified AI-driven remediation

Bridge the gap between security and engineering teams with integrated workflows and relevant context.

Within Defender for Cloud, security managers can see which security issues the engineering team already knows about, along with the status of those issues. Security managers open this view by selecting the View on GitHub link.

Security managers can assign security recommendations for resolution to the relevant engineering teams by generating a GitHub issue assignment.

The assignment is generated on the repository of origin. It provides runtime information and context to facilitate the engineering fix.

Engineering managers can assign an issue to a developer for further resolution. The assignee can use a Copilot coding agent for AI-powered automatic fixes.

AppSec teams can use Runtime Risk factors as part of the GHAS findings, focusing engineering work on findings associated with code that is truly deployed and running.

Those filters can be used to filter GHAS alerts directly or used for continues scheduled prioritization via campaigns.

[![Screenshot of code scanning campaign creation page with filter bar, search box, and a popup about filtering by artifact metadata.](media/github-advanced-security-overview/create-new-code.png)](media/github-advanced-security-overview/create-new-code.png#lightbox)

GitHub issue fixes, progress, and campaign advancements are tracked in real time. The statuses are reflected both in GitHub and in Defender for Cloud.

[![Screenshot of Defender for Cloud showing a GitHub ticket created for a runtime risk finding with ticket details popup.](media/github-advanced-security-overview/open-ticket.png)](media/github-advanced-security-overview/open-ticket.png#lightbox)

This approach ensures that fixes are delivered rapidly, creates clear accountability, and simplifies collaboration. All these benefits happen inside the tools that your teams already use.