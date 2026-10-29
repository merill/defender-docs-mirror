---
layout: Conceptual
title: Manage exemptions - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/manage-exemptions-defender
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to create and manage recommendation exemptions in the Microsoft Defender portal, including scope, permissions, lifecycle management, transition guidance, and limitations.
ms.topic: how-to
ms.date: 2026-10-28T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1030
ai-usage: ai-assisted
locale: en-us
document_id: 246364c6-4046-4ca7-fdfc-4c25f534aa79
document_version_independent_id: 246364c6-4046-4ca7-fdfc-4c25f534aa79
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/manage-exemptions-defender.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-exemptions-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/manage-exemptions-defender.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 6c6acca0-4487-4dfc-74b9-c22fb67d2fe4
---

# Manage exemptions - Microsoft Security Exposure Management | Microsoft Learn

Exemptions help security teams focus on the risks that require action while maintaining a governed record of findings that don't require remediation. Use an exemption when a finding has been reviewed and determined to be a false positive, covered by another control, temporarily deferred, or accepted as risk. Each exemption records its scope, matching conditions, justification, and review period, helping your organization reduce operational noise without losing visibility or accountability.

Note

Exemptions are currently available only for **Cloud resources**.

For **Devices**, use the **Exception options** directly from the recommendation experience.

For **SaaS Apps, Identities, and Data**, use **Edit Status & Action Plan** on the recommendation as the alternative way to manage exemptions.

