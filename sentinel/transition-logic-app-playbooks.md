---
layout: Conceptual
title: Update Logic App playbook automation - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/transition-logic-app-playbooks
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
ms.service: microsoft-defender
ms.subservice: unified-security-operations
search.appverid: met150
description: Learn how to update Microsoft Sentinel Logic App playbooks that query Log Analytics so they use Microsoft Defender XDR Advanced Hunting data.
author: guywi-ms
ms.author: guywild
ms.date: 2026-10-11T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1030
locale: en-us
document_id: 49def6b0-38c6-ce36-a39f-24cde418e720
document_version_independent_id: 5d03991e-3291-e075-12ea-76ffeeca3a0a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/transition-logic-app-playbooks.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/transition-logic-app-playbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/transition-logic-app-playbooks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 86b3748f-ce7b-24e3-31a1-c2a7d43a2963
---

# Update Logic App playbook automation - Microsoft Sentinel | Microsoft Learn

When you transition Microsoft Sentinel content from workspace-based data to Microsoft Defender XDR Advanced Hunting data, update Logic App playbooks that run Log Analytics queries so that they query Advanced Hunting instead.

The update changes the query data source and response format while preserving the rest of the automation flow where possible. Typically, the playbook trigger and downstream enrichment, notification, or response actions remain the same.

Note

This article applies to Logic App playbooks that query Log Analytics or Azure Monitor Logs. It doesn't describe the migration of automation rules associated with Microsoft Sentinel analytics rules. For analytics rule migration, see [Convert Microsoft Sentinel analytics rules to custom detections](transition-custom-detections).

For changes to KQL table names, time columns, and data types, see [Update Microsoft Sentinel content to use Advanced Hunting tables](transition-advanced-hunting-tables).

## Understand the playbook changes

The following table summarizes the main changes when you update a playbook to use Advanced Hunting.

| Current implementation | Target implementation |
| --- | --- |
| Log Analytics or Azure Monitor Logs connector | Microsoft Graph API call to Advanced Hunting |
| Workspace-based Microsoft Sentinel or Log Analytics tables | Microsoft Defender XDR Advanced Hunting tables |
| Queries that use `TimeGenerated` | Advanced Hunting queries that use `Timestamp` |
| Response parsing from the existing query action's output | Response parsing from `schema` and `results` |

The updated playbook flow is:

1. Start from the existing Logic App trigger.
2. Initialize or compose the Advanced Hunting query.
3. Call Microsoft Graph by using `POST /security/runHuntingQuery`.
4. Parse the response body.
5. Loop over the `results` array.
6. Run the existing enrichment, notification, or response actions.

## Prerequisites

Before you update a Logic App playbook, make sure that the following requirements are met.

| Requirement | Details |
| --- | --- |
| Microsoft Defender XDR access | Advanced Hunting data must be available in Microsoft Defender XDR. |
| Logic App identity | Use a system-assigned managed identity, user-assigned managed identity, or application registration. |
| Microsoft Graph permission | Grant `ThreatHunting.Read.All`. Admin consent is required. |
| Query validation access | An administrator or analyst must be able to validate each query in Advanced Hunting in the Microsoft Defender portal. |
| Change control | Test the changes in a nonproduction or cloned playbook before replacing production actions. |

Before you update a production playbook, confirm table availability, permissions, and query behavior in your tenant.

## Configure permissions and authentication

The Advanced Hunting API requires the `ThreatHunting.Read.All` Microsoft Graph permission.

| Permission type | Permission | Recommended use |
| --- | --- | --- |
| Application | `ThreatHunting.Read.All` | Recommended for production Logic App automation. |
| Delegated | `ThreatHunting.Read.All` | Useful for user-context testing or interactive scenarios. |

Use a managed identity where possible.

If you use an HTTP action, configure it with the following settings:

| Setting | Value |
| --- | --- |
| Authentication type | Managed Identity |
| Identity | System-assigned or user-assigned managed identity |
| Audience | `https://graph.microsoft.com` |
| HTTP method | `POST` |
| URI | `https://graph.microsoft.com/v1.0/security/runHuntingQuery` |

If you use a Microsoft Graph connector or custom connector instead of the generic HTTP action, configure it to call the same endpoint with the required permissions and request body.

## Call the Advanced Hunting API

Use the following Microsoft Graph endpoint:

```text
POST https://graph.microsoft.com/v1.0/security/runHuntingQuery
```

The request uses the following headers:

```text
Content-Type: application/json
Authorization: Bearer <token>
```

For example:

```json
{
  "Query": "DeviceProcessEvents | where Timestamp > ago(1h) | take 100"
}
```

You can also specify an explicit timespan:

