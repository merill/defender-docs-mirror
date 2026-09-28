---
layout: Conceptual
title: Create custom Microsoft Defender XDR reports using Microsoft Graph security API and Power BI - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-xdr-custom-reports
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Build custom Microsoft Defender XDR reports in Power BI by using Microsoft Graph security API data. Learn how to import, filter, and parameterize security data to create a SOC efficiency dashboard.
ms.service: defender-xdr
ms.sitesec: library
ms.pagetype: security
ms.localizationpriority: medium
author: poliveria
ms.author: pauloliveria
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.collection:
- m365-security
- tier2
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 1fde1f23-03da-b651-3a7d-965ef5c22a5a
document_version_independent_id: 1fde1f23-03da-b651-3a7d-965ef5c22a5a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-xdr-custom-reports.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-xdr-custom-reports
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-xdr-custom-reports.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/d3197845-b4ce-44c6-a237-cd4be160e76c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/aea905fb-0a9d-4d46-b30f-e9cbaf772d1b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 4d14e999-765a-8058-9299-865de1b8ccad
---

# Create custom Microsoft Defender XDR reports using Microsoft Graph security API and Power BI - Microsoft Defender XDR | Microsoft Learn

Empowering security professionals to visualize their data enables them to quickly recognize complex patterns, anomalies, and trends that might otherwise be lurking underneath the noise. With visualizations, SOC teams can rapidly identify threats, make informed decisions, and communicate insights effectively across the organization.

There are multiple ways to visualize Microsoft Defender security data:

- Navigating built-in reports in the Microsoft Defender portal.
- Using Microsoft Sentinel workbooks with prebuilt templates for every Defender product (requires integration with Microsoft Sentinel).
- Applying the render function in Advanced Hunting.
- Using Power BI to expand existing reporting capabilities.

In this article, we create a sample Security Operations Center (SOC) efficiency dashboard in Power BI using Microsoft Graph security API. We access the Microsoft Graph security API in user context, therefore the user must have [the required RBAC permissions](manage-rbac) to be able to view alerts and incidents data.

Note

**Example below is based on our new MS Graph security API**. Find out more at: [Use the Microsoft Graph security API](/en-us/graph/api/resources/security-api-overview).

## Importing data into Power BI

The following steps show how to get Microsoft Defender alerts data into Power BI.

