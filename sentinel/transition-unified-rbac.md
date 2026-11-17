---
layout: Conceptual
title: Update permissions and roles with Defender RBAC - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/transition-unified-rbac
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
description: Learn how to import Microsoft Sentinel roles into Microsoft Defender XDR Defender RBAC and activate the required Defender workloads before transitioning an existing Microsoft Sentinel deployment to ISOC.
author: robicz
ms.author: robicz
ms.localizationpriority: high
ms.collection:
- m365-security
- tier1
- usx-security
ms.topic: how-to
ai-usage: ai-assisted
ms.date: 2026-10-19T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1030
locale: en-us
document_id: f503a003-2692-481b-7123-009ef4402bd9
document_version_independent_id: 76ac1cb7-84a3-54cc-8322-76771492e67d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/transition-unified-rbac.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/transition-unified-rbac
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/transition-unified-rbac.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: cb206c17-83a8-4436-9718-c8628d1dd5e9
---

# Update permissions and roles with Defender RBAC - Microsoft Defender XDR | Microsoft Learn

Before you transition an existing Microsoft Sentinel deployment to Integrated Security Operations Center (ISOC), make sure users who currently access Microsoft Defender data through the Microsoft Sentinel workspace have the corresponding Microsoft Defender workload access.

Use Defender role-based access control (RBAC) in Microsoft Defender XDR to import supported Microsoft Sentinel roles and assignments. Review the roles and assignments before submitting the import, and activate Defender RBAC separately for any required Microsoft Defender workloads that aren't already active.

Important

Microsoft Sentinel workspace access alone doesn't provide access to the corresponding Microsoft Defender workload data. Complete and validate the permission changes before ingestion changes for the affected data.

## Before you begin

Ask your Defender RBAC administrator to perform the migration.

To import roles, the administrator needs:

- At least the Security Administrator role in Microsoft Entra ID, or all Authorization permissions in Microsoft Defender RBAC.
- Role-management permissions across all required scopes.
- Access to the primary Microsoft Sentinel workspace and authorization to onboard the workspace to Defender RBAC. Read access to the workspace alone isn't sufficient.
- Management access to the Microsoft Defender workloads that need to be included.

To activate Defender RBAC for Microsoft Defender workloads that aren't already active, the administrator must have at least the Security Administrator role in Microsoft Entra ID.

To activate a Microsoft Sentinel workspace in Defender RBAC, the administrator must have the Security Administrator role in Microsoft Entra ID and either Subscription Owner permissions or both User Access Administrator and Microsoft Sentinel Contributor permissions on the workspace. However, the source Microsoft Sentinel workspace doesn't need to be activated in Defender RBAC for this import.

The supported Microsoft Defender destination workloads are:

- Microsoft Defender for Endpoint.
- Microsoft Defender for Office 365.
- Microsoft Defender for Identity.
- Microsoft Defender for Cloud Apps.

These workloads are added as destinations only when they're eligible, provisioned, and the importing administrator has role-management permissions across all their scopes.

## How role import works

The import creates Defender RBAC roles and user or group assignments from supported Microsoft Sentinel roles.

For qualifying assignments scoped only to the primary Microsoft Sentinel workspace, the import can add eligible Microsoft Defender workloads that the administrator has permission to manage across all required scopes.

Users receive access to Microsoft Defender data through the resulting Defender RBAC assignments when Defender RBAC is active for the corresponding workload.

Importing roles and activating workloads are separate actions:

- Importing roles doesn't activate Defender RBAC for a workload.
- Activating a workload doesn't import Microsoft Sentinel roles.
- If a destination Microsoft Defender workload is already active, imported role assignments can take effect immediately without an additional activation step.
- The source Microsoft Sentinel workspace doesn't need Defender RBAC activated for the import.

Review the roles, permissions, assignments, and scopes before submitting the import, particularly for workloads where Defender RBAC is already active.

## Import Microsoft Sentinel roles

You can import Microsoft Sentinel roles in two ways: through Microsoft Sentinel settings or the Permissions and roles page.

### Import roles from Microsoft Sentinel settings

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/)
2. Go to **Setup & Configuration &gt; Settings &gt; Microsoft Sentinel.**
3. Select **Upgrade to ISOC**.

    ![Screenshot showing the Upgrade to ISOC button.](media/upgrade-to-isoc-button.png)
4. In **Get your Sentinel workspace ready for ISOC**, expand **3. Import Sentinel roles into Defender RBAC**.
5. Select **Go to import roles** to open the role import process.

    ![Screenshot showing the Go to import roles option.](media/import-roles-isoc-sentinel.png)
6. Continue to Complete the role import.

### Import roles from Permissions and roles

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/)
2. Go to **Setup & Configuration &gt; Permissions.**
3. Under **Microsoft Defender XDR**, select **Roles**.
4. In the **Get ready for ISOC** banner, select the **Start ISOC role import** button.

    ![Screenshot showing the Start ISOC role import button.](media/start-isoc-role-import-permission.png)

    If the banner provides options to import roles and activate workloads, start with the role import. Don't use the separate **Activate workloads** action before reviewing the roles and assignments.
5. Continue to Complete the role import.

### Complete the role import

In the **Import roles** wizard:

1. Confirm **Microsoft Sentinel** is selected as an import source.

    Microsoft Sentinel uses your primary workspace for the import. For users and groups who rely on Defender data in secondary Microsoft Sentinel workspaces, see Secondary workspaces role definition.

    You can also select other available workloads if you want to import their existing roles. These workloads are additional import sources; selecting them doesn't make them additional destinations for the Microsoft Sentinel role import.
