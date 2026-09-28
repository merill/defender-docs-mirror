---
layout: Conceptual
title: Microsoft Sentinel API request examples for creating Data Collection Rules (DCRs) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/api-dcr-reference
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
description: See samples of API requests for creating Data Collection Rules and their associations, for use with the Azure Monitor Agent.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: reference
ms.date: 2024-03-01T00:00:00.0000000Z
locale: en-us
document_id: 0d6198a2-c3b9-97de-8d63-d50b1382a304
document_version_independent_id: c110cf10-61a9-247e-c9b2-0c508518c8f9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/api-dcr-reference.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/api-dcr-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/api-dcr-reference.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
platformId: 4082a4d3-dd6d-7a52-e729-b68036cfb153
---

# Microsoft Sentinel API request examples for creating Data Collection Rules (DCRs) | Microsoft Learn

This article presents some examples of API requests and responses for creating Data Collection Rules (DCRs) and DCR Associations (DCRAs) for use with the Azure Monitor Agent (AMA).

## Syslog/CEF

The following examples are for DCRs using the AMA to collect Syslog and CEF messages.

### Syslog/CEF DCR

These examples are of the API request and response for creating a DCR.

#### Syslog/CEF DCR creation request URL and header

Example:

```http
PUT https://management.azure.com/subscriptions/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/resourceGroups/ContosoRG/providers/Microsoft.Insights/dataCollectionRules/Contoso-DCR-01?api-version=2022-06-01
```

#### Syslog/CEF DCR creation request body

The following is an example of a DCR creation request. For each data source stream—you can have several in one DCR—add a new subsection under `"syslog"` in the `"dataSources"` section and set the value of the `"streams"` field according to the source of the messages you want to ingest:

| Log source | `"streams"`field value |
| --- | --- |
| **Syslog** | `"Microsoft-Syslog"` |
| **CEF** | `"Microsoft-CommonSecurityLog"` |
| **Cisco ASA** | `"Microsoft-CiscoAsa"` |

See the example of multiple streams sections in the following code sample:

```json
{
  "location": "centralus",
  "kind": "Linux",
  "properties": {
    "dataSources": {
      "syslog": [
        {
          "name": "localsSyslog",
          "streams": [
            "Microsoft-Syslog"
          ],
          "facilityNames": [
            "auth",
            "local0",
            "local1",
            "local2",
            "local3",
            "syslog"
          ],
          "logLevels": [
            "Critical",
            "Alert",
            "Emergency"
          ]
        },
        {
          "name": "authprivSyslog",
          "streams": [
            "Microsoft-Syslog"
          ],
          "facilityNames": [
            "authpriv"
          ],
          "logLevels": [
            "Error",
            "Alert",
            "Critical",
            "Emergency"
          ]
        }
      ]
    },
    "destinations": {
      "logAnalytics": [
        {
          "workspaceResourceId": "/subscriptions/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/resourceGroups/ContosoRG/providers/Microsoft.OperationalInsights/workspaces/Contoso",
          "workspaceId": "11111111-2222-3333-4444-555555555555",
          "name": "DataCollectionEvent"
        }
      ]
    },
    "dataFlows": [
      {
        "streams": [
          "Microsoft-Syslog"
        ],
        "destinations": [
          "DataCollectionEvent"
        ]
      }
    ]
  }
}
```

#### Syslog/CEF DCR creation response

Here's the response you should receive according to the sample request above:

```json
  {
    "properties": {
      "immutableId": "dcr-0123456789abcdef0123456789abcdef",
      "dataSources": {
        "syslog": [
          {
            "streams": [
              "Microsoft-Syslog"
            ],
            "facilityNames": [
              "auth",
              "local0",
              "local1",
              "local2",
              "local3",
              "syslog"
            ],
            "logLevels": [
              "Critical",
              "Alert",
              "Emergency"
            ],
            "name": "localsSyslog"
          },
          {
            "streams": [
              "Microsoft-Syslog"
            ],
            "facilityNames": [
              "authpriv"
            ],
            "logLevels": [
              "Error",
              "Alert",
              "Critical",
              "Emergency"
            ],
            "name": "authprivSyslog"
          }
        ]
      },
      "destinations": {
        "logAnalytics": [
          {
            "workspaceResourceId": "/subscriptions/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/resourceGroups/ContosoRG/providers/Microsoft.OperationalInsights/workspaces/Contoso",
            "workspaceId": "11111111-2222-3333-4444-555555555555",
            "name": "DataCollectionEvent"
          }
        ]
      },
      "dataFlows": [
        {
          "streams": [
            "Microsoft-Syslog"
          ],
          "destinations": [
            "DataCollectionEvent"
          ]
        }
      ],
      "provisioningState": "Succeeded"
    },
    "location": "centralus",
    "kind": "Linux",
    "id": "/subscriptions/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/resourceGroups/ContosoRG/providers/Microsoft.Insights/dataCollectionRules/Contoso-DCR-01",
    "name": "Contoso-DCR-01",
    "type": "Microsoft.Insights/dataCollectionRules",
    "etag": "\"00000000-0000-0000-0000-000000000000\"",
    "systemData": {
    }
  }
```

### Syslog/CEF DCRA

#### Syslog/CEF DCRA creation request URL and header

```http
PUT 
https://management.azure.com/subscriptions/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/LogForwarder-VM-1/providers/Microsoft.Insights/dataCollectionRuleAssociations/contoso-dcr-assoc?api-version=2022-06-01
```

