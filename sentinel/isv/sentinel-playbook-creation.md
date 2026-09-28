---
layout: Conceptual
title: Create Playbooks for Microsoft Sentinel Solutions | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/isv/sentinel-playbook-creation
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
description: This article guides you through the process of creating and publishing playbooks for Microsoft Sentinel solutions.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: sshuster
ms.topic: how-to
ms.date: 2026-06-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 3bede6b5-97d3-b91e-4b16-058cced063e0
document_version_independent_id: 9a1902aa-a085-49e1-cce7-37237d3602e4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/isv/sentinel-playbook-creation.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/isv/sentinel-playbook-creation
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/isv/sentinel-playbook-creation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
platformId: 5a5fcba3-d846-acc0-2e7d-56f78aab9a28
---

# Create Playbooks for Microsoft Sentinel Solutions | Microsoft Learn

Playbooks in Microsoft Sentinel are sets of procedures that can respond to incidents, alerts, or specific entities. They help automate responses and can be set to run automatically when certain alerts or incidents occur. Playbooks can also be run manually.

This article uses example scenarios to walk you through the process of creating and publishing playbooks for Microsoft Sentinel solutions.

## Use cases for Microsoft Sentinel playbooks

Due to the growing number of alerts and incidents, security operations center (SOC) analysts can't manually handle everything. To maximize the benefits of Microsoft Sentinel, it's crucial to determine which automations help SOC analysts with each detection in your solution. Here are some of the common scenarios for playbooks:

- **Incident enrichment**: Enhance alerts with additional information for efficient investigation and resolution. Example: Collect more data on IP addresses associated with an incident.
- **Sync with ticketing systems**: Synchronize Microsoft Sentinel incidents with other systems (like ServiceNow) bidirectionally. Example: On incident creation, sync details with a ServiceNow ticket. For more information, see the [ServiceNow connector reference](/en-us/connectors/service-now/).
- **Automated response**: Take automated actions in response to suspicious activities. Example: Send a Teams message to the user for confirmation if a suspicious action is detected.

To understand more about potential use cases for playbooks, see [Recommended playbook use cases, templates, and examples](/en-us/azure/sentinel/automation/playbook-recommendations).

## Create and publish playbooks, for example, scenarios

Microsoft Sentinel playbooks are based on Azure Logic Apps, a cloud platform that enables the creation and execution of automated workflows with minimal to no coding. You can use the visual designer and select prebuilt operations to efficiently build workflows that integrate and manage your applications, data, services, and systems. For more information, see [What is Azure Logic Apps?](/en-us/azure/logic-apps/logic-apps-overview)

Logic Apps includes numerous out-of-the-box connectors, such as Salesforce, Office 365, and SQL Server. These connectors offer no-code options for various functions. For example, the Office 365 Outlook connector includes built-in actions for sending emails without needing any code. If the out-of-the-box connectors don't cover specific actions that a playbook requires, you need to create a custom connector.

### Scenario: Playbook that uses built-in connectors

#### Create the playbook

If your playbook doesn't require any custom actions outside the actions that the built-in connectors already provide, you can use the Logic Apps UI in Microsoft Sentinel to create the playbook. No other code is required.

For detailed instructions on how to create playbooks from the Azure portal or the Microsoft Defender portal, see [Create and manage Microsoft Sentinel playbooks](/en-us/azure/sentinel/automation/create-playbooks).

#### Generate the ARM template for the playbook

On the **Code view** tab of the Logic Apps editor, you can access the JSON Azure Resource Manager template (ARM template). Remove any organizational details, like tenant ID and subscription info, for privacy and security. Follow these steps to get a sanitized version of your playbook ARM template:

