---
layout: Conceptual
title: Create New Watchlists - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/watchlists-create
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
description: Learn how to create a watchlist in Microsoft Sentinel to build allowlists or blocklists, enrich event data, and investigate threats.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 12e5a970-b1ac-1298-f46f-1119dda0724f
document_version_independent_id: fb989cc5-882f-5971-44d5-da287faa1260
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/watchlists-create.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/watchlists-create
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/watchlists-create.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 99cdfbe9-35fc-0404-71be-7b11f1cae826
---

# Create New Watchlists - Microsoft Sentinel | Microsoft Learn

Watchlists in Microsoft Sentinel help you correlate data from a data source you provide with the events in your Microsoft Sentinel environment. For example, you might create a watchlist with a list of high value assets, terminated employees, or service accounts in your environment.

You can create a watchlist by using any of the following methods:

- Upload a watchlist file from a local folder
- Upload a watchlist file from your Azure Storage account
- Create a watchlist manually

You can upload local files up to 3.8 MB. A file that's over 3.8 MB and up to 500 MB is considered a large watchlist. To upload a large watchlist, upload the file to an Azure Storage account. Before you create a watchlist, review the [limitations of watchlists](watchlists#watchlist-limitations).

Data in the Log Analytics Watchlist table is retained for 28 days.

Important

