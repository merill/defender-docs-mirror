---
layout: Conceptual
title: Create and Manage Jupyter Notebook Jobs - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/notebook-jobs
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
description: Create and schedule Jupyter notebook jobs in the Microsoft Sentinel extension for Visual Studio Code to automate data processing, analysis, and writing results to custom tables.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: zeinam
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: b0b2d270-765e-0b5f-b334-e48d71454ec0
document_version_independent_id: bf7ca636-192c-4e0b-1c6a-fc03298a2ec4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/notebook-jobs.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/notebook-jobs
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/notebook-jobs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: fa11ec67-2c16-0df0-2971-157c0b11ba9b
---

# Create and Manage Jupyter Notebook Jobs - Microsoft Security | Microsoft Learn

You can create scheduled jobs to run at specific times or intervals using the Microsoft Sentinel extension for Visual Studio Code. Jobs allow you to automate data processing tasks to summarize, transform, or analyze data in the Microsoft Sentinel data lake and federated tables. Jobs are also used to process data and write results to custom tables in the lake tier or analytics tier.

The following sections explain how to create, schedule, edit, and manage notebook jobs, including configuring job schedules, viewing job details and run history, and monitoring jobs in the Microsoft Defender portal.

## Required permissions for notebook jobs

Microsoft Entra ID roles provide broad access across all workspaces in the data lake. To create and schedule jobs, read tables across all workspaces, write to the analytics and lake tiers, you must have one of the supported Microsoft Entra ID roles. For more information on roles and permissions, see [Roles and permissions in Microsoft Sentinel](../roles#roles-and-permissions-for-the-microsoft-sentinel-data-lake).

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

## Create and schedule a job

Before you create or schedule a job, make sure you have one of the [supported Microsoft Entra ID roles](../roles#roles-and-permissions-for-the-microsoft-sentinel-data-lake). If the job creates custom tables in the analytics tier, assign the data lake managed identity the **Log Analytics Contributor** role first. For more information, see Required permissions for notebook jobs.

You can create a job in one of three ways:

1. In the notebook editor, select **Create schedule Job** from the toolbar.
2. In the **Explorer** pane, right-click the notebook file and select **Microsoft Sentinel**, then select **Create schedule Job**.

    [![A screenshot showing how to create a new job in Visual Studio Code.](media/notebook-jobs/create-job.png)](media/notebook-jobs/create-job.png#lightbox)
3. From the list of jobs, select the **+** icon to create a new job.

    [![A screenshot showing how to create a new job from the jobs list in Visual Studio Code.](media/notebook-jobs/create-job-from-toolbar.png)](media/notebook-jobs/create-job-from-toolbar.png#lightbox)
4. Select **Use existing notebook** to select an existing notebook file, or select **Create new notebook** to create a new notebook file for the job.

    [![A screenshot showing how to select an existing notebook for the job.](media/notebook-jobs/new-or-existing-workbook.png)](media/notebook-jobs/new-or-existing-workbook.png#lightbox)
5. On the **Job configuration** page, in the **Job details** section enter a **name** and **description** for the job.
6. Select the spark pool size to run the job according to your jobs compute needs.
7. To run a job manually without a schedule, select **On demand** in the **Schedule** section, then select **Submit** to save the job configuration and publish the job.
8. To specify a schedule for the job, select **Scheduled** in the **Schedule** section.

    1. Select a **Repeat frequency** for the job. You can choose from **By the minute**, **Hourly**, **Weekly**, **Daily**, or **Monthly**.
    2. Additional schedule options, such as day of the week, time of day, or day of the month, are displayed depending on the frequency you select.
    3. Select a **Start on** time for the schedule to start running.
    4. Select an **End on** time for the schedule to stop running. If you don't want to set an end time for the schedule, select **Set job to run indefinitely**. Dates and times are in the user's timezone.
    5. Select **Submit** to save the job configuration and publish the job.

    [![A screenshot showing the job configuration page.](media/notebook-jobs/job-configuration.png)](media/notebook-jobs/job-configuration.png#lightbox)
9. To view your jobs, select the Microsoft Sentinel ![Screenshot of the Microsoft Sentinel icon in the VS Code activity bar, used to open the Microsoft Sentinel extension.](media/notebook-jobs/sentinel-icon.png) icon in the left toolbar. Jobs are displayed on the **Jobs** panel.
10. Select a job to see the job details.
11. You can run the job immediately by selecting **Run now**, disable and enable the job schedule, or delete the job.

    [![A screenshot showing the job details page.](media/notebook-jobs/job-details.png)](media/notebook-jobs/job-details.png#lightbox)
12. View the job history in the **Run history** tab.

    [![A screenshot showing the job runs page.](media/notebook-jobs/run-history.png)](media/notebook-jobs/run-history.png#lightbox)
13. Select an activity to see more details.

    [![A screenshot showing the job run details page.](media/notebook-jobs/run-details.png)](media/notebook-jobs/run-details.png#lightbox)

## Create and manage parameterized notebook jobs

Notebook jobs can use parameters defined in the notebook. Parameters help you reuse the same notebook job with different input values without editing the notebook code each time. For example, you might run the same analysis for different users, entities, time ranges, or other investigation inputs.

Parameterized notebook jobs support three levels of values:

- **Notebook values**: Default parameter values defined in the notebook.
- **Job configuration values**: Values saved with the notebook job and used for scheduled runs.
- **Runtime values**: Values provided when you run the job manually. Runtime values apply only to that job run.

### Create a parameterized notebook job

When you create a notebook job from a notebook that contains parameters, the Microsoft Sentinel extension reads the parameters from the notebook and displays them in the job configuration.

To create a parameterized notebook job:

1. In the notebook, create a code cell near the top of the notebook that contains the parameter defaults. Open the cell menu and select **Mark Cell as Parameters**.

    [![Screenshot of Visual Studio Code showing the Mark Cell as Parameters menu item for a notebook cell.](media/notebook-jobs/mark-cell-as-parameters.png)](media/notebook-jobs/mark-cell-as-parameters.png#lightbox)
2. Define the parameters in the cell. For example:

    ```python
    # Parameters
    lookback_days = [7, 14, 30, 90]
    min_failed_attempts = [5, 10, 20]
    ```
3. In the **Explorer** pane, right-click the notebook file, select **Microsoft Sentinel**, and then select **Create Scheduled Job**.

    [![Screenshot of Visual Studio Code showing the Microsoft Sentinel menu with Create Scheduled Job selected.](media/notebook-jobs/create-scheduled-job-from-notebook.png)](media/notebook-jobs/create-scheduled-job-from-notebook.png#lightbox)
4. In the job editor, expand **Default parameters**, and then select **Refresh parameters** to load the latest parameter definitions from the notebook.

    [![Screenshot of the scheduled notebook job editor showing the Refresh parameters button under Default parameters.](media/notebook-jobs/refresh-notebook-job-parameters.png)](media/notebook-jobs/refresh-notebook-job-parameters.png#lightbox)
5. Review or update the default parameter values, and then submit the job.

You can keep the notebook default values or change the values before you submit the job. Values that you change are saved with the job configuration and used for future scheduled runs.

If a parameter value doesn't match the expected type, the extension shows an inline validation error and prevents you from submitting the job until the error is fixed.

### Add parameters to an existing notebook job

To add parameters to an existing notebook job, download the latest notebook, update the notebook locally to define the parameters, and then edit the job. When you upload or refresh the updated notebook in the job configuration, the parameters are available for the job.

After the parameters are available, you can update their values and submit the job again. Updated parameter values are saved with the job configuration and used for future scheduled runs.

### Refresh parameters from the notebook

If the notebook is updated after the job is created, refresh the job parameters to sync the job configuration with the latest notebook parameters.

Refreshing parameters:

- Adds new parameters that were added to the notebook.
- Removes parameters that were removed from the notebook.
- Preserves existing job configuration values that you changed.

Refreshing parameters doesn't overwrite parameter values that were already edited in the job configuration.

### Reset parameter values

You can reset parameter values to the defaults defined in the notebook.

Use reset for an individual parameter to restore only that value. Use **Reset all** to restore all parameter values to the notebook defaults. When you reset all parameter values, confirm the reset before the values are restored.

### Run with custom runtime parameter values

When you select **Run now** for a parameterized notebook job, the Microsoft Sentinel extension opens a runtime parameters dialog. The dialog is prepopulated with the parameter values saved in the job configuration.

[![Screenshot of the Run job dialog showing parameter values that can be changed before running a notebook job.](media/notebook-jobs/run-job-with-parameter-overrides.png)](media/notebook-jobs/run-job-with-parameter-overrides.png#lightbox)

You can keep the saved values or change them for the current run. Runtime parameter changes apply only to that job run and don't update the saved job configuration or future scheduled runs.

Use runtime parameters when you want to reuse the same job for different inputs, such as running the same risk analysis for a different user.

### View job run history

After you run a parameterized notebook job, view the job status and run history the same way you view other notebook job runs. In the **Run history** tab, select a run to see more details.

### Jobs with no parameters

If the selected notebook doesn't define parameters, the job configuration shows an empty parameter state. To add parameters, update the notebook to include parameter definitions, save the notebook, and upload or refresh the job configuration.

## Edit a submitted job

Submitting a job creates a job definition that includes the notebook file, the job configuration, and the schedule. The job definition is uploaded from your VS Code editor and stored in the Microsoft Sentinel data lake. Once submitted, the job is no longer connected to the notebook file on your local file system. If you want to edit the code in the notebook job, you must download the job definition, edit the notebook file, and then resubmit the job.

To edit a submitted job follow the steps below:

1. In the **Jobs** section, select the job you want to edit.
2. Select the **Download** cloud icon to download the job definition to your local file system. In the jobs details editor, you can see the job configuration. You can also select **Download latest notebook**.

    [![A screenshot showing the edit and download job icon in VS Code.](media/notebook-jobs/edit-download-job.png)](media/notebook-jobs/edit-download-job.png#lightbox)
3. Edit the downloaded `ipynb` workbook file to make your changes.
4. Return to the **Job details** tab and select **Edit job**.
5. Edit the job name, description, cluster configuration, and schedule. Changing the job name creates a new job definition when you submit the job.
6. Select **Submit** to upload the updated notebook file and job configuration.
7. A confirmation is displayed when the job is successfully submitted.

    [![A screenshot showing the edit jib page in VS Code.](media/notebook-jobs/edit-job.png)](media/notebook-jobs/edit-job.png#lightbox)

## View jobs in the Microsoft Defender portal

In addition to viewing jobs in VS Code, you can also view your notebook jobs in the Defender portal. To view your jobs in the Defender portal, Select **Microsoft Sentinel** &gt; **Data lake exploration** &gt; **Jobs** .

The **Jobs** page shows a list of jobs and their types. Select a notebook job to view its details. You can enable and disable the job's schedule but you can't edit a notebook job in the Defender portal.

[![A screenshot showing the jobs page in the Defender portal.](media/notebook-jobs/view-jobs-in-defender-portal.png)](media/notebook-jobs/view-jobs-in-defender-portal.png#lightbox)

1. Select a job to view the job details.

    [![A screenshot showing the job details in the Defender portal.](media/notebook-jobs/portal-job-details.png)](media/notebook-jobs/portal-job-details.png#lightbox)
2. Select **View history** to see the history of job runs.

    [![A screenshot showing the jobs history page in the Defender portal.](media/notebook-jobs/portal-job-history.png)](media/notebook-jobs/portal-job-history.png#lightbox)

## Service parameters and limits

The following sections summarize column naming rules and service limits for notebook jobs in the Microsoft Sentinel data lake.

### Column name requirements for the save\_as method

The `save_as` method writes notebook output to a destination table in the Microsoft Sentinel data lake. The following column-naming rules apply when you use this method.

- Column names must start with a letter.
- The following standard columns aren't supported for export. The ingestion process overwrites these columns in the destination tier:

    - TenantId
    - \_TimeReceived
    - Type
    - SourceSystem
    - \_ResourceId
    - \_SubscriptionId
    - \_ItemId
    - \_BilledSize
    - \_IsBillable
    - \_WorkspaceId
- `TimeGenerated` is overwritten if it's older than two days. To preserve the original event time, write the source timestamp to a separate column.

For a list of service limits for the Microsoft Sentinel data lake, see [Microsoft Sentinel data lake service limits](notebooks#service-parameters-and-limits-for-vs-code-notebooks).

### Troubleshooting

For troubleshooting notebook jobs and data lake operations, see [Troubleshoot notebooks on the Microsoft Sentinel data lake](notebooks-troubleshooting).