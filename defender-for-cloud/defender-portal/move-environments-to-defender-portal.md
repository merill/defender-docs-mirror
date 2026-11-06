---
layout: Conceptual
title: Move Azure environments to full management in the Defender portal - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-portal/move-environments-to-defender-portal
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
description: Transfer Azure environments to Defender portal plan management, move remaining management capabilities, and track progress on the environments page.
ms.topic: how-to
ms.date: 2026-10-29T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5c5a3fc9-9727-48b2-79a1-40d7e37f0cf0
document_version_independent_id: 1635baa9-96ad-0637-8d4b-acb70c4ae584
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-portal/move-environments-to-defender-portal.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: ../toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-portal/move-environments-to-defender-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-portal/move-environments-to-defender-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 1298f79f-b75f-e022-f73b-291f91ab043f
---

# Move Azure environments to full management in the Defender portal - Microsoft Defender for Cloud | Microsoft Learn

Important

This feature is in preview. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Transition your organization's cloud security management from the Azure portal to the Microsoft Defender portal at your own pace, moving environments in stages or directly to full management. During the transition, some environments can be managed in Defender while others remain managed in Azure. Once an environment moves to full management in Defender, Defender becomes its authoritative management portal for all supported management operations, including plan enablement, settings, and policies. Use the environments page to see where each environment is managed and track progress toward full management.

## Take control of environment management in Defender

Taking control of full management is an explicit, one-time decision that makes the Microsoft Defender portal the authoritative management portal for the environments you select. All supported management operations for those environments, including plan enablement, settings, and policies, are performed in Defender.

You make this decision once for each scope, rather than opting in again for each release. New supported management capabilities are enabled automatically within that scope as they become available.

You can take control of an individual subscription or a management group. For a management group, the decision applies to the group and all subscriptions beneath it, including subscriptions added in the future.

## Understand the impact on Azure management

Important

Moving a scope to full management in Defender is a one-way, irreversible decision. You can't undo the transfer or return management of that scope to the Azure portal. Review the selected scope and the management changes before confirming.

After the transfer, manage all supported cloud security operations for that scope in the Defender portal, including plan enablement, settings, and policies. You can no longer perform these management operations in the Azure portal. The corresponding Azure portal controls might remain visible but be disabled or blocked.

The Azure portal can continue to display information about the scope, with capabilities available or limited depending on the current transition phase. This visibility doesn't restore management access in Azure or provide a way to reverse the transfer.

## Prerequisites

- Meet the [prerequisites for managing cloud security plans](manage-plans-defender-portal#prerequisites), including the required permissions and connected Azure environments.
- Review [what changes when you manage cloud security plans in the Defender portal](plan-management-changes-defender-portal), including billing, configuration scope, and plan changes.

Important

Moving plan management to the Defender portal uses Defender workload unit (DWU) billing. Existing resource-level plan configurations aren't preserved. Review the effects before confirming a transfer.

## Open the environments page

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **Cloud security**.
3. Under **Manage cloud security**, select **Define Cloud Security plans**.
4. Under **Per-environment plan configurations**, select **View environments**.
5. Use **All**, **Groups**, or **Environments** to review the hierarchy, and check the **Managed in** column.

The **Managed in** value determines the next step:

| Current value | Next step |
| --- | --- |
| **Azure** | Move plan enablement, billing, and all supported management capabilities to Defender in one flow. |
| **Defender (plans only)** | Move the remaining supported management capabilities to Defender. |
| **Defender (All capabilities)** | No further management transfer is needed. |

## Take control of an Azure-managed environment

If an environment is managed in Azure, move plan enablement, DWU billing, and all supported management capabilities to the Defender portal in a single flow.

1. On the environments page, select an environment whose **Managed in** value is **Azure**.
2. In the environment details pane, select **Review transition details**.
3. In the **Transfer to Defender** window, select **DWU**, and then select **Management**. **Management** is available only after you select **DWU**.

    [![Screenshot of the Migrate to Defender pane with plan enablement and billing and Move all management capabilities selected.](media/move-environments-to-defender-portal/defender-portal-transition-management-plan.png)](media/move-environments-to-defender-portal/defender-portal-transition-management-plan.png#lightbox)
4. Review the billing, plan enablement, and management changes, and then confirm the transfer.
5. Return to the environments page and verify that **Managed in** shows **Defender (All capabilities)**.

The environment now uses DWU billing, and all supported cloud security management operations are performed in the Defender portal. To change plan coverage, follow [Configure plans for selected environments](manage-plans-defender-portal#configure-plans-for-selected-environments).

## Expand a plans-only environment to full management

If an environment already uses DWU billing and plan enablement in Defender, move its remaining supported management capabilities without repeating the plan enablement and billing transfer.

1. On the environments page, select the name of an environment whose **Managed in** value is **Defender (plans only)**. Its details pane shows **Plans managed in Defender**.
2. In the environment details pane, under **Manage all security capabilities in Defender**, select **Review details**.

    [![Screenshot of a plans-only environment with the Review details button to move all security capabilities to Defender.](media/move-environments-to-defender-portal/transition-to-defender-plan-already-managed-in-defender.png)](media/move-environments-to-defender-portal/transition-to-defender-plan-already-managed-in-defender.png#lightbox)
3. In the **Move all management capabilities to Defender** pane, review the changes to policies, governance, and other supported management capabilities. After the move, Defender becomes the primary management portal for these capabilities, and you can no longer manage them in the Azure portal. New supported management capabilities are enabled automatically as they become available.

    [![Screenshot of the Move all management capabilities to Defender pane with management changes and the Move management to Defender button.](media/move-environments-to-defender-portal/confirm-move-management-to-defender.png)](media/move-environments-to-defender-portal/confirm-move-management-to-defender.png#lightbox)
4. Select **Move management to Defender** to confirm the transfer.
5. Return to the environments page and verify that **Managed in** shows **Defender (All capabilities)**.

All supported cloud security capabilities for that environment are now managed in the Defender portal. Plan enablement and DWU billing remain in Defender.

## Track progress toward full management

Use the **Environments fully managed in Defender** summary on the environments page to track management transfers.

[![Screenshot highlighting the Environments fully managed in Defender summary, showing one of four environments fully managed and a link to transfer three environments.](media/move-environments-to-defender-portal/track-environments-management.png)](media/move-environments-to-defender-portal/track-environments-management.png#lightbox)

The summary shows the number of fully managed environments out of the total. In the screenshot, **1/4** means that one of the four environments is fully managed in Defender. That environment has **Defender (All capabilities)** in the **Managed in** column.

The **Transfer 3 environments to Defender** link identifies the three environments that haven't yet moved to full management. In this example:

- Two environments show **Defender (plans only)**. Plan enablement and DWU billing have moved to Defender, but other cloud security capabilities remain managed in Azure. These environments need to move the remaining management capabilities.
- One environment shows **Azure**. Plan enablement and other cloud security capabilities remain managed in Azure. This environment needs to move plan enablement, billing, and management capabilities to Defender.

Review the **Managed in** column to identify the next transfer step for each environment.

Note

DWU billing and plan enablement management in Defender are prerequisites for full management. You can move them together with the remaining management capabilities in one flow, or move an environment that already shows **Defender (plans only)** to full management later. Moving only to DWU billing and plan enablement management doesn't make an environment fully managed; **Managed in** must show **Defender (All capabilities)**.