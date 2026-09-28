---
layout: Conceptual
title: Publish a notebook solution for Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/isv/publish-notebook-solutions
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
description: Learn how to publish a Jupyter notebook solution for Microsoft Sentinel as a SaaS offer in Microsoft Sentinel
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.custom: msecd-doc-authoring-1012
ms.date: 2026-06-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 1c73a67a-0a59-2b4c-f78d-f7bee31b6481
document_version_independent_id: bcc4867f-cc7e-1064-f26e-8a354b238ff3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/isv/publish-notebook-solutions.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/isv/publish-notebook-solutions
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/isv/publish-notebook-solutions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: 86c61fa0-559e-d20b-2655-119015b0b054
---

# Publish a notebook solution for Microsoft Sentinel | Microsoft Learn

As an ISV partner, you can package and publish Jupyter notebook analytics solutions to the Microsoft Security Store as SaaS offers. The Microsoft Sentinel data lake supports Jupyter notebooks that run on managed Spark pools against large security datasets. These notebooks are ideal for low-and-slow attack detection, behavioral baselining, AI/ML-based analytics, sensitive-data-path mapping, data visualizations, and enrichments that traditional KQL detections can't express.

A notebook platform solution is typically scheduled and batch-oriented. It writes output to a custom table in the data lake, where downstream analytic rules, hunting queries, Security Copilot agents, or MCP tools can consume the results. The `.zip` package you submit to Partner Center is declared as type `SentinelLake` and contains the notebook(s), any helper Python modules, and optionally an ARM template for downstream Azure resources the notebook needs.

This article walks you through building, testing, packaging, and publishing a Microsoft Sentinel platform - notebook solution to the Microsoft Security Store. After completing this guide, you'll have:

- A working Jupyter notebook that reads data from the Sentinel data lake
- A scheduled job that runs the notebook on a managed Spark pool
- A `SentinelLake` package zip (`PackageManifest` + notebook folder)
- A Partner Center SaaS offer listing in the Microsoft Security Store

## Prerequisites

### Required permissions

| Scope | Required role(s) |
| --- | --- |
| Microsoft Entra ID | Security Administrator (minimum required role, for data-lake onboarding) |
| Azure subscription | Subscription Owner OR User Access Administrator at subscription scope AND Microsoft Sentinel Contributor at the subscription or RG scope (for onboarding the Sentinel workspace to Defender portal); Subscription Owner or Contributor for onboarding the Sentinel workspace to Data Lake |
| Log Analytics workspace | Microsoft Sentinel Contributor (to create LAW and enable Sentinel) |
| Data lake (post-onboard) | Microsoft Sentinel Reader / Contributor—to run notebooks |
| LAW (for write-back to analytics tier) | Log Analytics Contributor assigned to the data-lake managed identity `msg-resources-<guid>` |
| Microsoft Partner Center | Marketplace Publisher account (one-time; same account used for SCC agent publishing) |

Note

The Subscription Owner role is required for a one-time data lake onboarding task. Use [Microsoft Entra Privileged Identity Management (PIM)](/en-us/entra/id-governance/privileged-identity-management/pim-configure) to temporarily elevate to this role only when needed, then remove access after onboarding completes.

### Required tools

- Azure subscription with the data-lake billing model accepted
- Microsoft Defender portal access—`security.microsoft.com`
- Visual Studio Code (latest stable release)
- Microsoft Sentinel VS Code extension (`ms-security.ms-sentinel`)
- GitHub Copilot VS Code extension (recommended to speed up notebook authoring)
- Python 3.10+ installed locally. The Spark kernel runs in Azure but VS Code needs a local interpreter for cell editing.

## Process overview

The publishing process starts with local notebook development moving to a packaged SaaS offer discoverable in the Microsoft Security Store.

1. Local notebook development (VS Code + Sentinel extension)
2. Run interactively against the Sentinel platform
3. Test against representative data; validate output table populates
4. Schedule as a Job (cron or on-demand)
5. Package as SentinelLake .zip (PackageManifest.yaml + folder)
6. Create SaaS Offer in Microsoft Partner Center
7. Upload package, create metadata, plan and pricing
8. Review and Publish, automated review, Go Live
9. Live in Microsoft Security Store

Tip

If your tenant already has the data lake onboarded for KQL queries or for a Security Copilot agent, you don't need to onboard again. There's exactly one data lake per tenant.

Verify in Defender portal &gt; **System** &gt; **Settings** &gt; **Microsoft Sentinel** &gt; **Data lake**. If the status reads **Provisioned**, skip the onboarding section and go to Install Visual Studio Code and the Microsoft Sentinel extension.

## Onboard to the Microsoft Sentinel data lake

Onboarding is a one-time process that takes about 60 minutes. Onboarding is done from the Defender portal.

