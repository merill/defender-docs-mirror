---
layout: Conceptual
title: Create Power BI reports with Microsoft Defender for Endpoint APIs - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/api-power-bi
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: yongrhee
description: Create a Power Business Intelligence (BI) report on top of Microsoft Defender for Endpoint APIs.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: how-to
ms.subservice: reference
ms.custom: api, msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 8e37d725-31cc-23bb-27bf-46c8342df8aa
document_version_independent_id: 8e37d725-31cc-23bb-27bf-46c8342df8aa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/api-power-bi.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/api-power-bi
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/api-power-bi.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d3197845-b4ce-44c6-a237-cd4be160e76c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/aea905fb-0a9d-4d46-b30f-e9cbaf772d1b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 681b0e1f-8ff5-f22f-49a6-0682c87e1356
---

# Create Power BI reports with Microsoft Defender for Endpoint APIs - Microsoft Defender for Endpoint | Microsoft Learn

Note

If you're a US Government customer, use the URIs listed in [Microsoft Defender for Endpoint for US Government customers](/en-us/defender-endpoint/gov#api).

Tip

For better performance, instead of using api.security.microsoft.com, use a server closer to your geolocation:

- us.api.security.microsoft.com
- eu.api.security.microsoft.com
- uk.api.security.microsoft.com
- au.api.security.microsoft.com
- swa.api.security.microsoft.com
- ina.api.security.microsoft.com
- aea.api.security.microsoft.com

Create Power BI reports on top of Defender for Endpoint APIs.

The first example demonstrates how to connect Power BI to Advanced Hunting API, and the second example demonstrates a connection to our OData APIs, such as Machine Actions or Alerts.

## Connect Power BI to Advanced Hunting API

Perform the following steps to connect Power BI to the Advanced Hunting API and build a report from query results.

1. Open Microsoft Power BI.
2. Select **Get Data** &gt; **Blank Query**.

    [![The Blank Query option under the Get Data menu item](../media/power-bi-create-blank-query.png)](../media/power-bi-create-blank-query.png#lightbox)
3. Select **Advanced Editor**.

    [![The Advanced Editor menu item](../media/power-bi-open-advanced-editor.png)](../media/power-bi-open-advanced-editor.png#lightbox)
4. Copy the code snippet below and paste it in the editor. This query uses the Advanced Hunting API to retrieve up to 20 `DeviceEvents` entries where the action type contains "Anti", and maps the response schema to Power BI data types:

    ```dax
        let
            AdvancedHuntingQuery = "DeviceEvents | where ActionType contains 'Anti' | limit 20",
    
            HuntingUrl = "https://api.security.microsoft.com/api/advancedqueries",
    
            Response = Json.Document(Web.Contents(HuntingUrl, [Query=[key=AdvancedHuntingQuery]])),
    
            TypeMap = #table(
                { "Type", "PowerBiType" },
                {
                    { "Double",   Double.Type },
                    { "Int64",    Int64.Type },
                    { "Int32",    Int32.Type },
                    { "Int16",    Int16.Type },
                    { "UInt64",   Number.Type },
                    { "UInt32",   Number.Type },
                    { "UInt16",   Number.Type },
                    { "Byte",     Byte.Type },
                    { "Single",   Single.Type },
                    { "Decimal",  Decimal.Type },
                    { "TimeSpan", Duration.Type },
                    { "DateTime", DateTimeZone.Type },
                    { "String",   Text.Type },
                    { "Boolean",  Logical.Type },
                    { "SByte",    Logical.Type },
                    { "Guid",     Text.Type }
                }),
    
            Schema = Table.FromRecords(Response[Schema]),
            TypedSchema = Table.Join(Table.SelectColumns(Schema, {"Name", "Type"}), {"Type"}, TypeMap , {"Type"}),
            Results = Response[Results],
            Rows = Table.FromRecords(Results, Schema[Name]),
            Table = Table.TransformColumnTypes(Rows, Table.ToList(TypedSchema, (c) => {c{0}, c{2}}))
    
        in Table
    ```
5. Select **Done**.
6. Select **Edit Credentials**.

    [![The Edit Credentials menu item](../media/power-bi-edit-credentials.png)](../media/power-bi-edit-credentials.png#lightbox)
7. Select **Organizational account** &gt; **Sign in**.

    [![The Sign in option in the Organizational account menu item](../media/power-bi-set-credentials-organizational.png)](../media/power-bi-set-credentials-organizational.png#lightbox)
8. Enter your credentials and wait to be signed in.
9. Select **Connect**.

    [![The sign-in confirmation message in the Organizational account menu item](../media/power-bi-set-credentials-organizational-cont.png)](../media/power-bi-set-credentials-organizational-cont.png#lightbox)

Now the results of your query appear as a table and you can start to build visualizations on top of it! You can duplicate this table, rename it, and edit the Advanced Hunting query inside to get any data you would like.

## Connect Power BI to OData APIs

The only difference between the Advanced Hunting API example and the OData API example is the query inside the editor.

1. Open Microsoft Power BI.
2. Select **Get Data** &gt; **Blank Query**.

    [![The Blank Query option under the Get Data menu item](../media/power-bi-create-blank-query.png)](../media/power-bi-create-blank-query.png#lightbox)
3. Select **Advanced Editor**.

    [![The Advanced Editor menu item](../media/power-bi-open-advanced-editor.png)](../media/power-bi-open-advanced-editor.png#lightbox)
4. Copy the following code, and paste it in the editor. This query uses the OData API to retrieve all **Machine Actions** from your organization, which you can use to build reports on response activities such as device isolation or antivirus scans:

    ```dax
        let
    
            Query = "MachineActions",
    
            Source = OData.Feed("https://api.security.microsoft.com/api/" & Query, null, [Implementation="2.0", MoreColumns=true])
        in
            Source
    ```

    You can do the same for **Alerts** and **Machines**. You also can use OData queries for queries filters. See [Using OData Queries](exposed-apis-odata-samples).

## Power BI dashboard samples in GitHub

See the [Power BI report templates](https://github.com/microsoft/MicrosoftDefenderATP-PowerBI).