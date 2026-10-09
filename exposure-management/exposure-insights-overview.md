---
layout: Conceptual
title: Exposure insights overview in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/exposure-insights-overview
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to get exposure insights into your corporate attack surface with Microsoft Security Exposure Management.
ms.topic: overview
ms.date: 2025-07-30T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 30ffca91-3ae5-80e4-a0ad-025aeaadf2ec
document_version_independent_id: 30ffca91-3ae5-80e4-a0ad-025aeaadf2ec
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/exposure-insights-overview.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: exposure-insights-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/exposure-insights-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 37811300-5b16-162e-6010-08de0e1724ba
---

# Exposure insights overview in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

Exposure insights in [Microsoft Security Exposure Management](microsoft-security-exposure-management) continuously aggregate security posture data and insights across workloads and resources, into a single pipeline.

## Exposure insights

Exposure insights provide rich context around the security posture state of your asset inventory.

Chief Information Security Officers (CISOs), decision makers, risk owners, and security teams can use security insights and context to understand and manage exposure risk across the entire organization, and to prioritize security efforts and investment.

Exposure insights provide visibility and granular context around security posture state. Insights enable you to:

- Break down organizational security posture into manageable security projects.
- Manage security projects as security initiatives in Security Exposure Management.
- Review, measure, and track risk exposure for each security initiative.
- Follow actionable recommendations and remediation steps to improve security posture and reduce risk.
- Monitor security posture state and improvements over time.

## Security initiatives

Security initiatives provide a simple way to assess security readiness for a specific security area or workload, and to constantly track and measure exposure risk for that area or workload over time.

Security Exposure Management provides initiatives that currently include:

- **Workload initiatives**: Assess and manage the risk associated with specific workload domains, such as security for endpoints, identity resources, and cloud assets.
- **Horizontal threat initiatives**: Assess and manage risk for specific threat areas, such as ransomware protection, or business email compromise - financial fraud.
- **Threat analytics initiatives**: Assess threat risk with initiatives that are based on up-to-date research from Microsoft threat analytics. Microsoft threat analytics is a set of reports from expert Microsoft security researchers that provide information about real and relevant threats. These threat initiatives focus on:

    - Threat actors and threat vectors.
    - Threat reports that have three or more recommendations.
- **Zero trust initiative**: Assess the risk associated with Zero Trust compliance. This initiative aligns with guidance provided by the [Zero Trust adoption framework](/en-us/security/zero-trust/adopt/zero-trust-adoption-overview).
- **External attack surface management initiative**: Assess the risk associated with your organization's or vendor's external attack surface. This initiative offers insights into identified exposures on the selected vendor. By leveraging this initiative, organizations can understand their risk exposure, prioritize security efforts, and proactively manage their security posture.

    For more information about the external attack surface management initiative, see [External attack surface management initiative](external-attack-surface-management-initiative).

Important

Initiatives that are in preview are marked accordingly. Preview initiatives are still in development, and are subject to change.

### Initiative elements

| **Element** | **Goal** | **Details** |
| --- | --- | --- |
| **Initiative** | Initiatives help you to gather security projects that have similar resources and workloads, and to assess and remediate the security posture of each project. | Each security initiative provides an all-up score that provides a fast measure of how strong security posture is for the initiative at the current point in time.The all-up score also provides a target score indicator, the number of critical assets affected, and shows how the score has moved over the last 24 hours. |
| **Metric** | Metrics in security initiatives help you to measure exposure risk for different areas within the initiative. | Each metric gathers together one or more recommendations for similar assets.Metrics can be associated with one or more initiatives.**Important**: Threat analytics initiatives don't have metrics. They have recommendations only. |
| **Recommendations** | Security recommendations help you to understand the compliance state for a specific security initiative. | All security initiatives have recommendations associated with them.Recommendations can be associated with one or more initiatives.Within initiatives, recommendations are assigned a compliance state. |
| **Events** | Events help you to monitor initiative changes. | Events notify you when there's a drop in an all-up initiative score or metric score, indicating that exposure risk grew. |

## Working with initiatives

Review the initiative score, and drill down into initiatives to see associated metrics and understand where gaps or risks reside. For step-by-step guidance, see [Review security initiatives](initiatives).

## Working with metrics

Metrics measure exposure risk for specific asset scopes within an initiative. You can review metric properties, filter findings, adjust metric weights, and drill down into recommendations. For details, see [Investigate security initiative metrics](security-metrics).

## Working with recommendations

Security Exposure Management consolidates recommendations from multiple sources — Exposure Management, [Microsoft Secure Score](/en-us/defender-xdr/microsoft-secure-score), and Microsoft Defender for Cloud — into a unified Recommendations Catalog in the Defender portal. Recommendations are organized by attack surface domain (Devices, Cloud, Identity, SaaS, Data) and issue type (misconfigurations, vulnerabilities, secrets). For details, see [Review security recommendations](security-recommendations).

## Monitoring and improving scores

The exposure state for a security initiative is reflected in the initiative score.

- **Initiatives with metrics**: For initiatives with metrics, the score is calculated based on the value and weight of metrics within the initiative.
- **Initiatives without metrics**: For threat initiatives that don't have metrics, the initiative score is calculated in the same way that [Secure Score is calculated](/en-us/defender-xdr/microsoft-secure-score#how-recommended-actions-are-scored).

For initiatives with metrics:

- As metrics improve the initiative score rises to reflect an improved posture for the security initiative.
- Metrics largely improve by applying the recommendations associated with the initiative.
- Changes in metrics, including deprecation/removal, value, and metric properties can affect the initiative score.

## Reviewing initiative history

Track score changes over time on the **History** tab of an initiative. For step-by-step guidance, see [Check history](initiatives#check-history).

## Reviewing events

Events track score drops and metric status changes. For details and steps, see [Review security events](initiatives#review-security-events).