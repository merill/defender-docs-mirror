---
layout: Conceptual
title: Stream data from Microsoft Purview Information Protection to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-microsoft-purview
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
description: Stream data from Microsoft Purview Information Protection (formerly Microsoft Information Protection) to Microsoft Sentinel so you can analyze and report on data from the Microsoft Purview labeling clients and scanners.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 39650628-9ac9-573f-1b0c-5be48cfa75ee
document_version_independent_id: 9e7acc85-83ac-9ee0-d248-a81f307f6a57
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-microsoft-purview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-microsoft-purview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-microsoft-purview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://authoring-docs-microsoft.poolparty.biz/devrel/c900d0ba-7127-44a2-8ba8-afc4f786377d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://authoring-docs-microsoft.poolparty.biz/devrel/179dea74-32c0-4804-9e75-383800f5d15e
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 77a066dd-16cb-9b8e-ff46-54a3d01c95b7
---

# Stream data from Microsoft Purview Information Protection to Microsoft Sentinel | Microsoft Learn

This article describes how to stream data from Microsoft Purview Information Protection (formerly Microsoft Information Protection or MIP) to Microsoft Sentinel. You can use the data ingested from the Microsoft Purview labeling clients and scanners to track, analyze, report on the data, and use it for compliance purposes.

Important

The Microsoft Purview Information Protection connector is currently in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Overview

Auditing and reporting are an important part of organizations' security and compliance strategy. With the continued expansion of the technology landscape that has an ever-increasing number of systems, endpoints, operations, and regulations, it becomes even more important to have a comprehensive logging and reporting solution in place.

With the Microsoft Purview Information Protection connector, you stream auditing events generated from unified labeling clients and scanners. The data is then emitted to the Microsoft 365 audit log for central reporting in Microsoft Sentinel.

With the connector, you can:

- Track adoption of labels, explore, query, and detect events.
- Monitor labeled and protected documents and emails.
- Monitor user access to labeled documents and emails, while tracking classification changes.
- Gain visibility into activities performed on labels, policies, configurations, files and documents. This visibility helps security teams identify security breaches, and risk and compliance violations.
- Use the connector data during an audit, to prove that the organization is compliant.

### Azure Information Protection connector vs. Microsoft Purview Information Protection connector

This connector replaces the Azure Information Protection (AIP) data connector. The Azure Information Protection (AIP) data connector uses the AIP audit logs (public preview) feature.

Important

As of **March 31, 2023**, the AIP analytics and audit logs public preview will be retired. Customers should use the [Microsoft 365 auditing solution](/en-us/microsoft-365/compliance/auditing-solutions-overview) moving forward.

For more information:

- See [Removed and retired services](/en-us/azure/information-protection/removed-sunset-services#azure-information-protection-analytics).
- Learn how to disconnect the AIP connector.

When you enable the Microsoft Purview Information Protection connector, audit logs stream into the standardized `MicrosoftPurviewInformationProtection` table. Data is gathered through the [Office Management API](/en-us/office/office-365-management-api/office-365-management-activity-api-schema), which uses a structured schema. The `MicrosoftPurviewInformationProtection` table schema enhances the deprecated schema used by AIP, with more fields and easier access to parameters.

Review the list of supported [audit log record types and activities](microsoft-purview-record-types-activities).

## Prerequisites

Before you begin, verify that you have:

- The Microsoft Sentinel solution enabled.
- A defined Microsoft Sentinel workspace.
- A valid license to M365 E3, M365 A3, Microsoft Business Basic or any other Audit eligible license. Read more about [auditing solutions in Microsoft Purview](/en-us/microsoft-365/compliance/audit-solutions-overview).
- [Enabled Sensitivity labels for Office](/en-us/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files?view=o365-worldwide#use-the-microsoft-purview-compliance-portal-to-enable-support-for-sensitivity-labels&amp;preserve-view=true) and [enabled auditing](/en-us/microsoft-365/compliance/turn-audit-log-search-on-or-off?view=o365-worldwide#use-the-compliance-center-to-turn-on-auditing&amp;preserve-view=true).
- The Security Administrator role on the tenant, or the equivalent permissions.

## Set up the connector

To set up the Microsoft Purview Information Protection connector, perform the following steps.

Note

If you set the connector on a workspace located in a different region than your Office 365 location, data might be streamed across regions.

1. Open the [Azure portal](https://portal.azure.com/) and navigate to the **Microsoft Sentinel** service.
2. In the **Data connectors** blade, in the search bar, type *Purview*.
3. Select the **Microsoft Purview Information Protection (Preview)** connector.
4. Below the connector description, select **Open connector page**.
5. Under **Configuration**, select **Connect**.

    When a connection is established, the **Connect** button changes to **Disconnect**. You're now connected to the Microsoft Purview Information Protection.

Review the list of supported [audit log record types and activities](microsoft-purview-record-types-activities).

## Disconnect the Azure Information Protection connector

We recommend using the Azure Information Protection connector and the Microsoft Purview Information Protection connector simultaneously (both enabled) for a short testing period. After the testing period, we recommend that you disconnect the Azure Information Protection connector to avoid data duplication and redundant costs.

To disconnect the Azure Information Protection connector:

1. In the **Data connectors** blade, in the search bar, type *Azure Information Protection*.
2. Select **Azure Information Protection**.
3. Below the connector description, select **Open connector page**.
4. Under **Configuration**, select **Connect Azure Information Protection logs**.
5. Clear the selection for the workspace from which you want to disconnect the connector, and select **OK**.

## Known issues and limitations

Be aware of the following known issues and limitations when using this connector:

- Sensitivity label events collected through the Office Management API do not populate the Label Names. Customers can use watchlists or enrichments defined in KQL as the example below.
- The Office Management API doesn't obtain a Downgrade Label with the names of the labels before and after the downgrade. To retrieve this information, extract the `labelId` of each label and enrich the results.

    Here's an example KQL query:

    ```kusto
    let labelsMap = parse_json('{'
     '"566a334c-ea55-4a20-a1f2-cef81bfaxxxx": "MyLabel1",'
     '"aa1c4270-0694-4fe6-b220-8c7904b0xxxx": "MyLabel2",'
     '"MySensitivityLabelId": "MyLabel3"'
     '}');
     MicrosoftPurviewInformationProtection
     | extend SensitivityLabelName = iff(isnotempty(SensitivityLabelId), 
    tostring(labelsMap[tostring(SensitivityLabelId)]), "")
     | extend OldSensitivityLabelName = iff(isnotempty(OldSensitivityLabelId), 
    tostring(labelsMap[tostring(OldSensitivityLabelId)]), "")
    ```
- The `MicrosoftPurviewInformationProtection` table and the `OfficeActivity` table might include some duplicated events.

See more information in the Kusto documentation for the functions and operators used in the example KQL query:

- [***let*** statement](/en-us/kusto/query/let-statement?view=microsoft-sentinel&amp;preserve-view=true)
- [***extend*** operator](/en-us/kusto/query/extend-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***parse\_json()*** function](/en-us/kusto/query/parse-json-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***iff()*** function](/en-us/kusto/query/iff-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***tostring()*** function](/en-us/kusto/query/tostring-function?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)