---
layout: Conceptual
title: Manage cloud security plans in the Defender portal - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-portal/manage-plans-defender-portal
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
description: Configure cloud security plan coverage across connected Azure environments in the Microsoft Defender portal.
ms.topic: how-to
ms.date: 2026-07-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 851f6eb1-aead-c68c-f89b-b907266de41a
document_version_independent_id: 35971eb8-ad82-7c7e-315f-70370afbd314
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-portal/manage-plans-defender-portal.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: ../toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-portal/manage-plans-defender-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-portal/manage-plans-defender-portal.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 0acf74e9-c242-43c0-67d4-822921ae7c1e
---

# Manage cloud security plans in the Defender portal - Microsoft Defender for Cloud | Microsoft Learn

Important

This feature is in preview. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Use the Microsoft Defender portal to configure cloud security plans across connected Azure environments. You can apply plans globally to all current and future connected environments or configure plans for selected management groups and subscriptions.

## Prerequisites

Before you begin:

- To configure plans for specific management groups or subscriptions, [connect the Azure environments](connect-azure-environments-defender-portal) that you want to manage. You don't need to connect each environment before configuring global plan enablement, which applies automatically to current and future connected environments.
- The **Global Administrator** or **Security Administrator** role in Microsoft Entra ID. Alternatively, you need the **Core security settings (Manage)** permission in [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/custom-permissions-details#authorization-and-settings).
- Review [changes to Defender for Cloud plan management in the Defender portal](plan-management-changes-defender-portal).

Note

Cloud security plan management in the Defender portal currently supports Azure commercial environments only. AWS, GCP, Azure national or sovereign clouds, Azure DevOps, GitLab, JFrog Artifactory, and Docker Hub aren't supported in this experience. GitHub is supported separately in public preview. For setup instructions, see [Create a GitHub connector](/en-us/security-exposure-management/create-github-connector).

## What happens when you manage plans in the Defender portal

Azure environments continue to use Azure-based plan management until one of the following actions occurs:

- You migrate a specific connected environment to the Defender portal.
- You configure global plan enablement at the tenant level. All current connected environments are migrated automatically, and future connected environments inherit the same configuration.

After migration, plan configuration is managed in the Defender portal and appears as view-only in the Azure portal. Cost information is available in the Cloud security cost report.

Important

Resource-level plan configurations aren't preserved when plan management moves to the Defender portal. Plan coverage is configured at the management-group or subscription level and applies to the resources under that scope.

## Choose how to edit and enable cloud security plans

You can enable cloud security plans in either of the following ways:

| Configuration | Use |
| --- | --- |
| Global plan enablement | Set cloud security plans globally for all connected and newly connected environments. |
| Per-environment plan configuration | Configure security plans for selected environments and groups. |

## Configure plans for selected environments

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **Cloud security**.
3. Under **Manage cloud security**, select **Define Cloud Security plans**.
4. Under **Per-environment plan configurations**, select **View environments**.
5. Select **Groups** or **Environments**, depending on the scope you want to configure.
6. When prompted, approve moving plan management for the selected environments to the Defender portal. To understand the effects of this change, see [What changes when managing cloud security plans in the Defender portal](plan-management-changes-defender-portal).

    [![Screenshot showing the environment details pane with the option to review migration details.](media/manage-plans-defender-portal/selected-environment-review-migration.png)](media/manage-plans-defender-portal/selected-environment-review-migration.png#lightbox)
7. Select **Edit plans**.

    If you selected multiple environments, select **Bulk edit coverage**.
8. Enable or disable the plans you want to apply.

    [![Screenshot showing the Edit plans pane for an Azure management group in the Defender portal.](media/manage-plans-defender-portal/selected-environment-edit-plans.png)](media/manage-plans-defender-portal/selected-environment-edit-plans.png#lightbox)
9. If prompted, choose whether to start the 30-day free trial for eligible subscriptions.
10. Configure the available plan settings and extensions.

To prevent child environments from overriding the configuration, select the lock icon.

## Configure global plan enablement

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **Cloud security**.
3. Under **Manage cloud security**, select **Define Cloud Security plans**.
4. Under **Global plans enablement**, select **Global plans enablement page**.
5. When prompted, approve moving cloud security plan management for current and future connected environments to the Defender portal. This is a one-time tenant-level approval that applies automatically to all existing and future connected environments.
6. Enable or disable the cloud security plans that you want to apply.

    [![Screenshot showing global security plan enablement settings, including plan selection and the Save and apply button.](media/manage-plans-defender-portal/global-plan-enablement.png)](media/manage-plans-defender-portal/global-plan-enablement.png#lightbox)
7. If prompted, choose whether to start the 30-day free trial for eligible subscriptions.
8. Configure the available settings and extensions for each plan.
9. Review the changes, and then confirm the configuration.

The configuration applies to all current and newly connected environments.

To prevent child environments from overriding the global configuration, select the lock icon.

## Cloud security trial behavior

You can start a 30-day free trial for all eligible cloud security plans when you enable plans in the Defender portal.

The trial requires explicit opt-in. During the trial, eligible environments receive access to all eligible cloud security plans.

The trial selection applies to the scope where you enable the plans. When you start the trial at the tenant or management-group level, the selection is inherited by eligible environments under that scope, including:

- Existing eligible environments.
- Future eligible environments added under that scope.

Each future eligible environment receives its own 30-day free trial when it becomes eligible.

If you enable plans without starting the trial, the trial is no longer available for those environments and billing begins immediately.

You can change the trial selection for a scope later. Changes apply from that point forward. A trial that already started for an environment isn't canceled, extended, or reset by a later change.

After the trial ends, DWU billing begins unless all cloud security plans are disabled before the trial expires.

Moving plan management from the Azure portal to the Defender portal doesn't create, extend, or reset trial eligibility. An environment that previously used its cloud security trial isn't eligible for another trial.

## Plan statuses and inheritance

Cloud security plan management uses the Azure management hierarchy to determine which plan configuration applies to an environment.

| Status | Meaning |
| --- | --- |
| **Unconfigured (Inherit)** | No configuration is applied directly. The environment inherits its plan setting from the nearest configured parent. |
| **Enabled** | The plan and its extensions are enabled. An inherited configuration appears as **Enabled (Inherited)**. |
| **Disabled** | The plan and its extensions are disabled. An inherited configuration appears as **Disabled (Inherited)**. |

The following inheritance rules apply:

- Settings configured at a higher scope flow down to underlying environments.
- A plan state configured directly in the Defender portal isn't automatically replaced by another higher-level setting.
- When **Enforce and lock** is enabled, the higher-level configuration overrides settings on child environments, including settings configured directly on those environments. Child environments can't override the enforced configuration.

## Configure plan extensions

You can configure the extensions associated with an enabled plan.

- Enabling a plan enables its extensions by default.
- Disabling a plan disables its extensions by default.
- Use the settings control next to a plan to enable or disable individual extensions.

## Review environment coverage

Use the environments page to verify the plan coverage applied to your Azure environments and see where their security plans are managed.

1. Go to **Cloud security**.
2. Under **Manage cloud security**, select **Define Cloud Security plans**.
3. Under **Per-environment plan configurations**, select **View environments**.
4. Use **All**, **Groups**, or **Environments** to choose the hierarchy level you want to review.
5. Review the plan enablement status, subscription coverage, and where security plans are managed for each environment.

    [![Screenshot showing the Environments management table with plan enablement status and the portal managing each plan highlighted.](media/manage-plans-defender-portal/environment-coverage-status.png)](media/manage-plans-defender-portal/environment-coverage-status.png#lightbox)

Hover over an environment's plan enablement status to view its current status. For detailed coverage information, select the environment and review the coverage across its hierarchy.