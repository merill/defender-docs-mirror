---
layout: Conceptual
title: Data connector definitions reference for the Codeless Connector Framework - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/data-connector-ui-definitions-reference
breadcrumb_path: breadcrumb/toc.json
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
description: This article provides a supplemental reference for creating the connectorUIConfig JSON section for the Data Connector Definitions API as part of the Codeless Connector Framework.
services: sentinel
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: krishsa
ms.topic: reference
ms.date: 2023-11-13T00:00:00.0000000Z
ms.custom:
- sfi-image-nochange
- sfi-ga-nochange
locale: en-us
document_id: 7bc2ff0b-8de4-9517-74f2-b0c9951cd037
document_version_independent_id: 69221bb1-be24-b37b-01b7-a37d05071f69
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/data-connector-ui-definitions-reference.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/data-connector-ui-definitions-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/data-connector-ui-definitions-reference.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/3439c05e-99ce-45d1-b266-9322ea647316
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/23472108-2f8d-47d2-b07a-c0b1e9d492b6
platformId: 019311a7-54c9-32e0-fca7-39583fe73e81
---

# Data connector definitions reference for the Codeless Connector Framework - Microsoft Sentinel | Microsoft Learn

To create a data connector with the Codeless Connector Framework (CCF), use this document as a supplement to the [Microsoft Sentinel REST API for Data Connector Definitions](/en-us/rest/api/securityinsights/data-connector-definitions) reference docs. Specifically this reference document expands on the following section:

- `connectorUiConfig` - defines the visual elements and text displayed on the data connector page in Microsoft Sentinel.

For more information, see [Create a codeless connector](create-codeless-connector).

## Data connector definitions - Create or update

Reference the Create Or Update operation in the REST API docs to find the latest stable or preview API version. Only the `update` operation requires the `etag` value.

**PUT** method

```http
https://management.azure.com/subscriptions/{{subscriptionId}}/resourceGroups/{{resourceGroupName}}/providers/Microsoft.OperationalInsights/workspaces/{{workspaceName}}/providers/Microsoft.SecurityInsights/dataConnectorDefinitions/{{dataConnectorDefinitionName}}?api-version={{apiVersion}}
```

## URI parameters

