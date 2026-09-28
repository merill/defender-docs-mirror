---
layout: Conceptual
title: Investigate Defender for Endpoint misconfiguration recommendations (agentless) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/endpoint-detection-misconfiguration
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
description: Use agentless scanning to identify and investigate Defender for Endpoint configuration issues, such as outdated signatures, disabled antivirus, or overdue scans.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 2ce5a269-a119-a11b-b5a0-fe32170e167b
document_version_independent_id: ed8eafe2-81d9-7083-c740-68b63ced733e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/endpoint-detection-misconfiguration.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/endpoint-detection-misconfiguration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/endpoint-detection-misconfiguration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 97791e2a-e939-6ae0-6af9-d8d224bcf29d
---

# Investigate Defender for Endpoint misconfiguration recommendations (agentless) - Microsoft Defender for Cloud | Microsoft Learn

Defender for Cloud uses agentless scanning with Defender for Endpoint integration to surface endpoint detection and response (EDR) misconfiguration recommendations for protected machines. Investigating and remediating these findings helps maintain endpoint protection health and keeps machine posture aligned with Defender for Cloud risk reduction workflows.

Microsoft Defender for Cloud integrates with [Microsoft Defender for Endpoint](/en-us/defender-endpoint/microsoft-defender-endpoint) to identify endpoint detection and response configuration issues for machines.

As part of the [Defender for Cloud and Defender for Endpoint integration](integration-defender-for-endpoint), Defender for Cloud uses agentless scanning to evaluate whether Defender for Endpoint is configured correctly on protected machines. Examples of these checks include:

- `Both full and quick scans are out of 7 days`
- `Signature out of date`
- `Anti-virus is off or partially configured`

When misconfigurations are found, Defender for Cloud generates recommendations. Complete remediation actions in Microsoft Defender for Endpoint or on the affected machine.

Note

- Defender for Cloud uses agentless scanning to assess endpoint detection and response (EDR) settings.
- Agentless scanning replaces the Log Analytics agent (also known as the Microsoft Monitoring Agent (MMA)), which was previously used to collect machine data.
- The use of MMA is retired. Scanning using the MMA was deprecated in November 2024.

## Prerequisites

Before you start, make sure that:

- [Defender for Cloud](connect-azure-subscription)is enabled on your subscription with one of the following plans:
    - [Defender for Servers Plan 2](tutorial-enable-servers-plan)
    - [Defender cloud security posture management (Defender CSPM)](tutorial-enable-cspm-plan)
- [Agentless scanning for machines](concept-agentless-data-collection) is enabled. If needed, you can [enable agentless scanning manually](enable-agentless-scanning-vms).
- Defender for Endpoint is running as the EDR solution on the virtual machines.

## Investigate misconfiguration recommendations

To investigate and remediate misconfiguration recommendations for Defender for Endpoint, perform the following steps:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Defender for Cloud**.
3. In the Defender for Cloud menu, select **Recommendations**.
4. Search for and select one of the following recommendations:

    - `EDR configuration issues should be resolved on virtual machines`
    - `EDR configuration issues should be resolved on EC2s`
    - `EDR configuration issues should be resolved on GCP virtual machines`

    [![Screenshot that shows the recommendations that configure your endpoint detection and solution and remediate misconfigurations.](media/endpoint-detection-response/configurable-solutions.png)](media/endpoint-detection-response/configurable-solutions.png#lightbox)
5. Select a security check to review the affected resources.

    [![Screenshot that shows a selected security check and the affected resources.](media/endpoint-detection-response/affected-resources.png)](media/endpoint-detection-response/affected-resources.png#lightbox)
6. Expand **Affected resources**.

    ![Screenshot that shows you where you need to select on screen to expand the affected resources section.](media/endpoint-detection-response/affected-resources-section.png)
7. Review the resource findings. [![Screenshot that shows the findings of an affected unhealthy resource.](media/endpoint-detection-response/resources-findings.png)](media/endpoint-detection-response/resources-findings.png#lightbox)
8. Drill into the security check to view the remediation steps provided with the recommendation, and complete the remediation in Defender for Endpoint or on the affected machine.

    ![Screenshot that shows the additional details section.](media/endpoint-detection-response/security-check-remediation.png)

After remediation is complete, it can take up to 24 hours for the machine to appear in the **Healthy resources** tab.