```json
{
  "Query": "DeviceProcessEvents | project Timestamp, DeviceName, FileName, ProcessCommandLine",
  "Timespan": "PT1H"
}
```

The `Timespan` parameter is optional. You can also restrict the time range directly in the KQL query. If both are used, the narrower time range applies.

## Update a Logic App playbook

Update each playbook that runs queries against Log Analytics, Azure Monitor Logs, or workspace-based Microsoft Sentinel data.

1. Identify every Logic App action that uses Log Analytics, Azure Monitor Logs, or workspace-based query execution.
2. Copy the existing KQL query and identify which output columns are used by downstream actions.
3. Map the Log Analytics tables and columns to their Advanced Hunting equivalents.

    For table and schema changes, see [Update Microsoft Sentinel content to use Advanced Hunting tables](transition-advanced-hunting-tables).
4. Replace `TimeGenerated` filters with `Timestamp`, where applicable.
5. Validate the updated KQL query in Advanced Hunting in the Microsoft Defender portal.
6. Replace the Log Analytics query action with a Microsoft Graph call to:

    ```text
    /security/runHuntingQuery
    ```
7. Update response parsing to use the `results` array.
8. Update downstream expressions to use named JSON properties instead of row indexes, where applicable.
9. Add handling for empty results and API errors.
10. Test the playbook end to end before enabling the updated version in production.

## Map commonly used tables

The following table provides examples of Advanced Hunting tables commonly used by playbooks.

| Data | Advanced Hunting table | Notes |
| --- | --- | --- |
| Defender XDR alert metadata | `AlertInfo` | Alert title, severity, category, service source, and alert ID |
| Alert entities or evidence | `AlertEvidence` | Related users, devices, files, URLs, IP addresses, and evidence |
| Device process activity | `DeviceProcessEvents` | Process creation and related endpoint process events |
| Device network activity | `DeviceNetworkEvents` | Inbound and outbound network connection events |
| Device file activity | `DeviceFileEvents` | File creation, modification, and file-system events |
| Device registry activity | `DeviceRegistryEvents` | Registry creation, modification, and deletion events |
| Device logon activity | `DeviceLogonEvents` | Device authentication and logon events |
| Email events | `EmailEvents` | Email delivery and message metadata |
| Email attachments | `EmailAttachmentInfo` | Attachment metadata for email messages |
| Email URLs | `EmailUrlInfo` | URLs observed in email messages |
| Post-delivery email actions | `EmailPostDeliveryEvents` | Post-delivery actions, such as zero-hour auto purge (ZAP) |
| Cloud app activity | `CloudAppEvents` | Cloud application and SaaS activity |
| Identity information | `IdentityInfo` or `IdentityAccountInfo` | Validate the table available in your tenant |
| Microsoft Entra ID sign-in events | `EntraIdSignInEvents` or `AADSignInEventsBeta` | Use the table available in your Advanced Hunting schema |

Table and column availability can vary based on licensing, tenant configuration, data-source onboarding, and schema changes. Validate the required tables in your tenant before updating a production playbook.

## Update response parsing

Log Analytics response formats depend on how the playbook runs the query. Azure Monitor Logs and Azure Log Analytics listing actions, including their deprecated versions, return a `value` array of objects with named fields. Direct Log Analytics query REST calls return `tables` and positional row arrays. Microsoft Graph Advanced Hunting returns `schema` and `results`.

Change the loop input to `results`. Replace positional field references with named properties where used. If expressions already use named properties, update only those affected by changes to the query output.

The following examples apply to playbooks that read `tables[0].rows`. They assume that the first two source columns map to `Timestamp` and `DeviceName`. Apply the same approach to every field the playbook uses.

| Log Analytics pattern | Advanced Hunting pattern |
| --- | --- |
| `body('Run_query')?['tables'][0]?['rows']` | `body('Run_Hunting_Query')?['results']` |
| `items('For_each')?[0]` | `items('For_each')?['Timestamp']` |
| `items('For_each')?[1]` | `items('For_each')?['DeviceName']` |

An Advanced Hunting response can look like the following example:

```json
{
  "schema": [
    {
      "name": "Timestamp",
      "type": "DateTime"
    },
    {
      "name": "DeviceName",
      "type": "String"
    },
    {
      "name": "FileName",
      "type": "String"
    }
  ],
  "results": [
    {
      "Timestamp": "2026-06-23T08:00:00Z",
      "DeviceName": "device01.contoso.com",
      "FileName": "powershell.exe"
    }
  ]
}
```

### Parse the response

Add a **Parse JSON** action after the Microsoft Graph call.

You can use the following schema as a starting point:

```json
{
  "type": "object",
  "properties": {
    "schema": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "name": {
            "type": "string"
          },
          "type": {
            "type": "string"
          }
        }
      }
    },
    "results": {
      "type": "array",
      "items": {
        "type": "object"
      }
    }
  }
}
```