For more information about the latest API version, see [Data Connector Definitions - Create or Update URI Parameters](/en-us/rest/api/securityinsights/data-connector-definitions/create-or-update#uri-parameters)

| Name | Description |
| --- | --- |
| **dataConnectorDefinitionName** | The data connector definition must be a unique name and is the same as the `name` parameter in the request body. |
| **resourceGroupName** | The name of the resource group, not case sensitive. |
| **subscriptionId** | The ID of the target subscription. |
| **workspaceName** | The *name* of the workspace, not the ID.Regex pattern: `^[A-Za-z0-9][A-Za-z0-9-]+[A-Za-z0-9]$` |
| **api-version** | The API version to use for this operation. |

## Request body

The request body for creating a CCF data connector definition with the API has the following structure:

```json
{
    "kind": "Customizable",
    "properties": {
        "connectorUIConfig": {}
    }
}
```

**dataConnectorDefinition** has the following properties:

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| **Kind** | True | String | `Customizable` for API polling data connector or `Static` otherwise |
| properties.**connectorUiConfig** | True | Nested JSONconnectorUiConfig | The UI configuration properties of the data connector |

## Configure your connector's user interface

This section describes the configuration options available to customize the user interface of the data connector page.

The following screenshot shows a sample data connector page, highlighted with numbers that correspond to notable areas of the user interface.

![Screenshot of a sample data connector page with sections labeled 1 through 9.](isv/media/create-codeless-connector/sample-data-connector-page.png)

Each of the following elements of the `connectorUiConfig` section needed to configure the user interface correspond to the CustomizableConnectorUiConfig portion of the API.

| Field | Required | Type | Description | Screenshot notable area # |
| --- | --- | --- | --- | --- |
| **title** | True | string | Title displayed in the data connector page | 1 |
| **id** |  | string | Sets custom connector ID for internal usage |  |
| **logo** |  | string | Path to image file in SVG format. If no value is configured, a default logo is used. | 2 |
| **publisher** | True | string | The provider of the connector | 3 |
| **descriptionMarkdown** | True | string in markdown | A description for the connector with the ability to add markdown language to enhance it. | 4 |
| **sampleQueries** | True | Nested JSONsampleQueries | Queries for the customer to understand how to find the data in the event log. |  |
| **graphQueries** | True | Nested JSONgraphQueries | Queries that present data ingestion over the last two weeks.Provide either one query for all of the data connector's data types, or a different query for each data type. | 5 |
| **graphQueriesTableName** |  | Sets the name of the table the connector inserts data to. This name can be used in other queries by specifying `{{graphQueriesTableName}}` placeholder in `graphQueries` and `lastDataReceivedQuery` values. |  |  |
| **dataTypes** | True | Nested JSONdataTypes | A list of all data types for your connector, and a query to fetch the time of the last event for each data type. | 6 |
| **connectivityCriteria** | True | Nested JSONconnectivityCriteria | An object that defines how to verify if the connector is connected. | 7 |
| **availability** |  | Nested JSONavailability | An object that defines the availability status of the connector. |  |
| **permissions** | True | Nested JSONpermissions | The information displayed under the **Prerequisites** section of the UI, which lists the permissions required to enable or disable the connector. | 8 |
| **instructionSteps** | True | Nested JSONinstructions | An array of widget parts that explain how to install the connector, and actionable controls displayed on the **Instructions** tab. | 9 |
| **isConnectivityCriteriasMatchSome** |  | Boolean | A boolean indicating whether to use 'OR'(SOME) or 'AND' between ConnectivityCriteria items. |  |

### connectivityCriteria

| Field | Required | Type | Description |
| --- | --- | --- | --- |
| Type | True | String | One of the two following options: `HasDataConnectors` – this value is best for API polling data connectors such as the CCF. The connector is considered connected with at least one active connection.`isConnectedQuery` – this value is best for other types of data connectors. The connector is considered connected when the provided query returns data. |
| Value | True when type is `isConnectedQuery` | String | A query to determine if data is received within a certain time period. For example: `CommonSecurityLog | where DeviceVendor == \"Vectra Networks\"\n| where DeviceProduct == \"X Series\"\n  | summarize LastLogReceived = max(TimeGenerated)\n | project IsConnected = LastLogReceived > ago(7d)"` |

### dataTypes

| Array Value | Type | Description |
| --- | --- | --- |
| **name** | String | A meaningful description for the`lastDataReceivedQuery`, including support for the `graphQueriesTableName` variable. Example: `{{graphQueriesTableName}}` |
| **lastDataReceivedQuery** | String | A KQL query that returns one row, and indicates the last time data was received, or no data if there are no results. Example: `{{graphQueriesTableName}}\n | summarize Time = max(TimeGenerated)\n | where isnotempty(Time)` |

### graphQueries

Defines a query that presents data ingestion over the last two weeks.

Provide either one query for all of the data connector's data types, or a different query for each data type.

| Array Value | Type | Description |
| --- | --- | --- |
| **metricName** | String | A meaningful name for your graph. Example: `Total data received` |
| **legend** | String | The string that appears in the legend to the right of the chart, including a variable reference.Example: `{{graphQueriesTableName}}` |
| **baseQuery** | String | The query that filters for relevant events, including a variable reference. Example: `TableName_CL | where ProviderName == "myprovider"` or `{{graphQueriesTableName}}` |

### availability

| Field | Required | Type | Description |
| --- | --- | --- | --- |
| **status** |  | Integer | The availability status of the connector.Available = 1Feature Flag = 2Coming Soon = 3Internal = 4 |
| **isPreview** |  | Boolean | A boolean indicating whether the connector is in preview mode. |

### permissions

| Array value | Type | Description |
| --- | --- | --- |
| **customs** | String | Describes any custom permissions required for your data connection, in the following syntax: `{``"name":`string`,``"description":`string`}`Example: The **customs** value displays in Microsoft Sentinel **Prerequisites** section with a blue informational icon. In the GitHub example, this value correlates to the line **GitHub API personal token Key: You need access to GitHub personal token...** |
| **licenses** | ENUM | Defines the required licenses, as one of the following values: `OfficeIRM`,`OfficeATP`, `Office365`, `AadP1P2`, `Mcas`, `Aatp`, `Mdatp`, `Mtp`, `IoT`Example: The **licenses** value displays in Microsoft Sentinel as: **License: Required Azure AD Premium P2** |
| **resourceProvider** | resourceProvider | Describes any prerequisites for your Azure resource. Example: The **resourceProvider** value displays in Microsoft Sentinel **Prerequisites** section as: **Workspace: read and write permission is required.** **Keys: read permissions to shared keys for the workspace are required.** |
| **tenant** | array of ENUM valuesExample:`"tenant": [``"GlobalADmin",``"SecurityAdmin"``]` | Defines the required permissions, as one or more of the following values: `"GlobalAdmin"`, `"SecurityAdmin"`, `"SecurityReader"`, `"InformationProtection"`Example: displays the **tenant** value in Microsoft Sentinel as: **Tenant Permissions: Requires `Global Administrator` or `Security Administrator` on the workspace's tenant** |

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

#### resourceProvider

| sub array value | Type | Description |
| --- | --- | --- |
| **provider** | ENUM | Describes the resource provider, with one of the following values: - `Microsoft.OperationalInsights/workspaces`- `Microsoft.OperationalInsights/solutions`- `Microsoft.OperationalInsights/workspaces/datasources`- `microsoft.aadiam/diagnosticSettings`- `Microsoft.OperationalInsights/workspaces/sharedKeys`- `Microsoft.Authorization/policyAssignments` |
| **providerDisplayName** | String | A list item under **Prerequisites** that displays a red "x" or green checkmark when the **requiredPermissions** are validated in the connector page. Example, `"Workspace"` |
| **permissionsDisplayText** | String | Display text for *Read*, *Write*, or *Read and Write* permissions that should correspond to the values configured in **requiredPermissions** |
| **requiredPermissions** | `{``"action":`Boolean`,``"delete":`Boolean`,``"read":`Boolean`,``"write":`Boolean`}` | Describes the minimum permissions required for the connector. |
| **scope** | ENUM | Describes the scope of the data connector, as one of the following values: `"Subscription"`, `"ResourceGroup"`, `"Workspace"` |

### sampleQueries

| array value | Type | Description |
| --- | --- | --- |
| **description** | String | A meaningful description for the sample query.Example: `Top 10 vulnerabilities detected` |
| **query** | String | Sample query used to fetch the data type's data. Example: `{{graphQueriesTableName}}\n | sort by TimeGenerated\n | take 10` |

### Configure other link options

To define an inline link using markdown, use the following example.

```json
{
   "title": "",
   "description": "Make sure to configure the machine's security according to your organization's security policy\n\n\n[Learn more >](https://aka.ms/SecureCEF)"
}
```

To define a link as an ARM template, use the following example as a guide:

```json
{
   "title": "Azure Resource Manager (ARM) template",
   "description": "1. Click the **Deploy to Azure** button below.\n\n\t[![Deploy To Azure](https://aka.ms/deploytoazurebutton)]({URL to custom ARM template})"
}
```

### instructionSteps

This section provides parameters that define the set of instructions that appear on your data connector page in Microsoft Sentinel and has the following structure:

```json
"instructionSteps": [
    {
        "title": "",
        "description": "",
        "instructions": [
        {
            "type": "",
            "parameters": {}
        }
        ],
        "innerSteps": {}
    }
]
```

| Array Property | Required | Type | Description |
| --- | --- | --- | --- |
| **title** |  | String | Defines a title for your instructions. |
| **description** |  | String | Defines a meaningful description for your instructions. |
| **innerSteps** |  | Array | Defines an array of inner instruction steps. |
| **instructions** | True | Array of instructions | Defines an array of instructions of a specific parameter type. |

#### instructions

Displays a group of instructions, with various parameters and the ability to nest more instructionSteps in groups. Parameters defined here correspond

| Type | Array property | Description |
| --- | --- | --- |
| **OAuthForm** | OAuthForm | Connect with OAuth |
| **Textbox** | Textbox | This pairs with `ConnectionToggleButton`. There are 4 available types:- `password`<br>- `text`<br>- `number`<br>- `email` |
| **ConnectionToggleButton** | ConnectionToggleButton | Trigger the deployment of the DCR based on the connection information provided through placeholder parameters. The following parameters are supported:- `name` : mandatory<br>- `disabled`<br>- `isPrimary`<br>- `connectLabel`<br>- `disconnectLabel` |
| **CopyableLabel** | CopyableLabel | Shows a text field with a copy button at the end. When the button is selected, the field's value is copied. |
| **Dropdown** | Dropdown | Displays a dropdown list of options for the user to select from. |
| **Markdown** | Markdown | Displays a section of text formatted with Markdown. |
| **DataConnectorsGrid** | DataConnectorsGrid | Displays a grid of data connectors. |
| **ContextPane** | ContextPane | Displays a contextual information pane. |
| **InfoMessage** | InfoMessage | Defines an inline information message. |
| **InstructionStepsGroup** | InstructionStepsGroup | Displays a group of instructions, optionally expanded or collapsible, in a separate instructions section. |
| **InstallAgent** | InstallAgent | Displays a link to other portions of Azure to accomplish various installation requirements. |

##### OAuthForm

This component requires that the `OAuth2` type is present in the [`auth` property of the data connector template](data-connector-connection-rules-reference#authentication-configuration).

```json
"instructions": [
{
  "type": "OAuthForm",
  "parameters": {
    "clientIdLabel": "Client ID",
    "clientSecretLabel": "Client Secret",
    "connectButtonLabel": "Connect",
    "disconnectButtonLabel": "Disconnect"
  }          
}
]
```

##### Textbox

Here are some examples of the `Textbox` type. These examples correspond to the parameters used in the example `auth` section in [Data connectors reference for the Codeless Connector Framework](data-connector-connection-rules-reference#authentication-configuration). For each of the 4 types, each has `label`, `placeholder`, and `name`.

```json
"instructions": [
{
  "type": "Textbox",
  "parameters": {
      {
        "label": "User name",
        "placeholder": "User name",
        "type": "text",
        "name": "username"
      }
  }
},
{
  "type": "Textbox",
  "parameters": {
      "label": "Secret",
      "placeholder": "Secret",
      "type": "password",
      "name": "password"
  }
}
]
```

##### ConnectionToggleButton

```json
"instructions": [
{
  "type": "ConnectionToggleButton",
  "parameters": {
    "connectLabel": "toggle",
    "name": "toggle"
  }          
}
]
```

##### CopyableLabel

Example:

![Screenshot of a copy value button in a field.](isv/media/create-codeless-connector/copy-field-value.png)

**Sample code**:

```json
{
    "parameters": {
        "fillWith": [
            "WorkspaceId",
            "PrimaryKey"
            ],
        "label": "Here are some values you'll need to proceed.",
        "value": "Workspace is {0} and PrimaryKey is {1}"
    },
    "type": "CopyableLabel"
}
```

| Array Value | Required | Type | Description |
| --- | --- | --- | --- |
| **fillWith** |  | ENUM | Array of environment variables used to populate a placeholder. Separate multiple placeholders with commas. For example: `{0},{1}`Supported values: `workspaceId`, `workspaceName`, `primaryKey`, `MicrosoftAwsAccount`, `subscriptionId` |
| **label** | True | String | Defines the text for the label above a text box. |
| **value** | True | String | Defines the value to present in the text box, supports placeholders. |
| **rows** |  | Rows | Defines the rows in the user interface area. By default, set to **1**. |
| **wideLabel** |  | Boolean | Determines a wide label for long strings. By default, set to `false`. |

##### Dropdown

```json
{
  "parameters": {
    "label": "Select an option",
    "name": "dropdown",
    "options": [
      {
        "key": "Option 1",
        "text": "option1"
      },
      {
        "key": "Option 2",
        "text": "option2"
      }
    ],
    "placeholder": "Select an option",
    "isMultiSelect": false,
    "required": true,
    "defaultAllSelected": false
  },
  "type": "Dropdown"
}
```

| Field | Required | Type | Description |
| --- | --- | --- | --- |
| **label** | True | String | Defines the text for the label above the dropdown. |
| **name** | True | String | Defines the unique name for the dropdown. This is used in Polling config. |
| **options** | True | Array | Defines the list of options for the dropdown. |
| **placeholder** |  | String | Defines the placeholder text for the dropdown. |
| **isMultiSelect** |  | Boolean | Determines whether multiple options can be selected. By default, set to `false`. |
| **required** |  | Boolean | If `true`, the dropdown is required to be filled. |
| **defaultAllSelected** |  | Boolean | If `true`, all options are selected by default. |

##### Markdown

```json
{
  "parameters": {
    "content": "## This is a Markdown section\n\nYou can use **bold** text, _italic_ text, and even [links](https://www.example.com)."
  },
  "type": "Markdown"
}
```

##### DataConnectorsGrid

```json
{
  "type": "DataConnectorsGrid",
  "parameters": {
    "mapping": [
      {
        "columnName": "Column 1",
        "columnValue": "Value 1"
      },
      {
        "columnName": "Column 2",
        "columnValue": "Value 2"
      }
    ],
    "menuItems": [
      "MyConnector"
    ]
  }
}

```

| Field | Required | Type | Description |
| --- | --- | --- | --- |
| **mapping** | True | Array | Defines the mapping of columns in the grid. |
| **menuItems** |  | Array | Defines the menu items for the grid. |

##### ContextPane

```json
{
  "type": "ContextPane",
  "parameters": {
    "isPrimary": true,
    "label": "Add Account",
    "title": "Add Account",
    "subtitle": "Add Account",
    "contextPaneType": "DataConnectorsContextPane",
    "instructionSteps": [
      {
        "instructions": [
          {
            "type": "Textbox",
            "parameters": {
              "label": "Snowflake Account Identifier",
              "placeholder": "Enter Snowflake Account Identifier",
              "type": "text",
              "name": "accountId",
              "validations": {
                "required": true
              }
            }
          },
          {
            "type": "Textbox",
            "parameters": {
              "label": "Snowflake PAT",
              "placeholder": "Enter Snowflake PAT",
              "type": "password",
              "name": "apikey",
              "validations": {
                "required": true
              }
            }
          }
        ]
      }
    ]
  }
}
```

| Field | Required | Type | Description |
| --- | --- | --- | --- |
| **title** | True | String | The title for the context pane. |
| **subtitle** | True | String | The subtitle for the context pane. |
| **contextPaneType** | True | String | The type of the context pane. |
| **instructionSteps** | True | ArrayinstructionSteps | The instruction steps for the context pane. |
| **label** |  | String | The label for the context pane. |
| **isPrimary** |  | Boolean | Indicates whether this is the primary context pane. |

##### InfoMessage

Here's an example of an inline information message:

![Screenshot of an inline information message.](isv/media/create-codeless-connector/inline-information-message.png)

In contrast, the following image shows an information message that's not inline:

![Screenshot of an information message that's not inline.](isv/media/create-codeless-connector/non-inline-information-message.png)

| Array Value | Type | Description |
| --- | --- | --- |
| **text** | String | Define the text to display in the message. |
| **visible** | Boolean | Determines whether the message is displayed. |
| **inline** | Boolean | Determines how the information message is displayed. - `true`: (Recommended) Shows the information message embedded in the instructions. - `false`: Adds a blue background. |

##### InstructionStepsGroup

Here's an example of an expandable instruction group:

![Screenshot of an expandable, extra instruction group.](isv/media/create-codeless-connector/accordion-instruction-area.png)

| Array Value | Required | Type | Description |
| --- | --- | --- | --- |
| **title** | True | String | Defines the title for the instruction step. |
| **description** |  | String | Optional descriptive text. |
| **canCollapseAllSections** |  | Boolean | Determines whether the section is a collapsible accordion or not. |
| **noFxPadding** |  | Boolean | If `true`, reduces the height padding to save space. |
| **expanded** |  | Boolean | If `true`, shows as expanded by default. |

For a detailed example, see the configuration JSON for the [Windows DNS connector](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Windows%20Server%20DNS/Data%20Connectors/template_DNS.JSON).

##### InstallAgent

Some **InstallAgent** types appear as a button, others appear as a link. Here are examples of both:

![Screenshot of a link added as a button.](isv/media/create-codeless-connector/link-by-button.png)

![Screenshot of a link added as inline text.](isv/media/create-codeless-connector/link-by-text.png)

| Array Values | Required | Type | Description |
| --- | --- | --- | --- |
| **linkType** | True | ENUM | Determines the link type, as one of the following values: `InstallAgentOnWindowsVirtualMachine``InstallAgentOnWindowsNonAzure``InstallAgentOnLinuxVirtualMachine``InstallAgentOnLinuxNonAzure``OpenSyslogSettings``OpenCustomLogsSettings``OpenWaf``OpenAzureFirewall``OpenMicrosoftAzureMonitoring``OpenFrontDoors``OpenCdnProfile``AutomaticDeploymentCEF``OpenAzureInformationProtection``OpenAzureActivityLog``OpenIotPricingModel``OpenPolicyAssignment``OpenAllAssignmentsBlade``OpenCreateDataCollectionRule` |
| **policyDefinitionGuid** | True when using `OpenPolicyAssignment` linkType. | String | For policy-based connectors, defines the GUID of the built-in policy definition. |
| **assignMode** |  | ENUM | For policy-based connectors, defines the assign mode, as one of the following values: `Initiative`, `Policy` |
| **dataCollectionRuleType** |  | ENUM | For DCR-based connectors, defines the type of data collection rule type as either `SecurityEvent`, or `ForwardEvent`. |

## Example data connector definition

The following example brings together some of the components defined in this article as a JSON body format to use with the Create Or Update data connector definition API.

For more examples of the `connectorUiConfig` review [other CCF data connectors](https://github.com/Azure/Azure-Sentinel/tree/master/DataConnectors#codeless-connector-platform-CCF-preview--native-microsoft-sentinel-polling). Even connectors using the legacy CCF have valid examples of the UI creation.

```json
{
    "kind": "Customizable",
    "properties": {
        "connectorUiConfig": {
          "title": "Example CCF Data Connector",
          "publisher": "My Company",
          "descriptionMarkdown": "This is an example of data connector",
          "graphQueriesTableName": "ExampleConnectorAlerts_CL",
          "graphQueries": [
            {
              "metricName": "Alerts received",
              "legend": "My data connector alerts",
              "baseQuery": "{{graphQueriesTableName}}"
            },   
           {
              "metricName": "Events received",
              "legend": "My data connector events",
              "baseQuery": "ASIMFileEventLogs"
            }
          ],
            "sampleQueries": [
            {
                "description": "All alert logs",
                "query": "{{graphQueriesTableName}} \n | take 10"
            }
          ],
          "dataTypes": [
            {
              "name": "{{graphQueriesTableName}}",
              "lastDataReceivedQuery": "{{graphQueriesTableName}} \n | summarize Time = max(TimeGenerated)\n | where isnotempty(Time)"
            },
             {
              "name": "ASIMFileEventLogs",
              "lastDataReceivedQuery": "ASIMFileEventLogs \n | summarize Time = max(TimeGenerated)\n | where isnotempty(Time)"
             }
          ],
          "connectivityCriteria": [
            {
              "type": "HasDataConnectors"
            }
          ],
          "permissions": {
            "resourceProvider": [
              {
                "provider": "Microsoft.OperationalInsights/workspaces",
                "permissionsDisplayText": "Read and Write permissions are required.",
                "providerDisplayName": "Workspace",
                "scope": "Workspace",
                "requiredPermissions": {
                  "write": true,
                  "read": true,
                  "delete": true
                }
              },
            ],
            "customs": [
              {
                "name": "Example Connector API Key",
                "description": "The connector API key username and password is required"
              }
            ] 
        },
          "instructionSteps": [
            {
              "title": "Connect My Connector to Microsoft Sentinel",
              "description": "To enable the connector provide the required information below and click on Connect.\n>",
              "instructions": [
               {
                  "type": "Textbox",
                  "parameters": {
                    "label": "User name",
                    "placeholder": "User name",
                    "type": "text",
                    "name": "username"
                  }
                },
                {
                  "type": "Textbox",
                  "parameters": {
                    "label": "Secret",
                    "placeholder": "Secret",
                    "type": "password",
                    "name": "password"
                  }
                },
                {
                  "type": "ConnectionToggleButton",
                  "parameters": {
                    "connectLabel": "toggle",
                    "name": "toggle"
                  }
                }
              ]
            }
          ]
        }
    }
}
```