1. [Download the PowerShell script](https://aka.ms/playbook-ARM-Template-Generator).
2. Extract the folder and open **playbook\_ARM\_Template\_Generator.ps1** in Visual Studio Code, Windows PowerShell, or PowerShell Core.

    Note

    Run the script from your machine. Allow PowerShell script execution by running this command in PowerShell: `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass`.
3. Enter your Azure tenant ID when you're prompted.
4. Authenticate with your credentials, and then select **Subscription** &gt; **playbooks**.
5. Select a location on your local drive to save the sanitized ARM template as **azuredeploy.json**. The tool converts Microsoft Sentinel connections to Microsoft Software Installer (MSI) during export. For more information, see the demonstration video [Export your SOAR playbooks with ease](https://www.youtube.com/watch?v=scTtVHVzrQw).
6. Update the metadata section of the **azuredeploy.json** file with your playbook's specific details.

    [![Screenshot of playbook metadata that needs to be updated.](media/sentinel-playbook-creation/playbook-update-metadata.png)](media/sentinel-playbook-creation/playbook-update-metadata.png#lightbox)
7. We recommend that you use a managed service identity rather than a user-assigned identity for connecting Azure services (such as Microsoft Sentinel, Azure Key Vault, and Azure Storage) with playbooks. Update the authentication type under `connectionProperties` to `"ManagedServiceIdentity"`.

    [![Screenshot of playbook identity updates.](media/sentinel-playbook-creation/sentinel-playbook-identity.png)](media/sentinel-playbook-creation/sentinel-playbook-identity.png#lightbox)
8. Update `Microsoft.Web/connections` resources.

    [![Screenshot of playbook web connections metadata.](media/sentinel-playbook-creation/sentinel-playbook-web-connections.png)](media/sentinel-playbook-creation/sentinel-playbook-web-connections.png#lightbox)

For more information, see the [azuredeploy.json file on GitHub](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/ThreatXCloud/Playbooks/ThreatXPlaybooks/ThreatX-BlockIP-URL/azuredeploy.json).

### Scenario: Playbook that uses custom connectors

Custom connectors extend Azure Logic Apps by integrating with APIs or services that built-in connectors don't cover. They're useful for connecting your logic apps to specific use cases, such as:

- Internal APIs within your organization.
- Third-party services that Azure doesn't directly support.
- Custom-built applications with a REST or SOAP API.

For more information, see [Custom connectors overview](/en-us/connectors/custom-connectors).

#### Create the playbook

To create a custom connector, describe the API so that the connector understands its operations and data structures. This example uses an OpenAPI definition for the Cognitive Services Text Analytics Sentiment API. For more information on creating custom connectors, see [Create a custom connector from an OpenAPI definition](/en-us/connectors/custom-connectors/define-openapi-definition).

After you create the custom connector, you can use it to build a playbook by using Azure Logic Apps. For step-by-step instructions on how to use custom connectors in a playbook, see [Use a custom connector in a logic app workflow](/en-us/connectors/custom-connectors/use-custom-connector-logic-apps).

#### Generate the ARM template for the playbook

On the **Code view** tab of the Azure Logic Apps editor, you can access the JSON ARM template. Remove any organizational details, like tenant ID and subscription info, for privacy and security. Follow these steps to get a sanitized version of your playbook ARM template:

1. [Download the PowerShell script](https://aka.ms/playbook-ARM-Template-Generator).
2. Extract the folder and open **playbook\_ARM\_Template\_Generator.ps1** in Visual Studio Code, Windows PowerShell, or PowerShell Core.

    Note

    Run the script from your machine. Allow PowerShell script execution by running this command in PowerShell: `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass`.
3. Enter your Azure tenant ID when you're prompted.
4. Authenticate with your credentials, and then select **Subscription** &gt; **playbooks**.
5. Select a location on your local drive to save the sanitized ARM template as **azuredeploy.json**. The tool converts Microsoft Sentinel connections to MSI during export. For more information, see the demonstration video [Export your SOAR playbooks with ease](https://www.youtube.com/watch?v=scTtVHVzrQw).
6. Update the metadata section of the **azuredeploy.json** file with your playbook's specific details.

    [![Screenshot of playbook metadata that needs to be updated.](media/sentinel-playbook-creation/playbook-update-metadata.png)](media/sentinel-playbook-creation/playbook-update-metadata.png#lightbox)
7. We recommend that you use a managed service identity rather than a user-assigned identity for connecting Azure services (such as Microsoft Sentinel, Azure Key Vault, and Azure Storage) with playbooks. Update the authentication type under `connectionProperties` to `"ManagedServiceIdentity"`.

    [![Screenshot of playbook identity updates.](media/sentinel-playbook-creation/sentinel-playbook-identity.png)](media/sentinel-playbook-creation/sentinel-playbook-identity.png#lightbox)
8. Update `Microsoft.Web/connections` resources.

    [![Screenshot of playbook web connections metadata.](media/sentinel-playbook-creation/sentinel-playbook-web-connections.png)](media/sentinel-playbook-creation/sentinel-playbook-web-connections.png#lightbox)

For more information, see the [azuredeploy.json file on GitHub](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/ThreatXCloud/Playbooks/ThreatXPlaybooks/ThreatX-BlockIP-URL/azuredeploy.json).

#### Generate the ARM template for the Logic Apps custom connector

1. Go to the Azure portal.
2. Search for **Logic Apps Custom Connector**.
3. Open the connector. Under **Automation**, select **Export template**.

    [![Screenshot that shows a template to export.](media/sentinel-playbook-creation/sentinel-playbook-export-template.png)](media/sentinel-playbook-creation/sentinel-playbook-export-template.png#lightbox)
4. Select **Copy template** and save the contents in a JSON file on your local computer.
5. In the JSON that you created in step 4, remove the `runtimeUrls`, `apiDefinitions`, and `wsdlDefinition` fields.
6. Select **Overview**, and then select **Download**. This step downloads the file that contains Swagger attributes.

    [![Screenshot of selections for downloading a Swagger file.](media/sentinel-playbook-creation/sentinel-playbook-download-swagger.png)](media/sentinel-playbook-creation/sentinel-playbook-download-swagger.png#lightbox)
7. Update the JSON file that you created in step 4 with the `swagger` and `backendService` values that you obtained from the Swagger file that you downloaded in step 6.
8. Validate the `host`, `basePath`, and `schemes` parameters in the Swagger file, and update them as needed.

    [![Screenshot that shows Swagger fields.](media/sentinel-playbook-creation/sentinel-playbook-swagger-fields.png)](media/sentinel-playbook-creation/sentinel-playbook-swagger-fields.png#lightbox)
9. Update the `parameters` section of the ARM template file for the custom connector.

    [![Screenshot that shows updated parameters.](media/sentinel-playbook-creation/playbook-update-parameters.png)](media/sentinel-playbook-creation/playbook-update-parameters.png#lightbox)

For reference or comparison to determine which other fields you need to modify in the ARM template, see the [azuredeploy.json file on GitHub](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Minemeld/Playbooks/CustomConnector/MinemeldCustomConnector/azuredeploy.json).

### Directory structure for playbook and custom connector contributions

Before you make a pull request to the Microsoft Sentinel GitHub repo, follow the proper directory structure. The ARM template file must be named **azuredeploy.json**. Also include a **Readme.md** file for all custom connectors and playbooks, to detail configuration steps during and after deployment.

Here are **Readme.md** file references:

- [Custom connector Readme.md file](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/Minemeld/Playbooks/CustomConnector/MinemeldCustomConnector)
- [Playbook Readme.md file](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/Minemeld/Playbooks/MinemeldPlaybooks/Minemeld-CreateIndicator)

[![Screenshot of the playbook folder structure in GitHub.](media/sentinel-playbook-creation/playbook-folder-structure.png)](media/sentinel-playbook-creation/playbook-folder-structure.png#lightbox)

## Playbook file structure and packaging requirements

Each playbook is an Azure Logic Apps workflow exported as an ARM template. The two required files are `azuredeploy.json` and `readme.md`, placed in `Solutions/<YourSolutionName>/Playbooks/<PlaybookName>/`.

### azuredeploy.json

The `$schema` must be `https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#`. Every template requires a `PlaybookName` parameter, a `metadata` block, connection variables derived from `PlaybookName`, and workflow tags:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "PlaybookName": {
      "defaultValue": "MyProduct-EnrichIncident",
      "type": "string"
    }
  },
  "variables": {
    "AzureSentinelConnectionName": "[concat('azuresentinel-', parameters('PlaybookName'))]",
    "MyProductConnectionName": "[concat('myproduct-', parameters('PlaybookName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('PlaybookName')]",
      "tags": {
        "LogicAppsCategory": "security",
        "hidden-SentinelTemplateName": "[parameters('PlaybookName')]",
        "hidden-SentinelTemplateVersion": "1.0"
      },
      "identity": { "type": "SystemAssigned" },
      "properties": {
        "definition": { ... },
        "parameters": { ... }
      },
      "metadata": {
        "title": "MyProduct - Enrich Incident",
        "description": "Enriches a Sentinel incident with threat data from MyProduct.",
        "prerequisites": ["MyProduct API key stored in Key Vault"],
        "postDeployment": [
          "1. Authorize Logic App connections.",
          "2. Assign Sentinel Responder role to managed identity.",
          "3. Attach to an automation rule."
        ],
        "lastUpdateTime": "2026-06-01T00:00:00.000Z",
        "entities": ["IP", "Account"],
        "tags": ["Enrichment"],
        "releaseNotes": [
          { "version": "1.0", "title": "Initial release", "notes": ["Initial release."] }
        ],
        "support": { "tier": "partner" },
        "author": { "name": "Your Company" }
      }
    }
  ]
}
```

| `metadata`field | Notes |
| --- | --- |
| `title` | Playbook display name. |
| `description` | What the playbook does and which entity or incident type it acts on. |
| `prerequisites` | Array of strings listing required API keys, licenses, and role assignments. Use `["None"]` if there are none. |
| `postDeployment` | Numbered steps: authorize connections, assign roles, attach to an automation rule. |
| `lastUpdateTime` | ISO 8601 timestamp, for example `"2026-06-01T00:00:00.000Z"`. |
| `entities` | Entity types the playbook acts on, such as `"Account"`, `"IP"`, `"URL"`, `"Host"`, and `"FileHash"`. |
| `tags` | Action tags: `"Enrichment"`, `"Remediation"`, `"Response"`, `"Notification"`, `"Utilities"`. |
| `releaseNotes` | Array of `{ "version", "title", "notes": [...] }` objects. Required. |
| `support.tier` | `"community"`, `"partner"`, or `"microsoft"`. |
| `author.name` | Author display name. |

### Trigger type

The playbook can be triggered by either a Sentinel incident or an individual alert. The two trigger types have different use cases and are implemented in different ways:

| - | Incident trigger | Alert trigger |
| --- | --- | --- |
| **When it fires** | When a Sentinel incident is created or updated | When an individual alert fires (before grouping into an incident) |
| **Attached via** | Automation rule | Analytics rule → automated response |
| **Recommended for** | Most use cases. Richer context, easier to write | Legacy scenarios |
| **ARM trigger type** | `ApiConnectionWebhook` with `sentinel-incident-trigger` body | `ApiConnectionWebhook` with `sentinel-alert-trigger` body |

The following directory structures are valid for playbooks with a single trigger type or both trigger types. The ARM template file must be named `azuredeploy.json`. Include a `readme.md` file at the playbook root to detail configuration steps during and after deployment.

```
Solutions/<YourSolutionName>/Playbooks/
└── <PlaybookName>/
    ├── azuredeploy.json
    └── readme.md
```

The layout below uses both trigger types. Each variant gets its own ARM template; one `readme.md` at the playbook root covers both:

```
└── <PlaybookName>/
    ├── incident-trigger/
    │   └── azuredeploy.json
    ├── alert-trigger/
    │   └── azuredeploy.json
    └── readme.md
```

Caution

Common ARM-TTK failures in playbook PRs include the following:

- Missing `PlaybookName` parameter. The workflow resource `name` must be `"[parameters('PlaybookName')]"`
- Connection names not derived from `PlaybookName`. Use `"[concat('azuresentinel-', parameters('PlaybookName'))]"`
- Wrong `$schema`. Use `2019-04-01`, not the older `2015-01-01`
- Hardcoded subscription IDs, tenant IDs, or resource group names. Use `subscription().subscriptionId` and `resourceGroup().location`
- Missing `releaseNotes` in `metadata`

### readme.md

The readme.md file is validated during PR review. Missing sections are consistently flagged as blockers. Copy and fill in the template below:

```markdown
# <PlaybookName>

<One sentence describing what the playbook does and which entity or incident type it acts on.>

## Quick Deployment

**Deploy with incident trigger** (recommended)

After deployment, attach this playbook to an **automation rule** so it runs when the incident is created.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FSolutions%2F<YourSolution>%2FPlaybooks%2F<PlaybookName>%2Fincident-trigger%2Fazuredeploy.json)
[![Deploy to Azure Gov](https://aka.ms/deploytoazuregovbutton)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FSolutions%2F<YourSolution>%2FPlaybooks%2F<PlaybookName>%2Fincident-trigger%2Fazuredeploy.json)

**Deploy with alert trigger**

After deployment, attach this playbook to an **analytics rule** under Automated response.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FSolutions%2F<YourSolution>%2FPlaybooks%2F<PlaybookName>%2Falert-trigger%2Fazuredeploy.json)
[![Deploy to Azure Gov](https://aka.ms/deploytoazuregovbutton)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FSolutions%2F<YourSolution>%2FPlaybooks%2F<PlaybookName>%2Falert-trigger%2Fazuredeploy.json)

## Prerequisites

<List required API keys, licenses, or custom connectors that must be deployed first. Use "None" if there are no prerequisites.>

## Post-deployment

1. Assign the **Microsoft Sentinel Responder** role to the Logic App's managed identity.
2. Authorize Logic App API connections: open each connection resource → **Edit API connection** → **Authorize** → sign in.
3. <If applicable: grant Graph/REST API permissions to the managed identity's service principal object ID.>
4. Attach the playbook to an automation rule (incident trigger) or analytics rule automated response (alert trigger).

## Screenshots

<Add at least one screenshot of the Logic App designer view.>
```

For a single-trigger playbook, include only the relevant button pair and omit the trigger subfolder from the path (`...%2FPlaybooks%2F<PlaybookName>%2Fazuredeploy.json`).

| Section | PR failure if missing? | Reason |
| --- | --- | --- |
| Quick Deployment buttons | Yes | Reviewers flag missing deploy buttons on every submission |
| Prerequisites | Yes | At least `None` must be present |
| Post-deployment steps | Yes | Missing role assignment steps are the most common blocker |
| Screenshots | Yes |  |

### Reference examples

- [Microsoft Entra ID — Block-AADUser (incident + alert + entity triggers)](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/Microsoft%20Entra%20ID/Playbooks/Block-AADUser)
- [CrowdStrike Falcon — CrowdStrike_Base (Key Vault + base playbook pattern)](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/CrowdStrike%20Falcon%20Endpoint%20Protection/Playbooks/CrowdStrike_Base)
- [Okta Single Sign-On — OktaCustomConnector (custom connector ARM template)](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/Okta%20Single%20Sign-On/Playbooks/OktaCustomConnector)