1. Open Microsoft Power BI Desktop.
2. Select **Get Data &gt; Blank Query**.
3. Select **Advanced Editor**.

    [![Screenshot that shows how to create a new data query in Power BI Desktop.](media/defender-xdr-custom-reports/manage-parameters.png)](media/defender-xdr-custom-reports/manage-parameters.png#lightbox)
4. Paste in Query:

    ```console
    let
        Source = OData.Feed("https://graph.microsoft.com/v1.0/security/alerts_v2", null, [Implementation="2.0"])
    in
        Source
    ```
5. Select **Done**.
6. When you're prompted for credentials, select **Edit Credentials**:

    [![Screenshot of how to edit credentials for API connection.](media/defender-xdr-custom-reports/edit-credentials-api.png)](media/defender-xdr-custom-reports/edit-credentials-api.png#lightbox)
7. Select **Organizational account &gt; Sign in**.

    [![Screenshot of the organizational account authentication window.](media/defender-xdr-custom-reports/sign-in-org-account.png)](media/defender-xdr-custom-reports/sign-in-org-account.png#lightbox)
8. Enter credentials for account with access to Microsoft Defender XDR incidents data.
9. Select **Connect**.

Now the results of your query appear as a table, and you can start building visualizations on top of it.

Tip

If you are looking to visualize other forms of Microsoft Graph security data like Incidents, Advanced Hunting, Secure Score, etc., see [Microsoft Graph security API Overview](/en-us/graph/api/resources/security-api-overview).

## Filter Microsoft Defender XDR report data in Power BI

Microsoft Graph API supports the Open Data Protocol (OData) query protocol for filtering and pagination, so users don't have to worry about pagination - or requesting the next page of results. However, filtering data is essential to improving load times in a busy environment.

Microsoft Graph API supports [query parameters](/en-us/graph/filter-query-parameter). Here are few examples of filters used in the report:

- The following query calculates a relative lookback date and retrieves recent alerts from Microsoft Graph for the past three days. Using this query in environments with high volumes of data might result in hundreds of megabytes of data that could take a moment to load. By using this hardcoded approach, you're able to quickly see your most recent alerts over the last three days as soon as you open the report.

    ```console
    let
        AlertDays = "3",
        TIME = "" & Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()), -AlertDays), "yyyy-MM-dd") & "",
        Source = OData.Feed("https://graph.microsoft.com/v1.0/security/alerts_v2?$filter=createdDateTime ge " & TIME & "", null, [Implementation="2.0"])
    in
        Source
    ```
- Instead of collecting data across a date range, we can gather alerts across more precise dates by inputting a date using the YYYY-MM-DD format.

    ```console
    let
        StartDate = "YYYY-MM-DD",
        EndDate = "YYYY-MM-DD",
        Source = OData.Feed("https://graph.microsoft.com/v1.0/security/ alerts_v2?$filter=createdDateTime ge " & StartDate & " and createdDateTime lt " & EndDate & "", null, [Implementation="2.0"])
    in
        Source
    ```
- When historical data is required (for example, comparing the number of incidents per month), filtering by date isn't an option (since we want to go as far back as possible). In this case, the following query uses date parameters to retrieve alerts from Microsoft Graph and selects only key fields such as id, title, severity, and createdDateTime to reduce the data volume:

    ```console
    let
        Source = OData.Feed("https://graph.microsoft.com/v1.0/security/alerts_v2?$filter=createdDateTime ge " & StartLookbackDate & " and createdDateTime lt " & EndLookbackDate &
    "&$select=id,title,severity,createdDateTime", null, [Implementation="2.0"])
    in
        Source
    ```

## Create report parameters in Power BI

Instead of constantly querying the code to adjust the timeframe, use parameters to set a Start and End Date each time you open the report.

1. Go to **Query Editor**.
2. Select **Manage Parameters** &gt; **New Parameter**.
3. Set desired parameters.

    In the following example, we use two different time frames, Start and End dates.

    [![Screenshot of how to manage Parameters in Power BI.](media/defender-xdr-custom-reports/manage-parameters.png)](media/defender-xdr-custom-reports/manage-parameters.png#lightbox)
4. Remove hardcoded values from the queries and make sure that StartDate and EndDate variable names correspond to parameter names. The following parameterized query retrieves incidents created within the date range defined by the StartDate and EndDate parameters:

    ```console
    let
        Source = OData.Feed("https://graph.microsoft.com/v1.0/security/incidents?$filter=createdDateTime ge " & StartDate & " and createdDateTime lt " & EndDate & "", null, [Implementation="2.0"])
    in
        Source
    ```

## Review the custom Microsoft Defender XDR report

Once Microsoft Defender alert and incident data has been queried and the parameters are set, you can review the report. During the first launch of the Power BI template (.pbit) file, you're prompted to provide the StartDate and EndDate parameters:

[![Screenshot of the Power BI template parameter prompt window.](media/defender-xdr-custom-reports/soc-overview-dashboard.png)](media/defender-xdr-custom-reports/soc-overview-dashboard.png#lightbox)

The dashboard offers three tabs intended to provide SOC insights. The first tab provides a summary of all recent alerts (depending on the selected timeframe). The first tab helps analysts clearly understand the security state over their environment using alert details broken down by detection source, severity, total number of alerts and mean-time-to-resolution.

[![Screenshot of the alerts tab of resulting Power BI report.](media/defender-xdr-custom-reports/alert-tab-powerbi.png)](media/defender-xdr-custom-reports/alert-tab-powerbi.png#lightbox)

The second tab offers more insight into the attack data collected across the incidents and alerts. The second tab can provide analysts with greater perspective into the types of attacks executed and how they map to the [MITRE ATT&CK framework](https://attack.mitre.org/), a knowledge base that categorizes adversary tactics and techniques.

[![Screenshot of the insights tab of resulting Power BI report.](media/defender-xdr-custom-reports/insights-tab-powerbi.png)](media/defender-xdr-custom-reports/insights-tab-powerbi.png#lightbox)

## Power BI dashboard samples

For more information, see the [Power BI report templates sample file](https://download.microsoft.com/download/0/1/6/01686830-b4e4-4cc1-af5b-7e07eab3ff55/defender-xdr-soc-overview.zip).