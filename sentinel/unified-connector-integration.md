---
layout: Conceptual
title: Connect to Microsoft Sentinel using a Unified Connector | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/unified-connector-integration
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
description: Learn how to connect to the Unified Connectors Platform that simplifies connector management across Microsoft security products including Microsoft Sentinel, Defender for Cloud, and Defender for Identity.
ms.author: monaberdugo
author: mberdugo
contributors: 
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 36e75342-5164-f3da-b4b9-7298b21d624b
document_version_independent_id: c94b80e0-5bca-d97d-07ed-1f9cd0911f97
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/unified-connector-integration.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/unified-connector-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/unified-connector-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 4e9ca038-7270-0d0a-ccb2-42f463baf2a3
---

# Connect to Microsoft Sentinel using a Unified Connector | Microsoft Learn

Use [unified connectors](unified-connector) to simplify connection management across Microsoft security products. If you already have an existing connector to a product, consider replacing it with a unified connector for centralized management.

## Prerequisites

### Microsoft Sentinel workspace

The following steps are required if you want to link an existing Okta connector to a Sentinel workspace:

1. In the Microsoft Security portal, go to **Settings** &gt; **Microsoft Sentinel**.
2. Find the connected Sentinel workspace.
3. You can link the Okta connector to any connected workspace. Choose which workspace to connect to your Okta account.

### Azure access permissions

The user setting up the Okta connector must have these roles:

- **Log Analytics Contributor**: Required to write data into the Log Analytics workspace and manage the Data Collection Rule (DCR).
- **Microsoft Sentinel Contributor**: Required to modify connector settings in Sentinel.

If you connect to both Sentinel and Defender for Identity, you need permissions for both products.

Check user roles under the **Access control (IAM)** section of the **Log analytics workspace**. If you assign the Log Analytics Contributor and Microsoft Sentinel Contributor roles, allow up to 15 minutes for the changes to take effect.

### Okta credentials

From your Okta account, you need the following information:

- **Domain name**: Your Okta URL without the `http://` prefix. For example, `yourcompany.okta.com`.
- **API token**: An Okta API token. To generate an API token, follow the instructions in [Create an API token](https://developer.okta.com/docs/guides/create-an-api-token/main/).

For information about integrating Okta with Defender for Identity, see [Integrate Okta with Microsoft Defender for Identity](/en-us/defender-for-identity/okta-integration).

## Configure a connector to a Sentinel workspace

To create a unified connector in Microsoft Sentinel:

1. Go to the [Data connectors Gallery](https://security.microsoft.com/sentinel/unified-connector), or navigate to it via **System** &gt; **Data management** &gt; **Data connectors**.

    ![Screenshot of connectors gallery.](media/unified-connector-integration/connectors-gallery.png)

    For more information, see [Data connectors Gallery](unified-connector#data-connectors-gallery) in the unified connectors article.
2. In the **My connectors** tab, find the **Unified connectors** section.

    ![Screenshot of Okta connector in the Connectors Gallery.](media/unified-connector-integration/okta-connector.png)
3. Select a connector, such as **Okta Single Sign-On**. A side panel opens with connector details and prerequisites.

    ![Screenshot of Okta connector configuration page.](media/unified-connector-integration/okta-connector-pane.png)
4. Select **Connect a connector** to open the connector configuration wizard.
5. In the **Name and connection details** section, provide the following information:

    - **Connector name**: A descriptive user friendly name for the connector.
    - **Domain name**: The Okta domain, such as `yourcompany.okta.com`.
    - **API key**: Paste the Okta API token. Include only the token value, not the *Authorization* prefix. Select **Next**.
6. In the **Select products** section, check the products you want to connect to. Check *SIEM* to enable the connector for Microsoft Sentinel.

    ![Screenshot of the select products section of the connector wizard.](media/unified-connector-integration/select-products.png)
7. Configure the product details for each product you selected:

    - Select the required workspace, whose permissions you validated in Azure access permissions.
    - Select the table manager.
8. Select **Connect**. The **Connect** button is only active when all the required fields are valid.

The connection process takes up to two minutes. If an error occurs, follow the error message to troubleshoot.

The initial state of the connector is *Pending* until data is received successfully. This takes up to 30 minutes. If data isn't successfully received, the connector shows an *Error* state.

Successfully connected connectors appear in the **My Connectors** tab, and Okta system logs flow to your Log Analytics workspace.

## Manage your connector

Existing connectors appear in the **My Connectors** tab.

![Screenshot of unified connectors list in the My connectors tab.](media/unified-connector-integration/my-connectors.png)

### Edit a connector

To edit a connector, select it and select **Manage** from the connector side panel.

![Screenshot of Okta health page with Manage button highlighted.](media/unified-connector-integration/manage-connector.png)

### Delete a connector

Warning

Deleting a connector stops data ingestion and removes the connector configuration. This action can't be undone.

You can delete a connector in one of two ways:

- Select it and select **Delete** from the connector side panel.
- Check the connector in the **My Connectors** tab and select **Delete** from above the connector list.

![Screenshot of Okta connector selected and the delete button highlighted.](media/unified-connector-integration/delete-connector.png)

## Verify data ingestion in Log analytics

To verify that the Okta connector is successfully ingesting data into your Log Analytics workspace, first make sure your Okta account is generating system logs. If no logs are generated, manually generate some test logs.

- From the Microsoft Security portal: go to **Investigation & response** &gt; **Hunting** &gt; **Advanced hunting**. After Okta logs arrive in your workspace, you should find an *OktaSystemLogs* table under the *Microsoft Sentinel* tab.
- From Azure portal, go to your selected **Log Analytics Workspace** &gt; **Logs** &gt; **OktaSystemLogs**.

Note

- It takes up to 30 minutes from when you create the the connector instance for the *OktaSystemLogs* table to appear, containing your Okta system logs.
- The connector will only ingest system logs from one hour before the instance was created.

## Considerations and limitations

Consider the following limitations when using unified connectors:

- Unified connectors aren't visible in the Content hub. To see all connectors, including the traditional Sentinel connectors, go to the [Data connectors Gallery](https://security.microsoft.com/sentinel/unified-connector).