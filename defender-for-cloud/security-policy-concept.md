---
layout: Conceptual
title: Security policies in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/security-policy-concept
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
description: Learn how to improve your cloud security posture in Microsoft Defender for Cloud with security policies, standards, and recommendations.
ms.topic: concept-article
ms.date: 2025-02-09T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: ffb7c1d0-79ab-c48c-159c-7eda86b2a224
document_version_independent_id: 2a77da5b-6343-8b29-1b4a-503efacbad0c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/security-policy-concept.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/security-policy-concept
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/security-policy-concept.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 49f4f3f0-659f-38ca-d319-b801ceacd5e3
---

# Security policies in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Security policies in Microsoft Defender for Cloud define how your cloud resources are evaluated for security across Azure, Amazon Web Services (AWS), and Google Cloud Platform (GCP). A policy specifies the standards, controls, and conditions Defender for Cloud uses to assess resource configurations and identify potential security risks.

Each policy includes [security standards](concept-regulatory-compliance-standards), which define the controls and assessment logic applied to your environment. Defender for Cloud continuously evaluates your resources against these standards. When a resource doesn’t meet a defined control, Defender for Cloud generates a security recommendation that describes the issue and the actions required to remediate it.

This enables Defender for Cloud to continuously assess resources and improve your organization’s security posture.

## Security standards

Security policies in Defender for Cloud can include several types of standards:

- **Security benchmarks** – Built-in baselines such as the [Microsoft Cloud Security Benchmark (MCSB)](concept-regulatory-compliance) and cloud-provider benchmarks that define foundational best practices.
- **Regulatory compliance standards** – Frameworks from industry and compliance programs available when you enable a [Defender for Cloud plan](defender-for-cloud-introduction).
- **Custom standards** – Organization-defined standards that include built-in or custom recommendations to align Defender for Cloud assessments with internal security policies.

Learn more about [security standards in Defender for Cloud](concept-regulatory-compliance-standards).

## Security recommendations

Security recommendations are actionable insights generated from assessments against security standards. Each recommendation includes:

- A short description of the issue
- Steps for remediation
- Affected resources
- Severity and risk factors
- Attack path context (when available)

The Defender for Cloud risk model prioritizes recommendations based on exposure, data sensitivity, lateral movement potential, and exploitability.

Important

[Risk prioritization](risk-prioritization) doesn't affect the secure score.

### Custom recommendations

You can create custom recommendations to define your own assessment logic by using [Kusto Query Language (KQL)](/en-us/azure/data-explorer/kusto/query). This capability is available for all clouds when the [Defender CSPM plan](concept-cloud-security-posture-management) is enabled.

Custom recommendations are created within a custom standard and can also be linked to additional standards if needed. Each recommendation includes query logic, remediation steps, severity, and applicable resource types. After creation, custom recommendations appear with built-in recommendations in the Regulatory compliance dashboard and contribute to your overall security posture assessment.

Learn more about [creating custom recommendations](create-custom-recommendations).

## Example

MCSB includes multiple controls that define expected security configurations. One of these controls is “Storage accounts should restrict network access using virtual network rules.”

Defender for Cloud continuously assesses resources. If it finds any that don’t satisfy this control, it marks them as noncompliant and triggers a recommendation. In this case, the guidance is to harden Azure Storage accounts that aren't protected with virtual network rules.