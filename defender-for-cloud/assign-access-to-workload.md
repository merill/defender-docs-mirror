---
layout: Conceptual
title: Assign access to workload owners - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/assign-access-to-workload
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
description: Learn how to assign access to a workload owner of an Amazon Web Service or Google Cloud Platform connector.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 2ffcce78-ca0a-4df7-ad44-b771affc0bc3
document_version_independent_id: 5e025548-bb91-a383-7fe7-1b5844c7ace7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/assign-access-to-workload.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/assign-access-to-workload
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/assign-access-to-workload.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 78184fc7-11db-bf52-0748-93e55539fc91
---

# Assign access to workload owners - Microsoft Defender for Cloud | Microsoft Learn

When you onboard your Amazon Web Service (AWS) or Google Cloud Platform (GCP) environments, Defender for Cloud creates a security connector as an Azure resource. It also sets up an Identity and Access Management (IAM) role as the identity provider.

To assign permissions on a specific account or project connector, first decide which AWS accounts or GCP projects your users need. Then find the security connectors that match those accounts or projects.

## Prerequisites

- An Azure account. If you don't already have an Azure account, you can [create your Azure free account today](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- At least one security connector for [Connect Azure subscriptions](connect-azure-subscription), [Onboard AWS accounts](quickstart-onboard-aws), or [Onboard GCP projects](quickstart-onboard-gcp).

## Configure permissions on the security connector

You manage permissions for security connectors through Azure role-based access control (RBAC). You can assign roles to users, groups, and applications at any level: subscription, resource group, or resource.

To configure connector permissions:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Locate the relevant AWS or GCP connector.
4. Assign permissions to workload owners by using **All resources** or **Azure Resource Graph** in the Azure portal.

# [All resources](#tab/all-resources)
1. Search for and select **All resources**.

        [![Screenshot that shows you how to search for and select all resources.](media/assign-access-to-workload/all-resources.png)](media/assign-access-to-workload/all-resources.png#lightbox)
    2. Select **Manage view** &gt; **Show hidden types**.

        [![Screenshot that shows you where on the screen to find the show hidden types option.](media/assign-access-to-workload/show-hidden-types.png)](media/assign-access-to-workload/show-hidden-types.png#lightbox)
    3. Select the **Types equals all** filter.
    4. Enter `securityconnector` in the value field and select `microsoft.security/securityconnectors`.

        [![Screenshot that shows where the field is located and where to enter the value on the screen.](media/assign-access-to-workload/security-connector.png)](media/assign-access-to-workload/security-connector.png#lightbox)
    5. Select **Apply**.
    6. Select the relevant resource connector.

# [Azure Resource Graph](#tab/azure-resource-graph)
1. Search for and select **Resource Graph Explorer**.

        [![Screenshot that shows you how to search for and select resource graph explorer.](media/assign-access-to-workload/resource-graph-explorer.png)](media/assign-access-to-workload/resource-graph-explorer.png#lightbox)
    2. Copy and paste the following query to locate the security connector:

# [AWS](#tab/aws)
```bash
        resources 
        | where type == "microsoft.security/securityconnectors" 
        | extend source = tostring(properties.environmentName)  
        | where source == "AWS" 
        | project name, subscriptionId, resourceGroup, accountId = properties.hierarchyIdentifier, cloud = properties.environmentName  
        ```

# [GCP](#tab/gcp)
```bash
        resources 
        | where type == "microsoft.security/securityconnectors" 
        | extend source = tostring(properties.environmentName)  
        | where source == "GCP" 
        | project name, subscriptionId, resourceGroup, projectId = properties.hierarchyIdentifier, cloud = properties.environmentName  
        ```

---
    3. Select **Run query**.
    4. Toggle formatted results to **On**.

        [![Screenshot that shows where the formatted results toggle is located on the screen.](media/assign-access-to-workload/formatted-results.png)](media/assign-access-to-workload/formatted-results.png#lightbox)
    5. Select the relevant subscription and resource group to locate the relevant security connector.

# [AWS](#tab/aws)
```bash
        resources 
        | where type == "microsoft.security/securityconnectors" 
        | extend source = tostring(properties.environmentName)  
        | where source == "AWS" 
        | project name, subscriptionId, resourceGroup, accountId = properties.hierarchyIdentifier, cloud = properties.environmentName  
        ```

# [GCP](#tab/gcp)
```bash
        resources 
        | where type == "microsoft.security/securityconnectors" 
        | extend source = tostring(properties.environmentName)  
        | where source == "GCP" 
        | project name, subscriptionId, resourceGroup, projectId = properties.hierarchyIdentifier, cloud = properties.environmentName  
        ```

---
5. Select **Access control (IAM)**.

    [![Screenshot of a security connector resource page with Access control (IAM) highlighted in the left navigation.](media/assign-access-to-workload/control-i-am.png)](media/assign-access-to-workload/control-i-am.png#lightbox)
6. Select **+Add** &gt; **Add role assignment**.
7. Select the desired role.
8. Select **Next**.
9. Select **+ Select members**.

    ![Screenshot that shows where the button is on the screen to select the + select members button.](media/assign-access-to-workload/select-members.png)
10. Search for and select the relevant user or group.
11. Select the **Select** button.
12. Select **Next**.
13. Select **Review + assign**.
14. Review the information.
15. Select **Review + assign**.

After you set permissions on the security connector, workload owners can view Defender for Cloud recommendations for associated AWS and GCP resources.