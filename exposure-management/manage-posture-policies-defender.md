---
layout: Conceptual
title: Manage posture policies - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/manage-posture-policies-defender
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to manage posture policies in the Microsoft Defender portal, including policy types, permissions, policy effects, transition guidance, and limitations.
ms.topic: how-to
ms.date: 2026-10-28T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1030
ai-usage: ai-assisted
locale: en-us
document_id: e47b0a6e-d15a-6101-0669-ed72a6b30aa8
document_version_independent_id: e47b0a6e-d15a-6101-0669-ed72a6b30aa8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/manage-posture-policies-defender.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-posture-policies-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/manage-posture-policies-defender.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: fd196915-2f67-2734-add0-b3f3ff26da5b
---

# Manage posture policies - Microsoft Security Exposure Management | Microsoft Learn

Posture policies define which security posture recommendations are evaluated and the scope in which they apply. Organizations can configure policies across different environments to align recommendation evaluation with their business, compliance, and operational requirements.

Note

Posture Policies are currently available only for **Cloud resources**.

## Why use posture policies?

Posture policies help organizations tailor Microsoft's default security recommendations to match their specific security, compliance, and operational requirements. While the Microsoft baseline provides a strong starting point, organizations often need additional flexibility to define which security rules should be evaluated, customize rule parameters, or adjust recommendation coverage for different environments.

By using posture policies, security teams can apply stricter requirements to highly sensitive environments, add organization-specific or compliance-driven rules, and reduce unnecessary noise in lower-risk environments. This helps ensure that recommendations are aligned with business priorities, regulatory obligations, and the security posture expected for each environment, resulting in more relevant and actionable findings.

## Before you begin

### Verify that an environment is managed in Defender

Policies created in Defender apply only to environments managed in Defender. You can verify the management location in either of the following ways:

- From the recommendations experience, review the **Managed in** property and confirm that the value is **Defender**.
- From cloud environment management, open the cloud **Environment management** page and confirm that the applicable environment is managed in Defender.

