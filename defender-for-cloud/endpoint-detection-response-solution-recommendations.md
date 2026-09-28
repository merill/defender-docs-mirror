---
layout: Conceptual
title: Remediate EDR solution recommendations - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/endpoint-detection-response-solution-recommendations
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
description: Identify and remediate security gaps in endpoint detection and response solutions on your virtual machine with Defender for Cloud recommendations.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: b61c8220-9daa-19da-e5f7-a04bd0d4b7c7
document_version_independent_id: 42514090-6158-329a-21ff-b973954a565a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/endpoint-detection-response-solution-recommendations.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/endpoint-detection-response-solution-recommendations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/endpoint-detection-response-solution-recommendations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
platformId: d09c52d6-99d8-c70d-8361-ac9fa799c4b9
---

# Remediate EDR solution recommendations - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud helps improve security posture for supported machines with endpoint detection and response (EDR). Defender for Cloud:

- Works with [Microsoft Defender for Endpoint](integration-defender-for-endpoint) as a built-in EDR solution.
- Scans Azure virtual machines (VMs), AWS machines, and GCP machines to check whether an EDR solution is installed and running. The EDR solution can be Defender for Endpoint or a [supported non-Microsoft solution](detect-endpoint-detection-response-solutions#supported-edr-solutions).

Based on scan results, Defender for Cloud provides [recommendations](detect-endpoint-detection-response-solutions) to help you install and run EDR solutions correctly. This article describes how to fix those recommendations.

Note

- Defender for Cloud uses agentless scanning to assess EDR settings.
- Agentless scanning replaces the Log Analytics agent (also known as the Microsoft Monitoring Agent (MMA)), which was previously used to collect machine data.
- Scanning using the MMA was deprecated in November 2024.
- To exempt resources from these EDR assessments, ensure that the **Azure CSPM initiative is assigned**. This initiative is enabled by default when Defender cloud security posture management (Defender CSPM) is turned on.

## Prerequisites

Before you investigate or remediate EDR solution recommendations, make sure you meet these requirements.

| **Requirement** | **Details** |
| --- | --- |
| **Plan** | [Defender for Cloud](connect-azure-subscription) must be available in the Azure subscription and one of these plans must be enabled:- [Defender for Servers Plan 2](tutorial-enable-servers-plan)- [Defender cloud security posture management (Defender CSPM)](tutorial-enable-cspm-plan) |
| **Agentless scanning** | [Agentless scanning for machines](concept-agentless-data-collection) must be turned on. Agentless scanning is enabled by default in both Defender for Servers Plan 2 and Defender CSPM. If you need to turn it on manually, see [Enable agentless scanning for VMs](enable-agentless-scanning-vms). |

## Investigate EDR solution recommendations

To review EDR recommendations for your machines:

1. In **Defender for Cloud**, open **Recommendations**.
2. Search for and select one of these recommendations:

    - `EDR solution should be installed on Virtual Machines`
    - `EDR solution should be installed on EC2s`
    - `EDR solution should be installed on Virtual Machines (GCP)`
3. In the recommendation details, select the **Healthy resources** tab.
4. Find the EDR solution for each machine in the **Discovered EDRs** column.

    [![Screenshot of the Healthy resources tab, which shows where you can see which endpoint detection and response solution is enabled on your machine.](media/endpoint-detection-response/discovered-solutions.png)](media/endpoint-detection-response/discovered-solutions.png#lightbox)

## Remediate EDR solution recommendations

To remediate EDR solution recommendations:

1. Select the relevant recommendation.

    [![Screenshot of the recommendations page showing the identified endpoint solution recommendations.](media/endpoint-detection-response/identify-recommendations.png)](media/endpoint-detection-response/identify-recommendations.png#lightbox)
2. Select one of the listed recommended actions to see the remediation steps for that action.

## Enable Defender for Endpoint integration

The **Enable Microsoft Defender for Endpoint integration** action appears when Defender for Endpoint can be installed on a machine. This action is available only when no [supported non-Microsoft EDR solution](detect-endpoint-detection-response-solutions) is detected on the machine.

Enable Defender for Endpoint on the machine as follows:

1. Select the affected machine. You can also select multiple machines with the `Enable Microsoft Defender for Endpoint integration` recommended action.
2. Select **Fix**.

    [![Screenshot that shows where the fix button is located.](media/endpoint-detection-response/enable-fix.png)](media/endpoint-detection-response/enable-fix.png#lightbox)
3. In **Enable EDR solution**, select **Enable**. This installs the Defender for Endpoint sensor on all Windows and Linux servers in the subscription.

    After the process completes, it can take up to 24 hours for your machine to appear in the **Healthy resources** tab.

    ![Screenshot that shows the pop-up window from which to enable the Defender for Endpoint integration on.](media/endpoint-detection-response/enable-endpoint.png)

## Turn on the required Defender plan

The **Upgrade Defender plan** action is available when:

- A [supported non-Microsoft EDR solution](detect-endpoint-detection-response-solutions) isn't detected on the machine.
- A required plan (Defender for Servers Plan 2 or Defender CSPM) isn't turned on for the machine.

Fix the recommendation as follows:

1. Select the affected machine. You can also select multiple machines with the `Upgrade Defender plan` recommended action.
2. Select **Fix**.

    [![Screenshot that shows where the fix button is located on the screen.](media/endpoint-detection-response/upgrade-fix.png)](media/endpoint-detection-response/upgrade-fix.png#lightbox)
3. In **Enable EDR solution**, select a plan in the dropdown menu. Each plan has a cost. See [Defender for Cloud pricing details](https://azure.microsoft.com/pricing/details/defender-for-cloud/).
4. Select **Enable**.

    ![Screenshot that shows the pop-up window that allows you to select which Defender for Servers plan to enable on your subscription.](media/endpoint-detection-response/enable-plan.png)

After the process completes, it can take up to 24 hours for your machine to appear on the **Healthy resources** tab.

## Troubleshoot Defender for Endpoint onboarding

The **Troubleshoot onboarding** action appears when Defender for Endpoint is found on a machine but didn't onboard correctly.

1. Select the affected VM.
2. Select **Remediation steps**.

    [![Screenshot that shows where the remediation steps are located in the recommendation.](media/endpoint-detection-response/remediation-steps.png)](media/endpoint-detection-response/remediation-steps.png#lightbox)
3. Fix onboarding issues for your platform:

    - [Troubleshoot onboarding for Windows](/en-us/defender-endpoint/troubleshoot-onboarding)
    - [Troubleshoot onboarding for Linux](/en-us/defender-endpoint/microsoft-defender-endpoint-linux)

After you finish, it can take up to 24 hours for your machine to show on the **Healthy resources** tab.