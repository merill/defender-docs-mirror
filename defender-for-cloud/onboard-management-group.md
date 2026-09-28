---
layout: Conceptual
title: Onboard a Management Group to Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/onboard-management-group
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
description: Learn how to use a supplied Azure Policy definition to enable Microsoft Defender for Cloud for all the subscriptions in a management group.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 75ca6720-966a-440e-396f-6afca92bc304
document_version_independent_id: b6ca2db4-1c9a-d331-914d-9edfe53a3937
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/onboard-management-group.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/onboard-management-group
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/onboard-management-group.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 3119948b-2ba2-823e-04bf-3545cd53cf25
---

# Onboard a Management Group to Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

## Overview

You can use Azure Policy to enable Microsoft Defender for Cloud on all the Azure subscriptions in the same management group. This approach is more convenient than accessing them individually from the portal, and works even if the subscriptions belong to different owners.

## Prerequisites

Before you onboard the management group, register the required resource provider.

Enable the resource provider `_Microsoft.Security_` for the management group. The following Azure CLI command registers the `Microsoft.Security` resource provider at the management group scope so that Defender for Cloud policies can be assigned and evaluated:

```azurecli
az provider register --namespace Microsoft.Security --management-group-id …
```

## Onboard a management group and all its subscriptions

To onboard a management group and all its subscriptions:

1. As a user with **Security Admin** permissions, open Azure Policy and search for the definition `Enable Microsoft Defender for Cloud on your subscription`.

    [![Screenshot showing the Azure Policy definition Enable Defender for Cloud on your subscription.](media/get-started/enable-microsoft-defender-for-cloud-policy.png)](media/get-started/enable-microsoft-defender-for-cloud-policy-extended.png#lightbox)
2. Select **Assign** and ensure you set the scope to the management group level.

    [![Screenshot showing how to assign the definition Enable Defender for Cloud on your subscription.](media/get-started/assign-policy.png)](media/get-started/assign-policy.png#lightbox)

    Tip

    Other than the scope, there are no required parameters.
3. Select **Remediation**, and then select **Create a remediation task** to ensure all existing subscriptions that don't have Defender for Cloud enabled get onboarded.

    [![Screenshot that shows how to create a remediation task for the Azure Policy definition Enable Defender for Cloud on your subscription.](media/get-started/remediation-task.png)](media/get-started/remediation-task.png#lightbox)
4. Select **Review + create**.
5. Review your information and select **Create**.

When you assign the definition, it:

- Detects all subscriptions in the management group that aren't yet registered with Defender for Cloud.
- Marks those subscriptions as *non-compliant*.
- Marks as *compliant* all registered subscriptions, regardless of whether they have Defender for Cloud's enhanced security features on or off.

The remediation task then enables Defender for Cloud's basic functionality on the non-compliant subscriptions.

## Optional policy definition modifications

You might choose to modify the Azure Policy definition in various ways:

- **Define compliance differently.** The supplied policy classifies all subscriptions in the management group that aren't yet registered with Defender for Cloud as *non-compliant*. You might choose to set it to all subscriptions without Defender for Cloud's enhanced security features enabled.

    The supplied definition defines *either* of the `pricing` settings below as compliant. Meaning that a subscription set to `standard` or `free` is compliant.

    Tip

    When any Microsoft Defender plan is enabled, it's described in a policy definition as being on the `standard` setting. When it's disabled, it's `free`. To learn about the differences between these plans, see [Microsoft Defender for Cloud's Defender plans](defender-for-cloud-introduction#cloud-workload-protection-platform-cwpp).

    ```json
    "existenceCondition": {
        "anyof": [
            {
                "field": "microsoft.security/pricings/pricingTier",
                "equals": "standard"
            },
            {
                "field": "microsoft.security/pricings/pricingTier",
                "equals": "free"
            }
        ]
    },
    ```

    If you change the `existenceCondition` to the following, only subscriptions set to `standard` would be classified as compliant:

    ```json
    "existenceCondition": {
            "field": "microsoft.security/pricings/pricingTier",
            "equals": "standard"
          },
    ```
- **Define some Defender plans to apply when enabling Defender for Cloud.** The supplied policy enables Defender for Cloud without any of the optional enhanced security features. You might choose to enable one or more of the Defender plans.

    The supplied definition's `deployment` section has a parameter `pricingTier`. By default, this parameter is set to `free`, but you can modify it.