[![Screenshot showing Defender portal in the Plans managed in column for an environment.](media/manage-posture-policies-defender/environment-management-defender.png)](media/manage-posture-policies-defender/environment-management-defender.png#lightbox)

If an environment is managed in Azure, you can connect the environment to Defender and continue managing posture policies through Defender or continue managing the applicable configuration in Azure.

### Plans

Posture policies are available only for environments that have an eligible Microsoft Defender plan enabled.

- Only environments with an active eligible plan can be selected as a policy scope.
- Environments without any enabled eligible plans aren't available for policy assignment.
- If no plans are enabled across the organization, the Recommendation Policies experience isn't available.

### Permissions

[Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac) controls access to recommendation policies:

| Role or permission | Access |
| --- | --- |
| Global Administrator or Security Administrator | Can view, create, edit, enable, disable, and delete policies across all existing and future scopes, including tenant-wide policies. |
| Core security settings (Manage) | Can create, edit, enable, disable, and delete policies for the scopes assigned to the user. Manage permission is required for every scope included in the policy. |
| Core security settings (Read) | Can view policies and their configuration for assigned scopes but can't change them. |

To delegate policy management, go to **System** &gt; **Permissions** &gt; **Microsoft Defender XDR** &gt; **Roles** in the Microsoft Defender portal and create or update a role with the required permission and scope.

[![Screenshot showing Core security settings permissions for posture policy management in Microsoft Defender unified RBAC.](media/manage-posture-policies-defender/posture-policy-permissions.png)](media/manage-posture-policies-defender/posture-policy-permissions.png#lightbox)

## Understand policy types

The Defender portal includes a Microsoft-managed baseline policy and supports custom recommendation policies.

| Policy type | Purpose | Supported management actions |
| --- | --- | --- |
| MDC Baseline Policy | Provides an out-of-the-box set of Microsoft-recommended security rules focused on improving an organization's security posture. | Enable or disable the policy and edit supported scope and parameters. The policy can't be deleted or renamed, and its rules and categories can't be changed. |
| Custom policy | Defines organization-specific security requirements by combining selected rules, categories, scope, and parameters. | View, edit, enable, disable, and delete. |

### MDC Baseline Policy

The MDC Baseline Policy is a Microsoft-managed policy that provides a recommended set of security posture rules based on Microsoft's security research, threat intelligence, and best practices. It is designed to help organizations strengthen their security posture by identifying and reducing common attack paths, misconfigurations, and exploitable exposures.

Unlike compliance-focused frameworks that are primarily designed to satisfy regulatory requirements, the MDC Baseline Policy focuses on improving security outcomes and reducing risk. It delivers immediate posture value with minimal configuration and serves as the recommended starting point for most organizations.

[![Screenshot showing the MDC security baseline policy details in the Microsoft Defender portal.](media/manage-posture-policies-defender/security-baseline-policy.png)](media/manage-posture-policies-defender/security-baseline-policy.png#lightbox)

Key characteristics of the MDC Baseline Policy:

- Microsoft manages and continuously updates the policy content to reflect evolving threats, security research, and best practices.
- The policy is Microsoft-managed and intentionally provides limited customization. Organizations can modify rule parameters, change the assignment scope, edit parameters of rules, and enable or disable the policy, but the underlying set of Microsoft-recommended security controls is maintained by Microsoft.
- The policy can't be deleted and can only be disabled when not required. Keeping the policy available ensures organizations can easily re-enable Microsoft's recommended security baseline without needing to recreate or reconfigure it.

### Default assignment

To help organizations realize security value immediately, the MDC Baseline Policy is assigned to **All connected environments** by default.

- Existing connected environments are automatically included in the policy scope.
- Newly connected environments are automatically assigned to the policy.
- Organizations can modify the assignment and restrict the policy to selected environments when needed.

## Create a custom policy

Go to **Exposure Management** &gt; **Policies**, and then select **Create policy**.

[![Screenshot of the cloud scope options when creating a posture policy in the Microsoft Defender portal.](media/manage-posture-policies-defender/create-posture-policy-details-scope.png)](media/manage-posture-policies-defender/create-posture-policy-details-scope.png#lightbox)

The creation process includes three main decisions:

| Creation section | What you define | Key guidance |
| --- | --- | --- |
| Details and scope | The policy name, description, and Defender-managed environments to which the policy applies. | Select only environments that should follow the same security requirements. Only Global Administrators and Security Administrators can create policies that apply to all connected environments. |
| Predefined rules and categories | Rules are individual security checks that generate recommendations. You can directly configure supported rule parameters, enable or disable individual rules, and tailor the policy to your organization's requirements. | Use predefined rules to select the security checks that are relevant to your organization's business, security, and compliance requirements. Configure supported rule parameters to align recommendations with internal policies, operational needs, and risk tolerance levels, while reducing unnecessary noise and focusing on the findings that matter most to your environment. |
| Additional categories | Categories provide an additional set of Microsoft-defined recommendations grouped around a common security outcome. Unlike predefined rules, categories can't be customized or configured. Organizations can only choose whether to include or exclude a category from the policy. Category selections are additive and don't affect the predefined rule selections. | Microsoft recommends using both predefined rules and categories. Predefined rules provide granular control and customization, while categories provide broader coverage. Categories complement predefined rules rather than replace them. |

[![Screenshot of the regulatory compliance framework filter during posture policy rule selection.](media/manage-posture-policies-defender/create-posture-policy-rules.png)](media/manage-posture-policies-defender/create-posture-policy-rules.png#lightbox)

After the policy is created, Microsoft Defender runs applicable security assessments. New or updated recommendations are generated when assets in the selected scope don't meet the policy requirements. Policy processing and recommendation updates aren't immediate.

## Compliance policies

Microsoft supports compliance-related recommendations and maps recommendations to common regulatory frameworks, such as HIPAA, PCI DSS, ISO 27001, and NIST. However, Recommendation Policies don't include out-of-the-box policies for specific compliance frameworks.

This approach helps keep policy management streamlined by avoiding a large set of predefined compliance policies that might not be relevant to your organization. Instead, organizations can create targeted compliance-focused policies by selecting recommendations mapped to the regulatory frameworks they follow. This provides the flexibility to build compliance policies tailored to specific requirements while reducing unnecessary complexity and administrative overhead.

To create a compliance-focused policy:

1. Create a new policy.
2. Assign the policy to the environments that are required to meet the selected compliance framework and regulatory requirements.
3. Filter rules by the desired regulatory framework.
4. Select all the rules.

For more information, see [Assign regulatory compliance standards](/en-us/azure/defender-for-cloud/assign-regulatory-compliance-standards).

## Rules management

Use Rule Management when you need to understand how a specific recommendation is configured and applied across your organization. This view simplifies administration by providing a single place to track rule assignments, understand policy relationships, and manage rule configurations without navigating through multiple policies.

[![Screenshot showing the Rules management page for posture policies in the Microsoft Defender portal.](media/manage-posture-policies-defender/posture-policy-rules-management.png)](media/manage-posture-policies-defender/posture-policy-rules-management.png#lightbox)

## Understand the effect of a policy

Posture policies determine which security checks are evaluated for selected assets. When an asset doesn't meet the requirements defined by an enabled policy, Microsoft Defender generates a recommendation to help address the identified security gap.

If multiple policies apply to the same asset, a recommendation is generated whenever the asset fails the requirements of at least one applicable policy. When policy evaluations differ, the most restrictive outcome takes precedence.

## Transition to Defender

Organizations can continue to manage posture policies and security standards from both the Azure portal and the Microsoft Defender portal during the transition to **Managed in Defender**.

Recommendations are evaluated across all applicable policy sources and surfaced consistently in both portals. This provides a single recommendation queue and prevents duplicate recommendations from being generated when the same security requirement is configured in multiple places.

[![Screenshot showing Azure security policies with an option to go to Microsoft Defender for additional policies.](media/manage-posture-policies-defender/azure-security-policies-go-to-defender.png)](media/manage-posture-policies-defender/azure-security-policies-go-to-defender.png#lightbox)

### Policy ownership

Policy ownership remains with the portal where the policy or standard was created:

- Security standards and policies created in Azure continue to be managed in Azure.
- Policies created in Defender are managed from the **Posture policies** page in Microsoft Defender.
- Policy definitions aren't synchronized or copied between Azure and Defender.
- Recommendations generated by Azure and Defender configurations are surfaced in both supported experiences.

### Managing recommendations

Use the **Policy source** information on a recommendation to:

- Understand whether the recommendation is driven by Azure, Defender, or both.
- Navigate to the appropriate policy management experience.
- Update, disable, or remove the policy configuration responsible for the recommendation.

### Best practice for existing environments

Microsoft recommends managing posture policies in Defender whenever possible and using Azure security policies only for scenarios that aren't currently supported in Defender, such as policies that require a Deny effect or [custom recommendations](/en-us/azure/defender-for-cloud/create-custom-recommendations).

To reduce operational overhead and avoid overlapping policy management, disable Azure security standards that are no longer required for environments managed through Defender.

For scenarios that require Azure-only capabilities, create dedicated Azure security standards containing only those controls. This approach enables organizations to centralize recommendation management in Defender while continuing to use Azure policies for capabilities that don't have an equivalent Defender experience.

### Best practice for new subscriptions

New Azure subscriptions inherit Azure security standards by default. When adopting Microsoft Defender as the primary posture management experience, review the Azure standards assigned to newly created subscriptions and disable any standards that you don't intend to manage from Azure.

As long as Azure standards remain enabled, they can continue to generate recommendations alongside Defender-managed policies. Recommendations are surfaced as a single recommendation experience, and the **Policy source** field can be used to identify whether a recommendation originates from an Azure security standard, a Defender posture policy, or both.

### Foundational CSPM

Microsoft Defender doesn't include a free Foundational CSPM plan. Instead, it provides a single [Defender CSPM](/en-us/azure/defender-for-cloud/concept-cloud-security-posture-management) plan, which is a paid offering and the recommended Microsoft experience for posture management.

Organizations that want to continue receiving posture recommendations in environments managed by Defender must enable Defender CSPM, even if they continue to manage policies and security standards from the Azure portal.

Organizations that previously relied on Azure Foundational CSPM must enable Defender CSPM to continue receiving posture recommendations, even if policy and security standard management remains in the Azure portal. Without Defender CSPM, posture recommendations aren't generated for environments managed in Defender.

## Limitations

The following limitations apply to posture policy management in the Microsoft Defender portal:

- Only Azure environments are supported.
- Existing Azure policies continue to be honored but aren't automatically migrated to the Defender portal.
- Custom recommendation creation isn't currently supported in Defender. [Custom recommendations](/en-us/azure/defender-for-cloud/create-custom-recommendations) can continue to be managed in Azure, and the resulting recommendations are visible in both Azure and Defender.
- Defender posture policies currently support Audit-based recommendation evaluation only. Policy effects such as Deny aren't supported in Defender and must continue to be managed through Azure Policy.
- Recommendation updates aren't immediate and require additional processing time. Microsoft continues to improve processing times across the posture management experience.

## Why use policy management in Microsoft Defender?

Azure continues to support its existing policy configuration capabilities, while Microsoft Defender provides a unified posture management experience across cloud, endpoint, identity, and other Defender-managed workloads. This enables security teams to manage posture requirements, recommendations, exposure insights, and related governance decisions from a single location.

Organizations can transition posture policy management to Microsoft Defender and benefit from the following:

- **Top-down policy management**: Define security requirements centrally and apply them consistently across the environments that require them.
- **Reduced administrative overhead**: Reusable policies reduce repetitive configuration and simplify posture management across environments.
- **Flexible security scopes**: Apply policies across Defender-managed environments without being limited to Azure resource hierarchy boundaries.
- **Microsoft-managed baseline**: Start with the MDC Baseline Policy, which focuses on improving security posture and reducing exposure, then add custom policies only where business, security, or compliance requirements differ.
- **Granular security permissions**: Use [Microsoft Defender unified RBAC](/en-us/defender-xdr/manage-rbac) to separate read and management permissions and delegate policy management to specific security teams.
- **Cross-workload governance**: Manage posture requirements through a common experience across cloud, endpoint, identity, and other supported Defender workloads.
- **Improved recommendation processing**: Policy and recommendation processing times are optimized for the Defender experience and continue to improve.