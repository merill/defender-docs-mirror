---
layout: Conceptual
title: API security posture overview - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/api-security-posture-overview
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
description: Learn how Microsoft Defender for Cloud enhances API security posture management for your APIs across Azure API Management, Function Apps, and Logic Apps.
ms.topic: concept-article
ms.date: 2026-06-18T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 916b7da3-a35e-bb46-d181-9b254a466908
document_version_independent_id: 781034fb-11aa-34f9-40cc-ed9002cad220
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/api-security-posture-overview.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/api-security-posture-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/api-security-posture-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/bf4dbf7f-261c-4ae9-9fee-5989668a780a
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/1c4b5d48-3f26-4bd8-9592-816d9c1a3420
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: c4088713-44b8-dcb1-9650-db6a74ec5ec6
---

# API security posture overview - Microsoft Defender for Cloud | Microsoft Learn

APIs are entry points into cloud-native apps. They connect services, apps, and data, making them targets for attackers. API security posture management helps protect APIs by assessing risks from misconfigurations and vulnerabilities. The Defender cloud security posture management (Defender CSPM) plan in Microsoft Defender for Cloud offers API discovery and posture across your Azure Function Apps and Logic Apps and your managed APIs across your Azure API Management platform.

## Capabilities

API security posture management in Defender for Cloud offers the following capabilities:

- **Gain visibility into your APIs**: Get a centralized view of managed APIs across Azure API Management and APIs hosted in Function Apps and Logic Apps, with automated onboarding into Defender for Cloud.
- **Assess API security recommendations with risk factors** to:

    - Identify and remediate unauthenticated API risks.
    - Detect APIs exposed to the internet.
    - Identify sensitive data exposure in API endpoints, including requests and responses, URL paths, and query parameters (integrated with Microsoft Purview), powered by analyzing sampled API traffic logs (*Azure API Management only)*
- **Identify inactive or dormant APIs**: Surface APIs that are no longer in use across Azure API Management, Function Apps, and Logic Apps.
- **Identify APIs allowing unencrypted traffic**: Surface APIs that permit unencrypted communication, which might introduce risk.
- **Understand cloud application exposure risks** by linking APIs to backend environments like virtual machines, containers, storage, and databases.
- **Address API-driven attack paths** and prioritize mitigation with cloud [security explorer and API-led attack path analysis](concept-attack-path).

## Unified inventory

Defender for Cloud continuously discovers APIs across Azure API Management, Function Apps, and Logic Apps. You can view all APIs with posture insights in the Defender for Cloud [asset inventory](asset-inventory) and [API Security dashboard](defender-for-apis-introduction#review-api-security-findings). This insight helps you address API risks efficiently.

## Prioritize and implement API security best practices

Assess and secure your APIs against high-risk issues such as lack of encryption and anonymous access with broken or weak authentication. Gain insights into inactive APIs and those exposed directly to the internet. Defender for Cloud scans for API risks, considering potential exploitability and business impact. [Security recommendations](security-recommendations#understanding-risk-prioritization) are prioritized based on these factors, so you can fix critical vulnerabilities first.

## Classify APIs exposing sensitive data

Improve data security by assessing sensitive data exposed in API URL path parameters, query parameters, and request and response bodies, including the source of the data exposure. By using [Microsoft Purview](/en-us/purview/sit-sensitive-information-type-learn-about), you can use custom sensitive information types and sensitivity labels to create a common taxonomy, covering data-in-transit risks.

### Sampling

Defender CSPM plan assesses sensitive data exposure in your APIs by using sampling methods. This approach saves both cost and time.

## Explore API risks and prioritize remediation

Attack path analysis identifies risks to your API endpoints, especially with multiple security insights like unauthenticated access and external exposure. Use Defender CSPM’s [cloud security explorer](how-to-manage-cloud-security-explorer) to enrich API risk exploration by linking APIs with backend compute environments like virtual machines and load balancers. This visibility helps security teams quickly prioritize and mitigate API attack surfaces, offering insight into potential lateral movement or data exfiltration risks.

## Enable API security posture management

To use API security posture capabilities in Microsoft Defender for Cloud, you must:

1. **Enable the Defender cloud security posture management (Defender CSPM) plan** in your subscription.
2. **Enable the [API Security Posture Management extension](enable-api-security-posture)** to allow Defender for Cloud to discover APIs and assess their posture.

After you enable these features, Defender for Cloud automatically starts onboarding supported APIs and providing visibility and security insights.