The features for watchlist templates, the ability to create a watchlist from a file in Azure Storage, and the ability to create a watchlist manually are currently in **PREVIEW**. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](overview#changes-for-new-customers-starting-july-2025).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

## Upload a watchlist from a local folder

You have two ways to upload a CSV file from your local machine to create a watchlist.

- For a watchlist file you created without a watchlist template: Select **Add new** and enter the required information.
- For a watchlist file created from a template downloaded from Microsoft Sentinel: Go to the watchlist **Templates (Preview)** tab. Select the option **Create from template**. Azure pre-populates the name, description, and watchlist alias for you.

### Upload a watchlist from a file you created

If you didn't use a watchlist template to create the CSV watchlist file:

1. In the [Defender portal](https://security.microsoft.com/), go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Watchlist**.
2. Select **+ New** to open the **Watchlist wizard**.

    [![Screenshot of the Microsoft Sentinel Watchlist page with the New button highlighted.](media/watchlists-create/sentinel-watchlist-new-defender.png)](media/watchlists-create/sentinel-watchlist-new-defender.png#lightbox)
3. On the **General** page, enter the name, description, and alias for the watchlist, and then select **Next: Source**.

    ![Screenshot of watchlist general tab in the watchlists wizard.](media/watchlists-create/sentinel-watchlist-general-country.png)
4. On the **Source** page, use the information in the following table to upload your watchlist data, and then select **Next: Review + create**.

    | Field | Description |
    | --- | --- |
    | Source type | Local file |
    | File type | CSV file with a header (.csv) |
    | Number of lines before row with headings | Enter the number of lines before the header row that's in your data file. |
    | Upload file | Either drag and drop your data file, or select **Browse for files** and select the file to upload. |
    | SearchKey | Enter the name of a column in your watchlist that you expect to use as a join with other data or a frequent object of searches. For example, if your server watchlist contains country/region names and their respective two-letter country codes, and you expect to use the country codes often for search or joins, use the **Code** column as the SearchKey. |

    Note

    If your CSV file is larger than 3.8 MB, you need to use the instructions for Create a large watchlist from file in Azure Storage.

    [![Screenshot showing the watchlist source tab.](media/watchlists-create/sentinel-watchlist-source.png)](media/watchlists-create/sentinel-watchlist-source.png#lightbox)
5. Review the information, verify that it's correct, and then select **Create**.

    ![Screenshot of the watchlist review page.](media/watchlists-create/sentinel-watchlist-review.png)

    A notification appears once the watchlist is created.

It might take several minutes for the watchlist to be created and the new data to be available in queries.

### Upload a watchlist created from a template (preview)

To create a watchlist from a populated watchlist template file:

1. In the [Defender portal](https://security.microsoft.com/), go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Watchlist**.
2. Select the tab **Templates (Preview)**.
3. Select the appropriate template from the list to view details of the template in the right pane.
4. Select **Create from template** to open the **Watchlist wizard**.

    [![Screenshot of the option to create a watchlist from a built-in template.](media/watchlists-create/create-watchlist-from-template.png)](media/watchlists-create/create-watchlist-from-template.png#lightbox)
5. On the **General** page, notice that the **Name**, **Description**, and **Alias** fields are all read-only. Select **Next: Source**.
6. On the **Source** page, select **Browse for files**, and then select the file you created from the template.
7. Select **Next: Review + create**, and then select **Create**. A notification appears once the watchlist is created.

It might take several minutes for the watchlist to be created and the new data to be available in queries.

## Create a large watchlist from file in Azure Storage (preview)

If you have a large watchlist up to 500 MB, upload your watchlist file to your Azure Storage account. Then create a shared access signature URL for Microsoft Sentinel to retrieve the watchlist data. A shared access signature URL is a URI that contains both the resource URI and shared access signature token of a resource like a CSV file in your storage account. Finally, create the watchlist in your Microsoft Sentinel workspace by using the uploaded file's SAS URL.

For more information about shared access signatures, see [Azure Storage shared access signature token](/en-us/azure/storage/common/storage-sas-overview#sas-token).

### Step 1: Upload a watchlist file to Azure Storage

To upload a large watchlist file to your Azure Storage account, use AzCopy or the Azure portal.

1. If you don't already have an Azure Storage account, [create a storage account](/en-us/azure/storage/common/storage-account-create). The storage account can be in a different resource group or region from your workspace in Microsoft Sentinel.
2. Use either AzCopy or the Azure portal to upload your CSV file with your watchlist data into the storage account.

#### Upload your file with AzCopy

Upload files and directories to Blob storage by using the AzCopy v10 command-line utility. To learn more, see [Upload files to Azure Blob storage by using AzCopy](/en-us/azure/storage/common/storage-use-azcopy-blobs-upload).

1. If you don't already have a storage container, create the destination blob container in your storage account to hold the watchlist file. Run the following command.

    ```azcopy
    azcopy make 
    https://<storage-account-name>.<blob or dfs>.core.windows.net/<container-name>
    ```
2. Upload the local watchlist CSV file to the blob container so it can be referenced by a SAS URL. Run the following command.

    ```azcopy
    azcopy copy '<local-file-path>' 'https://<storage-account-name>.<blob or dfs>.core.windows.net/<container-name>/<blob-name>'
    ```

#### Upload your file in Azure portal

If you don't use AzCopy, upload your watchlist CSV file by using the Azure portal. Go to your storage account in Azure portal to upload the CSV file with your watchlist data.

1. If you don't already have an existing storage container, [create a container](/en-us/azure/storage/blobs/storage-quickstart-blobs-portal#create-a-container). For the level of public access to the container, use the default which is set to **Private (no anonymous access)**.
2. [Upload a block blob](/en-us/azure/storage/blobs/storage-quickstart-blobs-portal#upload-a-block-blob) to upload your CSV file to the storage account.

### Step 2: Create shared access signature URL

Create a public Blob SAS URL for Microsoft Sentinel to retrieve the watchlist data. Only public Blob SAS URI is supported.

1. Follow the steps in [Create SAS tokens for blobs in the Azure portal](/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=blobs#create-sas-tokens-in-the-azure-portal).
2. Set the shared access signature token expiry time to at least six hours.
3. Keep the default value for **Allowed IP addresses** as blank.
4. Copy the value for **Blob SAS URL**.

### Step 3: Add Azure to the Cross-Origin Resource Sharing (CORS) tab

Before you use a SAS URI, add the Azure portal to the Cross-Origin Resource Sharing (CORS) configuration.

1. Go to the storage account settings, **Resource sharing** page.
2. Select the **Blob service** tab.
3. Add `https://*.portal.azure.net` to the allowed origins table.
4. Select the appropriate **Allowed methods** of `GET` and `OPTIONS`.
5. Save the configuration.

For more information, see [CORS support for Azure Storage](/en-us/rest/api/storageservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services).

### Step 4: Add the watchlist to a workspace

To add the watchlist from Azure Storage to your Microsoft Sentinel workspace, complete the following steps:

1. In the [Defender portal](https://security.microsoft.com/), go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Watchlist**.
2. Select **+ New** to open the **Watchlist wizard**.
3. On the **General** page, enter the name, description, and alias for the watchlist, and then select **Next: Source**.
4. On the **Source** page, use the information in the following table to upload your watchlist data, and then select **Next: Review + create**.

    | Field | Description |
    | --- | --- |
    | Source type | Azure Storage (Preview) |
    | Select a type for the dataset | CSV file with a header (.csv) |
    | Number of lines before row with headings | Enter the number of lines before the header row that's in your data file. |
    | Blob SAS URL (Preview) | Paste the shared access URL you created. |
    | SearchKey | Enter the name of a column in your watchlist that you expect to use as a join with other data or a frequent object of searches. For example, if your server watchlist contains country/region names and their respective two-letter country codes, and you expect to use the country codes often for search or joins, use the **Code** column as the SearchKey. |
5. Review the information, verify that it's correct, and then select **Create**. A notification appears once the watchlist is created.

It might take a while for a large watchlist to be created and for the new data to be available in queries.

## Create a watchlist manually (preview)

To create a watchlist from scratch:

1. In the [Defender portal](https://security.microsoft.com/), go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Watchlist**.
2. Select **+ New** to open the **Watchlist wizard**.
3. On the **General** page, enter the name, description, and alias for the watchlist, and then select **Next: Source**.
4. On the **Source** page, choose **Manual (Preview)** as the **Source type**.
5. Add and define the column names for your watchlist. Choose the column that serves as your **Search Key**. This key is the column in your watchlist that you expect to use as a join with other data or a frequent object of searches.

    [![Screenshot of the option to create a watchlist manually.](media/watchlists-create/create-watchlist-manual.png)](media/watchlists-create/create-watchlist-manual.png#lightbox)
6. Select **Next: Review + create**.
7. Review the information, verify that it's correct, and then select **Create**. A notification appears once the watchlist is created.

It might take several minutes for the watchlist to be created and the new data to be available in queries.

Note

Watchlists you create manually automatically contain a single entry that uses default values. You can update this entry as needed. For more information, see [Manage watchlists](watchlists-manage).

## View watchlist status

To view the status of a watchlist in your workspace:

1. In the [Defender portal](https://security.microsoft.com/), go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Watchlist**.
2. On the **My Watchlists** tab, select the watchlist.
3. On the details page, review the **Status (Preview)**.

    [![Screenshot that shows the status on the watchlist.](media/watchlists-create/view-status-uploading.png)](media/watchlists-create/view-status-uploading.png#lightbox)
4. When the status is **Succeeded**, select **View in logs** to use the watchlist in a query. It might take several minutes for the watchlist to show in Log Analytics.

    [![Screenshot of the watchlist page with View in logs button highlighted.](media/watchlists-create/large-watchlist-status-view-in-log.png)](media/watchlists-create/large-watchlist-status-view-in-log.png#lightbox)

## Download watchlist template (preview)

Download one of the watchlist templates from Microsoft Sentinel to populate with your data. Then upload the populated template CSV file when you create the watchlist in Microsoft Sentinel.

Each built-in watchlist template has its own set of data listed in the CSV file attached to the template. For more information, see [Built-in watchlist schemas](watchlist-schemas).

To download one of the watchlist templates:

1. In the [Defender portal](https://security.microsoft.com/), go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Watchlist**.
2. Select the tab **Templates (Preview)**.
3. Select a template from the list to view details of the template in the right pane.
4. Select the ellipses **...** at the end of the row.
5. Select **Download Schema**.

    ![Screenshot of the Watchlist Templates tab with the Download Schema option selected from the context menu.](media/watchlists-create/create-watchlist-download-schema.png)
6. Populate your local version of the file and save it locally as a CSV file.
7. Follow the steps in Upload a watchlist created from a template (Preview).

## Understand deleted and recreated watchlists in Log Analytics

If you delete and recreate a watchlist, you might see both the deleted and recreated entries in Log Analytics within the five-minute SLA for data ingestion. If you see these entries together in Log Analytics for a longer period of time, submit a support ticket.