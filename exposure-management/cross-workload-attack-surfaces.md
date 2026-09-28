---
layout: Conceptual
title: Overview of attack surface management in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/cross-workload-attack-surfaces
author: dlanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn about attack surface management in Microsoft Security Exposure Management. s
ms.topic: overview
ms.date: 2025-10-26T00:00:00.0000000Z
locale: en-us
document_id: 12be8987-2805-3f32-c3a2-d40a9121ad15
document_version_independent_id: 12be8987-2805-3f32-c3a2-d40a9121ad15
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/cross-workload-attack-surfaces.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: cross-workload-attack-surfaces
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/cross-workload-attack-surfaces.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: a9eb3236-5e03-7284-3641-e16d6d2cf76f
---

# Overview of attack surface management in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

[Microsoft Security Exposure Management](microsoft-security-exposure-management) helps you to visualize, analyze, and remediate cross-workload attack surfaces spanning on-premises, cloud, and hybrid environments. With the integration of Defender for Cloud in the Defender portal, attack surface management includes hybrid attack paths that bridge on-premises and cloud contexts, providing comprehensive visibility across your entire digital estate.

## Enterprise exposure graph

The enterprise exposure graph is the central tool for exploring and managing attack surfaces. The graph gathers information about assets, users, workloads, and more, from across your enterprise to provide a unified, comprehensive view of your organizational security posture.

### Graph schemas

Graph schemas provide a framework for organizing and analyzing interconnected assets from multiple workloads across the organization.

- Schemas are made up of tables that provide either event information or information about devices, alerts, identities, and other entity types.
- You query against schemas for proactive threat hunting across data and events. You can build queries in [advanced hunting](/en-us/defender-xdr/advanced-hunting-modes).
- To understand schemas and build effective queries, you can use a built-in schema reference that provides table information.

### Enterprise exposure graph schemas

The enterprise exposure graph and the exposure graph schemas extend the existing Defender XDR [advanced hunting schemas](/en-us/defender-xdr/advanced-hunting-schema-tables).

- The schemas provide attack surface information to help understand how potential threats can reach and compromise valuable assets.
- You use the schema tables and operators to query the enterprise exposure graph. Queries allow you to inspect and search attack surface data, and to retrieve exposure information to help prevent risk.
- The enterprise exposure graph currently includes assets, findings, and entity relationships from:
    - Microsoft Defender for Cloud (including Azure, AWS, and GCP resources)
    - Microsoft Defender for Endpoint
    - Microsoft Defender Vulnerability Management
    - Microsoft Defender for Identity
    - Microsoft Entra ID
    - External data sources through Exposure Management connectors (ServiceNow CMDB, Tenable, Qualys, Rapid7)

By correlating exposure queries with other graph data, such as incident data, you can uncover risk to a greater degree.

## Attack surface map

The attack surface map helps you to visualize the exposure data that you query using the exposure graph schema, including cloud resources and their relationships.

In the map you can explore the data across hybrid environments, check what assets are at risk, contextualize them in a broader network framework that spans on-premises and cloud, and prioritize security focus.

For example, you can check whether a particular asset has unwanted connections across cloud and on-premises environments, see whether a device has a path to the internet through cloud resources, identify how cloud misconfigurations might expose on-premises assets, and understand the full scope of hybrid attack paths.