#### Syslog/CEF DCRA creation request body

```json
{
  "properties": {
    "dataCollectionRuleId": "/subscriptions/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/resourceGroups/ContosoRG/providers/Microsoft.Insights/dataCollectionRules/Contoso-DCR-01"
  }
}
```

#### Syslog/CEF DCRA creation response

```json
{
    "properties": {
      "dataCollectionRuleId": "/subscriptions/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/resourceGroups/ContosoRG/providers/Microsoft.Insights/dataCollectionRules/Contoso-DCR-01"
    },
    "id": "/subscriptions/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/LogForwarder-VM-1/providers/Microsoft.Insights/dataCollectionRuleAssociations/contoso-dcr-assoc",
    "name": "contoso-dcr-assoc",
    "type": "Microsoft.Insights/dataCollectionRuleAssociations",
    "etag": "\"00000000-0000-0000-0000-000000000000\"",
    "systemData": {
    }
  }
```

## Custom logs from text files

The following examples are for DCRs using the AMA to collect custom logs from text files.

### Custom text logs DCR

These examples are of the API request for creating a DCR.

#### Custom text logs DCR creation request body

The following is an example of a DCR creation request for a custom log text file. Replace *`{PLACEHOLDER_VALUES}`* with actual values.

The `outputStream` parameter is required only if the transform changes the schema of the stream.

```json
{
    "type": "Microsoft.Insights/dataCollectionRules",
    "name": "{DCR_NAME}",
    "location": "{WORKSPACE_LOCATION}",
    "apiVersion": "2022-06-01",
    "properties": {
        "streamDeclarations": {
            "Custom-Text-{TABLE_NAME}": {
                "columns": [
                    {
                        "name": "TimeGenerated",
                        "type": "datetime"
                    },
                    {
                        "name": "RawData",
                        "type": "string"
                    },
                ]
            }
        },
        "dataSources": {
            "logFiles": [
                {
                    "streams": [ 
                        "Custom-Text-{TABLE_NAME}" 
                    ],
                    "filePatterns": [ 
                        "{LOCAL_PATH_FILE_1}","{LOCAL_PATH_FILE_2}" 
                    ],
                    "format": "text",
                    "name": "Custom-Text-{TABLE_NAME}"
                }
            ],
        },
        "destinations": {
            "logAnalytics": [
                {
                    "workspaceResourceId": "{WORKSPACE_RESOURCE_PATH}",
                    "workspaceId": "{WORKSPACE_ID}",
                    "name": "DataCollectionEvent"
                }
            ],
        },
        "dataFlows": [
            {
                "streams": [
                    "Custom-Text-{TABLE_NAME}" 
                ],
                "destinations": [ 
                    "DataCollectionEvent" 
                ],
                "transformKql": "source",
                "outputStream": "Custom-{TABLE_NAME}"
            }
        ]
    }
}
```

#### Custom text logs DCR creation response

```json
{
    "properties": {
        "immutableId": "dcr-00112233445566778899aabbccddeeff",
        "dataCollectionEndpointId": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/Contoso-RG-1/providers/Microsoft.Insights/dataCollectionEndpoints/Microsoft-Sentinel-aaaabbbbccccddddeeeefff",
        "streamDeclarations": {
            "Custom-Text-ApacheHTTPServer_CL": {
                "columns": [
                    {
                        "name": "TimeGenerated",
                        "type": "datetime"
                    },
                    {
                        "name": "RawData",
                        "type": "string"
                    }
                ]
            }
        },
        "dataSources": {
            "logFiles": [
                {
                    "streams": [
                        "Custom-Text-ApacheHTTPServer_CL"
                    ],
                    "filePatterns": [
                        "C:\\Server\\bin\\log\\Apache24\\logs\\*.log"
                    ],
                    "format": "text",
                    "settings": {
                        "text": {
                            "recordStartTimestampFormat": "ISO 8601"
                        }
                    },
                    "name": "Custom-Text-ApacheHTTPServer_CL"
                }
            ]
        },
        "destinations": {
            "logAnalytics": [
                {
                    "workspaceResourceId": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/contoso-rg-1/providers/Microsoft.OperationalInsights/workspaces/CyberSOC",
                    "workspaceId": "cccccccc-3333-4444-5555-dddddddddddd",
                    "name": "DataCollectionEvent"
                }
            ]
        },
        "dataFlows": [
            {
                "streams": [
                    "Custom-Text-ApacheHTTPServer_CL"
                ],
                "destinations": [
                    "DataCollectionEvent"
                ],
                "transformKql": "source",
                "outputStream": "Custom-ApacheHTTPServer_CL"
            }
        ],
        "provisioningState": "Succeeded"
    },
    "location": "centralus",
    "tags": {
        "createdBy": "Sentinel"
    },
    "id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/Contoso-RG-1/providers/Microsoft.Insights/dataCollectionRules/DCR-CustomLogs-01",
    "name": "DCR-CustomLogs-01",
    "type": "Microsoft.Insights/dataCollectionRules",
    "etag": "\"00000000-1111-2222-3333-444444444444\"",
    "systemData": {
        "createdBy": "gbarnes@contoso.com",
        "createdByType": "User",
        "createdAt": "2024-08-12T09:29:15.1083961Z",
        "lastModifiedBy": "gbarnes@contoso.com",
        "lastModifiedByType": "User",
        "lastModifiedAt": "2024-08-12T09:29:15.1083961Z"
    }
}
```