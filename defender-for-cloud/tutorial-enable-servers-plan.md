---
layout: Conceptual
title: Protect your servers with Defender for Servers - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/tutorial-enable-servers-plan
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
description: Learn how to enable the Defender for Servers plan in Microsoft Defender for Cloud to protect your virtual machines and reduce security risks.
ms.topic: install-set-up-deploy
ms.date: 2025-09-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 75b6fc97-ec44-e336-d321-13068c735fe6
document_version_independent_id: 70172c2f-5e5d-22e9-5624-72a2afb7f192
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/tutorial-enable-servers-plan.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/tutorial-enable-servers-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/tutorial-enable-servers-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: fa4d8100-8f51-ca2b-df40-0cb1bdaf26ce
---

# Protect your servers with Defender for Servers - Microsoft Defender for Cloud | Microsoft Learn

The Defender for Servers plan in Microsoft Defender for Cloud protects Windows and Linux virtual machines (VMs) that run in Azure, Amazon Web Service (AWS), Google Cloud Platform (GCP), and in on-premises environments. Defender for Servers provides recommendations to improve the security posture of machines and protects machines against security threats.

This article helps you deploy a Defender for Servers plan.

Note

After you enable a plan, a 30-day trial period begins. You can't stop, pause, or extend this trial period. To get the most out of the full 30-day trial, [plan your evaluation goals](plan-defender-for-servers).

## Prerequisites

