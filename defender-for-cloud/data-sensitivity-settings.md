---
layout: Conceptual
title: Customize Data Sensitivity Settings - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/data-sensitivity-settings
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
description: Learn how to customize data sensitivity settings in Microsoft Defender for Cloud to better manage and protect your organization's sensitive data.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: c46870ca-fbc4-c8c3-65d5-193dc094a44e
document_version_independent_id: b1e16432-c459-2cc9-f2c5-01fa86dd2126
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/data-sensitivity-settings.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/data-sensitivity-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/data-sensitivity-settings.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
platformId: 0f6bbe46-b6ac-634f-07a5-1ae2ef4e63aa
---

# Customize Data Sensitivity Settings - Microsoft Defender for Cloud | Microsoft Learn

You can customize data sensitivity settings in Microsoft Defender for Cloud. Data sensitivity settings are used to identify and focus on managing the critical sensitive data in your organization. Defender cloud security posture management (Defender CSPM) refers to the Defender CSPM plan in Microsoft Defender for Cloud.

- Select sensitive information types and sensitivity labels from the Microsoft Purview portal in Defender for Cloud.

    - By default, Defender for Cloud uses [built-in sensitive information types](/en-us/microsoft-365/compliance/sensitive-information-type-learn-about) from Microsoft Purview.
    - Some information types and labels are enabled by default.
    - Sensitive data discovery supports a subset of the built-in sensitive information types from Microsoft Purview. See the [reference list of supported sensitive information types](sensitive-info-types).
    - Modify the default settings on the **Data sensitivity** page.
- If you import labels, set sensitivity thresholds that determine the minimum threshold sensitivity level for a label to be marked as sensitive in Defender for Cloud.

Customizing data sensitivity settings helps you focus on your critical sensitive resources and improve the accuracy of the sensitivity insights.

## Prerequisites

Before you customize data sensitivity settings, ensure the following requirements are met:

- Review [prerequisites and requirements for configuring data sensitivity settings](concept-data-security-posture-prepare#configure-data-sensitivity-settings).
- In Defender for Cloud, enable sensitive data discovery capabilities in the [Defender CSPM](data-security-posture-enable) or [Defender for Storage](defender-for-storage-data-sensitivity) plans.

Changes in sensitivity settings take effect the next time that resources are discovered.

## Import custom sensitivity info types/labels

Defender for Cloud automatically imports custom sensitivity information types and sensitivity labels. If you have the Enterprise Mobility and Security E5/A5/G5 license, you don't need to manually provide consent in the Microsoft Defender XDR portal. For more information, see [Microsoft Purview sensitivity labeling licensing](/en-us/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-purview-service-description#microsoft-purview-information-protection-sensitivity-labeling).

Defender for Cloud only imports sensitivity labels with automatic labeling rules. Defender for Cloud ignores the *location* section in the automatic labeling rule and applies the label to all resource types and locations.

## Customize sensitive data categories/types

To customize data sensitivity settings in Defender for Cloud, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Data sensitivity**.
4. Select the info type category that you want to customize:

    - The **Finance**, **PII**, and **Credentials** categories contain the default info type data that attackers typically seek.
    - The **Custom** category contains custom info types from your Microsoft Purview portal configuration.
    - The **Other** category contains all of the rest of the built-in available info types.
5. Select the info types that you want to mark as sensitive.
6. Select **Apply** and **Save**.

    ![Screenshot of the data sensitivity page, showing the sensitivity settings.](media/concept-data-security-posture/data-sensitivity.png)

## Set the threshold for sensitive data labels

If you use Microsoft Purview sensitivity labels, make sure that:

- You set the label scope to **files and other data assets**, and configure the [auto-labeling rule for Office apps](/en-us/purview/apply-sensitivity-label-automatically#how-to-configure-auto-labeling-for-office-apps).
- Your labels are [published with a label policy](/en-us/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy) that is in effect.

You can set a threshold to determine the minimum sensitivity level for a label to be marked as sensitive in Defender for Cloud.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Data sensitivity**. The current minimum sensitivity threshold is shown.
4. Select **Change** to see the list of sensitivity labels and select the lowest sensitivity label that you want marked as sensitive.
5. Select **Apply** and **Save**.

    ![Screenshot of the data sensitivity page, showing the sensitivity label threshold.](media/concept-data-security-posture/sensitivity-threshold.png)

When you turn on the threshold, you select a label with the lowest setting that should be considered sensitive in your organization. Any resources with this minimum label or higher are presumed to contain sensitive data. For example, if you select **Confidential** as minimum, then **Highly Confidential** is also considered sensitive. **General**, **Public**, and **Non-Business** aren't.

You can't select a sublabel in the threshold. However, you can see the sublabel as the affected label on resources in attack path/Cloud Security Explorer if the parent label is included in the threshold, meaning it is one of the selected sensitive labels.

The same settings apply to any supported resource, including object storage and databases.