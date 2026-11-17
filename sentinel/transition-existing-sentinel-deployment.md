---
layout: Conceptual
title: Transition an existing Microsoft Sentinel deployment to ISOC | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/transition-existing-sentinel-deployment
breadcrumb_path: breadcrumb/toc.json
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
description: Learn how to prepare an existing Microsoft Sentinel deployment for transition to Integrated Security Operations Center (ISOC) in Microsoft Defender.
author: mberdugo
ms.author: monaberdugo
ms.localizationpriority: high
ms.collection:
- m365-security
- tier1
- usx-security
ms.topic: how-to
ai-usage: ai-assisted
ms.date: 2026-11-15T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1032
locale: en-us
document_id: 4052d5ab-2736-0593-a7d6-04a33aaf55da
document_version_independent_id: 9bd213c3-8d9f-4396-fcbb-b1c54f0fb843
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/transition-existing-sentinel-deployment.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/transition-existing-sentinel-deployment
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/transition-existing-sentinel-deployment.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b42a862e-632f-7b54-9018-215a46495889
---

# Transition an existing Microsoft Sentinel deployment to ISOC | Microsoft Learn

If you already use Microsoft Sentinel, you can opt in your existing Microsoft Sentinel deployment to Integrated Security Operations Center (ISOC) in Microsoft Defender.

Before you opt in, complete the required prerequisites and review the content and integrations that depend on your existing Microsoft Sentinel data.

## Prerequisites