Configure the **For each** action to iterate over:

```text
body('Parse_JSON')?['results']
```

## Update common playbook queries

The following examples show how common Log Analytics queries can be updated to use Advanced Hunting.

### Alert enrichment

A Log Analytics query might use:

```kusto
SecurityAlert
| where TimeGenerated > ago(1h)
| where SystemAlertId == "<alert-id>"
| project TimeGenerated, AlertName, ProviderName, AlertSeverity
```

Use the following Advanced Hunting query instead:

```kusto
AlertInfo
| where Timestamp > ago(1h)
| where AlertId == "<alert-id>"
| project Timestamp, AlertId, Title, ServiceSource, Severity
```

The following fields change:

| Log Analytics field | Advanced Hunting field |
| --- | --- |
| `TimeGenerated` | `Timestamp` |
| `SystemAlertId` | `AlertId` |
| `AlertName` | `Title` |
| `ProviderName` | `ServiceSource` |
| `AlertSeverity` | `Severity` |

### Device process investigation

For example:

```json
{
  "Query": "DeviceProcessEvents | where Timestamp > ago(24h) | where DeviceName == '<device-name>' | project Timestamp, DeviceName, FileName, ProcessCommandLine"
}
```

### Email investigation

For example:

```kusto
EmailEvents
| where Timestamp > ago(24h)
| where RecipientEmailAddress =~ "<user@contoso.com>"
| project Timestamp, NetworkMessageId, SenderFromAddress, RecipientEmailAddress, Subject, DeliveryAction
```

## Handle empty results and errors

A successful Advanced Hunting query can return no rows. Check the number of results before running downstream actions:

```text
length(body('Run_Hunting_Query')?['results'])
```

Continue only when the length is greater than `0`. Otherwise, end the flow gracefully or handle the no-results condition explicitly.

Use the following guidance to troubleshoot common issues:

| Issue | Likely cause | Recommended resolution |
| --- | --- | --- |
| `403 Forbidden` | Missing Microsoft Graph permission or admin consent | Grant `ThreatHunting.Read.All` and confirm admin consent. |
| `401 Unauthorized` | Authentication configuration issue | Verify the managed identity, audience, and Microsoft Graph authentication configuration. |
| Empty results | Table, field, time range, or data availability mismatch | Validate the query in Advanced Hunting and confirm that the expected data is available. |
| Expression failure | The playbook still expects Log Analytics row arrays | Update expressions to use `results` and named JSON properties. |
| Query timeout | The query is too broad or resource intensive | Add time filters, project fewer columns, reduce joins, and limit results. |
| Field not found | The Advanced Hunting schema differs from Log Analytics | Review the Advanced Hunting schema and update the column names. |

## Optimize query performance and reliability

When you use Advanced Hunting queries in Logic App playbooks:

- Include a time filter, such as `Timestamp > ago(1h)`.
- Apply filters as early as possible.
- Use `project` to return only the columns required by the playbook.
- Avoid broad search operations across large datasets.
- Use `take` or `limit` when the playbook doesn't require all matching rows.
- Test query runtime in Advanced Hunting before using the query in automation.
- Handle authentication, authorization, throttling, timeout, and empty-result scenarios.

For example, prefer:

```kusto
DeviceProcessEvents
| where Timestamp > ago(1h)
| where DeviceName == "device01.contoso.com"
| project Timestamp, DeviceName, FileName, ProcessCommandLine
| take 100
```

Avoid broad queries such as:

```kusto
DeviceProcessEvents
| search "powershell"
```

## Validate the updated playbook

Before you use the updated playbook in production, confirm that:

- The Logic App no longer depends on the Log Analytics query action for the updated flow.
- The playbook calls Microsoft Graph at `/security/runHuntingQuery`.
- The Logic App identity has `ThreatHunting.Read.All` with admin consent.
- The KQL query works as expected in Advanced Hunting.
- Log Analytics tables and columns are mapped to the appropriate Advanced Hunting equivalents.
- Response parsing uses `results`.
- Downstream actions reference named properties instead of row indexes.
- Empty-result handling is configured.
- Error handling is configured for authentication, authorization, throttling, and timeout scenarios.
- The playbook has been tested end to end with a controlled test case.

## API limits and operational considerations

Microsoft Graph Advanced Hunting queries can return up to 100,000 rows per request. The optional `Timespan` parameter defaults to 30 days.

The API is also subject to tenant-level quotas and resource allocation. A `429` response indicates throttling or resource pressure. Retry the request later and review the response for more information.

Long-running requests can time out. Optimize the KQL query and narrow the time range when needed.

Explicitly define the time scope used by automation, either in KQL or through the request timespan.