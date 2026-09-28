---
layout: Conceptual
title: Create a security automation for specific security alerts by using an Azure Resource Manager template (ARM template) or Bicep - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/quickstart-automation-alert
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
description: Learn how to create a Microsoft Defender for Cloud automation to trigger a logic app, which will be triggered by specific Defender for Cloud alerts by using an Azure Resource Manager template (ARM template) or Bicep.
ms.topic: quickstart
ms.custom: subject-armqs, mode-arm, devx-track-bicep, devx-track-arm-template
ms.date: 2025-05-18T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: b0abdda4-7441-c005-88b4-bfe088a1e778
document_version_independent_id: e8478815-1ca7-19ed-ea58-c18b662a3cc9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/quickstart-automation-alert.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
interactive_type: azurepowershell,azurecli
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/quickstart-automation-alert
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/quickstart-automation-alert.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
platformId: 225053f0-2bbd-7be6-aefa-836e2405f117
---

# Create a security automation for specific security alerts by using an Azure Resource Manager template (ARM template) or Bicep - Microsoft Defender for Cloud | Microsoft Learn

In this quickstart, you'll learn how to use an Azure Resource Manager template (ARM template) or a Bicep file to create a workflow automation. The workflow automation will trigger a logic app when specific security alerts are received by Microsoft Defender for Cloud.

## Prerequisites

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

For a list of the roles and permissions required to work with Microsoft Defender for Cloud's workflow automation feature, see [workflow automation](workflow-automations).

The examples in this quickstart assume you have an existing Logic App. To deploy the example, you pass in parameters that contain the logic app name and resource group. For information about deploying a logic app, see [Quickstart: Create and deploy a Consumption logic app workflow in multitenant Azure Logic Apps with Bicep](/en-us/azure/logic-apps/quickstart-create-deploy-bicep) or [Quickstart: Create and deploy a Consumption logic app workflow in multitenant Azure Logic Apps with an ARM template](/en-us/azure/logic-apps/quickstart-create-deploy-azure-resource-manager-template).

## ARM template tutorial

An [Azure Resource Manager template](/en-us/azure/azure-resource-manager/templates/overview) is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax. You describe your intended deployment without writing the sequence of programming commands to create the deployment.

If your environment meets the prerequisites and you're familiar with using ARM templates, select the **Deploy to Azure** button. The template will open in the Azure portal.

[![Button to deploy the Resource Manager template to Azure.](../../reusable-content/ce-skilling/azure/media/template-deployments/deploy-to-azure-button.svg)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2fAzure%2fazure-quickstart-templates%2fmaster%2fquickstarts%2fmicrosoft.security%2fsecuritycenter-create-automation-for-alertnamecontains%2fazuredeploy.json)

