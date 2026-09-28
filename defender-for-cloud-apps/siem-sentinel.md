---
layout: Conceptual
title: Integrate Microsoft Sentinel with Microsoft Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/siem-sentinel
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Learn how to set up the Microsoft Sentinel integration for Microsoft Defender for Cloud Apps to monitor alerts and discovery data. SIEM agents are deprecated; Microsoft Sentinel integration (Preview) is still supported.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Naama-Goldbart
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: cb69adc1-6ce6-7108-abdc-47ce4053f0a9
document_version_independent_id: cb69adc1-6ce6-7108-abdc-47ce4053f0a9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/siem-sentinel.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: siem-sentinel
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/siem-sentinel.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 28a74cd5-14b5-d679-5e11-52b6bdb97301
---

# Integrate Microsoft Sentinel with Microsoft Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn

## Integrate Microsoft Defender for Cloud Apps with Microsoft Sentinel

Important

**Deprecation Notice: Microsoft Defender for Cloud Apps SIEM Agents**

As part of our ongoing convergence process across Microsoft Defender workloads, Microsoft Defender for Cloud Apps SIEM agents will be deprecated starting **November 2025**.

Existing Microsoft Defender for Cloud Apps SIEM agents will continue to function as is until November 2025. As of June 19, 2025, **no new SIEM agents can be configured**, but [Microsoft Sentinel](siem-sentinel) agent integration (Preview), will remain supported and can still be added.

We recommend transitioning to APIs that support the management of activities and alerts data from multiple workloads. These APIs enhance security monitoring and management and offer additional capabilities using data from multiple Microsoft Defender workloads.

To ensure continuity and access to data currently available through Microsoft Defender for Cloud Apps SIEM agents, we recommend transitioning to supported APIs such as the Microsoft Defender XDR Streaming API, IdentityLogonEvents, the Microsoft Graph Security Alerts API, and the Microsoft Defender XDR incidents API:

- For alerts and activities, see: [Microsoft Defender XDR Streaming API](/en-us/defender-xdr/streaming-api).
- For Microsoft Entra ID Protection logon events, see [IdentityLogonEvents](/en-us/defender-xdr/advanced-hunting-identitylogonevents-table) table in the advanced hunting schema.
- For Microsoft Graph Security Alerts API, see: [List alerts_v2](/en-us/graph/api/security-list-alerts_v2?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true)
- To view Microsoft Defender for Cloud Apps alerts data in the Microsoft Defender XDR incidents API, see [Microsoft Defender XDR incidents APIs and the incidents resource type](/en-us/graph/api/security-list-alerts_v2?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true)

You can integrate Microsoft Defender for Cloud Apps with Microsoft Sentinel (a scalable, cloud-native SIEM and SOAR) to enable centralized monitoring of alerts and discovery data. Integrating with Microsoft Sentinel allows you to better protect your cloud applications while maintaining your usual security workflow, automating security procedures, and correlating between cloud-based and on-premises events.

Benefits of using Microsoft Sentinel include:

- Longer data retention provided by Log Analytics.
- Out-of-the-box visualizations.
- Use tools such as Microsoft Power BI or Microsoft Sentinel workbooks to create your own discovery data visualizations that fit your organizational needs.

Other supported integration solutions for Defender for Cloud Apps include:

- **Generic SIEMs** - Integrate Defender for Cloud Apps with your generic SIEM server. For information in integrating with a Generic SIEM, see [Generic SIEM integration](siem).
- **Microsoft security graph API** - An intermediary service (or broker) that provides a single programmatic interface to connect multiple security providers. For more information, see [Security solution integrations using the Microsoft Graph Security API](/en-us/graph/security-integration#list-of-connectors-from-microsoft).

Integrating with Microsoft Sentinel includes configuration in both Defender for Cloud Apps and Microsoft Sentinel.

## Prerequisites

To integrate with Microsoft Sentinel:

- You must have a valid Microsoft Sentinel license
- You must be at least a Security Administrator in your tenant.

### US Government support

The direct Defender for Cloud Apps - Microsoft Sentinel integration is available to commercial customers only.

However, all Defender for Cloud Apps data is available in Microsoft Defender XDR, and therefore available in Microsoft Sentinel via the Microsoft Defender XDR connector.

We recommend that GCC, GCC High, and DoD customers who are interested in seeing Defender for Cloud Apps data in Microsoft Sentinel install the Microsoft Defender XDR solution.

For more information, see:

- [Microsoft Defender XDR integration with Microsoft Sentinel](/en-us/azure/sentinel/microsoft-365-defender-sentinel-integration)
- [Microsoft Defender for Cloud Apps for US Government offerings](editions-cloud-app-security-gcc)

### Integrating with Microsoft Sentinel

Use the following steps to integrate Defender for Cloud Apps with Microsoft Sentinel.

1. In the Microsoft Defender Portal, select **Settings &gt; Cloud Apps**.
2. Under **System**, select **SIEM agents &gt; Add SIEM agent &gt; Sentinel**. For example:

    ![Screenshot of the SIEM agents page in Defender for Cloud Apps showing the Add SIEM agent option with Sentinel selected.](media/siem0.png)

    Note

    The option to add Microsoft Sentinel is not available if you have previously performed the integration.
3. In the wizard, select the data types you want to forward to Microsoft Sentinel. You can configure the integration, as follows:

    - **Alerts**: Alerts are automatically turned on once Microsoft Sentinel is enabled.
    - **Discovery logs**: Use the slider to enable and disable them, by default, everything is selected, and then use the **Apply to** drop-down to filter which discovery logs are sent to Microsoft Sentinel.

    For example:

    ![Screenshot of the Configure Microsoft Sentinel integration wizard where you select alerts and discovery logs data types to forward.](media/siem-sentinel-configuration.png)
4. Select **Next**, and continue to Microsoft Sentinel to finalize the integration. For information on configuring Microsoft Sentinel, see [Microsoft Sentinel data connector for Defender for Cloud Apps](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-for-cloud-apps). For example:

    ![Screenshot of the completion page confirming that the Microsoft Sentinel integration setup is finished and ready to finalize in Microsoft Sentinel.](media/siem-sentinel-configuration-complete.png)

Note

New discovery logs will usually appear in Microsoft Sentinel within 15 minutes of configuring them in Defender for Cloud Apps. However, it may take longer depending on system environment conditions. For more information, see [Handle ingestion delay in analytics rules](/en-us/azure/sentinel/ingestion-delay).

## Alerts and discovery logs in Microsoft Sentinel

Once the integration is completed, you can view Defender for Cloud Apps alerts and discovery logs in Microsoft Sentinel.

In Microsoft Sentinel, under **Logs**, under **Security Insights**, you can find the logs for the Defender for Cloud Apps data types, as follows:

| Data type | Table |
| --- | --- |
| Discovery logs | McasShadowItReporting |
| Alerts | SecurityAlert |

The following table describes each field in the **McasShadowItReporting** schema:

| Field | Type | Description | Examples |
| --- | --- | --- | --- |
| **TenantId** | String | Workspace ID | aaaabbbb-0000-cccc-1111-dddd2222eeee |
| **SourceSystem** | String | Source system – static value | Azure |
| **TimeGenerated [UTC]** | DateTime | Date of discovery data | 2019-07-23T11:00:35.858Z |
| **StreamName** | String | Name of the specific stream | Marketing Department |
| **TotalEvents** | Integer | Total number of events per session | 122 |
| **BlockedEvents** | Integer | Number of blocked events | 0 |
| **UploadedBytes** | Integer | Amount of uploaded data | 1,514,874 |
| **TotalBytes** | Integer | Total amount of data | 4,067,785 |
| **DownloadedBytes** | Integer | Amount of downloaded data | 2,552,911 |
| **IpAddress** | String | Source IP address | 127.0.0.0 |
| **UserName** | String | User name | `Raegan@contoso.com` |
| **EnrichedUserName** | String | Enriched user name with Microsoft Entra username | `Raegan@contoso.com` |
| **AppName** | String | Name of cloud app | Microsoft OneDrive for Business |
| **AppId** | Integer | Cloud app identifier | 15600 |
| **AppCategory** | String | Category of cloud app | Cloud storage |
| **AppTags** | String array | Built-in and custom tags defined for the app | ["sanctioned"] |
| **AppScore** | Integer | The risk score of the app in a scale 0-10, 10 being a score for a non-risky app | 10 |
| **Type** | String | Type of logs – static value | McasShadowItReporting |

## Use Power BI with Defender for Cloud Apps data in Microsoft Sentinel

Once the integration is completed, you can also use the Defender for Cloud Apps data stored in Microsoft Sentinel in other tools.

You can use Microsoft Power BI with Defender for Cloud Apps data in Microsoft Sentinel to shape and combine data and build reports and dashboards that meet the needs of your organization.

To get started:

1. In Power BI, import queries from Microsoft Sentinel for Defender for Cloud Apps data. For more information, see [Import Azure Monitor log data into Power BI](/en-us/azure/azure-monitor/logs/log-powerbi).
2. [Install the Defender for Cloud Apps Shadow IT Discovery app](https://aka.ms/MCASShadowITReporting) and connect it to your discovery log data to view the built-in Shadow IT Discovery dashboard. To connect the app, open it in Power BI, select **Connect**, enter your Microsoft Sentinel workspace ID, and then sign in. For detailed steps, see Connect the Defender for Cloud Apps Shadow IT Discovery app.

    Note

    Currently, the app is not published on Microsoft AppSource. Therefore, you may need to contact your Power BI admin for permissions to install the app.

    For example:

    ![Screenshot of the Shadow IT Discovery dashboard in Power BI showing discovered cloud app usage and activity metrics from Defender for Cloud Apps.](media/siem-sentinel-configuration-powerbi-dashboard.png)
3. Optionally, build custom dashboards in Power BI Desktop and tweak it to fit the visual analytics and reporting requirements of your organization.

### Connect the Defender for Cloud Apps app

Use the following steps to connect the Defender for Cloud Apps Shadow IT Discovery app in Power BI.

1. In Power BI, select **Apps &gt; Shadow IT Discovery** app.
2. On the **Get started with your new app** page, select **Connect**. For example:

    ![Screenshot of the Power BI Get started with your new app page where you select Connect to link the Shadow IT Discovery app to Microsoft Sentinel data.](media/siem-sentinel-powerbi-connect.png)
3. On the workspace ID page, enter your Microsoft Sentinel workspace ID as displayed in your log analytics overview page, and then select **Next**. For example:

    ![Screenshot of the Power BI prompt to enter the Microsoft Sentinel workspace ID for connecting the Shadow IT Discovery app.](media/siem-sentinel-powerbi-workspace-id.png)
4. On the authentication page, specify the authentication method and privacy level, and then select **Sign in**. For example:

    ![Screenshot of the authentication page for signing in to connect the Power BI Shadow IT Discovery app to Microsoft Sentinel data.](media/siem-sentinel-powerbi-authentication.png)
5. After connecting your data, go to the workspace **Datasets** tab and select **Refresh**. This will update the report with your own data.

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).