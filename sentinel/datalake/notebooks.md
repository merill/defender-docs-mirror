---
layout: Conceptual
title: Running Notebooks on the Microsoft Sentinel Data Lake - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/notebooks
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
ms.subservice: sentinel-platform
search.appverid: met150
description: This article describes how to explore and interact with data lake data using Jupyter notebooks in Visual Studio Code.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: zeinam
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 45cf0317-b92f-9202-dfc6-8bc59024748b
document_version_independent_id: bf2963ff-5b54-3caf-815d-1463293fd2fe
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/notebooks.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/notebooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/notebooks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/911a44a7-2f6c-477c-810f-dc8b7d425cce
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/14f2b9d5-6f06-45a8-ac5f-313eaa351153
platformId: e4ad2d47-9d01-cdb9-b75f-95e6deeaeec0
---

# Running Notebooks on the Microsoft Sentinel Data Lake - Microsoft Security | Microsoft Learn

Jupyter notebooks provide an interactive environment for exploring, analyzing, and visualizing data in the Microsoft Sentinel data lake and federated tables. With notebooks, you can write and execute code, document your workflow, and view results—all in one place. This all-in-one notebook environment makes it easy to perform data exploration, build advanced analytics solutions, and share insights with others. By leveraging Python and Apache Spark within Visual Studio Code, notebooks help you transform raw security data into actionable intelligence.

This article shows you how to explore and interact with data lake data using Jupyter notebooks in Visual Studio Code.

## Prerequisites

### Onboard to the Microsoft Sentinel data lake

To use notebooks in the Microsoft Sentinel data lake, you must first onboard to the data lake. If you haven't onboarded to the Sentinel data lake, see [Onboarding to Microsoft Sentinel data lake](sentinel-lake-onboarding). If you have recently onboarded to the data lake, it may take some time until sufficient volume of data is ingested before you can create meaningful analyses using notebooks.

### Required permissions for data lake notebooks