| **Requirement** | **Details** |
| --- | --- |
| **Plan your deployment** | Review the [Defender for Servers planning guide](plan-defender-for-servers).[Check permissions needed](plan-defender-for-servers-roles) to deploy and work with the plan, [choose a plan and deployment scope](plan-defender-for-servers-select-plan), or check out the [differences between the Defender for Servers plans](defender-for-servers-overview#defender-for-servers-plans), and [understand how data is collected and stored](plan-defender-for-servers-data-workspace). |
| **Compare plan features** | [Understand and compare](defender-for-servers-overview) Defender for Servers plan features. |
| **Review pricing** | Review Defender for Servers pricing on the [Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator). |
| **Get an Azure subscription** | You need a Microsoft Azure subscription. [Sign up for a free one](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) if you need to. |
| **Turn on Defender for Cloud** | Make sure Defender for Cloud is [available in the subscription](connect-azure-subscription). |
| **Onboard AWS/GCP machines** | To protect AWS and GCP machines, connect [AWS accounts](quickstart-onboard-aws) and [GCP projects](quickstart-onboard-gcp) to Defender for Cloud.By default the connection process onboards machines as Azure Arc-enabled VMs. |
| **Onboard on-premises machines** | [Onboard on-premises machines as Azure Arc VMs](quickstart-onboard-machines) for full functionality in Defender for Servers. If you onboard on-premises machines by [directly installing the Defender for Endpoint agent](onboard-machines-with-defender-for-endpoint) instead of onboarding Azure Arc, only Plan 1 functionality is available. In Defender for Servers Plan 2, you get only the premium Defender Vulnerability Management features in addition to Plan 1 functionality. |
| **Review support requirements** | Check [Defender for Servers requirements and support](support-matrix-defender-for-servers) information. |
| **Take advantage of 500 MB free data ingestion** | When Defender for Servers Plan 2 is enabled, a benefit of free 500-MB data ingestion is available for specific data types. [Learn about requirements and set up free data ingestion](data-ingestion-benefit) |
| **Defender integration** | Defender for Endpoint and Defender for Vulnerability Management are integrated by default in Defender for Cloud. When you enable Defender for Servers, you give consent for the Defender for Servers plan to access Defender for Endpoint data related to vulnerabilities, installed software, and endpoint alerts. |
| **Enable at resource level** | Although we recommend enabling Defender for Servers for a subscription, you can enable Defender for Servers at resource level if needed, for Azure VMs, Azure Arc-enabled servers, and Azure Virtual Machine Scale Sets. You can enable Plan 1 at the resource level. You can disable Plan 1 and Plan 2 at the resource level. |

## Enable on Azure, AWS, or GCP

You can enable a Defender for Servers plan for an Azure subscription, AWS account, or GCP project.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. In the Defender for Cloud menu, select **Environment settings**.
4. Select the relevant Azure subscription, AWS account, or GCP project.
5. On the Defender plans page, toggle the Servers switch to **On**.

    [![Screenshot that shows you how to toggle the Defender for Servers plan to on.](media/tutorial-enable-servers-plan/enable-servers-plan.png)](media/tutorial-enable-servers-plan/enable-servers-plan.png#lightbox)
6. By default, this turns on Defender for Servers Plan 2. If you want to switch the plan, select **Change plans**.

    [![Screenshot that shows you where on the environment settings page to select change plans.](media/tutorial-enable-servers-plan/servers-change-plan.png)](media/tutorial-enable-servers-plan/servers-change-plan.png#lightbox)
7. In the popup window, select **Plan 2** or **Plan 1**.

    [![Screenshot of the popup where you can select plan 1 or plan 2.](media/tutorial-enable-servers-plan/servers-plan-selection.png)](media/tutorial-enable-servers-plan/servers-plan-selection.png#lightbox)
8. Select **Confirm**.
9. Select **Save**.

After enabling the plan, you can [configure the features of the plan](configure-servers-coverage) to suit your needs.

## Disable Defender for Servers on a subscription

1. In **Microsoft Defender for Cloud**, select **Environment settings**.
2. Toggle the plan switch to **Off**.

Note

If you enabled Defender for Servers Plan 2 on a Log Analytics workspace, you need to disable it explicitly. To do that, navigate to the plans page for the workspace and toggle the switch to **Off**.

## Enable Defender for Servers at the resource level

Although we recommend enabling the plan for an entire Azure subscription, you might need to mix plans, exclude specific resources, or enable Defender for Servers on specific machines only. To do this, you can enable or disable Defender for Servers at the resource level. Review [deployment scope options](plan-defender-for-servers-select-plan#decide-on-deployment-scope) before you start.

## Configure on individual machines

Enable or disable the plan on specific machines.

### Enable Plan 1 on a machine using the REST API

1. To enable Plan 1 for the machine, in [Update Pricing](/en-us/rest/api/defenderforcloud-composite/pricings/update?view=rest-defenderforcloud-composite-latest&amp;tabs=HTTP&amp;preserve-view=true#update-pricing-on-resource-%28example-for-virtualmachines-plan%29), create a PUT request with the endpoint.
2. In the PUT request, replace the subscriptionId, resourceGroupName, and machineName in the endpoint URL with your own settings.

    ```rest
        PUT
        https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{machineName}/providers/Microsoft.Security/pricings/virtualMachines?api-version=2024-01-01
    ```
3. Add this request body.

    ```json
    {
     "properties": {
    "pricingTier": "Standard",
    "subPlan": "P1"
      }
    }
    ```

### Disable the plan on a machine using the REST API

1. To disable Defender for Servers at the machine level, create a PUT request with the endpoint URL.
2. In the PUT request, replace the subscriptionId, resourceGroupName, and machineName in the endpoint URL with your own settings.

    ```rest
        PUT
        https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{machineName}/providers/Microsoft.Security/pricings/virtualMachines?api-version=2024-01-01
    ```
3. Add this request body.

    ```json
    {
     "properties": {
    "pricingTier": "Free",
      }
    }
    ```

### Remove the resource-level configuration using the REST API

1. To remove the machine-level configuration using the REST API, create a DELETE request with the endpoint URL.
2. In the DELETE request, replace the subscriptionId, resourceGroupName, and machineName in the endpoint URL with your own settings.

    ```rest
        DELETE
        https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{machineName}/providers/Microsoft.Security/pricings/virtualMachines?api-version=2024-01-01
    ```

### Enable Plan 1 using a script

### Enable Plan 1 with a script

1. [Download and save this file](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/Defender%20for%20Servers%20on%20resource%20level) as a PowerShell file.
2. Run the downloaded script.
3. Customize as needed. Select resources by **tag**.
4. Follow the rest of the on-screen instructions.

### Enable Plan 1 using Azure Policy (on resource tag)

1. Sign in to the Azure portal and navigate to the **Policy** dashboard.
2. In the **Policy** dashboard, select **Definitions** from the left-side menu.
3. In the **Security Center – Granular Pricing** category, search for and then select [Configure Azure Defender for Servers to be enabled (with 'P1' subplan) for all resources with the selected tag](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9e4879d9-c2a0-4e40-8017-1a5a5327c843). This policy enables Defender for Servers Plan 1 on all resources (Azure VMs, Virtual Machine Scale Sets, and Azure Arc-enabled servers) under the assignment scope.
4. Select the policy and review it.
5. Select **Assign** and edit the assignment details according to your needs.
6. In the **Parameters** tab, clear **Only show parameters that need input or review**.
7. In **Inclusion Tag Name**, enter the custom tag name. Enter the tag's value in the **Inclusion Tag Values** array.
8. In the **Remediation** tab, select **Create a remediation task**.
9. Edit all details, select **Review + create**, and then select **Create**.

Note

Defender for Servers doesn't require a specific tag name or value for onboarding or exclusion. Use any tag your organization chooses and configure your Azure Policy or script to match it.

### Disable the plan using a script

1. [Download and save this script](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/Defender%20for%20Servers%20on%20resource%20level) as a PowerShell file.
2. Run the downloaded script.
3. Customize as needed. Select resources by **tag**.
4. Follow the rest of the on-screen instructions.

### Disable the plan using Azure Policy (for resource tag)

1. Sign in to the Azure portal and navigate to the **Policy** dashboard.
2. In the **Policy** dashboard, select **Definitions** from the left-side menu.
3. In the **Security Center – Granular Pricing** category, search for and then select [Configure Azure Defender for Servers to be disabled for resources (resource level) with the selected tag](https://ms.portal.azure.com/#view/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F080fedce-9d4a-4d07-abf0-9f036afbc9c8). This policy disables Defender for Servers on all resources (Azure VMs, Virtual Machine Scale Sets, and Azure Arc-enabled servers) under the assignment scope based on the tag you defined.
4. Select the policy and review it.
5. Select **Assign** and edit the assignment details according to your needs.
6. In the **Parameters** tab, clear **Only show parameters that need input or review**.
7. In **Inclusion Tag Name**, enter the custom tag name. Enter the tag's value in the **Inclusion Tag Values** array.
8. In the **Remediation** tab, select **Create a remediation task**.
9. Edit all details, select **Review + create**, and then select **Create**.

### Remove the per-resource configuration using a script (tag)

1. [Download and save this script](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/Defender%20for%20Servers%20on%20resource%20level) as a PowerShell file.
2. Run the downloaded script.
3. Customize as needed. Select resources by **tag**.
4. Follow the rest of the on-screen instructions.

## View your current coverage

Defender for Cloud provides access to [workbooks](custom-dashboards-azure-workbooks) through [Azure workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview). Workbooks are customizable reports that provide insights into your security posture.

The [coverage workbook](custom-dashboards-azure-workbooks#coverage-workbook) helps you understand your current coverage by showing which plans are enabled on your subscriptions and resources.