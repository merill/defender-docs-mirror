---
layout: Conceptual
title: Microsoft Sentinel CCF for Azure Government | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/isv/azure-government-publishing-guidelines
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Learn how to prepare Microsoft Sentinel CCF data connector solutions for Azure Government and enable availability in Partner Center.
author: marjoriehahn
ms.author: marjoriehahn
ms.topic: how-to
ms.date: 2026-09-28T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1030
ai-usage: ai-assisted
locale: en-us
document_id: 43a81247-19a4-51e6-ad8b-277175d27abc
document_version_independent_id: 2ab7b282-a867-24fa-7f5c-79b74f85e011
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/isv/azure-government-publishing-guidelines.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/isv/azure-government-publishing-guidelines
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/isv/azure-government-publishing-guidelines.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/15545907-caea-48c1-a546-e84930c5b845
- https://authoring-docs-microsoft.poolparty.biz/devrel/3439c05e-99ce-45d1-b266-9322ea647316
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fd70c557-2c67-40b8-b517-cf047ce6d0c3
- https://authoring-docs-microsoft.poolparty.biz/devrel/23472108-2f8d-47d2-b07a-c0b1e9d492b6
platformId: 4aa70138-3e70-07ef-a28e-69d0b1ae775a
---

# Microsoft Sentinel CCF for Azure Government | Microsoft Learn

Publish your Microsoft Sentinel codeless connector framework (CCF) solution to make it available to Azure Government customers in the content hub. As a solution publisher, review the connector endpoints and enable Azure Government availability in Microsoft Partner Center.

Before you begin, complete public-cloud publishing and confirm that you have the required Partner Center role.

## Prerequisites

