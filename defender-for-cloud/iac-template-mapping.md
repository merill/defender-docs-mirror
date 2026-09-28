---
layout: Conceptual
title: Map Infrastructure as Code templates from code to cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/iac-template-mapping
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
description: Learn how to map your Infrastructure as Code (IaC) templates to your cloud resources.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: ignite-2023, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 08644d51-e53e-2df6-fa3d-bb4167ff119d
document_version_independent_id: fca141fd-527a-9531-6c25-df9db6ebdcce
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/iac-template-mapping.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/iac-template-mapping
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/iac-template-mapping.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 6bb0f185-8d86-6530-57be-a7a9590152e5
---

# Map Infrastructure as Code templates from code to cloud - Microsoft Defender for Cloud | Microsoft Learn

Mapping Infrastructure as Code (IaC) templates to cloud resources helps you ensure consistent, secure, and auditable infrastructure provisioning. It supports rapid response to security threats and a security-by-design approach. You can use mapping to discover misconfigurations in runtime resources. Then, remediate at the template level to help prevent drift between the IaC templates and deployed cloud resources and to support CI/CD deployments.

## Prerequisites

To set Microsoft Defender for Cloud to map IaC templates to cloud resources, you need:

- An Azure account with Defender for Cloud configured. If you don't already have an Azure account, [create an Azure account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An [Azure DevOps](quickstart-onboard-devops) environment set up in Defender for Cloud.
- [Defender Cloud Security Posture Management (CSPM)](tutorial-enable-cspm-plan) enabled.
- Azure Pipelines set up to run the [Microsoft Security DevOps Azure DevOps extension](configure-azure-devops-extension) with the IaCFileScanner tool running.
- IaC templates and cloud resources set up with tag support. You can use open-source tools like [Yor_trace](https://github.com/bridgecrewio/yor) to automatically tag IaC templates. Tag values need to be unique GUIDs.
- Supported cloud platforms: Microsoft Azure, Amazon Web Services, Google Cloud Platform

    - Supported source code management systems: Azure DevOps
    - Supported template languages: Azure Resource Manager, Bicep, CloudFormation, Terraform

Note

Microsoft Defender for Cloud uses only the following tags from IaC templates for mapping:

- `yor_trace`
- `mapping_tag`

## See the mapping between your IaC template and your cloud resources

To see the mapping between your IaC template and your cloud resources on the [Cloud Security Explorer](how-to-manage-cloud-security-explorer) page in Defender for Cloud:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.
3. In the dropdown menu, search for and select all your cloud resources.
4. To add more filters to your query, select **+**.
5. In the **Identity & Access** category, add the subfilter **Provisioned by**.
6. In the **DevOps** category, select **Code repositories**.
7. After you build your query, select **Search** to run the query.

Alternatively, select the built-in template **Cloud resources provisioned by IaC templates with high severity misconfigurations**.

![Screenshot that shows the IaC mapping Cloud Security Explorer template.](media/iac-template-mapping/iac-mapping.png)

Note

Mapping between your IaC templates and your cloud resources might take up to 12 hours to appear in Cloud Security Explorer.

## (Optional) Create sample IaC mapping tags

To create sample IaC mapping tags in your code repositories:

1. In your repository, add an IaC template that includes tags.

    You can start with an [IaC mapping sample template](https://github.com/microsoft/security-devops-azdevops/tree/main/samples/IaCMapping).
2. To commit directly to the main branch or create a new branch for this commit, select **Save**.
3. Confirm that you included the **Microsoft Security DevOps** task in your Azure pipeline.
4. Verify that pipeline logs show a finding that says **An IaC tag(s) was found on this resource**. The finding indicates that Defender for Cloud successfully discovered tags.