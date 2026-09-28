---
layout: Conceptual
title: Create Parsers for Microsoft Sentinel Solutions | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/isv/sentinel-parsers-creation
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
description: This article guides you through the process of creating and publishing parsers for Microsoft Sentinel solutions.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: tbeerthuis
ms.topic: how-to
ms.date: 2026-06-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 7e110a5a-c40d-161c-51d1-bba7abfd00c5
document_version_independent_id: f8ba2a8a-7c9e-b687-b86c-6a45d3cfda37
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/isv/sentinel-parsers-creation.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/isv/sentinel-parsers-creation
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/isv/sentinel-parsers-creation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 2adfc6de-72c6-1be2-ed0c-c56fcee356bb
---

# Create Parsers for Microsoft Sentinel Solutions | Microsoft Learn

A parser is a Kusto function saved to your Log Analytics workspace that sits in front of raw log data and normalizes it into clean, queryable fields. Instead of writing field extraction logic in every query, customers call the parser alias once and get structured results. Parsers are defined as YAML files and deployed automatically when a customer installs your solution.

This article walks you through the process of creating and publishing parsers for Microsoft Sentinel solutions.

Note

Include a parser whenever your connector uses a custom log table (`_CL`), Syslog, or CEF. Place each parser as a `.yaml` file in `Solutions/<YourSolutionName>/Parsers/`.

## YAML structure

Every parser file must contain the following top-level fields:

```yaml
id: <UUID v4>
Function:
  Title: Parser for <ProductName>
  Version: '1.0.0'
  LastUpdated: '2024-01-15'
Category: Microsoft Sentinel Parser
FunctionName: MyProductEvent
FunctionAlias: MyProductEvent
FunctionQuery: |
  MyProduct_CL
  | extend EventVendor = 'MyVendor'
  | extend EventProduct = 'MyProduct'
  ...
```

## Field reference

| Field | Rules |
| --- | --- |
| `id` | Valid UUID v4. Must be unique in the repo. One UUID per file. |
| `Function.Title` | Descriptive string, for example `"Parser for CiscoISEEvent"` |
| `Function.Version` | SemVer format, **must be quoted**: `'1.0.0'` not `1.0.0` (unquoted parses as a number and fails validation) |
| `Function.LastUpdated` | ISO 8601 date, **must be quoted**: `'2024-01-15'` not `2024-01-15` |
| `Category` | Must be exactly `Microsoft Sentinel Parser` (case-sensitive). Any other value is a validation error. |
| `FunctionName` | Alphanumeric + underscore only. Must match `FunctionAlias`. |
| `FunctionAlias` | Must match `FunctionName`. |
| `FunctionQuery` | Valid KQL. Must reference at least one table after any `let` bindings. Maximum practical length is a few hundred lines; reviewers flag overly complex queries. |
| `FunctionParams` | Optional. Use when building a parameterized parser (for ASIM `vim` variants). See the CrowdStrikeReplicatorV2 example. |

Caution

The following are common issues in parser PRs:

- **Unquoted `Version` or `LastUpdated`**: YAML parses `1.0.0` as a float and `2024-01-15` as a date object; both fail schema validation. Always quote them.
- **Table name mismatch**: If your parser queries a custom table (for example, `FortinetFortiNdrCloudRaw_CL`), the table name in `FunctionQuery` must exactly match the `Name` property in your `CustomTables/` schema JSON file, and that file must be named `<TableName>.json`. A mismatch causes the KQL validation CI job to fail with "table does not exist." For examples of custom table schemas see See [CustomTables schemas](https://github.com/Azure/Azure-Sentinel/tree/master/.script/tests/KqlvalidationsTests/CustomTables).

## Parts of a parser query

The `FunctionQuery` is the heart of your parser. It's a KQL query that has three parts, applied in order:

**Filter** &gt; **Parse** &gt; **Prepare fields**

The following sections describe each part and what you need to define. For in-depth guidance and ASIM-specific patterns, see [Develop Advanced Security Information Model (ASIM) parsers](../normalization-develop-parsers).

### Filter the relevant records

A single table often holds multiple event types. For example, the `Syslog` table holds data from many sources, and a custom table can hold several event types from one source. Start your query by filtering only the records relevant to the target schema, using the `where` operator:

```kql
Event | where Source == "Microsoft-Windows-Sysmon" and EventID == 1
```

Follow these filtering guidelines:

- **Don't filter by time.** The query that calls the parser applies its own time range.
- **Filter on built-in (physical) fields, not parsed fields.** Filtering on parsed fields dramatically reduces performance.
- **Use performance-optimized operators** such as `==`, `has`, and `startswith`. Avoid `contains` and `matches regex`, which are much slower.
- **Skip the filter when a parameter keeps its default value.** In a parameterized parser, only filter when the caller passes a value.

### Parse the records

After the query selects the relevant records, parse them if multiple event fields are packed into a single text field. Choose the most performant operator that fits your data. The following operators are ordered from most to least performant:

| Operator or function | Use it to |
| --- | --- |
| [`split()`](/en-us/kusto/query/split-function) | Parse a string of delimited values. |
| [`parse_csv()`](/en-us/kusto/query/parse-csv-function) | Parse a string formatted as a CSV line. |
| [`parse-kv`](/en-us/kusto/query/parse-kv-operator) | Extract structured information into key/value pairs. |
| [`parse`](/en-us/kusto/query/parse-operator) | Parse multiple values from a string using a pattern or regular expression. |
| [`extract_all()`](/en-us/kusto/query/extract-all-function) | Parse multiple values from a string using a regular expression. |
| [`extract()`](/en-us/kusto/query/extract-function) | Extract a single value from a string using a regular expression. |
| [`parse_json()`](/en-us/kusto/query/parse-json-function) | Parse values from a JSON-formatted string. |
| [`parse_xml()`](/en-us/kusto/query/parse-xml-function) | Parse values from an XML-formatted string. |

### Prepare fields

The final part normalizes parsed values into the target schema and selects the result set. This part has three jobs:

- **Map field names.** Rename a source field to its normalized name with `project-rename`, which keeps the field physical and performant:

    ```kql
    | project-rename ActorUserId = InitiatingProcessAccountSid
    ```
- **Normalize formats, types, and values.** Use `extend` with KQL functions to fix formats and cast types so output matches the schema. For example, cast an integer ID to a string, or map source codes to schema values with `iff`, `case`, or `lookup`:

    ```kql
    | extend EventOriginalUid = tostring(ReportId)
    | extend EventResult = iff(EventId == 257 and ResponseCode == 0, 'Success', 'Failure')
    ```
- **Add enrichment fields.** Set the constant fields that every normalized event includes, such as the vendor, product, and schema identifiers:

    ```kql
    | extend
        EventCount = int(1),
        EventVendor = 'MyVendor',
        EventProduct = 'MyProduct',
        EventSchemaVersion = '0.1.0'
    ```

Optionally, use `project-away` to remove temporary fields used during parsing, such as type-suffixed source columns:

```kql
| project-away *_d, *_s, *_b, *_g
```

Tip

When an event stream contains variants that need different parsing logic, handle them with conditional statements (`iff`, `case`) or by creating a separate function per variant and combining them with `union`. If the variants represent different event types that map to different schemas, build a separate parser for each.

## Use `column_ifexists()` for schema evolution

If your connector evolved over time for example, renaming columns, adding V2 tables, switching from `_s`/`_d` suffixed columns to flat column names, use `column_ifexists()` to make the parser resilient to schema version changes. For example, if your connector originally had a `ClientIP_s` column but later changed to `ClientIP`, use the following in your parser query to support both versions:

```kql
| extend SrcIpAddr = tostring(column_ifexists("ClientIP_s", column_ifexists("ClientIP", "")))
```

This allows a single parser function to work for both the legacy `_CL` table with type-suffix columns and a new CCF/DCR table with clean column names, without breaking existing customer workbooks.

## ASIM parsers

If your data maps to an [ASIM schema](/en-us/azure/sentinel/normalization-about-schemas), you need two parser variants:

- **`ASim<Schema><Product>.yaml`** — parameter-less version, placed in `Solutions/<Name>/Parsers/`.
- **`vim<Schema><Product>.yaml`** — parameterized version with `FunctionParams`, placed in the same folder.

Both variants must also be registered in the corresponding ASIM unifying parser in `Parsers/ASim<Schema>/`. Reviewers consistently ask for this registration if it's missing — it's required for the parser to appear in Sentinel's normalized query layer. For the ASIM-specific CHANGELOG and full workflow, see the [ASIM contribution guide](https://github.com/Azure/Azure-Sentinel/blob/master/ASIM/README.md).

For more information on building ASIM parsers, see [Develop Advanced Security Information Model (ASIM) parsers](../normalization-develop-parsers).

Note

When accessing fields on `dynamic` objects (from `parse_json()` or bag expansion), always apply an explicit type cast before assigning to ASIM schema columns. Use a cast such as `tostring(d.fieldName)`, `toint(d.count)`, or `tobool(d.flag)`. Assigning a `dynamic` value directly fails KQL validation or produces silent type errors at query runtime.

## Reference examples

See the following reference examples in the Azure-Sentinel repository for guidance on parser design and layout:

- [Cloudflare CCF — Cloudflare.yaml](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Cloudflare%20CCF/Parsers/Cloudflare.yaml)
- [CrowdStrike Falcon — CrowdStrikeReplicatorV2.yaml](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/CrowdStrike%20Falcon%20Endpoint%20Protection/Parsers/CrowdStrikeReplicatorV2.yaml)