- Review the [ISOC eligibility and workspace requirements](/en-us/defender-xdr/isoc-overview).
- Identify all Microsoft Sentinel workspaces that are part of your deployment.
- Have the required [permissions to connect Microsoft Sentinel workspaces to the Microsoft Defender portal](microsoft-sentinel-onboard#microsoft-sentinel-prerequisites).
- Identify the primary Microsoft Sentinel workspace that you plan to use with ISOC.

## Review transition limitations

ISOC is in preview. Capabilities and availability might change during the preview period. Before you opt in, review these limitations:

- The transition converts all Microsoft Sentinel workspaces in your tenant to ISOC. The process is permanent and can't be undone.
- Customers who onboarded to the Microsoft Sentinel data lake before September 23, 2026, can't currently opt in to ISOC.

## Review billing changes before transitioning to ISOC

After transitioning to ISOC, your invoice shows ISOC charges instead of Microsoft Sentinel charges. Review the following billing changes:

- **Existing discounts:** Discounts negotiated for Microsoft Sentinel don't carry over to ISOC. Work with your Microsoft account team to review applicable discounts for ISOC before transitioning.
- **Commitment tiers:** ISOC doesn't offer commitment-tier pricing.
- **Microsoft 365 data benefit:** The Microsoft 365 data ingestion benefit of 5 MB per user per day doesn't apply to ISOC usage.
- **Dedicated clusters:** If your workspace is linked to a dedicated cluster, you can continue to use its functionality. However, ISOC usage is billed separately and doesn't count toward your existing dedicated cluster commitment. You continue to be charged for any unused cluster commitment.

## Connect all Microsoft Sentinel workspaces to the Defender portal

Before opting in to ISOC, connect every Microsoft Sentinel workspace in your deployment to the unified security operations experience in the Microsoft Defender portal.

**Required permissions:** **User Access Administrator** or **Microsoft Sentinel Contributor** with subscription **Owner** rights. Multi-workspace onboarding of a primary workspace requires **Global Administrator** or **Security Administrator** permissions.

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **System** &gt; **Settings** &gt; **Microsoft Sentinel**.
2. Select **Connect a workspace** and connect all remaining Microsoft Sentinel workspaces.
3. Choose your primary workspace, review the changes, and complete the connection.

For more information, see [Connect Microsoft Sentinel to the Microsoft Defender portal](microsoft-sentinel-onboard).

## Align table retention to supported ISOC values

ISOC supports specific retention values. Update tables configured with unsupported values, such as 120 or 150 days, before transitioning to ISOC. Aligning retention settings helps reduce the risk of unexpected billing changes.

**Required permissions:** Workspace-level **Owner**, **Contributor**, or **Log Analytics Contributor** permissions to modify table retention.

1. Go to **Setup & Configuration** &gt; **Data Management** &gt; **Data & Connectors** &gt; **Tables**.
2. Identify tables with unsupported retention values.
3. Update each affected table to a supported value, such as 90 or 180 days for Microsoft Defender XDR scenarios.
4. Repeat for all Microsoft Sentinel workspaces.

Note

ISOC includes 90 days of default retention for eligible tables and supports retention of 180 days and beyond for Microsoft Defender data. Retention beyond 90 days and up to 180 days is billed at the 180-day retention rate.

## Import Microsoft Sentinel roles into Defender RBAC

Microsoft Sentinel role assignments don't automatically transfer to Microsoft Defender role-based access control (RBAC). Importing existing roles helps preserve analyst and engineering access, simplifies permission management, and reduces the need to manually recreate role assignments. Skipping this step might result in some users losing access to Microsoft Defender data after conversion.

**Required permissions:** **Security Administrator** or **Global Administrator** permissions.

1. Open **Import roles** during the ISOC onboarding process.
2. Review the preselected roles from your primary workspace.
3. Review users, groups, and permissions, resolve any import errors, and complete the role import.

For more information, see [Update permissions and roles with Unified RBAC](transition-unified-rbac).

## Activate Defender RBAC workloads

Imported role assignments only take effect after you [activate Defender RBAC for the relevant workloads](/en-us/defender-xdr/activate-defender-rbac). If you skip activation, imported roles remain inactive and users might not have their intended access.

**Required permissions:** **Security Administrator** or **Global Administrator** permissions.

1. Select **Activate workloads** during the ISOC onboarding process.
2. Activate Defender RBAC for workloads that aren't yet enabled.
3. Verify that key users and groups have the expected access.

For tenants with multiple workspaces, this experience only applies to the primary workspace. For any secondary workspace containing Microsoft Defender tables, assign roles to the relevant users manually.

For more information, see [Update permissions and roles with Unified RBAC](transition-unified-rbac).

## Update content to use Microsoft Defender data

After transitioning to ISOC, Microsoft Defender data is no longer duplicated into Microsoft Sentinel workspace tables in the same way.

Review SOC optimization recommendations to update existing detections, workbooks, and automation to use Microsoft Defender advanced hunting data. These updates help maintain security coverage while reducing duplicate Microsoft Defender data ingestion costs. Don't reduce ingestion until you validate dependent content.

**Required permissions:** Defender RBAC permissions for detection tuning and security data access, plus **Microsoft Sentinel Contributor** permissions where applicable.

1. Go to **SOC optimization** and review recommendations under **Lower Defender data costs**. For more information about the recommendations, see the [SOC optimization reference](soc-optimization/soc-optimization-reference).
2. For each recommendation, update queries, analytics rules, workbooks, and playbooks to use Microsoft Defender advanced hunting data for the affected table.
3. Before reducing ingestion for each affected table, validate that:

    - Advanced hunting queries return expected results.
    - Detections generate the expected alerts.
    - Workbooks display accurate data.
    - Playbooks and automation execute successfully.
    - Users and automation identities retain the required access.
    - CI/CD pipelines reference the correct tables and schemas.

Update and validate dependent content before ingestion changes. If ingestion changes first, detections, workbooks, automation, and other content might continue to reference data that is no longer arriving in the Microsoft Sentinel workspace.

Work through the transition table by table instead of updating all affected content at once.

For more information, see [Review SOC optimization recommendations](transition-soc-optimization-recommendations).

## Stop duplicate Microsoft Defender data ingestion where applicable

ISOC includes 90 days of default retention for eligible Microsoft Defender data at no additional cost. Review SOC optimization recommendations to stop duplicate ingestion into Microsoft Sentinel workspaces while preserving investigation and analysis capabilities through Microsoft Defender advanced hunting.

Only stop duplicate ingestion after validating that dependent detections, workbooks, and automation have been updated. Stopping ingestion prematurely can create security coverage gaps.

**Required permissions:** Workspace-level Azure RBAC write permissions, such as **Log Analytics Contributor**, **Contributor**, or **Owner**.

1. Go to **Setup & Configuration** &gt; **Data Management** &gt; **Data & Connectors** &gt; **Tables**.
2. Select **Configure workspace** to stop streaming all eligible Microsoft Defender tables.

    ![Screenshot of the Tables page showing Configure workspace to prepare the workspace for an ISOC upgrade.](media/transition-existing-sentinel-deployment/configure-workspace.png)
3. If you have multiple workspaces, repeat this step for each workspace.

For information about supported data, included retention, and additional ingestion charges, see [Data ingestion, retention, and billing for ISOC in Microsoft Defender](/en-us/defender-xdr/integrated-security-operations-data-billing-retention).

Note

ISOC includes 90 days of default retention for eligible tables and supports retention of 180 days and beyond for Microsoft Defender data. Retention beyond 90 days and up to 180 days is billed at the 180-day retention rate.

## Review MSSP considerations

If your Microsoft Sentinel deployment is managed by a managed security service provider (MSSP), review the deployment and delegation changes that apply before completing the transition.

For more information, see [Transition MSSP-managed deployments to Microsoft Defender](transition-mssp-deployments).

## Review what changes when you move to ISOC

Review the changes that apply to your deployment:

- **Tenant-wide transition:** All Microsoft Sentinel workspaces in your tenant transition to ISOC together. A combination of ISOC and non-ISOC workspaces isn't supported.
- **Pricing and billing:** ISOC pricing and billing meters replace applicable Microsoft Sentinel pricing and meters. Review the discount, commitment-tier, and benefit changes described earlier with your Microsoft account team, and renegotiate discounts before transitioning.
- **Data retention:** ISOC introduces 90-day default retention benefits and new pricing. Review your existing retention settings.
- **Security operations:** Your workspaces become part of ISOC. Some existing detections, queries, workbooks, and automation might require updates.