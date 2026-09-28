---
layout: Conceptual
title: DevOps environment posture management overview - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-devops-environment-posture-management-overview
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
description: Learn how to discover security posture violations in DevOps environments
ms.date: 2025-07-14T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: aa3647ab-3ff7-a0df-f5b9-36cedc9e12c3
document_version_independent_id: 9c604fe4-46a5-3393-8e2d-1babfaeaea75
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/concept-devops-environment-posture-management-overview.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/concept-devops-environment-posture-management-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/concept-devops-environment-posture-management-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 823bf9c6-35c9-3ae0-2018-a816fb46e858
---

# DevOps environment posture management overview - Microsoft Defender for Cloud | Microsoft Learn

With an increase of cyber attacks on source code management systems and continuous integration/continuous delivery pipelines, securing DevOps platforms against the diverse range of threats identified in the [DevOps Threat Matrix](https://www.microsoft.com/security/blog/2023/04/06/devops-threat-matrix/) is crucial. Such cyber attacks can enable code injection, privilege escalation, and data exfiltration, potentially leading to extensive impact.

DevOps posture management is a feature in Microsoft Defender for Cloud that:

- Provides insights into the security posture of the entire software supply chain lifecycle.
- Uses advanced scanners for in-depth assessments.
- Covers various resources, from organizations, pipelines, and repositories.
- Allows customers to reduce their attack surface by uncovering and acting on the provided recommendations.

## DevOps scanners

To provide findings, DevOps posture management uses DevOps scanners to identify weaknesses in source code management and continuous integration/continuous delivery pipelines by running checks against the security configurations and access controls.

Azure DevOps and GitHub scanners are used internally within Microsoft to identify risks associated with DevOps resources, reducing attack surface and strengthening corporate DevOps systems.

Once a DevOps environment is connected, Defender for Cloud autoconfigures these scanners to conduct recurring scans every 24 hours across multiple DevOps resources, including:

- Builds
- Secure Files
- Variable Groups
- Service Connections
- Organizations
- Repositories

## DevOps threat matrix risk reduction

DevOps posture management assists organizations in discovering and remediating harmful misconfigurations in the DevOps platform. This leads to a resilient, zero-trust DevOps environment, which is strengthened against a range of threats defined in the DevOps threat matrix. The primary posture management controls include:

- **Scoped secret access**: Minimize the exposure of sensitive information and reduce the risk of unauthorized access, data leaks, and lateral movements by ensuring each pipeline only has access to the secrets essential to its function.
- **Restriction of self-hosted runners and high permissions**: prevent unauthorized executions and potential escalations by avoiding self-hosted runners and ensuring that pipeline permissions default to read-only.
- **Enhanced branch protection**: Maintain the integrity of the code by enforcing branch protection rules and preventing malicious code injections.
- **Optimized permissions and secure repositories**: Reduce the risk of unauthorized access, modifications by tracking minimum base permissions, and enablement of [secret push protection](https://docs.github.com/enterprise-cloud@latest/code-security/secret-scanning/push-protection-for-repositories-and-organizations) for repositories.
- Learn more about the [DevOps threat matrix](https://www.microsoft.com/security/blog/2023/04/06/devops-threat-matrix/).

## DevOps posture management recommendations

When the DevOps scanners uncover deviations from security best practices within source code management systems and continuous integration/continuous delivery pipelines, Defender for Cloud outputs precise and actionable recommendations. These recommendations have the following benefits:

- **Enhanced visibility**: Obtain comprehensive insights into the security posture of DevOps environments, ensuring a well-rounded understanding of any existing vulnerabilities. Identify missing branch protection rules, privilege escalation risks, and insecure connections to prevent attacks.
- **Priority-based action**: Filter results by severity to spend resources and efforts more effectively by addressing the most critical vulnerabilities first.
- **Attack surface reduction**: Address highlighted security gaps to significantly minimize vulnerable attack surfaces, thereby hardening defenses against potential threats.
- **Real-time notifications**: Ability to integrate with workflow automations to receive immediate alerts when secure configurations alter, allowing for prompt action and ensuring sustained compliance with security protocols.