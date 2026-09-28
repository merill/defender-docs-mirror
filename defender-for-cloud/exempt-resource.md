---
layout: Conceptual
title: Exempt resources from recommendations - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/exempt-resource
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
description: Create exemption rules to remove resources or recommendations from secure score impact in Microsoft Defender for Cloud.
ms.topic: how-to
ms.custom: ignite-2023, msecd-doc-authoring-1013
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 92ccd18f-5671-dfad-71f1-5e3500bd6081
document_version_independent_id: e859b88d-0fe0-433b-1aaa-7cc66edc0edc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/exempt-resource.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/exempt-resource
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/exempt-resource.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: be5f7b8b-2603-aaf3-4f2f-6eed8bc412c9
---

# Exempt resources from recommendations - Microsoft Defender for Cloud | Microsoft Learn

When you investigate security recommendations in Microsoft Defender for Cloud, you review the list of affected resources. Occasionally, you find a resource that shouldn't be in the list, or you find a recommendation that appears in a scope where it doesn't belong. For example, Defender for Cloud might not track a remediation process, or a recommendation might not apply to a specific subscription. Your organization might decide to accept the risks related to the specific resource or recommendation.

In such cases, create an exemption rule to:

- **Exempt a resource** to remove it from the list of unhealthy resources and from secure score impact. Defender for Cloud lists the resource as **Not applicable** and shows the reason as **Exempted** with the justification that you select.
- **Exempt a subscription or management group** to prevent the recommendation from affecting your secure score or appearing for that scope. The exemption applies to existing resources and to resources that you create later. Defender for Cloud marks the recommendation with the justification that you select for that scope.

For each scope, create an exemption rule to:

- Mark a specific **recommendation** as **Mitigated** or **Risk accepted** for one or more subscriptions, or for a management group.
- Mark **one or more resources** as **Mitigated** or **Risk accepted** for a specific recommendation.

Resource exemption is limited to 5,000 resources per subscription. If you add more than 5,000 exemptions per subscription, you might experience load issues on the exemption page.

## Prerequisites

Defender for Cloud exemptions rely on the [Microsoft Cloud Security Benchmark (MCSB)](/en-us/security/benchmark/azure/introduction) initiative. MCSB must be assigned on the subscription before you create exemptions.

Important

Without MCSB assigned:

- Some portal features might not work as expected.
- Resources might not appear in compliance views.
- Exemption options might occasionally be unavailable.

You can create exemptions for recommendations that belong to the default MCSB initiative or to other built-in regulatory standards. Some recommendations in MCSB don't support exemptions. You can find a list of these recommendations in [the exemptions FAQ](faq-general).

*Permissions*:

To create exemptions, you need the following permissions:

- **Owner** or **Security Admin** on the scope where you create the exemption.
- To create a rule, you need permissions to edit policies in Azure Policy. For details, see [Azure RBAC permissions in Azure Policy](/en-us/azure/governance/policy/overview#azure-rbac-permissions-in-azure-policy).
- You must have exemption permission on all initiative assignments at the target scope. If multiple initiatives contain a recommendation, you must create the exemption with permissions across all of them. A missing permission on even one initiative can cause the exemption to fail.

You need the following role-based access control (RBAC) actions:

| Action | Description |
| --- | --- |
| `Microsoft.Authorization/policyExemptions/write` | Create an exemption |
| `Microsoft.Authorization/policyExemptions/delete` | Delete an exemption |
| `Microsoft.Authorization/policyExemptions/read` | View an exemption |
| `Microsoft.Authorization/policyAssignments/exempt/action` | Perform an exemption operation on a linked scope |

Note

If any of these actions are missing, the **Exempt** button might be hidden. Custom roles offer limited support for exemption operations.

To manage exemptions, use one of the following built-in roles:

- **Security Admin** (recommended)
- **Owner**
- **Contributor** (at the subscription level)
- **Resource Policy Contributor**

- Subscription-level permissions don't inherit upward to management groups. If the policy assignment is at the management group level, you need the role assigned at that level.
- To manage exemptions for specific resources, you need the required RBAC actions at the resource or resource group level. Subscription-scoped role assignments might not provide sufficient access to create or delete exemptions on individual resources. Verify that your role assignment covers the scope of the resource you want to exempt.
- When you create an exemption at the management group level, ensure the *Microsoft Azure Security Resource Provider* has the necessary permissions by assigning it the **Reader** role on that management group. Grant this role the same way that you grant user permissions.

*Limitations*:

- You don't create exemptions for custom recommendations.
- Preview recommendations might not support exemptions. Check whether the recommendation shows a **Preview** tag.
- If you disable a recommendation, you also exempt all of its subrecommendations.
- Kusto Query Language (KQL)-based recommendations use standard assignments and don't use Azure Policy exemption events in the Activity Logs. To determine whether a recommendation is KQL-based or policy-based, open the recommendation in the portal and check the **Assessment key** field. KQL-based recommendations show a standard assessment key format and don't have an associated Azure Policy definition link. Policy-based recommendations display a direct link to the underlying policy definition.
- When you create an exemption from the Defender for Cloud portal, Defender for Cloud identifies all initiatives that contain the recommendation and creates the exemption across all of them automatically. If you create the exemption through the Azure Policy API instead, you must create a separate exemption for each initiative manually. For more information, see [Exemptions FAQ](faq-general).
- When you assign a new initiative that contains a recommendation with an existing exemption, the exemption doesn't carry over to the new initiative. Create a new exemption for the recommendation under the newly assigned initiative.

Tip

If you run into issues after you create an exemption, see [Review and manage recommendation exemptions](review-exemptions) for guidance on:

- [Resolving unhealthy status](review-exemptions#resolve-an-exemption-that-doesnt-update-the-recommendation-status)
- [Permission errors at management group level](review-exemptions#resolve-permission-errors-at-management-group-level)
- [Missing exemptions in the portal](review-exemptions#find-exemptions-that-arent-visible-in-the-portal)
- [Deleting exemptions](review-exemptions#delete-an-exemption)
- [Cleaning up duplicate exemptions](review-exemptions#resolve-duplicate-or-conflicting-exemptions)

## Define an exemption

We recommend creating exemptions in the Defender for Cloud portal. Exemptions created through the Azure Policy API might not fully integrate with Defender for Cloud. They can cause unexpected results, such as exemptions that don't propagate across all relevant initiatives. If you need to use the API, see [Azure Policy exemption structure](/en-us/azure/governance/policy/concepts/exemption-structure).

To create an exemption rule:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Defender for Cloud** &gt; **Recommendations**.
3. Select a recommendation.
4. Select **Exempt**.

    [![Create an exemption rule for a recommendation to be exempted from a subscription or management group.](media/exempt-resource/exempting-recommendation.png)](media/exempt-resource/exempting-recommendation.png#lightbox)
5. Select the scope for the exemption.

    - If you select a management group, Defender for Cloud exempts the recommendation from all subscriptions in that group.
    - If you create this rule to exempt one or more resources from the recommendation, choose **Selected resources** and select the relevant resources from the list.
6. Enter a name.
7. (Optional) Set an expiration date.
8. Select the category for the exemption:

    - **Resolved through third-party service (mitigated)** – if you use a non-Microsoft service for remediation that Defender for Cloud doesn't track.

    Note

    When you exempt a resource as mitigated, it counts as healthy. You don't gain points for the remediation, but Defender for Cloud doesn't deduct points for leaving it unhealthy, so exempted resources don't lower your score.

    - **Risk accepted (waiver)** – if you decide to accept the risk of not mitigating this recommendation.
9. Enter a description.
10. Select **Create**.

    [![Steps to create an exemption rule to exempt a recommendation from your subscription or management group.](media/exempt-resource/defining-recommendation-exemption.png)](media/exempt-resource/defining-recommendation-exemption.png#lightbox)

## After you create the exemption

An exemption can take up to 24 hours to take effect. Defender for Cloud evaluates resources every 12 to 24 hours. After the exemption takes effect:

- The recommendation or resources don't affect your secure score.
- If you exempt specific resources, Defender for Cloud lists them in the **Not applicable** tab of the recommendation details page.
- If you exempt a recommendation, Defender for Cloud hides it by default on the **Recommendations** page. This happens because the default **Recommendation status** filter excludes **Not applicable** recommendations. The same behavior occurs if you exempt all recommendations in a security control.

### Understand how the exemption type affects the recommendation status

The exemption type that you select determines how the exemption affects the recommendation and secure score:

- **Mitigated** exemptions: Exempt resources count as healthy. Secure score increases.
- **Waiver** exemptions: Exempt resources are excluded from the secure score calculation. Resources don't count toward secure score but might still appear in recommendations.

Note

Preview recommendations have no impact on secure score regardless of exemption status.

### Verify that the exemption is working

If the recommendation still shows resources as unhealthy after 24 hours, see [Resolve an exemption that doesn't update the recommendation status](review-exemptions#resolve-an-exemption-that-doesnt-update-the-recommendation-status) for detailed steps.