### Verify prerequisites

Confirm you have the following requirements before starting:

- Microsoft Entra ID: Security Administrator or higher.
- Azure RBAC: For onboarding Sentinel Workspace to Defender portal and set it as Primary, you need one of:

    - Subscription Owner
    - User Access Administrator at subscription scope AND Microsoft Sentinel Contributor at the subscription or resource group scope that contains the Sentinel workspace
    - Subscription Owner or Contributor for onboarding Sentinel workspaces to Data Lake
- Confirm you have access to the Defender portal at https://security.microsoft.com.
- Decide which region to use. The data lake is onboarded in the same region as your primary Sentinel workspace. After onboarding, the region can't be changed through the Defender portal.

### Create or confirm your Log Analytics workspace and add Sentinel

If you already have a workspace in a data-lake-supported region, skip to Connect the workspace in the Defender portal.

1. Sign in to the Azure portal at https://portal.azure.com/.
2. Search for **Microsoft Sentinel** &gt; **Create** &gt; **Create a new workspace**.
3. Select or create a resource group.
4. Enter a descriptive workspace name.
5. Select a data-lake-supported region. Your data lake is provisioned in the same region as your primary Sentinel workspace region.
6. Select **Review + create** &gt; **Create** and wait for the deployment to finish.
7. Search for **Microsoft Sentinel** again &gt; **Create** &gt; select the workspace you created &gt; **Add Microsoft Sentinel**.

### Connect the workspace to the Defender portal and set it as primary

To connect your Sentinel workspace and set it as primary, complete the following steps:

1. Sign in to https://security.microsoft.com/.
2. If the onboarding banner appears, select **Get started**. If dismissed, go to **System** &gt; **Settings** &gt; **Microsoft Sentinel**.
3. Under **SIEM workspaces**, select your Sentinel workspace &gt; **Connect workspace** &gt; set it as **Primary**.

Important

If your Sentinel workspace doesn't appear in the Defender portal, or the **Subscription** filter is blank or shows **Undefined**, you likely have a missing role. Recheck the prerequisites before retrying.

### Start the data lake setup

To start onboarding from the Defender portal:

1. Select **Start setup** under **Data lake**.
2. Select the subscription and resource group to use for billing.
3. Select **Set up data lake**.

Onboarding can take up to 60 minutes. You can close the panel while setup runs—the portal displays a **Setup in progress** banner.

Caution

Don't delete the billing subscription or resource group selected during onboarding. Deleting either breaks the data lake setup, and the Defender portal shows **Something went wrong, please try again** with no recovery path.

### Validate onboarding

After the setup completes, confirm the data lake is ready:

1. In the Defender portal &gt; **SIEM workspaces**, confirm your Sentinel workspace appears as **Connected** and **Primary**.
2. Confirm the **Data lake** settings page loads without errors and shows your configured subscription and resource group.
3. Under **Microsoft Sentinel** in the left navigation bar, confirm the **Data lake** exploration options are available.

For more information, see [Onboard to Microsoft Sentinel data lake from the Defender portal](../datalake/sentinel-lake-onboarding).

## Install Visual Studio Code and the Microsoft Sentinel extension

All notebook development happens locally in VS Code with the Microsoft Sentinel extension installed. The Spark kernel runs in Azure—VS Code is the editor and submission client.

1. Download Visual Studio Code from `https://code.visualstudio.com/` and install with default options.
2. Open VS Code &gt; **Extensions** marketplace (**Ctrl+Shift+X** or **Cmd+Shift+X**).
3. Search for **Sentinel** and install the **Microsoft Sentinel** extension (publisher: `ms-security`).

    After installation, the Microsoft Sentinel icon appears in the left toolbar.
4. (Recommended) Search for **GitHub Copilot** in the marketplace, install it, and sign in to GitHub when prompted.

    Copilot knows the `MicrosoftSentinelProvider` API and autocompletes PySpark transforms.
5. Select the Microsoft Sentinel icon in the left toolbar.
6. Approve the sign-in dialog, then select the account with Sentinel Reader / Contributor on your workspace.

The left pane shows **Lake tables** and **Jobs**, confirming the extension reached the data lake.

