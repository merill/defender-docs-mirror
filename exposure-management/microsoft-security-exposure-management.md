---
layout: Conceptual
title: What is Microsoft Security Exposure Management? - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/microsoft-security-exposure-management
author: dlanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how Microsoft Security Exposure Management enhances and extends security posture management.
ms.topic: overview
ms.date: 2025-07-30T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: b794f70f-a6d4-c17b-39e5-59d0e3e2a193
document_version_independent_id: b794f70f-a6d4-c17b-39e5-59d0e3e2a193
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/microsoft-security-exposure-management.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-security-exposure-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/microsoft-security-exposure-management.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 71b98dfd-ab1b-9ff7-b12c-f8bf8a093a0f
---

# What is Microsoft Security Exposure Management? - Microsoft Security Exposure Management | Microsoft Learn

Microsoft Security Exposure Management is a security solution that provides a unified view of security posture across company assets and workloads spanning endpoints, cloud resources, and external attack surfaces. Security Exposure Management enriches asset information with security context that helps you to proactively manage attack surfaces, protect critical assets, and explore and mitigate exposure risk across your entire digital estate.

With the integration of Defender for Cloud in the Defender portal, MSEM now provides comprehensive exposure management across endpoints and cloud environments, aggregating signals from Azure, AWS, and GCP (via Defender for Cloud integration) alongside traditional on-premises signals. This unified exposure graph covers devices, identities, cloud assets, and external attack surfaces, aligning with Gartner's Continuous Threat Exposure Management (CTEM) approach to provide end-to-end visibility and risk management.

Note

Microsoft Security Exposure Management is available in Public Cloud only. It's not available in national/sovereign clouds (US Gov, China Gov, or other sovereign clouds).

## Who uses Security Exposure Management?

Security Exposure Management is aimed at:

- Security and compliance admins responsible for maintaining and improving organizational security posture.
- Security operations (SecOps) and partner teams who need visibility into data and workloads across organizational silos to effectively detect, investigate, and mitigate security threats.
- Security architects responsible for solving systematic issues in overall security posture.
- Chief Information Security Officers (CISOs) and security decision makers who need insights into organizational attack surfaces and exposure in order to understand security risk within organizational risk frameworks.

## What can I do with Security Exposure Management?

With Security Exposure Management you can:

- **Get a unified view across the organization**: Security Exposure Management continuously discovers assets and workloads across endpoints, cloud environments, and external attack surfaces, gathering discovered data into a unified and up-to-date view of your inventory and attack surface.
- **Manage and investigate attack surfaces**: Visualize, analyze, and manage cross-workload attack surfaces spanning on-premises, cloud, and hybrid environments.

    - The enterprise exposure graph gathers information from multiple sources including cloud misconfigurations, multi-cloud assets, and external attack surface data to provide a comprehensive view of security posture and exposure across the business.
    - Graph schemas provide contextual information about specific organizational entities such as devices, identities, machines, cloud resources, and storage across all environments.
    - Query the enterprise exposure graph to explore assets, assess risk, and hunt for threats across on-premises, hybrid, and multicloud environments including Azure, AWS, and GCP.
    - Visualize your environment and graph queries with the attack surface map, which now includes cloud resources and their relationships.
- **Discover and safeguard critical assets**: Security Exposure Management marks predefined assets and assets you customize as critical across all domains including devices, identities, and cloud resources. This enables you to focus and prioritize on those critical assets to ensure security and business continuity.
- **Manage exposure**: Security Exposure Management provides tools to manage security exposure, and mitigate exposure risk.

    - The **Overview**dashboard organizes work around two core actions:
        - **Resolve Now** — Prioritized, actionable items across Patch, Mitigate, and Fix categories, focused on internet-exposed and business-critical assets.
        - **Monitor Exposure** — A real-time view of internet-exposed resources (cloud assets, devices, shadow resources) and domain initiative scores across Code, Endpoint, Cloud, Identity, and SaaS.
    - Exposure insights aggregate security posture data, and provide rich context around the security posture state of your asset inventory.
    - Use these insights to prioritize security efforts and investments.
    - Insights include security events, recommendations, metrics, and security initiatives.
    - As you manage exposure risk, attack paths show you how an attacker might breach your attack surface, including hybrid attack paths that span on-premises and cloud contexts.
        - Security Exposure Management generates attack paths based on data collected across assets and workloads from multiple environments. It simulates attack scenarios, and identifies weaknesses that an attacker could exploit across endpoints and cloud resources.
        - You can use the enterprise exposure graph and attack surface map to visualize and understand potential threats across your hybrid infrastructure.
        - You can also focus on choke points through which many attack paths flow, including those that bridge on-premises and cloud environments.
        - Actionable recommendations help you to mitigate identified attack paths across all domains.
    - You can assess, prioritize, and remediate vulnerabilities across devices and cloud resources through [Microsoft Defender Vulnerability Management integration in Security Exposure Management](vulnerability-management-integration).
- **Connect your data**: Security Exposure Management supports a variety of data connectors to integrate with different security solutions and data sources, including external vendors and cloud platforms.

    - Consolidate security data from multiple sources including third-party tools (ServiceNow CMDB, Tenable, Qualys, Rapid7) into a single, unified view within the Exposure Management platform.
    - Gain deeper insights into your security posture by integrating data from various environments and external sources.
    - Simplify the management of security data across different platforms and solutions through unified exposure management connectors.