[![Screenshot showing the Exemptions tab on the Policies page in the Microsoft Defender portal.](media/manage-exemptions-defender/manage-exemptions.png)](media/manage-exemptions-defender/manage-exemptions.png#lightbox)

## Why use exemptions?

Exemptions provide a structured alternative to informally suppressing a security finding. They help organizations:

- Focus remediation resources on security findings that require action.
- Apply a documented risk decision consistently across the relevant scope.
- Reduce repetitive work by managing exceptions through centralized rules.
- Record the justification and supporting context needed for governance, audit, and compliance.
- Reassess accepted risks through expiration dates and lifecycle review.
- Preserve the security context of exempted findings in investigation and attack-path experiences.

## Use cases

Create an exemption after a finding has been generated and reviewed, and your organization determines that remediation is not currently required. Common scenarios include:

- The finding is a false positive.
- The organization reviewed and accepted the risk.
- A third-party control addresses the risk.
- An alternative mitigation is already in place.
- Remediation is deferred for a documented business or technical reason.

## Remove a rule or create an exemption?

Both recommendation policies and exemptions allow you to control recommendation behavior, but they serve different governance purposes. Use a policy change when a recommendation should not be evaluated for a specific scope. Use an exemption when the recommendation remains valid, but remediation is temporarily not required and should be tracked for governance, audit, or compliance purposes.

| Action | What it does | Choose it when |
| --- | --- | --- |
| Remove the rule from a policy | Stops the rule from generating recommendations and findings for the selected policy scope. Assets within that scope will no longer be evaluated against the rule. | The recommendation is not relevant for the selected scope and should never apply there. This is a long-term policy decision that defines which security controls should be evaluated. Learn more in [Manage posture policies](manage-posture-policies-defender). |
| Create an exemption | Keeps the rule active and continues evaluating the finding, but marks matching findings as **Exempted** for the approved scope and review period. | The finding is valid, but remediation is temporarily postponed or accepted as an exception. Exemption preserves visibility, justification, ownership, and review tracking for governance, audit, and compliance needs. |

## Before you begin

### Verify that an environment is managed in Defender

Exemptions created in Defender apply only to assets that belong to environments managed in Defender. You can verify the management location in either of the following ways:

- From the recommendations experience, review the **Managed in** property and confirm that the value is **Defender**.
- From cloud environment management, open the cloud **Environment management** page and confirm that the applicable environment is managed in Defender.

[![Screenshot showing Defender portal in the Plans managed in column for an environment.](media/manage-exemptions-defender/environment-management-defender.png)](media/manage-exemptions-defender/environment-management-defender.png#lightbox)

If a finding affects assets managed in Azure, you have two options:

- Connect the environment to Defender and continue managing exemptions through Defender.
- Create the exemption in Azure. For more information, see [Exempt resources from recommendations](/en-us/azure/defender-for-cloud/exempt-resource).

### Permissions

[Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac) controls access to exemptions:

| Role or permission | Access |
| --- | --- |
| Global Administrator or Security Administrator | Can view, create, edit, and delete exemptions across all existing and future scopes, including tenant-wide exemptions. |
| Exposure Management (Manage) | Can create, edit, and delete exemptions for the scopes assigned to the user. Manage permission is required for every scope included in the rule. |
| Exposure Management (Read) | Can view exemptions for assigned scopes but can't create, edit, or delete them. |

To delegate exemption management, go to **System** &gt; **Permissions** &gt; **Microsoft Defender XDR** &gt; **Roles** in the Microsoft Defender portal and create or update a role with the required permission and scope.

[![Screenshot showing Security posture permissions for exemption management in Microsoft Defender unified RBAC.](media/manage-exemptions-defender/exemption-permissions.png)](media/manage-exemptions-defender/exemption-permissions.png#lightbox)

## Create an exemption

Go to **Exposure Management** &gt; **Policies** &gt; **Exemption**, and then select **Create Exemption**. The creation process includes four decisions:

| Creation section | What you define | Key guidance |
| --- | --- | --- |
| Details and scope | The exemption name and the environments or assets to which the exemption applies. | Use the narrowest scope possible to represent the approved risk decision. Only Defender-managed environments and assets can be selected. Only Global Administrators and Security Administrators can create exemptions that apply to **All connected environments**. |
| Conditions | The findings that the exemption applies to, such as specific recommendations, recommendation categories, or risk criteria. | Carefully review whether the condition is static or dynamic. Dynamic conditions can automatically apply to future findings that match the defined criteria, for example, all recommendations with a **Low** risk level. |
| Justification and duration | The business justification, supporting evidence, and exemption duration. | Document the reason for accepting the risk, any compensating controls, and relevant evidence. Use a time-bound exemption with a defined review or expiration date. |
| Review and create | The complete exemption configuration before submission. | Verify the selected scope and affected findings to ensure the exemption isn't broader than the approved business decision. |

After the exemption is submitted, Microsoft Defender processes the exemption and updates matching findings. Changes to finding status, exposure calculations, and related posture metrics might not be reflected immediately.

[![Screenshot showing the Name and scope step when creating an exemption in the Microsoft Defender portal.](media/manage-exemptions-defender/create-exemption-name-scope.png)](media/manage-exemptions-defender/create-exemption-name-scope.png#lightbox)

## Create an exemption from a recommendation

You can also create an exemption directly from a recommendation. When launched from a recommendation, Defender automatically prepopulates the exemption conditions based on the selected recommendation to reduce configuration effort and ensure the exemption targets the intended finding:

[![Screenshot of the Create exemption and Manage in Azure portal actions for a security recommendation.](media/manage-exemptions-defender/create-exemption-from-recommendation.png)](media/manage-exemptions-defender/create-exemption-from-recommendation.png#lightbox)

### What is prepopulated?

- The exemption condition is automatically set to **By recommendation** and is based on the recommendation from which the exemption was created. This condition can't be changed during the creation flow.
- The scope is automatically populated with the assets selected when the exemption was created. You can further refine, narrow, or expand the scope as needed before submitting the exemption.

If the selection includes both Defender-managed and Azure-managed assets, the Defender exemption applies only to the supported Defender-managed assets. Manage the remaining assets in Azure or move the relevant environment to Defender management.

Tip

If your goal is to exempt all assets that currently have a specific recommendation, switch to the **By recommendation title** view before creating the exemption. This makes it easier to review all impacted assets and apply a consistent exemption decision across the entire recommendation set.

## Manage exemption lifecycle

Use the **Exemption rules** page to review the organization's exemption decisions and manage their lifecycle.

- Edit a rule when its scope, matching conditions, justification, owner, or review period changes.
- Delete a rule when the exception is no longer valid and matching findings should return to active remediation tracking.
- Review expiring rules before the approved risk period ends.
- Review expired rules as historical evidence of previous decisions and determine whether a new assessment is required.

Note

If multiple exemptions apply to the same recommendation, the recommendation remains exempted until the last active exemption expires or is removed, regardless of whether the exemption was created in Azure or in Microsoft Defender.

When an exemption is deleted or reaches its expiration date, Microsoft Defender automatically re-evaluates the affected findings. Any findings that still require remediation return to an **Active** state and once again contribute to posture and risk calculations. Findings that are no longer applicable remain unaffected.

## Understand the effect of an exemption

When an exemption is active, matching findings are marked as **Exempted**. The exemption changes how the finding is treated, but it doesn't remove the finding, its supporting evidence, or its relationship to other security signals.

Exempted findings remain available throughout Microsoft Defender investigation and drill-down experiences. Depending on the current filters, exempted findings might be hidden by default. To review them, update the status filter to include **Exempted** findings.

### Score impact

Exempted findings are excluded from the applicable security score calculations while the exemption remains active. The impact on the score depends on the exemption scope and the product experience.

### Attack paths

Exempting a recommendation doesn't remove it from associated attack paths. Microsoft Defender continues to include the recommendation in attack path analysis and clearly identifies it as **Exempted**. This helps security teams understand the potential impact of the accepted risk, maintain visibility into how the recommendation contributes to overall exposure, and reassess the exemption if the security posture or business requirements change.

## Existing Azure exemptions and the transition to Defender

This section is primarily relevant for organizations that historically managed recommendations and exemptions in Azure and are now transitioning their environments to be **Managed in Defender**. During this transition, Microsoft preserves existing Azure exemption configurations while establishing Defender as the central location for managing new exemption decisions.

### How exemption ownership works

Microsoft Defender and Azure can coexist during the transition period. While exemption rules remain owned by the portal where they were originally created, recommendation status remains consistent across experiences.

- Exemption rules created in Azure continue to be managed in Azure.
- Exemption rules created in Defender are managed from the **Exemption rules** page in Defender.
- Exemption rule definitions aren't synchronized or copied between Azure and Defender.
- Both Azure and Defender exemptions affect the corresponding recommendations.
- Recommendation status and exemption state remain consistent regardless of which portal owns the exemption rule.

### Existing Azure exemptions

When an environment becomes **Managed in Defender**, Microsoft continues to honor exemption rules that were previously created in Azure.

- Existing Azure exemptions continue to influence recommendation status and posture calculations.
- Security teams can continue to edit or remove these exemptions in Azure.
- These Azure-created exemptions don't appear as manageable exemption rules in Defender.

This approach allows organizations to move to Defender without disrupting existing risk-acceptance decisions or requiring immediate migration of historical exemption rules.

### Creating new exemptions

After an environment becomes **Managed in Defender**, new exemptions for that scope must be created in Defender. New Azure exemptions can't be created for those scopes through the supported portal experience.

This ownership model gives security teams centralized control over new exemption decisions while preserving existing Azure configurations. It also prevents teams from creating new, competing rules for the same Defender-managed scope in different portals.

## Limitations

The following limitations apply to exemption management in the Microsoft Defender portal:

- Existing Azure exemptions continue to be honored after an environment is managed in Defender, but they aren't automatically migrated to the Defender portal.
- Processing, status updates, score recalculation, and cross-portal status propagation aren't immediate and require additional processing time.

## Why use exemption management in Microsoft Defender?

Organizations that choose to manage their cloud posture in Microsoft Defender can benefit from a centralized exemption management experience integrated directly into the entire exposure management workflow. Azure continues to support exemption management, while Defender offers a unified experience for organizations looking to manage security posture across all workloads and related decisions from a single location.

- **Flexible scopes**: Defender enables organizations to create exemptions across supported environments and assets, providing more flexibility in scope selection than traditional Azure hierarchy-based scoping.
- **Reduced administrative overhead**: Centralized and reusable exemption rules help reduce the number of exemptions that need to be created and maintained across multiple Azure subscriptions, management groups, and scopes.
- **Granular security permissions**: Microsoft Defender XDR unified RBAC enables organizations to separate read and manage permissions and delegate exemption management to specific security teams without relying solely on Azure administrative roles.
- **Lifecycle governance by design**: While Azure also supports exemption management, Defender provides a more security-focused governance experience. Exemptions include review periods and mandatory expiration dates, making temporary risk-acceptance decisions easier to track, review, and validate during audits and compliance assessments. Security teams can easily identify exemptions that are approaching expiration, review expired exemptions, and periodically reassess accepted risks.
- **Faster exemption processing**: Exemptions created in Defender are typically reflected in recommendation status, score calculations, and related experiences faster than equivalent exemptions in Azure. Microsoft continues to improve processing efficiency to further reduce the time required for exemption changes to take effect.