[![Screenshot of the Microsoft Sentinel VS Code extension showing the Lake tables, Jobs, and graphs sections.](media/publish-notebook-solutions/sentinel-extension-panel.png)](media/publish-notebook-solutions/sentinel-extension-panel.png#lightbox)

Caution

If you have multiple guest tenants signed in, switching accounts at the bottom-left of VS Code kills any active PySpark sessions—you need to restart the kernel after switching. Plan account switches between runs, not during them.

## Develop your notebook

Notebooks use this authoring pattern:

- Read a data-lake table into a Spark DataFrame
- Transform with PySpark
- Optionally enrich with external data
- Write results to a custom table that Sentinel can consume

Note

Notebooks use pySpark, not pandas. The `MicrosoftSentinelProvider` returns Spark DataFrames that scale to millions of rows. Be careful converting to pandas for transformations—this pulls all data into memory and can crash the kernel. Use Spark APIs for filtering, grouping, and joins. Only convert to pandas for small samples or visualizations.

### Explore the Lake tables panel

To identify the input tables your notebook will use, explore the Lake tables panel:

1. Select the Sentinel icon and expand **Lake tables**.
2. Tables are grouped by database and category (System, Custom, Federated). Select any table to see its column definitions and types.
3. Identify the input tables your notebook reads and note the exact names.

### Create a new notebook

To create a new Jupyter notebook for your solution, complete the following steps:

1. Press **Ctrl+Shift+P** / **Cmd+Shift+P** &gt; type **Create New Jupyter Notebook**, or select **File** &gt; **New File** &gt; **Jupyter Notebook**.
2. Save the notebook with a descriptive name (for example, `failed-signin-baseline.ipynb`).

### Read a table

Paste this template into the first cell and replace the table name with yours:

```python
from sentinel_lake.providers import MicrosoftSentinelProvider
data_provider = MicrosoftSentinelProvider(spark)

# Read a table from the data lake
table_name = "EntraGroups"
df = data_provider.read_table(table_name)

# Quick sanity check—show 100 rows
df.select("displayName", "groupTypes", "mail", "tenantId").show(100, truncate=False)
```

### Select a runtime pool and run the cell

To run the cell against the data lake, select a pool and submit:

1. Select the **Run** triangle on the cell.
2. When prompted, choose **Microsoft Sentinel** as the runtime.
3. Choose a pool size: **Small** for exploration, **Medium** for transforms, **Large** for ML or aggregations over tens of millions of rows.

The first run takes 3 to 5 minutes to spin up the Spark session. Subsequent cells run in seconds.

### Transform and write back to a custom table

The `save_as_table()` method writes a DataFrame to a custom table in the lake tier (or analytics tier). The destination table is created on first write.

```python
df_transformed = (
    df.filter(df.mail.isNotNull())
    .select("displayName", "groupTypes", "mail", "mailNickname", "description", "tenantId")
)

write_options = {"mode": "overwrite"}
data_provider.save_as_table(
    df_transformed,
    "EntraGroups_Processed_SPRK",
    write_options=write_options,
)
```

### Notebook authoring patterns

The following patterns cover the most common scenarios:

| Pattern | When to use it |
| --- | --- |
| Baseline + drift | Compute per-user or per-host normal behavior; flag rows that drift from baseline. Classic for failed-signin and process-execution analytics. |
| Cross-table join | Join the lake table you own with built-in tables (SigninLogs, SecurityAlert, DeviceProcessEvents) on shared entities (UPN, host, IP). |
| ML scoring | Train or load a pretrained model in the notebook; score each row; write top-N risky rows to a custom output table for downstream alerting. |
| Visual investigation | Plot timelines, heatmaps, and process trees with matplotlib, bokeh, or plotly; export the notebook as HTML for hand-off. |

Tip

Use markdown cells liberally to document your code. A Security Store reviewer—and the SOC analyst who runs your notebook—needs to understand what each section does without reading the code. Place a markdown cell above every code block explaining purpose, inputs, outputs, and expected output. Reviewers treat unclear notebooks as a hard fail.

## Test the notebook

Testing requires proving the notebook runs end-to-end on realistic data and produces a usable output table.

### Smoke test on Small pool

Run the notebook end-to-end to confirm every cell completes without error:

1. Restart the kernel to clear any stale state.
2. Run all cells from top to bottom—every cell must complete without error.

If a transform cell takes more than 5 minutes on Small, your input filters are too loose. Tighten the date or column projection before scaling up.

### Validate the output table

Confirm the output table was created and contains the expected data:

1. In the Sentinel extension's **Lake tables** panel, refresh and confirm your output table appears with the expected schema.
2. Run a verification cell:

```python
verify_df = data_provider.read_table("EntraGroups_Processed_SPRK")
print("Row count:", verify_df.count())
verify_df.printSchema()
verify_df.show(5, truncate=False)
```

### Scale test on Medium or Large pool

Verify the notebook produces consistent results on larger pool sizes:

1. Rerun the notebook on Medium (and Large if your dataset warrants it).
2. Confirm row counts and column distributions match the Small run. If they diverge, you have a non-deterministic transform that needs investigation.

### Test edge cases

- **Empty input**: Point at a table or date range with zero rows. The notebook should fail gracefully or write an empty output—not crash.
- **Schema drift**: If your input table gains a column, the notebook should still run. Never use `select(*)` and assume positional order.

## Schedule the notebook as a job

Most published notebook solutions run on a schedule—hourly baseline, daily anomaly scan, and so on. The Sentinel extension turns any saved notebook into a scheduled job that runs unattended on a managed Spark pool.

### Create the job

To convert the notebook into a scheduled job, complete the following steps:

1. Open your notebook in VS Code.
2. Select **Create schedule Job** in the notebook, then choose **Use existing notebook** when prompted.

### Configure the job

To configure the scheduled job, fill in the following fields:

1. Enter a kebab-case **Job name** that describes the notebook (for example, `failed-signin-baseline-hourly`).
2. Enter a one-sentence **Description** covering the job's purpose and output table.
3. Select the **Spark pool size** that you validated during testing. Don't oversize—jobs run on this pool every invocation.
4. For the **Schedule**, choose **On demand** for manual runs, or **Scheduled** with a repeat frequency (minute, hourly, daily, weekly, or monthly).
5. Select **Submit** to publish the job.

### Verify the job

After submitting, confirm the job is running correctly:

1. Switch to the **Jobs** panel in the Sentinel extension—your job should appear.
2. Select the job &gt; **Run now** for an immediate validation run.
3. After the run completes, switch to the **Run history** tab to inspect logs and timing.

Caution

Submitted jobs are decoupled from your local `.ipynb` file. Editing the local file doesn't update the running job. To update a job: open it in the **Jobs** panel &gt; **Download the notebook** &gt; edit &gt; **Edit job** &gt; **Submit** to upload the updated version.

### (Optional) View the job in the Defender portal

Navigate to **Microsoft Sentinel** &gt; **Data lake exploration** &gt; **Jobs**. You can enable or disable the schedule and view run history here, but can't edit the notebook from the portal.

## Package and publish your notebook solution

Once your notebook is tested and materialized, package it for deployment to customers. For detailed packaging instructions, see [Package and publish Microsoft Sentinel graph and notebook solutions](package-publish-notebook-graph-solutions).

## Troubleshoot

### Notebook authoring

| Symptom | Likely cause and fix |
| --- | --- |
| `MicrosoftSentinelProvider` not found | Extension not signed in, or you opened a non-Spark kernel. Sign in to the Microsoft Sentinel extension and select the **Microsoft Sentinel** runtime when prompted. |
| Cell hangs at "Starting Spark session" | First-cell startup takes 3 to 5 minutes. After 6 minutes, check the vCore-utilization indicator in the status bar—your pool may be at capacity. Try a smaller pool size. |
| `save_as_table` fails with permission denied on analytics tier | The data-lake managed identity `msg-resources-<guid>` doesn't have Log Analytics Contributor on the LAW. Assign it per the prerequisites and retry. |
| Schema drift between Small and Large pool runs | Non-deterministic transform (often `groupBy` over a column with nulls, or `monotonically_increasing_id`). Add an explicit `orderBy` or `.dropna(subset=[...])` before the grouping. |
| Output table appears in **Lake tables** panel but is empty | A `.filter()` likely removed all rows. Add a row count print immediately before `save_as_table` to localize the issue. |

For more information, see [Notebooks troubleshooting](../datalake/notebooks-troubleshooting).

### Job scheduling

| Symptom | Likely cause and fix |
| --- | --- |
| Edits to local `.ipynb` not reflected in scheduled job | Submitted jobs are decoupled from the local file. Download the job from VS Code, edit it, then use **Edit job** &gt; **Submit** to upload the new version. |
| Job fails with "Module not found" | The notebook imports a package not pre-installed in the runtime. Add it to `requirements.txt` and use `%pip install -r requirements.txt` at the top of the notebook. |
| Job runs but produces no output | Check the **Run history** tab in the **Jobs** panel—the run log usually shows the failing cell. The most common cause is the notebook reading from a table the running identity doesn't have access to. |

For more information, see [Notebooks troubleshooting](../datalake/notebooks-troubleshooting).

### Packaging and Partner Center

| Symptom | Likely cause and fix |
| --- | --- |
| Package zip rejected with "Invalid package structure" | `PackageManifest.yaml` isn't at the root, or the subfolder name in `manifest[].id` doesn't match the actual folder name. |
| Hidden files in zip rejected | Re-zip with `zip -r out.zip . -x '.*' -x '__MACOSX'`. Never use the macOS Finder **Compress** option. |
| **Microsoft Security services** tab missing from left nav | The **My offer integrates with Microsoft Security services** checkbox in offer setup isn't checked. Check it, save the draft, and reload the page. |
| Solution name contains a Microsoft product name | Rename in **Offer name**, **Plan name**, and the description text body, then resubmit. |
| **Review and Publish** button is greyed out | **Technical configuration** is incomplete. Fill all four fields—dummy values are acceptable. |