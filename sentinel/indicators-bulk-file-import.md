---
layout: Conceptual
title: Add threat intelligence in bulk by file - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/indicators-bulk-file-import
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
description: Learn how to add threat intelligence in bulk from flat files like .csv or .json into Microsoft Sentinel.
ms.author: pauloliveria
author: poliveria
ms.reviewer: yoninave
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 4ccbe00b-f692-398a-ef6a-032f9f628be4
document_version_independent_id: 75b96eea-b437-f49d-c727-d4924743e8a6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/indicators-bulk-file-import.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/indicators-bulk-file-import
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/indicators-bulk-file-import.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 1f266050-bf3e-f31a-0660-5040405e8f83
---

# Add threat intelligence in bulk by file - Microsoft Sentinel | Microsoft Learn

This article demonstrates how to add indicators from a CSV or STIX objects from a JSON file into Microsoft Sentinel threat intelligence. Because threat intelligence sharing still happens across emails and other informal channels during an ongoing investigation, the ability to import that information quickly into Microsoft Sentinel is important to relay emerging threats to your team. The imported threat intelligence objects are then available to power other analytics, such as producing security alerts, incidents, and automated responses.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](overview#changes-for-new-customers-starting-july-2025).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

## Prerequisites

You must have read and write permissions to the Microsoft Sentinel workspace to store your threat intelligence.

## Select an import template for your threat intelligence

Add multiple threat intelligence objects with a specially crafted CSV or JSON file. Download the file templates to get familiar with the fields and how they map to the data you have. Review the required fields for each template type to validate your data before you import it.

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Threat management**, select **Threat intelligence**.

    For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Threat management** &gt; **Threat intelligence**.
2. Select **Import** &gt; **Import using a file**.

# [Defender portal](#tab/defender-portal)
[![Screenshot that shows the menu options to import threat intelligence by using a file menu from the Defender portal.](media/indicators-bulk-file-import/import-using-file-menu-defender-portal.png)](media/indicators-bulk-file-import/import-using-file-menu-defender-portal.png#lightbox)

# [Azure portal](#tab/azure-portal)
[![Screenshot that shows the menu options to import threat intelligence by using a file menu.](media/indicators-bulk-file-import/import-using-file-menu-fixed.png)](media/indicators-bulk-file-import/import-using-file-menu-fixed.png#lightbox)

---
3. On the **File format** dropdown menu, select **CSV** or **JSON**.

    ![Screenshot that shows the dropdown menu to upload a CSV or JSON file, choose a template to download, and specify a source.](media/indicators-bulk-file-import/format-select-and-download.png)

    Note

    The CSV template only supports indicators. The JSON template supports indicators and other STIX objects like threat actors, attack patterns, identities and relationships. For more information about crafting supported STIX objects in JSON, see [Upload API reference](stix-objects-api).
4. After you choose a bulk upload template, select the **Download template** link.
5. Consider grouping your threat intelligence by source because each file upload requires a source.

The CSV and JSON templates provide all the fields you need to create a single valid indicator, including required fields and validation parameters. Replicate the template field structure to populate more indicators in one file, or add STIX objects to the JSON file. For more information on the templates, see [Understand the import templates](indicators-bulk-file-import#understand-the-import-templates).

## Upload the threat intelligence file

Upload your prepared CSV or JSON file and provide the source details for the import.

1. Change the file name from the template default, but keep the file extension as .csv or .json. When you create a unique file name, it's easier to monitor your imports from the **Manage file imports** pane.
2. Drag your bulk threat intelligence file to the **Upload a file** section, or browse for the file by using the link.
3. Enter a source for the threat intelligence in the **Source** text box. The source value is stamped on all the indicators included in that file. View this property as the `SourceSystem` field. The source value is also displayed in the **Manage file imports** pane. For more information, see [Work with threat indicators](work-with-threat-indicators#find-and-view-threat-intelligence-with-queries).
4. Choose how you want Microsoft Sentinel to handle invalid entries by selecting one of the buttons at the bottom of the **Import using a file** pane:

    - Import only the valid entries and leave aside any invalid entries from the file.
    - Don't import any entries if a single object in the file is invalid.

    ![Screenshot that shows the dropdown menu to upload a CSV or JSON file, choose a template, and specify a source highlighting the Import button.](media/indicators-bulk-file-import/upload-file-pane.png)
5. Select **Import**.

## Manage file imports

Monitor your imports and view error reports for partially imported or failed imports.

1. Select **Import** &gt; **Manage file imports**.

    ![Screenshot that shows the menu option to manage file imports.](media/indicators-bulk-file-import/manage-file-imports.png)
2. Review the status of imported files and the number of invalid entries. The valid entry count is updated after the file is processed. Wait for the import to finish to get the updated count of valid entries.

    ![Screenshot that shows the Manage file imports pane with example ingestion data. The columns show sorted by imported number with various sources.](media/indicators-bulk-file-import/manage-file-imports-pane.png)
3. View and sort imports by selecting **Source**, the threat intelligence file **Name**, the number **Imported**, the **Total** number of entries in each file, or the **Created** date.
4. Select the preview of the error file or download the error file that contains the errors about invalid entries.

Microsoft Sentinel maintains the status of the file import for 30 days. The actual file and the associated error file are maintained in the system for 24 hours. After 24 hours, the file and the error file are deleted, but any ingested indicators continue to show in threat intelligence.

## Understand the import templates

Review the CSV and JSON templates to ensure that your threat intelligence is imported successfully. Be sure to reference the instructions in the CSV or JSON template file and the supplemental guidance in the CSV template structure and JSON template structure sections.

### CSV template structure

Use the CSV template options to choose the correct structure for your indicator data.

1. On the **Indicator type** dropdown menu, select **CSV**. Then choose between the **File indicators** or **All other indicator types** options.

    The CSV template needs multiple columns to accommodate the file indicator type because file indicators can have multiple hash types like MD5 and SHA256. All other indicator types like IP addresses only require the observable type and the observable value.
2. The column headings for the CSV **All other indicator types** template include fields such as `threatTypes`, single or multiple `tags`, `confidence`, and `tlpLevel`. The `tlpLevel` field sets the Traffic Light Protocol (TLP) level, which is a sensitivity designation to help make decisions on threat intelligence sharing.
3. Only the `validFrom`, `observableType`, and `observableValue` fields are required.
4. Delete the entire first row from the template to remove the comments before upload.

    The maximum file size for a CSV file import is 50 MB.

The following CSV example shows how to format a domain-name indicator for bulk import using the CSV template schema:

```CSV
threatTypes,tags,name,description,confidence,revoked,validFrom,validUntil,tlpLevel,severity,observableType,observableValue
Phishing,"demo, csv",MDTI article - Franken-Phish domainname,Entity appears in MDTI article Franken-phish,100,,2022-07-18T12:00:00.000Z,,white,5,domain-name,1776769042.tailspintoys.com
```

### JSON template structure

The JSON template uses a single STIX 2.1 structure for all supported object types. Review the following details when you prepare your JSON file.

1. There's only one JSON template for all STIX object types. The JSON template is based on the STIX 2.1 format.
2. The `type` element supports `indicator`, `attack-pattern`, `identity`, `threat-actor`, and `relationship`.
3. For indicators, the `pattern` element supports indicator types of `file`, `ipv4-addr`, `ipv6-addr`, `domain-name`, `url`, `user-account`, `email-addr`, and `windows-registry-key`.
4. Remove the template comments before upload.
5. Close the last object in the array by using the `}` without a comma.

    The maximum file size for a JSON file import is 250 MB.

The following JSON example shows how to define an `ipv4-addr` indicator and an `attack-pattern` object for bulk import using the STIX 2.1 format:

```json
[
    {
      "type": "indicator",
      "id": "indicator--dbc48d87-b5e9-4380-85ae-e1184abf5ff4",
      "spec_version": "2.1",
      "pattern": "[ipv4-addr:value = '198.168.100.5']",
      "pattern_type": "stix",
      "created": "2022-07-27T12:00:00.000Z",
      "modified": "2022-07-27T12:00:00.000Z",
      "valid_from": "2016-07-20T12:00:00.000Z",
      "name": "Sample IPv4 indicator",
      "description": "This indicator implements an observation expression.",
      "indicator_types": [
        "anonymization",
        "malicious-activity"
      ],
      "kill_chain_phases": [
          {
            "kill_chain_name": "mandiant-attack-lifecycle-model",
            "phase_name": "establish-foothold"
          }
      ],
      "labels": ["proxy","demo"],
      "confidence": "95",
      "lang": "",
      "external_references": [],
      "object_marking_refs": [],
      "granular_markings": []
    },
    {
        "type": "attack-pattern",
        "spec_version": "2.1",
        "id": "attack-pattern--fb6aa549-c94a-4e45-b4fd-7e32602dad85",
        "created": "2015-05-15T09:12:16.432Z",
        "modified": "2015-05-20T09:12:16.432Z",
        "created_by_ref": "identity--f431f809-377b-45e0-aa1c-6a4751cae5ff",
        "revoked": false,
        "labels": [
            "heartbleed",
            "has-logo"
        ],
        "confidence": 55,
        "lang": "en",
        "object_marking_refs": [
            "marking-definition--34098fce-860f-48ae-8e50-ebd3cc5e41da"
        ],
        "granular_markings": [
            {
                "marking_ref": "marking-definition--089a6ecb-cc15-43cc-9494-767639779123",
                "selectors": [
                    "description",
                    "labels"
                ],
                "lang": "en"
            }
        ],
        "extensions": {
            "extension-definition--d83fce45-ef58-4c6c-a3f4-1fbc32e98c6e": {
                "extension_type": "property-extension",
                "rank": 5,
                "toxicity": 8
            }
        },
        "external_references": [
            {
                "source_name": "capec",
                "description": "spear phishing",
                "external_id": "CAPEC-163"
            }
        ],
        "name": "Attack Pattern 2.1",
        "description": "menuPass appears to favor spear phishing to deliver payloads to the intended targets. While the attackers behind menuPass have used other RATs in their campaign, it appears that they use PIVY as their primary persistence mechanism.",
        "kill_chain_phases": [
            {
                "kill_chain_name": "mandiant-attack-lifecycle-model",
                "phase_name": "initial-compromise"
            }
        ],
        "aliases": [
            "alias_1",
            "alias_2"
        ]
    }
]
```