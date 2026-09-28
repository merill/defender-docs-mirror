---
layout: Conceptual
title: Troubleshoot solutions in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/isv/troubleshoot-sentinel-solutions
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
description: Troubleshoot Microsoft Sentinel data ingestion, analytics, packaging, and agent integration issues, and prepare information for Support.
ms.topic: troubleshooting
ms.date: 2025-09-17T00:00:00.0000000Z
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
locale: en-us
document_id: 25e97f74-bcbe-4c05-7b7f-36150f1becc3
document_version_independent_id: 6c401daf-6056-3aff-d275-3eb987874ffa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/isv/troubleshoot-sentinel-solutions.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/isv/troubleshoot-sentinel-solutions
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/isv/troubleshoot-sentinel-solutions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: f31fbca8-91e6-7dd3-2d8e-8652a5e386cf
---

# Troubleshoot solutions in Microsoft Sentinel | Microsoft Learn

Use this guide to diagnose issues, validate configurations, and understand support responsibilities for your Microsoft Sentinel solution.

## Before you contact support

Before opening a support case, complete the following checks:

- **Verify data availability:** Confirm that source data is arriving and that expected schemas and tables are present. If you use the Advanced Security Information Model (ASIM), make sure analytics rely on normalized fields.
- **Check platform health:** Review Sentinel health signals at [Auditing and health monitoring in Microsoft Sentinel](../health-audit) to confirm platform status and identify any issues.
- **Collect diagnostic artifacts:** Gather UTC timestamps, tenant and workspace IDs, solution name and version, failing API calls, and sanitized payloads.
- **Validate packaging:** Confirm that the manifest and schema are correct. Document any required Content Hub dependencies if your app or agent ships through the Security Store.
- **Confirm access and roles:** Verify that role-based access control (RBAC) is configured for service principals and agent identities (user-on-behalf-of versus app identity).

## Information to include when opening a support case

Provide the following details when contacting Microsoft Support:

- Tenant ID
- Workspace ID(s)
- Solution or package name and version
- Precise UTC timeframe
- Reproduction steps
- Sanitized request and response samples
- Job run IDs
- Error messages
- Health query results
- Roles and permissions involved

## Support model

Important

Independent software vendors should create self-help guides for their solutions. These guides should include common symptoms, checks, solutions, health KQL queries, error codes, and instructions for collecting logs.

**Microsoft Support covers** Microsoft Support can assist with:

- Platform availability and behavior (SIEM and data lake)
- Onboarding to Microsoft Sentinel
- Installation of solutions from the Azure Marketplace and Content Hub

**Independent software vendor (ISV) responsibilities** Independent software vendors are responsible for:

- Custom content such as rules, parsers, and workbooks
- Code and Model Context Protocol (MCP) tools or agents
- External dependencies that integrate with Microsoft Sentinel
- Providing reproducible cases and supporting artifacts to Microsoft Support when issues with ISV content are escalated

## Troubleshooting common problems

Use the following scenario-based checks and solutions to troubleshoot common issues:

### Data connectors and ingestion not working

| **Checks to perform** | **Solution** |
| --- | --- |
| - Confirm connector prerequisites and permissions. - Validate schema alignment.  - Verify ASIM normalization if applicable. | - Reapply configuration.  - Correct schema or mapping issues.  - Document any implications for downstream analytics when data is lake-only. |

### Analytics rules (SIEM) not firing

| **Checks to perform** | **Solution** |
| --- | --- |
| - Confirm data freshness.  - Review rule scheduling and lookback versus latency.  - Verify that the required parser is installed and enabled. | - Test the rule with a query.  - Widen the lookback window.  - Reinstall the parser. - Add a verification workbook. |

### Jobs and notebooks over the data lake failing

| **Checks to perform** | **Solution** |
| --- | --- |
| - Validate explicit workspace and database parameters.  - Review retry and backoff configuration.  - Check job status and terminal states. | - Parameterize notebooks.  - Make jobs idempotent. - Emit structured stage logs. - Test across multiple workspaces or tenants. |

### Packaging and publishing issues

| **Checks to perform** | **Solution** |
| --- | --- |
| - Confirm manifest fields and versioning.  - Review cross-offer prerequisites (Content Hub versus Security Store). | - Run local validation.  - Keep directory and filenames stable.  - Document installation, upgrade, and uninstallation flows. |

### Agentic experiences via Model Context Protocol (MCP) not working in Visual Studio Code

| **Checks to perform** | **Solution** |
| --- | --- |
| - Confirm MCP server collections and tool registration.  - Validate endpoint reachability.  - Review token scope and expiry.  - Ensure Visual Studio Code can discover tools. | - Group tools logically.  - Rotate tokens before they expire.  - Provide example prompts.  - Document known errors with resolutions. |

## Audit logs

When a solution or package is installed, updated, or deleted, its components are created, updated, or removed as defined in the package configuration. Actions on individual package components are recorded in audit logs.

For Microsoft Sentinel platform components, see: [Audit log for Microsoft Sentinel data lake](../datalake/auditing-lake-activities)

For Microsoft Sentinel SIEM components, see: [Audit Microsoft Sentinel queries and activities](../audit-sentinel-data)