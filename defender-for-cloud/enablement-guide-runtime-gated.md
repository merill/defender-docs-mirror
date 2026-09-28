---
layout: Conceptual
title: Configure gated deployment rules for Kubernetes container images - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/enablement-guide-runtime-gated
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
description: Learn how to configure gated deployment rules in Microsoft Defender for Containers to audit or block Kubernetes deployments based on container image vulnerability findings.
ms.date: 2026-06-07T00:00:00.0000000Z
ms.topic: how-to
locale: en-us
document_id: 82a309fb-f360-1c52-6c1d-e073e2af2d93
document_version_independent_id: 88ba05ea-9c59-7b93-da6a-7e24e3ae0f24
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/enablement-guide-runtime-gated.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/enablement-guide-runtime-gated
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/enablement-guide-runtime-gated.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cb49e66a-8528-497d-adaa-eade2d009d1b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/472c9d15-157b-443c-afa2-e209c8fecf58
platformId: 01dd134b-60c1-7135-98ab-04515f56b9c1
---

# Configure gated deployment rules for Kubernetes container images - Microsoft Defender for Cloud | Microsoft Learn

This article shows you how to configure gated deployment rules in Microsoft Defender for Containers.

Gated deployment uses an admission controller to evaluate container images before they're admitted into a Kubernetes cluster. It uses vulnerability scan results from supported container registries to audit or deny deployments when images don't meet your organization's vulnerability policy.

## Prerequisites

Before you begin, make sure that:

- You have a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Defender for Cloud is enabled](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- [Defender for Containers is enabled](defender-for-containers-enable-plan) for the environment that contains your Kubernetes cluster and container registry, with the following components enabled:

    - **Defender sensor** with **Security Gating**
    - **Registry access** with **Security findings**

    Note

    If the Kubernetes cluster and container registry are in different environments, enable Defender for Containers and the required components for both environments.
- **AKS clusters:** The cluster has an [OpenID Connect (OIDC) issuer](/en-us/azure/aks/use-oidc-issuer) enabled.
- Your Kubernetes environment and container registry are supported for gated deployment. See the [Defender for Containers support matrix](support-matrix-defender-for-containers#containers-software-supply-chain-protection-features).
- Vulnerability scan results are available for the container images you want to evaluate. Gated deployment uses vulnerability assessment findings from supported registries.
- You have the required permissions:

    - To create or change gated deployment rules, you need **Security Admin** or higher permissions.
    - To view gated deployment rules, you need **Security Reader** or higher permissions.

## Configure a gated deployment rule

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Security rules**.

    [![Screenshot of the Security Rules tile in Microsoft Defender for Cloud.](media/enablement-guide-runtime-gating/security-rules.png)](media/enablement-guide-runtime-gating/security-rules.png#lightbox)
4. Select **Gated deployment** &gt; **Vulnerability assessment**.

    [![Screenshot of the Vulnerability Assessment tab in Security Rules.](media/enablement-guide-runtime-gating/vulnerability-assessment.png)](media/enablement-guide-runtime-gating/vulnerability-assessment.png#lightbox)

    Note

    By default, after the required prerequisites are met, Defender for Containers creates an audit rule that flags image deployments with high or critical vulnerabilities.
5. Select **Add rule**.
6. Enter a **Rule name**.
7. Select an **Action**:

    - **Audit**: Allows the deployment and creates an admission event for review.
    - **Deny**: Blocks deployments that match the rule conditions.

    Tip

    Start with **Audit** to understand the effect of the rule before you use **Deny** mode to block deployments.

    Note

    Deny mode can introduce a one- or two-second delay during deployment because the image is evaluated before the workload is admitted into the cluster.
8. If needed, enter a **Rule description**.
9. Enter a **Scope name**.
10. Select the **Cloud scope**.
11. Under **Resource scope**, keep the default scope or select **Add condition** to narrow the rule scope.

    Tip

    Start with a narrow scope, such as namespace or deployment, before applying broader enforcement.

    [![Screenshot of the rule creation wizard in Microsoft Defender for Cloud.](media/enablement-guide-runtime-gating/rule-creation-wizard.png)](media/enablement-guide-runtime-gating/rule-creation-wizard.png#lightbox)
12. Select **Next**.
13. Toggle on **Block all deployments with missing artifacts** if you want to block deployments when vulnerability findings artifacts aren't available.
14. Select **Add condition**, and define at least one condition for the rule.

    [![Screenshot of the vulnerability assessment rule configuration pane.](media/enablement-guide-runtime-gating/edit-vulnerability-assessment-rule.png)](media/enablement-guide-runtime-gating/edit-vulnerability-assessment-rule.png#lightbox)
15. Select **Next**.
16. To exempt specific vulnerabilities, select **Add allowed vulnerabilities**, and then enter the CVE IDs that you want to exempt.
17. To make the vulnerability exemption temporary, toggle on **Time bound**, and then select a **Valid until** date.
18. To exempt specific resources, select **Add exemption**, and then define the resource-based exemption.

    [![Screenshot of the exemption configuration pane with the time-bound option.](media/enablement-guide-runtime-gating/exemption-configuration-panel.png)](media/enablement-guide-runtime-gating/exemption-configuration-panel.png#lightbox)
19. Select **Add Rule**.

## Monitor gated deployment events

You can monitor gated deployment events to review rule evaluations, triggered actions, and affected resources. Use these events to help refine rule scope, conditions, and exemptions.

To investigate a specific admission event:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Security rules**.
4. Select **Gated deployment** &gt; **Admission Monitoring**.

    [![Screenshot of the Admission Monitoring view showing rule evaluations and actions.](media/enablement-guide-runtime-gating/admission-monitoring.png)](media/enablement-guide-runtime-gating/admission-monitoring.png#lightbox)
5. Select an event from the list.

    The details pane shows:

    - The event timestamp and admission action.
    - The container image digest, detected violations, and triggered rule.
    - The vulnerability assessment policy and criteria used for evaluation.
    - The rule conditions and exemptions that were applied.

    [![Screenshot of the admission event details pane.](media/enablement-guide-runtime-gating/admission-event-details.png)](media/enablement-guide-runtime-gating/admission-event-details.png#lightbox)

## Disable or delete a gated deployment rule

To disable or delete a gated deployment rule:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Security Rules**.
4. Select the **Vulnerability Assessment** tab.
5. Select the rule.
6. Select **Disable** or **Delete rule**.