2. Select **Next**, and review the roles selected for import.

    Eligible Microsoft Sentinel roles are preselected and required. Review:

    - Role details.
    - Assigned users and groups.
    - Permissions.
    - Additional data sources.

    You can deselect optional roles imported from other workloads.

    Before submitting, confirm that the selected roles and assignments provide the intended permissions and scopes, particularly for destination workloads where Defender RBAC is already active.
3. Complete the review and submit the import.
4. Review the import result for each role.

    The import can partially succeed, with some roles imported successfully and others failing.

    If any roles fail to import, review the errors and resolve the failures before activating additional workloads or changing ingestion.

    Don't reimport roles that were imported successfully. Importing the same role again can create duplicate roles and assignments.

## Secondary workspaces role definition

The guided role-import flow adds eligible Defender access only for qualifying primary-workspace assignments.

If your secondary Microsoft Sentinel workspaces contain Defender tables, review access for users and groups who rely on that data as part of your role transfer process.

Importing Sentinel roles from secondary workspaces does not, by itself, grant the corresponding Defender access. Some users may therefore need additional permissions to access the data directly in Defender.

Please follow the next steps:

1. Check existing access first. Users who already have the required Defender permissions, through the primary-workspace migration or other assignments, do not need additional grants. Confirm that their existing access covers the data and activities they need.
2. Add permissions only where needed. Create or reuse a custom Defender RBAC role.
3. Select these specific permissions rather than all read or manage permissions:

    1. For read-only hunting, select Security data basics (Read).
    2. For email and collaboration hunting, also select Email & collaboration metadata (Read).

    **Reference:** current Sentinel import mapping. The management permissions below are needed only when those Defender actions are required, not simply to retain read access.

    | Existing Sentinel role | Permissions in the imported role |
    | --- | --- |
    | Sentinel Reader | Security data basics (Read) |
    | Sentinel Responder | Security data basics (Read), Alerts (Manage), Response (Manage) |
    | Sentinel Contributor | Security data basics (Read), Alerts (Manage), Response (Manage), Detection tuning (Manage) |

    These roles take effect for the assigned users and groups when the corresponding workload uses Defender RBAC. If activation is required, follow the activation guidance and prepare existing users' access before switching permission models.
4. Scope the assignment.

    On **Assign users and data sources &gt; Add assignment**,

    - Select the affected users/groups and only the required Defender data sources.
    - Leave **Include future data sources automatically** unchecked. A Defender data source applies the selected permissions to that service, not just the data copied into a particular workspace.
    - Select the following as needed:
        - **Microsoft Defender for Endpoint** for device data
        - **Microsoft Defender for Office 365** for email and collaboration data
        - **Microsoft Defender for Identity** for identity workload data
        - **Microsoft Defender for Cloud Apps** for cloud-app activity
    - Apply resource restrictions supported by each service.
        - For Endpoint, review device-group access separately.
        - Do not configure Sentinel workspace permissions. Workload-level grants may expose additional tables and do not recreate the original workspace's table restrictions.
        - Review that additional data access and approve any broader access before assigning the roles.
5. Validate access and dependent content.

    - Have representative affected users confirm access to the data and history they need.
    - Check the intended resource restrictions.
    - Update and test queries, detections, and automation that previously used the workspace copies. Permission changes do not redirect those queries or migrate historical data.

## Activate the required workloads

After the import results are reviewed and any failures are resolved, activate Defender RBAC for the required Microsoft Defender workloads that aren't already active.

If a destination workload is already active, its imported assignments can already be in effect. Review those permissions and scopes before proceeding.

For workloads that aren't active:

1. Review the imported Defender RBAC roles and assignments together with any existing legacy access.
2. Select **Activate workloads** or **Workload settings** from the **Permissions and roles** page.
3. Enable Defender RBAC for each required Microsoft Defender workload that isn't already active.
4. Confirm the activation and review the resulting role assignments and workload scopes.

You don't need to activate Defender RBAC for the source Microsoft Sentinel workspace to complete this import.

## Validate effective access

Before you continue with ingestion changes:

1. Ask affected users to confirm that they can access the required Microsoft Defender data and actions.
2. Validate the permissions for each required workload.
3. Validate any resource or workload-specific scopes.
4. Review users whose Microsoft Sentinel access comes from role assignments at the resource-group or subscription level. Don't assume that inherited access was included in the import. Verify the resulting assignments and configure any missing access as needed.
5. Confirm that users who previously relied on Microsoft Sentinel workspace permissions have the corresponding Microsoft Defender access they need.

Don't assume that restrictions or scopes configured for Microsoft Sentinel are reproduced automatically in Microsoft Defender.

Note

This process doesn't change data ingestion and doesn't automatically migrate application or automation permissions. Review automation identities and application permissions separately before changing ingestion.

If the role-import option isn't available or role import is disabled, ask your Defender RBAC administrator to verify their permissions and feature availability.

## Further guidance

- [Create custom roles](/en-us/defender-xdr/create-custom-rbac-roles)
- [Import roles](/en-us/defender-xdr/import-rbac-roles)
- [Activate Defender RBAC](/en-us/defender-xdr/activate-defender-rbac)
- [Permission definitions](/en-us/defender-xdr/custom-permissions-details)
- [Endpoint device groups](/en-us/defender-endpoint/machine-groups)
- [Microsoft Defender RBAC permissions](/en-us/defender-xdr/manage-rbac)