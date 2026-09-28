---
layout: Conceptual
title: Microsoft Sentinel platform solution quality guidelines | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/isv/platform-solution-quality-guidance
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Learn quality guidance for Microsoft Sentinel platform solutions that use the data lake, graph, notebook jobs, MCP tools, and Security Copilot experiences.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: smarapareddy
ms.topic: best-practice
ms.date: 2026-05-25T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1012
ai-usage: ai-assisted
locale: en-us
document_id: 135a81b3-7ae1-8dd4-0a08-dbdea9e4bad9
document_version_independent_id: 740b9b19-ed6e-8ff4-ee5e-94f5fc565496
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/isv/platform-solution-quality-guidance.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/isv/platform-solution-quality-guidance
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/isv/platform-solution-quality-guidance.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: 08a64e34-7784-0a18-94dc-3838878ed927
---

# Microsoft Sentinel platform solution quality guidelines | Microsoft Learn

Use these guidelines to build platform solutions that rely on Microsoft Sentinel data lake, graph, notebook jobs, Model Context Protocol (MCP) tools, and Microsoft Security Copilot integrations.

## Use Microsoft Sentinel data lake and graph intentionally

Platform solutions use the Microsoft Sentinel data lake to maximize long-term data coverage. Define which scenarios require data lake tables, graph access, or both, and document those dependencies in your solution description.

When you design data access:

- Use only required tables and graph entities for each scenario.
- Document retention and freshness assumptions for each required data source.
- Validate query cost and runtime for large datasets before publishing.

## Build Security Copilot and MCP experiences securely

For Security Copilot and MCP-based experiences, reduce authentication burden while maintaining least privilege.

- **Use Security Copilot plugins first** when a plugin already supports your scenario. For Microsoft plugins, Security Copilot handles authentication. See [Security Copilot plugins overview](/en-us/copilot/security/plugin-overview).
- **Use delegated auth when supported** to avoid storing client secrets and passwords. See [API plugins documentation for Security Copilot](/en-us/copilot/security/plugin-api).
- **Use secret-based auth only when needed** and store secrets by using a secure store such as [Azure Key Vault](/en-us/azure/key-vault/general/overview).
- **Scope permissions to minimum access** and require multifactor authentication for identities that install or run agents.

## Create notebook jobs for deterministic data processing

[Notebook jobs](/en-us/azure/sentinel/datalake/notebook-jobs) transform data and support advanced machine learning workflows. Notebook output can be written to custom data lake tables and used by Copilot and MCP experiences.

When you build notebook jobs, use these best practices:

- Author notebook jobs by using the [Visual Studio Code Sentinel extension](/en-us/azure/sentinel/datalake/notebooks-overview).
- Review [example notebooks](../datalake/notebook-examples) to speed up design and implementation.
- Add workspace autodetection logic when your solution might run in multiple workspaces.
- Use the System tables workspace when your solution needs a dependable write target.
- Document all notebook dependencies, schedules, and expected outputs.

## Define platform prerequisites and permissions

Before customers install your platform solution, provide a clear prerequisites section that includes:

- Required roles and permissions. For more information, see [Roles and permissions in the Microsoft Sentinel platform](/en-us/azure/sentinel/roles).
- Data lake or graph dependencies required for each feature.
- Any external services, identities, or API endpoints your solution requires.

## Maintain platform solutions after publishing

After publication, maintain and update your platform solution regularly:

- Plan for service or feature deprecations at least six months before end-of-life milestones.
- Keep the solution description page accurate and fix broken links quickly.
- Address GitHub CodeQL alerts in a timely manner.