---
layout: Conceptual
title: Overview of Mend.io integration - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/integration-mend-io
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
description: Learn how to enhance vulnerability analysis and provide comprehensive visibility of critical vulnerabilities by integrating Mend.io with Microsoft Defender.
ms.topic: overview
ms.date: 2025-05-20T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 6be8de31-5f75-265f-8294-5f2772ce9e27
document_version_independent_id: 40ebef8c-417f-3f49-e894-8e1fcc4cd47c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/integration-mend-io.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/integration-mend-io
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/integration-mend-io.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 1cebc6e0-bfc1-46e4-a1df-4cbc3f228e9f
---

# Overview of Mend.io integration - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud integrates with Mend.io to improve vulnerability analysis using reachability-based Software Composition Analysis (SCA). SCA shows exploitable vulnerabilities from code to runtime.

Reachable vulnerabilities are security flaws in open-source dependencies with a direct and exploitable execution path. These vulnerabilities are high risk because malicious actors can actively trigger them within the application's current flow. Addressing these vulnerabilities is critical to prevent potential attacks.

The integration with Mend.io identifies vulnerable security combinations, such as exploitable vulnerabilities in open-source packages used in internet-exposed workloads. Defender for Cloud users can see full attack paths from code committed in Azure DevOps, GitHub, or GitLab to running workloads on Azure, Amazon Web Services (AWS), or Google Cloud Platform (GCP).

## Benefits of Integrating Mend.io

Mend.io is a security platform that identifies and mitigates vulnerabilities in partner dependencies within software applications. Mend.io offers advanced reachability analysis that assesses the execution paths of these vulnerabilities, allowing security teams to prioritize and address them effectively.

Integrating Mend.io with Microsoft Defender for Cloud allows you to:

- Streamline the discovery and remediation of reachable vulnerabilities.
- View a comprehensive list of security risks within an application's code flow.
- Prevent potential attacks by identifying high-risk vulnerabilities early in the development lifecycle, ensuring robust application security from code to runtime.

With this integration, reachability analysis findings from Mend.io are accessible within the Defender for Cloud experiences, including recommendations, attack path analysis, and security explorer. The integration provides visibility into the health of the code for central security teams. This visibility enables them to better prioritize and mitigate open-source vulnerabilities from code development to runtime. They achieve this visibility through advanced function-level reachability and exploitability analysis.