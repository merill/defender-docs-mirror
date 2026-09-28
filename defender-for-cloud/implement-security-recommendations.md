---
layout: Conceptual
title: Remediate Security Recommendations in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/implement-security-recommendations
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
description: Remediate security recommendations in Defender for Cloud for Azure, AWS, and GCP. Review assessments, apply practical fixes, and improve security posture.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 899cbe83-4917-7d76-92a0-e2cda443c73d
document_version_independent_id: b826d6a3-fd26-472a-a220-cf16cb40f379
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/implement-security-recommendations.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/implement-security-recommendations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/implement-security-recommendations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: d923979c-fb98-df7b-493f-05bdbd51318c
---

# Remediate Security Recommendations in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

When you use Defender for Cloud to help protect your resources and workloads, it assesses them against built-in and custom security standards that you enable in your Azure subscriptions, Amazon Web Services (AWS) accounts, and Google Cloud Platform (GCP) projects. Based on these security assessments, security recommendations provide practical steps to remediate security issues and improve your security posture.

You can remediate security recommendations in your Defender for Cloud deployment.

Before you attempt to remediate a recommendation, review it in detail. See [review security recommendations](review-security-recommendations).

## Remediate a recommendation

By default, recommendations are prioritized based on the risk level of the security issue.

In addition to risk level, prioritize the security controls in the default [Microsoft cloud security benchmark](concept-regulatory-compliance) standard in Defender for Cloud. The security controls in this standard affect your [Microsoft Secure Score](secure-score-security-controls).

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Recommendations**.

    [![Screenshot of the recommendations page that shows all the affected resources by their risk level.](media/implement-security-recommendations/recommendations-page.png)](media/implement-security-recommendations/recommendations-page.png#lightbox)
3. Select a recommendation.
4. Select **Take action**.
5. Locate the **Remediate** section and follow the remediation instructions.

    [![Screenshot that shows manual remediation steps for a recommendation.](media/implement-security-recommendations/remediate-recommendation.png)](media/implement-security-recommendations/remediate-recommendation.png#lightbox)

## Use the Fix option

To simplify the remediation process, a button labeled **Fix** might appear in a recommendation. The **Fix** button helps you quickly remediate a recommendation on multiple resources. If there isn't a **Fix** button in the selected recommendation, then you can't apply a quick fix. Follow the presented remediation steps to address the selected recommendation.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Recommendations**.
3. Select a recommendation to remediate.
4. Select **Take action** &gt; **Fix**.

    [![Screenshot that shows recommendations with the Fix action.](media/implement-security-recommendations/microsoft-defender-for-cloud-recommendations-fix-action.png)](media/implement-security-recommendations/microsoft-defender-for-cloud-recommendations-fix-action.png#lightbox)
5. Follow the rest of the remediation steps.

After remediation finishes, it can take several minutes for the recommendation status to update.

## Use automated remediation scripts

Security admins can also fix issues at scale with automatic script generation in AWS and GCP CLI script language. When you select **Take action** &gt; **Fix** on a recommendation where an automated script is available, an automated remediation script window opens.

[![Screenshot that shows recommendations with the automated remediation script.](media/implement-security-recommendations/automated-remediation-scripts.png)](media/implement-security-recommendations/automated-remediation-scripts.png#lightbox)

To remediate the selected recommendation, copy and run the script.