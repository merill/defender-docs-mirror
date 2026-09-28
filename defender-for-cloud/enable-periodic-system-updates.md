---
layout: Conceptual
title: Remediate system updates and patches recommendations - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-periodic-system-updates
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
description: Understand and remediate Defender for Cloud recommendations for missing system updates and patches. This article covers assessment powered by Azure Update Manager and configuration requirements.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 4f9ffa7b-c335-828a-40c5-bbc555ebabc9
document_version_independent_id: fb10c620-9c46-e264-5f07-d1538117a154
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/enable-periodic-system-updates.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/enable-periodic-system-updates
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/enable-periodic-system-updates.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0b50effa-3606-438a-8419-9923bb3eb276
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a3cdf918-3710-494c-93c0-584d8cd4f016
platformId: eec38a44-10fe-c10a-d7e0-f1a2284f9d9e
---

# Remediate system updates and patches recommendations - Microsoft Defender for Cloud | Microsoft Learn

Defender for Cloud uses update assessment signals from Azure Update Manager to surface recommendations for missing system updates and patches across protected machines. Remediating these recommendations helps reduce exploitable vulnerabilities and keeps machine security hygiene aligned with Defender for Servers protections.

Microsoft Defender for Cloud provides security recommendations to improve your organizational security posture and reduce risk. An important element in risk reduction is to harden machines across your business environment.

As part of the hardening strategy, Defender for Cloud assesses machines to check that the latest system updates and patches are installed, and issues security recommendations if they're not. System updates and patches are crucial for keeping machines secure and healthy. Updates often contain security patches for vulnerabilities that, if left unfixed, are exploitable by attackers.

Defender for Servers Plan 2 automatically assesses updates and patches on machines and generates the following recommendations as needed:

- [Machines should be configured to periodically check for missing system updates](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/2Fbd876905-5b84-4f73-ab2d-2e7a7c4568d9)
- [System updates should be installed on your machines (powered by Azure Update Manager)](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/e1145ab1-eb4f-43d8-911b-36ddf771d13f)

These recommendations rely on [Azure Update Manager](/en-us/azure/update-manager/overview), which uses a [VM extension](/en-us/azure/update-manager/workflow-update-manager?tabs=azure-vms%2Cupdate-win).

Note

The older method for update assessment used the Log Analytics agent (also known as the Microsoft Monitoring Agent (MMA)) to gather data. Use of the MMA is now deprecated.

## Prerequisites

Before you verify or remediate system updates, make sure the following prerequisites are met:

- [Defender for Servers Plan 2](defender-for-servers-overview) must be enabled.
- To verify system updates, machines must meet the [Azure Update Manager support requirements](/en-us/azure/update-manager/support-matrix).
- On-premises machines must be [connected as Azure Arc-enabled VMs](quickstart-onboard-machines).
- Multicloud (AWS/GCP machines) must be onboarded with Azure Arc when you connect [AWS](quickstart-onboard-aws) or [GCP](quickstart-onboard-gcp).
- If you're using Defender for Servers Plan 2, there's no additional cost for assessing, remediating, and patching system updates on supported Azure VMs and Azure Arc VMs.
- If Defender for Servers Plan 2 isn't enabled on your subscription or multicloud connector, assessments for Azure Arc-enabled VMs in the subscription are subject to [Azure Update Manager charges](https://azure.microsoft.com/pricing/details/azure-update-management-center/).

## Enable periodic assessment on machines

To enable periodic assessment for system updates, complete the following steps:

1. In Defender for Cloud, open the **Recommendations** page.
2. Select the recommendation `Machines should be configured to periodically check for missing system updates (powered by Azure Update Manager)`.

    - Under **Remediation steps**, review quick fix and manual fix details. If you follow the quick fix, the [periodic assessment](/en-us/azure/update-manager/assessment-options#periodic-assessment) update setting is enabled on machines.
    - In the **Unhealthy resources** list, drill down to see resource details.
3. Select **Fix**. For more information, see [Use the fix option](implement-security-recommendations#use-the-fix-option).
4. Select the relevant machine, and then select **Fix 1 resource**.

Periodic assessment can also be [enabled at scale with Azure Policy](/en-us/azure/update-manager/periodic-assessment-at-scale?branch=main).

## Remediate update recommendations

To remediate system update recommendations, complete the following steps:

1. In Defender for Cloud, open the **Recommendations** page.
2. Select the recommendation `System updates should be installed on your machines (powered by Azure Update Manager)`.
3. Review the recommendation.
4. Select **Fix** to install the missing updates. The updates are applied as a one-time fix.

    [![Screenshot that shows where the fix button is located.](media/enable-periodic-system-updates/fix-updates.png)](media/enable-periodic-system-updates/fix-updates.png#lightbox)

## Remediate recommendations at scale

You can remediate recommendations on many machines at the same time.

1. In Defender for Cloud, open the **Recommendations** page.
2. Select the recommendation `System updates should be installed on your machines (powered by Azure Update Manager)`.
3. Review the update details.
4. On the details page, select **View recommendation for all resources**.

    [![Screenshot that shows where the view recommendation for all resources button is located.](media/enable-periodic-system-updates/view-recommendations.png)](media/enable-periodic-system-updates/view-recommendations.png#lightbox)
5. Select all machines you want to fix.
6. Select **Fix**.