- Complete testing, certification, and publishing in the public cloud. If you haven't packaged and published a solution before, see [Build and publish Microsoft Sentinel SIEM solutions](sentinel-integration-guide).
- You need the **Developer** role in Partner Center to upload packages and submit offers. This role provides the least-privileged access required for this procedure. For more information, see [Roles, permissions, and workspace access for users](/en-us/partner-center/account-settings/permissions-overview#all-roles-applicable-to-microsoft-marketplace-program-or-microsoft-365-copilot-program).

## Prepare the CCF data connector for Azure Government

Most CCF polling, Google Cloud Platform (GCP), blob, and push data connectors don't need changes for Azure Government. However, check your connector instructions for references to public cloud endpoints. This check is especially important for CCF push connectors, whose instructions are more likely to reference those endpoints.

### Update solution templates for Azure Government

If your CCF data connector references an Azure public cloud endpoint, add the corresponding Azure Government endpoint. Customers can then choose the appropriate endpoint for their environment.

#### Example: NordStellar (Push) connector

[![Screenshot of an example of a CCF Push data connector configuration with the public Azure Monitor OAuth scope highlighted.](media/azure-government-publishing-guidelines/public-endpoint-reference-example.png)](media/azure-government-publishing-guidelines/public-endpoint-reference-example.png#lightbox)

The NordStellar CCF push connector instructions in the screenshot specify the OAuth bearer token scope `https://monitor.azure.com//.default`. This scope isn't valid in Azure Government and causes an authorization failure during connection setup. For Azure Government, customers must use `https://monitor.azure.us//.default` instead.

Include both endpoints in the connector instructions and identify the environment for each endpoint. This helps customers install and use the data connector and prevent connection failures.

The following table lists common Azure public cloud endpoints and their Azure Government equivalents:

| Service | Azure public cloud endpoint | Azure Government endpoint |
| --- | --- | --- |
| Azure Resource Manager | `https://management.azure.com` | `https://management.usgovcloudapi.net` |
| Microsoft Entra ID | `https://login.microsoftonline.com` | `https://login.microsoftonline.us` |
| Log Analytics | `https://api.loganalytics.io` | `https://api.loganalytics.us` |
| Key Vault | `https://<vault-name>.vault.azure.net` | `https://<vault-name>.vault.usgovcloudapi.net` |
| Storage | `https://<account>.blob.core.windows.net` | `https://<account>.blob.core.usgovcloudapi.net` |
| Azure Monitor | `https://monitor.azure.com` | `https://monitor.azure.us` |
| Azure portal | `https://portal.azure.com` | `https://portal.azure.us` |

For a complete list of Azure services and their public and government endpoints, see [Azure Government guidance for developers](/en-us/azure/azure-government/compare-azure-government-global-azure#guidance-for-developers).

To update the CCF data connector's instructions, modify the connector content files and repackage the solution. For build and test guidance, see [Develop a SIEM solution for Microsoft Sentinel](develop-siem-solutions-overview). For packaging steps, see [Package a SIEM solution for Microsoft Sentinel](package-siem-solutions-overview).

Before you enable Azure Government availability in Partner Center, make sure the updated package is merged into the Azure-Sentinel repository's `master` branch. Follow the packaging guide's merge requirements.

## Enable Azure Government availability in Partner Center

After you confirm the solution template is ready for Azure Government, publish it from Partner Center. The Azure Government publishing procedure assumes you've already published the solution to the content hub in the public cloud. For first-time publishing instructions, see [Build and publish Microsoft Sentinel SIEM solutions](sentinel-integration-guide#publish).

Azure Government availability can't be revoked after you publish the solution. Make sure you're ready to publish the offer to Azure Government before you enable availability.

Important

Partner Center recommends validating the solution in Azure Government whenever possible because service endpoints might differ. To stage and test the solution, [request a trial account](https://go.microsoft.com/fwlink/?linkid=2126894). Azure Government serves eligible US federal, state, local, and tribal customers and partners. As the publisher, you're responsible for applicable compliance controls, security measures, and best practices. For more information, see [Azure Government](https://go.microsoft.com/fwlink/?linkid=2126893).

To make the solution available in the Microsoft Sentinel content hub for Azure Government, follow these steps:

1. In Partner Center, open your marketplace offer, go to **Plan overview**, and select the plan.

    [![Screenshot of the Partner Center Plan overview page showing the solution plan.](media/azure-government-publishing-guidelines/partner-center-plan-overview.png)](media/azure-government-publishing-guidelines/partner-center-plan-overview.png#lightbox)
2. On the **Plan setup** page, select **Azure Government** under **Azure regions**.

    [![Screenshot of the Partner Center Plan setup page with Azure Government selected under Azure regions.](media/azure-government-publishing-guidelines/partner-center-azure-government-plan-setup.png)](media/azure-government-publishing-guidelines/partner-center-azure-government-plan-setup.png#lightbox)
3. If you updated the solution templates for Azure Government, upload the latest package on the **Technical configuration** page. See Update solution templates for Azure Government.

    [![Screenshot of the Partner Center Technical configuration page with the uploaded solution package highlighted.](media/azure-government-publishing-guidelines/partner-center-technical-configuration-package.png)](media/azure-government-publishing-guidelines/partner-center-technical-configuration-package.png#lightbox)
4. Select **Save draft**, then **Review and publish**.
5. On the **Offer overview** page, confirm that the offer shows **Package provisioning (Azure Government)** and **Azure government links**.

    [![Screenshot of the Partner Center Offer overview page showing successful Azure Government package provisioning and Azure Government links.](media/azure-government-publishing-guidelines/partner-center-azure-government-publishing.png)](media/azure-government-publishing-guidelines/partner-center-azure-government-publishing.png#lightbox)

After publishing completes and the changes propagate, the solution appears in the Microsoft Sentinel content hub for Azure Government tenants.

## Considerations

- Some Azure services and features aren't available in Azure Government. Check [Microsoft Sentinel feature availability](../feature-availability) for the latest support information.
- If you need additional assistance publishing your Microsoft Sentinel SIEM solution to Azure Government, submit [our intake form](https://aka.ms/appassurerequest).