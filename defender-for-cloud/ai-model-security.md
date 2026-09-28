---
layout: Conceptual
title: Discover AI models (Preview) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/ai-model-security
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
zone_pivot_group_filename: defender-for-cloud/zone-pivots/zone-pivot-groups.json
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn about AI model security in Microsoft Defender for Cloud.
ms.topic: concept-article
ms.date: 2026-04-14T00:00:00.0000000Z
zone_pivot_groups: defender-portal-experience
ai-usage: ai-assisted
locale: en-us
document_id: c5bacdbc-02b3-d06d-2812-c6ca89c21f07
document_version_independent_id: 87e368b4-02a6-b1f0-a763-b790678746a4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/ai-model-security.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/ai-model-security
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/ai-model-security.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/d6f38669-3d05-40f2-afd8-e49f7dd20884
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/55265cca-de9b-48dc-a77a-9047cc39a575
platformId: f85da9ea-239a-5113-b91a-2d88edbb90eb
---

# Discover AI models (Preview) - Microsoft Defender for Cloud | Microsoft Learn

Important

This feature is currently in preview and included with the Microsoft Defender for AI Services plan. During preview, there is no additional charge for AI model scanning. However, enabling the Defender for AI Services plan may incur costs related to threat protection features. Continued inclusion of AI model scanning feature as part of Defender for AI Services is not guaranteed when it becomes generally available (GA), and licensing requirements may change. If that occurs, a notification will be sent before the feature is disabled with options to re‑enable it under the applicable license. AI model scanning is intended to assist customers in identifying potential security risks within supported model artifacts. Scan results may not identify all malicious, unsafe, or otherwise abusive content and may produce false positives or false negatives. Detection coverage varies based on supported model formats, scanning techniques, and available threat intelligence. Customers should independently review and validate scan findings and should not rely solely on scan results when making deployment, security, or compliance decisions.

As organizations increasingly use artificial intelligence (AI) models to drive automation, insights, and intelligent decision-making, security teams need visibility and control to assess the safety and compliance of AI models entering their environments. These models often have broad access to data and infrastructure. Without these capabilities, it becomes increasingly difficult to enforce internal standards.

Microsoft Defender for Cloud's Defender for AI security supports AI model scanning. AI model scanning provides proactive detection of unsafe or malicious artifacts and continuously monitors models for risk throughout the AI lifecycle.

AI model security automatically scans AI models for security risks such as embedded malware, unsafe operators, and exposed secrets before those models reach production. Integrated directly with Azure Machine Learning and CI/CD pipelines, the service surfaces real-time findings and actionable remediation guidance, so teams can stop risky models early in the development process.

By using AI model security, security teams can scan custom AI models uploaded to Azure Machine Learning workspaces and registries to identify threats like embedded malware, unsafe operators, and exposed secrets. Defender for Cloud presents the results, giving teams visibility into security findings along with severity ratings, remediation guidance, and relevant model metadata to support effective triage and prioritization. Developers can also trigger model scans during build or release stages by using CLI tools integrated with Azure DevOps or GitHub pipelines, enabling static scanning and early risk detection before models reach production.

## Prerequisites

- You must have an Azure subscription that contains AI models registered in [Azure Machine Learning](/en-us/azure/machine-learning/quickstart-create-resources) (Azure Machine Learning) registries or workspaces.

Note

Workspaces and registries that use a private link aren't supported.

- [Enable the Defender for Cloud Security Posture Management plan](tutorial-enable-cspm-plan).
- You must [enable threat protection for AI services](ai-onboarding) and the [AI model security](ai-onboarding#enable-ai-model-security) component of the plan.
- Required permissions: To enable the plan, you need **Owner** or **Contributor** level permissions on the Azure Machine Learning resources.
- Supported model file formats: `Pickle (.pkl)`, `HDF5 (.h5)`, `TorchScript (.pt)`, `ONNX (.onnx)`, `SafeTensors (.safetensors)`, `TensorFlow SavedModel / TFLite (FlatBuffers)`, `NumPy (.npy)`, `Arrow, MsgPack, dill, joblib`, `PMML, JSON, POJO, MOJO, GGUF`.
- File size limit: 10 GB. Model files larger than 10 GB can't be scanned.
- The scan occurs once a week.

::: zone pivot="azure-portal"

## Locate all AI models in your environment

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Defender for Cloud**.
3. Select **Cloud Security Explorer**.
4. Select **AI & Mls** &gt; **AI models**.

    [![Screenshot that shows where to select AI models from the drop-down list in the Cloud Security Explorer.](media/models/ai-models.png)](media/models/ai-models.png#lightbox)
5. Select **Done**.
6. Select **+**.
7. Select **Metadata** &gt; **AI Model Metadata**.

    [![Screenshot that shows how to select the 'AI Models Metadata' option.](media/models/ai-models-metadata.png)](media/models/ai-models-metadata.png#lightbox)
8. Select **Search**.

The Cloud Security Explorer displays all AI models in your environment. You can select **view details** to see more information about each selected model.

## Locate AI models with security findings

Use the Cloud Security Explorer to find AI models that have active security findings.

1. Follow steps 1-7 from the Locate all AI models in your environment section.
2. Select **+**.
3. Select **Recommendations** &gt; **All recommendations**.

    [![Screenshot that shows how to select the 'All recommendations' option.](media/models/all-recommendations.png)](media/models/all-recommendations.png#lightbox)
4. Select **Search**.

The Cloud Security Explorer displays all AI models in your environment that have active security findings. Select **view details** to see more information about each model and the associated findings.

::: zone-end

::: zone pivot="defender-portal"

## Locate all AI models in your environment

The Defender portal **Assets** page provides a comprehensive view of all AI models in your environment.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Go to **Assets** &gt; **Cloud** &gt; **AI** &gt; **AI models**.

    [![Screenshot that shows how to navigate to the Defender portals asset page with all of the AI models presented.](media/models/defender-ai-models.png)](media/models/defender-ai-models.png#lightbox)
3. Select an AI model with recommendations.

    ![Screenshot that shows AI models that have at least one recommendation affecting them.](media/models/ai-models-recommendation.png)
4. Select **Open asset page**.

    [![Screenshot that shows where the 'Open asset page' button is located.](media/models/asset-page.png)](media/models/asset-page.png#lightbox)
5. Select **Security recommendations** &gt; the relevant recommendation.
6. Review and remediate the security finding as needed.

You can also manage the recommendation in the Azure portal.

::: zone-end