### Review the template

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/securitycenter-create-automation-for-alertnamecontains/).

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "metadata": {
    "_generator": {
      "name": "bicep",
      "version": "0.5.6.12127",
      "templateHash": "5191074894407113732"
    }
  },
  "parameters": {
    "automationName": {
      "type": "string",
      "maxLength": 24,
      "minLength": 3
    },
    "location": {
      "type": "string",
      "defaultValue": "[resourceGroup().location]",
      "metadata": {
        "description": "Location for the automation"
      }
    },
    "logicAppName": {
      "type": "string",
      "minLength": 3
    },
    "logicAppResourceGroupName": {
      "type": "string",
      "minLength": 3
    },
    "subscriptionId": {
      "type": "string",
      "defaultValue": "[subscription().subscriptionId]",
      "metadata": {
        "description": "The Azure resource GUID id of the subscription"
      }
    },
    "alertSettings": {
      "type": "object",
      "metadata": {
        "description": "The alert settings object used for deploying the automation"
      }
    }
  },
  "variables": {
    "automationDescription": "automation description for subscription {0}",
    "scopeDescription": "automation scope for subscription {0}"
  },
  "resources": [
    {
      "type": "Microsoft.Security/automations",
      "apiVersion": "2019-01-01-preview",
      "name": "[parameters('automationName')]",
      "location": "[parameters('location')]",
      "properties": {
        "description": "[format(variables('automationDescription'), parameters('subscriptionId'))]",
        "isEnabled": true,
        "actions": [
          {
            "actionType": "LogicApp",
            "logicAppResourceId": "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]",
            "uri": "[listCallbackURL(resourceId(parameters('subscriptionId'), parameters('logicAppResourceGroupName'), 'Microsoft.Logic/workflows/triggers', parameters('logicAppName'), 'manual'), '2019-05-01').value]"
          }
        ],
        "scopes": [
          {
            "description": "[format(variables('scopeDescription'), parameters('subscriptionId'))]",
            "scopePath": "[subscription().id]"
          }
        ],
        "sources": [
          {
            "copy": [
              {
                "name": "ruleSets",
                "count": "[length(range(0, length(parameters('alertSettings').alertSeverityMapping)))]",
                "input": {
                  "rules": [
                    {
                      "propertyJPath": "[parameters('alertSettings').alertSeverityMapping[range(0, length(parameters('alertSettings').alertSeverityMapping))[copyIndex('ruleSets')]].jpath]",
                      "propertyType": "String",
                      "expectedValue": "[parameters('alertSettings').alertSeverityMapping[range(0, length(parameters('alertSettings').alertSeverityMapping))[copyIndex('ruleSets')]].expectedValue]",
                      "operator": "[parameters('alertSettings').alertSeverityMapping[range(0, length(parameters('alertSettings').alertSeverityMapping))[copyIndex('ruleSets')]].operator]"
                    },
                    {
                      "propertyJPath": "Severity",
                      "propertyType": "String",
                      "expectedValue": "[parameters('alertSettings').alertSeverityMapping[range(0, length(parameters('alertSettings').alertSeverityMapping))[copyIndex('ruleSets')]].severity]",
                      "operator": "Equals"
                    }
                  ]
                }
              }
            ],
            "eventSource": "Alerts"
          }
        ]
      }
    }
  ]
}
```

### Relevant resources

- [**Microsoft.Security/automations**](/en-us/azure/templates/microsoft.security/automations): The automation that will trigger the logic app, upon receiving a Microsoft Defender for Cloud alert that contains a specific string.
- [**Microsoft.Logic/workflows**](/en-us/azure/templates/microsoft.logic/workflows): An empty triggerable Logic App.

For other Defender for Cloud quickstart templates, see these [community contributed templates](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Security&amp;pageNumber=1&amp;sort=Popular).

### Deploy the template

- **PowerShell**:

    ```azurepowershell
    New-AzResourceGroup -Name <resource-group-name> -Location <resource-group-location> #use this command when you need to create a new resource group for your deployment
    New-AzResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.security/securitycenter-create-automation-for-alertnamecontains/azuredeploy.json
    ```
- **CLI**:

    ```azurecli
    az group create --name <resource-group-name> --location <resource-group-location> #use this command when you need to create a new resource group for your deployment
    az deployment group create --resource-group <my-resource-group> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.security/securitycenter-create-automation-for-alertnamecontains/azuredeploy.json
    ```
- **Portal**:

    [![Button to deploy the Resource Manager template to Azure.](../../reusable-content/ce-skilling/azure/media/template-deployments/deploy-to-azure-button.svg)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2fAzure%2fazure-quickstart-templates%2fmaster%2fquickstarts%2fmicrosoft.security%2fsecuritycenter-create-automation-for-alertnamecontains%2fazuredeploy.json)

    To find more information about this deployment option, see [Use a deployment button to deploy templates from GitHub repository](/en-us/azure/azure-resource-manager/templates/deploy-to-azure-button).

### Review deployed resources

Use the Azure portal to check the workflow automation has been deployed.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Select **filter**.
4. Select the specific subscription on which you deployed the new workflow automation.
5. From Microsoft Defender for Cloud's menu, open **workflow automation** and check for your new automation. [![List of configured automations.](media/quickstart-automation-alert/validating-template-run.png)](media/quickstart-automation-alert/validating-template-run.png#lightbox)

    Tip

    If you have many workflow automations on your subscription, use the **filter by name** option.

### Clean up resources

When no longer needed, delete the workflow automation using the Azure portal.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Select **filter**.
4. Select the specific subscription on which you deployed the new workflow automation.
5. From Microsoft Defender for Cloud's menu, open **workflow automation** and find the automation to be deleted. [![Steps for removing a workflow automation.](media/quickstart-automation-alert/deleting-workflow-automation.png)](media/quickstart-automation-alert/deleting-workflow-automation.png#lightbox)
6. Select the checkbox for the item to be deleted.
7. From the toolbar, select **Delete**.

## Bicep tutorial

[Bicep](/en-us/azure/azure-resource-manager/bicep/overview) is a domain-specific language (DSL) that uses declarative syntax to deploy Azure resources. It provides concise syntax, reliable type safety, and support for code reuse. Bicep offers the best authoring experience for your infrastructure-as-code solutions in Azure.

### Review the Bicep file

The Bicep file used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/securitycenter-create-automation-for-alertnamecontains/).

```bicep
@minLength(3)
@maxLength(24)
param automationName string

