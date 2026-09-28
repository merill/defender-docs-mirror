---
layout: Conceptual
title: Configure Unified RBAC for Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/configure-unified-rbac-defender-office-365
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Step-by-step guide to configure and activate Microsoft Defender unified role-based access control (Unified RBAC) for Microsoft Defender for Office 365, including role creation, persona templates, and migration from legacy roles.
ms.service: defender-office-365
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-07-10T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 21052500-b24a-9459-d229-6c32e059bdcb
document_version_independent_id: 21052500-b24a-9459-d229-6c32e059bdcb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/configure-unified-rbac-defender-office-365.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/configure-unified-rbac-defender-office-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/configure-unified-rbac-defender-office-365.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: d308ca6c-5c6d-9414-f6c6-f98ada99218c
---

# Configure Unified RBAC for Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Microsoft Defender unified role-based access control (RBAC) provides a single permission model for all Defender workloads, including Microsoft Defender for Office 365. Unified RBAC replaces legacy Email & collaboration roles with granular permissions, custom role design, and precise control over investigation and remediation access.

Important

Starting July 2026, Unified RBAC is the default permission model for new Microsoft Defender for Office 365 Plan 2 organizations. Existing organizations can manually activate Unified RBAC at any time. For more information, see [MC1246006](https://admin.microsoft.com/Adminportal/Home#/MessageCenter/:/messages/MC1246006).

## What you need

- [Microsoft Defender for Office 365 Plan 2](../mdo-about#defender-for-office-365-plan-2-capabilities).
- At least the Security Administrator role in Microsoft Entra ID (to activate Unified RBAC).
- About 20 to 30 minutes to complete the configuration.

## Understand the scope

Before you start, understand what Unified RBAC controls and what it doesn't:

| Area | Controlled by |
| --- | --- |
| Microsoft Defender portal access | Unified RBAC |
| PowerShell access | [Exchange Online role groups](/en-us/exchange/permissions-exo/permissions-exo) |
| Global admin capabilities | Microsoft Entra roles |
| Exchange admin center | Exchange Online role groups |
| Microsoft Purview portal | Purview RBAC |

Note

Microsoft Entra roles (for example, Security Administrator, Security Reader) always grant access regardless of Unified RBAC activation.

## Before and after activation

The following table summarizes what changes and what stays the same when you activate Unified RBAC for Defender for Office 365:

| Before activation | After activation |
| --- | --- |
| Legacy [Email & collaboration roles](../scc-permissions) control Defender portal access | Legacy roles stop controlling Defender portal access |
| Exchange Online roles control Defender portal access | Unified RBAC controls Defender portal access |
| Microsoft Entra roles work | No change |
| Exchange Online roles control PowerShell | No change |
| Exchange admin center access works | No change |
| Microsoft Purview admin center access works | No change |

Caution

Activation takes effect after a few minutes. The ability to deactivate Unified RBAC will be removed in a future update.

## Step 1: Evaluate Microsoft Entra role mappings

If your organization already uses Microsoft Entra roles, evaluate whether those roles provide sufficient access before you create custom roles:

| Microsoft Entra role | Defender for Office 365 access level |
| --- | --- |
| Security Administrator | Full access (policies, response, metadata, quarantine) |
| Security Operator | Policy management, response actions, metadata read |
| Security Reader | Read access, metadata read, response actions |
| Global Reader | Read access, metadata read, response actions |

For the complete Microsoft Entra role-to-Unified RBAC permission mapping, see [Microsoft Entra global roles access](/en-us/defender-xdr/compare-rbac-roles#microsoft-entra-global-roles-access).

Tip

If Microsoft Entra roles provide the access you need, you can skip creating custom roles and go directly to Step 4: Activate Unified RBAC.

## Step 2: Create custom roles

If you need more granular access control, create custom roles in the Defender portal:

1. On the Microsoft Defender XDR **Permissions and roles** page in the Defender portal at https://security.microsoft.com/mtp_roles, select ![](../media/defender-portal-icon-create.png)**Create custom role**.
2. The custom role wizard opens. On the **Set up the basics** page, configure the following information:

    - **Role name**: Enter a unique, descriptive role name (for example, *MDO SOC Analyst*).
    - **Description**: Enter an optional description.

    When you're finished on the **Set up the basics** page, select **Next**.
3. On the **Choose permissions** page, select the permissions for the role. For guidance, see the persona templates section.

    1. Select an available permission group:

        - **Security operations**
        - **Security posture**
        - **Authorization and settings**
        - **Data operations**
        - **AI code security**
    2. In the permission group details flyout that opens, select the permissions. To clear your selections and start over in the flyout, select ![](../media/defender-portal-icon-remove.png)**Clear all permissions**.

        The following screenshot shows the details flyout for the **Security operations** permission group:

        [![Screenshot of the details flyout of the Security operations permission group showing the available permissions and options.](../media/configure-unified-rbac-defender-office-365-security-operations-details-flyout.png)](../media/configure-unified-rbac-defender-office-365-security-operations-details-flyout.png#lightbox)

        When you're finished selecting permissions in the permission group details flyout, select **Apply**.
    3. Back on the **Choose permissions** page, repeat the previous steps as many times as necessary.

    When you're finished on the **Choose permissions** page, select **Next**.
4. On the **Assign users and data sources** page, select **Create assignment** or ![](../media/defender-portal-icon-create.png)**Add assignment** to assign users or groups to the role.

    In the **Add assignment** flyout that opens, configure the following options:

    - **Assignment name**: Enter a unique, descriptive name.
    - **Employees**: Start typing a user or group name in the box to filter the list, or click in the empty box to see the full list. Select a user or group from the list, and it appears in the box. Repeat this step as many times as necessary.
    - **Data sources**: Verify that **Microsoft Defender for Office 365** is selected.

        Tip

        Depending on your Microsoft 365 subscription, other workloads might also be available and selected (for example, **Microsoft Defender for Endpoint**).
    - **Include future data sources automatically**: This option is selected by default.

    When you're finished on the **Assign users and data sources** page, select **Next**.
5. On the **Review and finish** page, review the settings. You can select **Edit** in each section to modify the settings within the section. Or you can select **Back** or the specific page in the wizard.

    When you're finished on the **Review and finish** page, select **Submit**.
6. After the role is created, select **Done**.

For more information, see [Create custom roles in Microsoft Defender unified RBAC](/en-us/defender-xdr/create-custom-rbac-roles).

### Persona templates

Use the following templates as starting points for common security roles. Adjust permissions based on your organization's needs.

#### Defender for Office 365 Security Administrator (full access)

Full control over all Defender for Office 365 settings, investigations, and response actions.

| Permission group | Permission | Level |
| --- | --- | --- |
| Authorization and settings | Core security settings | Manage |
| Authorization and settings | Detection tuning | Manage |
| Authorization and settings | System settings | Manage |
| Security operations | Alerts | Manage |
| Security operations | Response | Manage |
| Security operations | Email & collaboration quarantine | Manage |
| Security operations | Email & collaboration advanced actions | Manage |
| Raw data (Email & collaboration) | Email & collaboration metadata | Read |
| Raw data (Email & collaboration) | Email & collaboration content | Read |

#### Security Analyst (investigate and remediate)

Investigate threats and take response actions without policy management access.

| Permission | Level |
| --- | --- |
| Alerts | Manage |
| Response | Manage |
| Email & collaboration quarantine | Manage |
| Email & collaboration advanced actions | Manage |
| Email & collaboration metadata | Read |
| Email & collaboration content | Read |

#### SOC Tier 1 Operator (triage only)

Triage alerts and manage quarantine without remediation or content access.

| Permission | Level |
| --- | --- |
| Alerts | Manage |
| Email & collaboration quarantine | Manage |
| Email & collaboration metadata | Read |

#### Compliance/Audit Reader (read-only)

View policies, settings, and email metadata without the ability to take actions.

| Permission | Level |
| --- | --- |
| Core security settings | Read |
| System settings | Read |
| Security data basics | Read |
| Email & collaboration metadata | Read |

#### Tenant Allow/Block List Manager

Manage allow and block entries without broader policy or investigation access.

| Permission | Level |
| --- | --- |
| Core security settings | Read |
| Detection tuning | Manage |
| Security data basics | Read |

### SOC 3-tier model

For organizations with tiered security operations center (SOC) teams, use the following model and deployment steps:

| Tier | Role name | Responsibility | Permissions |
| --- | --- | --- | --- |
| Tier 1 | MDO SOC Tier 1 | Triage: alerts and quarantine | Alerts (manage), Quarantine (manage), Metadata (read) |
| Tier 2 | MDO SOC Tier 2 | Investigation and remediation | Tier 1 permissions plus Response (manage), Content (read) |
| Tier 3 | MDO SOC Tier 3 | Policies and tuning | Tier 2 permissions plus Core settings (manage), Detection tuning (manage) |

1. Create Microsoft Entra security groups for each tier (for example, *MDO-SOC-Tier1*, *MDO-SOC-Tier2*, *MDO-SOC-Tier3*).
2. Create the three custom roles with the permissions shown in the table.
3. Assign the corresponding security group to each role.

## Step 3: Assign roles

1. On the **Roles** page in the Defender portal, select the role, and then select **Edit**.
2. Go to the **Assignments** tab.
3. Add users, groups, or select all users as needed.
4. Optionally, scope the role to specific workloads (for example, Defender for Office 365 only).
5. Save the assignment.

Tip

Use Microsoft Entra security groups for role assignments instead of individual user accounts. Groups simplify ongoing user management and support Privileged Identity Management (PIM).

## Step 4: Activate Unified RBAC

Warning

Before you activate Unified RBAC, verify that you created all required custom roles and assignments. Activation takes effect after a few minutes.

1. On the Microsoft Defender XDR **Permissions and roles** page in the Defender portal at https://security.microsoft.com/mtp_roles, do one of the following steps:

    - Select **Activate workloads** in the banner.
    - Select ![](../media/defender-portal-icon-gear.png)**Workload settings** at the top of the page.
2. In the **Email & collaboration** section of the **Activate unified role-based access control** flyout or page that opens, slide the **Defender for Office 365** toggle to ![](../media/scc-toggle-on.png)**Active**.

    Tip

    Sliding the **Exchange Online permissions** toggle to **Active** also brings Exchange Online permissions under Unified RBAC.
3. Select **Activate** on the confirmation message.

Tip

Activation covers both **Defender for Office 365** permissions and **Exchange Online** permissions. Toggle both workloads to Active so that security data and response actions that depend on Exchange Online behave consistently in the Defender portal.

For more information, see [Activate Microsoft Defender unified RBAC](/en-us/defender-xdr/activate-defender-rbac).

## Step 5: Verify access

After activation, verify that users have the correct access:

| Persona | Can do | Can't do |
| --- | --- | --- |
| Security Admin | Edit policies, manage all settings | N/A |
| Security Analyst | Remediate emails, manage incidents | Modify policies |
| SOC Tier 1 | View alerts, manage quarantine | Remediate emails |
| Compliance Reader | View policies and reports | Take any actions |
| Tenant Allow/Block List Manager | Manage Tenant Allow/Block List entries | Access policies |

Tip

Have a user from each role sign in to the Defender portal and verify that they can perform expected tasks and are blocked from unauthorized actions.

## Step 6: Understand features outside Unified RBAC scope

Unified RBAC doesn't control the following features, which require separate role assignments:

| Feature | Permission model |
| --- | --- |
| Attack Simulation Training | Microsoft Entra roles |
| Message trace | Exchange Online roles |
| Mail flow reports | Exchange Online roles |
| Mail flow connectors | Exchange Online roles |
| PowerShell cmdlets | Exchange Online roles |

## Step 7: Migrate from legacy roles (existing organizations)

For existing organizations that already use **Email & collaboration** roles, choose between the import and rebuild approaches to migrate your roles. The following table can help you decide:

| Approach | Best for |
| --- | --- |
| Import | Fast migration with minimal disruption; roles that already align well with your needs |
| Rebuild | Simplification; SOC alignment; organizations with outdated or overly complex role structures |

### Option A: Import existing roles

Use the import feature for a fast migration that preserves your current role structure. You select the product to import from (for example, **Email & collaboration**), choose specific roles, and submit. For detailed steps, see [Import existing roles to Microsoft Defender unified RBAC](/en-us/defender-xdr/import-rbac-roles).

### Option B: Rebuild roles

Use the rebuild approach to simplify and align roles with SOC personas:

1. Audit your current roles and their members.
2. Map roles to the persona templates in this article.
3. Create new custom roles.
4. Assign users and groups.

## Troubleshooting

The following table lists common issues after Unified RBAC activation and how to resolve them:

| Issue | Cause | Fix |
| --- | --- | --- |
| User can't access Threat Explorer | Missing **Email & collaboration metadata (read)** | Add the permission to the user's role |
| User can't preview email content | Missing **Email & collaboration content (read)** | Add the permission to the user's role |
| User can't edit policies | Missing **Core security settings (manage)** | Add the permission to the user's role |
| User lost access after activation | Legacy roles weren't recreated in Unified RBAC | Import or rebuild the missing roles |
| Permission changes are delayed | Normal propagation delay | Wait about 5 minutes |
| PowerShell cmdlets fail | PowerShell isn't controlled by Unified RBAC | Assign the appropriate [Exchange Online role groups](/en-us/exchange/permissions-exo/permissions-exo) |
| User can't approve remediation actions | Missing **Response (manage)** | Add the permission to the user's role |
| User can't manage Tenant Allow/Block List | Missing **Detection tuning (manage)** | Add the permission to the user's role |