Microsoft Entra ID roles provide broad access across all workspaces in the data lake. Alternatively you can grant access to individual workspaces using Azure RBAC roles. Users with Azure RBAC permissions to Microsoft Sentinel workspaces can run notebooks against those workspaces in the data lake tier. For more information, see [Roles and permissions in Microsoft Sentinel](../roles#roles-and-permissions-for-the-microsoft-sentinel-data-lake).

Optionally, Microsoft Sentinel scoping or row-level RBAC can be configured to further restrict data access within a workspace. When enabled, row-level scoping limits the data returned by queries based on the user’s assigned scope. If row-level scoping isn’t configured, the existing workspace-level permission model applies unchanged. For more information, see [Configure Microsoft Sentinel scoping (row-level RBAC) (preview)](../scoping).

To create new custom tables in the analytics tier, the data lake managed identity must be assigned the **Log Analytics Contributor** role in the Log Analytics workspace.

To assign the role, follow the steps below:

1. In the Azure portal, navigate to the Log Analytics workspace that you want to assign the role to.
2. Select **Access control (IAM)** in the left navigation pane.
3. Select **Add role assignment**.
4. In the **Role** table, select **Log Analytics Contributor**, then select **Next**
5. Select **Managed identity**, then select **Select members**.
6. Your data lake managed identity is a system assigned managed identity named `msg-resources-<guid>`. Select the managed identity, then select **Select**.
7. Select **Review and assign**.

For more information on assigning roles to managed identities, see [Assign Azure roles using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal).

### Install Visual Studio Code and the Microsoft Sentinel extension

If you don't already have Visual Studio Code, download and install Visual Studio Code for [Mac](https://code.visualstudio.com/docs/?dv=osx), [Linux](https://code.visualstudio.com/docs/?dv=linux), or [Windows](https://code.visualstudio.com/docs/?dv=win).

The Microsoft Sentinel extension for Visual Studio Code (VS Code) is installed from the extensions marketplace. To install the extension, follow these steps:

1. Select the Extensions Marketplace in the left toolbar.
2. Search for *Sentinel*.
3. Select the **Microsoft Sentinel** extension and select **Install**.
4. After the extension is installed, the Microsoft Sentinel ![Image of the Microsoft Sentinel extension icon in the Visual Studio Code toolbar](media/notebook-jobs/sentinel-icon.png) icon appears in the left toolbar.

[![A screenshot showing the extension market place.](media/notebooks/install-sentinel-extension.png)](media/notebooks/install-sentinel-extension.png#lightbox)

Install the GitHub Copilot extension for Visual Studio Code to enable code completion and suggestions in notebooks.

1. Search for *GitHub Copilot* in the Extensions Marketplace and install it.
2. After installation, sign in to GitHub Copilot using your GitHub account.

## Explore data lake tier tables

After installing the Microsoft Sentinel extension, you can start exploring data lake tier tables and creating Jupyter notebooks to analyze the data.

### Sign in to the Microsoft Sentinel extension

To sign in to the Microsoft Sentinel extension, follow these steps:

1. Select the Microsoft Sentinel ![Image of the Microsoft Sentinel extension icon used to open the extension in Visual Studio Code](media/notebook-jobs/sentinel-icon.png) icon in the left toolbar.
2. A dialog appears with the following text **The extension "Microsoft Sentinel" wants to sign in using Microsoft**. Select **Allow**.

    [![A screenshot showing the sign in dialog.](media/notebooks/sign-in.png)](media/notebooks/sign-in.png#lightbox)
3. Select your account name to complete the sign in.

    [![A screenshot showing the account selection list at the top of the page.](media/notebooks/select-account.png)](media/notebooks/select-account.png#lightbox)

    If you have multiple guest accounts associated with your login, you can seamlessly switch between accounts. To switch between accounts, select the account name at the bottom left of the Visual Studio Code window. Only one account can be selected at a time.

    [![A screenshot showing how to switch accounts in Visual Studio Code.](media/notebooks/account-picker.png)](media/notebooks/account-picker.png#lightbox)

    Important

    Switching between accounts disconnects any active pyspark sessions.

### View data lake tables and jobs

Once you sign in, the Sentinel extension displays a list of **Lake tables** and **Jobs** in the left pane. The tables are grouped by the database and category. Federated tables are displayed under the **Federated tables** category under **System tables**. Select a table to see the column definitions.

For information about scheduling notebook jobs, see Create and manage notebook jobs and schedules in this article. For more information on federated tables, see [Using federated tables in the Microsoft Sentinel data lake](using-data-federation).

[![Screenshot of the Sentinel extension showing Lake tables and Jobs in the left pane and metadata for the selected table.](media/notebooks/tables-and-jobs.png)](media/notebooks/tables-and-jobs.png#lightbox)

## Create a new notebook

To create a new Jupyter notebook in Visual Studio Code, follow these steps:

1. To create a new notebook, use one of the following methods.
2. Enter *&gt;* in the search box or press **Ctrl+Shift+P** and then enter *Create New Jupyter Notebook*. [![A screenshot showing how to create a new notebook from the search bar.](media/notebooks/create-new-notebook.png)](media/notebooks/create-new-notebook.png#lightbox)
3. Select File &gt; New File, then select **Jupyter Notebook** from the dropdown.[![A screenshot showing how to create a new notebook form the file menu.](media/notebooks/new-file-notebook.png)](media/notebooks/new-file-notebook.png#lightbox)
4. In the new notebook, paste the following code into the first cell.

    ```python
    from sentinel_lake.providers import MicrosoftSentinelProvider
    data_provider = MicrosoftSentinelProvider(spark)
    
    table_name = "EntraGroups"  
    df = data_provider.read_table(table_name)  
    df_filtered = df.select("displayName", "groupTypes", "mail", "mailNickname", "description", "tenantId").show(100,   truncate=False)  
    
    # Transform the dataframe
    df_transformed = df.filter(df.mail.isNotNull()).select("displayName", "groupTypes", "mail", "mailNickname", "description", "tenantId")
    
    write_options = {
         'mode': 'overwrite'
     }
    # Save to a new table
    data_provider.save_as_table(df_transformed, "EntraGroups_Processed_SPRK", write_options=write_options)
    ```

    The editor provides intellisense code completion for both the `MicrosoftSentinelProvider` class and the table names in the data lake.
5. Select the **Run** triangle to execute the code in the notebook. The results are displayed in the output pane below the code cell.[![A screenshot showing how to run a notebook cell.](media/notebooks/run-notebook.png)](media/notebooks/run-notebook.png#lightbox)
6. Select **Microsoft Sentinel** from the list for a list of runtime pools. [![A screenshot showing the runtime picker.](media/notebooks/select-runtime.png)](media/notebooks/select-runtime.png#lightbox)
7. Select **Medium** to run the notebook in the medium sized runtime pool. For more information on the different runtimes, see Select the appropriate runtime pool. [![A screenshot showing the run pool size picker.](media/notebooks/select-kernel-size.png)](media/notebooks/select-kernel-size.png#lightbox)

Note

Selecting the kernel starts the Spark session and runs the code in the notebook. After selecting the pool, it can take 3-5 mins for the session to start. Subsequent runs a faster as the session is already active.

When the session is started, the code in the notebook runs and the results are displayed in the output pane below the code cell, for example: [![A screenshot showing the results from running a notebook cell.](media/notebooks/results.png)](media/notebooks/results.png#lightbox)

For sample notebooks that demonstrate how to interact with the Microsoft Sentinel data lake, see [Sample notebooks for Microsoft Sentinel data lake](notebook-examples).

### Monitor notebook state from the status bar

The status bar at the bottom of the notebook provides information about the current state of the notebook and the Spark session. The status bar includes the following information:

- The vCore utilization percentage for the selected Spark pool. Hover over the percentage to see the number of vCores used and the total number of vCores available in the pool. The percentages represent the current usage across interactive and job workloads for the logged in account.
- The connection status of the Spark session for example `Connecting`, `Connected`, or `Not Connected`.

[![A screenshot showing the status bar at the bottom of the notebook.](media/notebooks/status-bar.png)](media/notebooks/status-bar.png#lightbox)

## Set session timeouts

You can set the session timeout and timeout warnings for interactive notebooks. These settings are persisted in the extension settings so they're preserved across sessions.

To change the timeout, select the connection status in the status bar at the bottom of the notebook. Choose from the following options:

- **Set session timeout period**: Sets the time in minutes before the session times out. The default is 30 minutes.
- **Reset session timeout period**: Resets the session timeout to the default value of 30 minutes.
- **Set session timeout warning period**: Sets the time in minutes before the timeout that a warning is displayed that the session is about to time out. The default is 5 minutes.
- **Reset session timeout warning period**: Resets the session timeout warning to the default value of 5 minutes.

    [![A screenshot showing the session timeout setting.](media/notebooks/set-timeouts.png)](media/notebooks/set-timeouts.png#lightbox)

## Use GitHub Copilot in notebooks

Use GitHub Copilot to help you write code in notebooks. GitHub Copilot provides code suggestions and autocompletion based on the context of your code. To use GitHub Copilot, ensure that you have the [GitHub Copilot extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) installed in Visual Studio Code.

Copy code from the [Sample notebooks for Microsoft Sentinel data lake](notebook-examples) and save it in your notebooks folder to provide context for GitHub Copilot. GitHub Copilot will then be able to suggest code completions based on the context of your notebook.

The following example shows GitHub Copilot generating a code review.

[![A screenshot showing GitHub Copilot generating a code review.](media/notebooks/copilot.png)](media/notebooks/copilot.png#lightbox)

## Use the Microsoft Sentinel Provider class

To connect to the Microsoft Sentinel data lake, use the `MicrosoftSentinelProvider` class. The `MicrosoftSentinelProvider` class is part of the `sentinel_lake.providers` module and provides methods to interact with the data lake. To connect your Spark notebook to Microsoft Sentinel data lake tables, import the class and create an instance using a `spark` session. The following code initializes the Sentinel Lake data provider so the notebook can query Microsoft Sentinel tables from Spark:

```python
from sentinel_lake.providers import MicrosoftSentinelProvider
data_provider = MicrosoftSentinelProvider(spark)
```

For more information on the available methods, see [Microsoft Sentinel Provider class reference](sentinel-provider-class-reference).

### Select the appropriate runtime pool

There are three runtime pools available to run your Jupyter notebooks in the Microsoft Sentinel extension. Each pool is designed for different workloads and performance requirements. The choice of runtime pool affects the performance, cost, and execution time of your Spark jobs.

| Runtime Pool | Recommended Use Cases | Characteristics |
| --- | --- | --- |
| **Small** | Development, testing, and lightweight exploratory analysis. Small workloads with simple transformations. Cost efficiency prioritized. | Suitable for small workloads  Simple transformations. Lower cost, longer execution time. |
| **Medium** | ETL jobs with joins, aggregations, and ML model training. Moderate workloads with complex transformations. | Improved performance over Small. Handles parallelism and moderate memory-intensive operations. |
| **Large** | Deep learning and ML workloads.  Extensive data shuffling, large joins, or real-time processing. Critical execution time. | High memory and compute power. Minimal delays.  Best for large, complex, or time-sensitive workloads. |

Note

When first accessed, kernel options may take about 30 seconds to load. After selecting a runtime pool, it can take 3–5 minutes for the session to start.

## View messages, logs, and errors

Messages logs and error messages are displayed in three areas in Visual Studio Code.

1. The **Output** pane.

    1. In the **Output** pane, select **Microsoft Sentinel** from the drop-down.
    2. Select **Debug** to include detailed log entries.

    [![A screenshot showing the output pane.](media/notebooks/output-pane.png)](media/notebooks/output-pane.png#lightbox)
2. In-line messages in the notebook provide feedback and information about the execution of code cells. These messages include execution status updates, progress indicators, and error notifications related to the code in the preceding cell
3. A notification pop-up in the bottom right corner of Visual Studio Code, also know as a toast message, provides real-time alerts and updates about the status of operations within the notebook and the spark session. These notifications include messages, warnings, and error alerts such as successful connection to a spark session, and timeout warnings.

    [![A screenshot showing a toast message and an in-line error message.](media/notebooks/inline-toast-messages.png)](media/notebooks/inline-toast-messages.png#lightbox)

## Create and manage notebook jobs and schedules

You can schedule jobs to run at specific times or intervals using the Microsoft Sentinel extension for Visual Studio Code. Jobs allow you to automate data processing tasks to summarize, transform, or analyze data in the Microsoft Sentinel data lake. Jobs are also used to process data and write results to custom tables in the data lake tier or analytics tier. For more information on creating and managing jobs, see [Create and manage Jupyter notebook jobs](notebook-jobs).

## Service parameters and limits for VS Code Notebooks

The following section lists the service parameters and limits for Microsoft Sentinel data lake when using VS Code Notebooks.

| Category | Parameter/limit |
| --- | --- |
| Custom table in the analytics tier | Custom tables in analytics tier can't be deleted from a notebook; Use Log Analytics to delete these tables. For more information, see [Add or delete tables and columns in Azure Monitor Logs](/en-us/azure/azure-monitor/logs/create-custom-table?tabs=azure-portal-1%2Cazure-portal-2%2Cazure-portal-3#delete-a-table) |
| Gateway web socket timeout | 2 hours |
| Interactive query timeout | 2 hours |
| Interactive session inactivity timeout | 20 minutes |
| Language | Python |
| Graph query timeout | 7.5 minutes |
| Notebook job timeout | 8 hours |
| Max concurrent notebook jobs | 3, subsequent jobs are queued |
| Max concurrent users on interactive querying | 8-10 on Large pool |
| Session start-up time | Spark compute session takes about 5-6 minutes to start. You can view the status of the session at the bottom of your VS Code Notebook. |
| Supported libraries | Only [Azure Synapse libraries 3.4](https://github.com/microsoft/synapse-spark-runtime/tree/main#readme) and the Microsoft Sentinel Provider library for abstracted functions are supported for querying the data lake. Pip installs or custom libraries aren't supported. |
| VS Code UX limit to display records | 100,000 rows |

## Troubleshooting

For common errors and solutions when working with notebooks, see [Troubleshoot notebooks on the Microsoft Sentinel data lake](notebooks-troubleshooting).