@description('Location for the automation')
param location string = resourceGroup().location

@minLength(3)
param logicAppName string

@minLength(3)
param logicAppResourceGroupName string

@description('The Azure resource GUID id of the subscription')
param subscriptionId string = subscription().subscriptionId

@description('The alert settings object used for deploying the automation')
param alertSettings object

var automationDescription = 'automation description for subscription {0}'
var scopeDescription = 'automation scope for subscription {0}'

resource automation 'Microsoft.Security/automations@2019-01-01-preview' = {
  name: automationName
  location: location
  properties: {
    description: format(automationDescription, subscriptionId)
    isEnabled: true
    actions: [
      {
        actionType: 'LogicApp'
        logicAppResourceId: resourceId('Microsoft.Logic/workflows', logicAppName)
        uri: listCallbackURL(resourceId(subscriptionId, logicAppResourceGroupName, 'Microsoft.Logic/workflows/triggers', logicAppName, 'manual'), '2019-05-01').value
      }
    ]
    scopes: [
      {
        description: format(scopeDescription, subscriptionId)
        scopePath: subscription().id
      }
    ]
    sources: [
      {
        eventSource: 'Alerts'
        ruleSets: [for j in range(0, length(alertSettings.alertSeverityMapping)): {
          rules: [
            {
              propertyJPath: alertSettings.alertSeverityMapping[j].jpath
              propertyType: 'String'
              expectedValue: alertSettings.alertSeverityMapping[j].expectedValue
              operator: alertSettings.alertSeverityMapping[j].operator
            }
            {
              propertyJPath: 'Severity'
              propertyType: 'String'
              expectedValue: alertSettings.alertSeverityMapping[j].severity
              operator: 'Equals'
            }
          ]
        }]
      }
    ]
  }
}
```

### Relevant resources

- [**Microsoft.Security/automations**](/en-us/azure/templates/microsoft.security/automations): The automation that will trigger the logic app, upon receiving a Microsoft Defender for Cloud alert that contains a specific string.
- [**Microsoft.Logic/workflows**](/en-us/azure/templates/microsoft.logic/workflows): An empty triggerable Logic App.

For other Defender for Cloud quickstart templates, see these [community contributed templates](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Security&amp;pageNumber=1&amp;sort=Popular).

### Deploy the Bicep file

1. Save the Bicep file as **main.bicep** to your local computer.
2. Deploy the Bicep file using either Azure CLI or Azure PowerShell.

# [CLI](#tab/CLI)
```azurecli
    az group create --name exampleRG --location eastus
    az deployment group create --resource-group exampleRG --template-file main.bicep --parameters automationName=<automation-name> logicAppName=<logic-name> logicAppResourceGroupName=<group-name> alertSettings={alert-settings}
    ```

# [PowerShell](#tab/PowerShell)
```azurepowershell
    New-AzResourceGroup -Name exampleRG -Location eastus
    New-AzResourceGroupDeployment -ResourceGroupName exampleRG -TemplateFile ./main.bicep -automationName "<automation-name>" -logicAppName "<logic-name>" -logicAppResourceGroupName "<group-name>" -alertSettings "{alert-settings}"
    ```

---

    You're required to enter the following parameters:

    - **automationName**: Replace **&lt;automation-name&gt;** with the name of the automation. It has a minimum length of three characters and a maximum length of 24 characters.
    - **logicAppName**: Replace **&lt;logic-name&gt;** with the name of the logic app. It has a minimum length of three characters.
    - **logicAppResourceGroupName**: Replace **&lt;group-name&gt;** with the name of the resource group in which the resources are located. It has a minimum length of three characters.
    - **alertSettings**: Replace **{alert-settings}** with the alert settings object used for deploying the automation.

    Note

    When the deployment finishes, you should see a message indicating the deployment succeeded.

### Review deployed resources

Use the Azure portal, Azure CLI, or Azure PowerShell to list the deployed resources in the resource group.

# [CLI](#tab/CLI)
```azurecli
az resource list --resource-group exampleRG
```

# [PowerShell](#tab/PowerShell)
```azurepowershell
Get-AzResource -ResourceGroupName exampleRG
```

---

### Clean up resources

When no longer needed, use the Azure portal, Azure CLI, or Azure PowerShell to delete the resource group and all of its resources.

# [CLI](#tab/CLI)
```azurecli
az group delete --name exampleRG
```

# [PowerShell](#tab/PowerShell)
```azurepowershell
Remove-AzResourceGroup -Name exampleRG
```

---