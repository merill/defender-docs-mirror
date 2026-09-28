---
layout: Conceptual
title: Connect Microsoft Dynamics 365 Finance and Operations to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/dynamics-365/deploy-dynamics-365-finance-operations-solution
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
ms.reviewer: mapankra
description: Learn how to deploy the Microsoft Sentinel solution for Business Applications with Microsoft Dynamics 365 Finance and Operations.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: d66621b4-6448-9792-f854-0c5749d27590
document_version_independent_id: 58df1ab1-95c0-87b4-81bf-aa306b2a74ca
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/dynamics-365/deploy-dynamics-365-finance-operations-solution.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/dynamics-365/deploy-dynamics-365-finance-operations-solution
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/dynamics-365/deploy-dynamics-365-finance-operations-solution.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/410e33a0-5420-48ba-a8e2-7fb3dc6a9163
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/437f62ae-23a5-4ffc-9ff2-ac42acc41d76
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 370ed19d-e559-2fd3-6a39-376cc89b26db
---

# Connect Microsoft Dynamics 365 Finance and Operations to Microsoft Sentinel | Microsoft Learn

This article shows how to deploy Dynamics 365 Finance and Operations content in the Microsoft Sentinel solution for Business Applications. The solution helps monitor and protect your Dynamics 365 Finance and Operations system. It collects audit and activity logs and detects threats and suspicious actions. For more details, see the [Dynamics 365 Finance and Operations solution overview](dynamics-365-finance-operations-solution-overview).

Before you start, review the prerequisites. You need a Microsoft Sentinel workspace and Dynamics 365 Finance version 10.0.33 or later.

## Prerequisites

Before you begin, verify that:

- The Microsoft Sentinel solution for Microsoft Business Applications solution is enabled.
- You have a defined Microsoft Sentinel workspace and have read and write permissions to the workspace.
- [Microsoft Dynamics 365 Finance version 10.0.33 or above](/en-us/dynamics365/finance/get-started/whats-new-changed-changed-10-0-33) is enabled and you have administrative access to the monitored environments.
- You can create [Data Collection Rules/Endpoints](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview) with the permissions:

    - `Microsoft.Insights/DataCollectionEndpoints`, and `Microsoft.Insights/DataCollectionRules`

## Collect the environment URL from your Finance and Operations cloud environment

To find the environment URL and version for your Finance and Operations environment, follow these steps:

1. Open your Dynamics 365 project in [Microsoft Dynamics Lifecycle Services (LCS)](https://lcs.dynamics.com) and select the specific Finance and Operations environment you want to monitor with Microsoft Sentinel.
2. In the **Environment version information** section, make sure that you're using application release version 10.0.33 or above.

    [![Screenshot of the Finance and Operations environment version information.](media/deploy-dynamics-365-finance-operations-solution/environment-version-information.png)](media/deploy-dynamics-365-finance-operations-solution/environment-version-information.png#lightbox)
3. To collect your environment URL, select **Log on to environment** and save the URL in the browser to use in the Deploy the data connector step; for example, `https://sentineldevc055b257489f70f5devaos.axcloud.dynamics.com`.

    Note

    The URL may look different, depending on the environment you use, for example, you could be using a sandbox, or a cloud hosted environment. Remove any trailing slashes: `/`.

    ![Screenshot of the Finance and Operations environment details.](media/deploy-dynamics-365-finance-operations-solution/environment-details-new.png)

## Deploy the solution and enable the data connector

To install the Microsoft Business Applications solution from Content hub, follow these steps:

1. Go to the **Microsoft Sentinel** service.
2. Select **Content hub**. In the search bar, search for *Microsoft Business Applications*.
3. Select **Microsoft Business Applications**.
4. Select **Install**.

    For more information about how to manage the solution components, see [Discover and deploy out-of-the-box content](../sentinel-solutions-deploy).

## Deploy the data connector

After installing the solution, use the following steps to open the Dynamics 365 Finance and Operations data connector:

1. Once the solution deployment is complete, return to your Sentinel workspace and select **Data connectors**.
2. In the search bar, type *Dynamics 365,* and select **Dynamics 365 Finance and Operations**.
3. Select **Open connector page**.

In the connector page, make sure that you meet the required prerequisites and complete the steps to configure the data connector.

## Configure the data connector

To enable data collection, you create a new role in Finance and Operations with permissions to view the Database Log entity. The role is then assigned to a dedicated Finance and Operations user, mapped to the Microsoft Entra client ID of an app registration.

### Register an app for data collection

To collect the managed identity application ID from Microsoft Entra ID:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Browse to **Microsoft Entra ID** &gt; **App registrations**.
3. Create a new registration and enter a name for the app registration.
4. Select Accounts in this organization only (single tenant) and click register.
5. From the overview page of the new app registration, take note of the **tenant ID** and **application (Client) ID** for use in the next steps.
6. Within the Certificates & Secrets menu, create a new client secret.
7. Store the **client secret** in a secure location for use in the next steps.

### Create a role for data collection in Finance and Operations

1. In the Finance and Operations portal, navigate to **Workspaces &gt; System administration**, and select **Security Configuration**.
2. Under **Roles**, select **Create new** and give the new role a name, for example, *Database Log Viewer*.
3. Select the new role from the list of roles, and select **Privileges** &gt; **Add references**.
4. Select **Database log Entity View** from the list of privileges.
5. Select **Unpublished objects**, and select **Publish all** to publish the role.

#### Create a user for data collection in Finance and Operations

1. In the Finance and Operations portal, navigate to **Modules &gt; System administration**, and select **Users**.
2. Create a new user and assign the role you created in the Create a role for data collection in Finance and Operations step to the user.

#### Register the app registration in Finance and Operations

1. In the Finance and Operations portal, navigate to **System administration &gt; Setup &gt; Microsoft Entra ID** applications.
2. Create a new entry in the table:

    - For the **Client Id**, type the application ID of the app registration.
    - For the **Name**, type a name for the application.
    - For the **User ID**, type the user ID created in Create a user for data collection in Finance and Operations.

### Enable auditing on the relevant Dynamics 365 Finance and Operations data tables

Note

Before you enable auditing on Dynamics 365 F&O, review the [database logging recommended practices](/en-us/dynamics365/fin-ops-core/dev-itpro/sysadmin/configure-manage-database-log#database-logging-and-performance).

The analytics rules provided with this solution monitor and detect threats based on logs generated in the System Database Log.

If you're planning to use the analytics rules provided in this solution, enable auditing for the following tables:

| Category | Table |
| --- | --- |
| System | `UserInfo` |
| Bank | `BankAccountTable` |
| Not specified | `SysAADClientTable` |

Enable auditing on tables using the **Database log setup** wizard in the Finance and Operations portal.

- In the **Tables and fields** page, you might want to select the **Show table names** checkbox to make it easier to find your tables.
- To enable auditing of all fields in the selected tables, in the **Types of change** page, select all four check boxes for any relevant table names with empty field labels. Sort the table list by the **Field label** column in ascending order (A-Z).
- Select **Yes** for all warning messages.

For more information, see [Set up database logging](/en-us/dynamics365/fin-ops-core/dev-itpro/sysadmin/configure-manage-database-log#set-up-database-logging).

### Enable data collection in the connector

After completing the Finance and Operations configuration, connect the data connector in Microsoft Sentinel:

1. Navigate to the data connectors blade in Microsoft Sentinel, search for **Dynamics 365 Finance and Operations**.
2. Using the **Tenant ID**, **Client ID, Client Secret** and **Environment URL**, connect the data connector.

### Verify that the data connector is ingesting logs to Microsoft Sentinel

To verify that log ingestion is working:

1. Run activities (create, update, delete) on any of the tables you enabled for monitoring in Enable auditing on the relevant Dynamics 365 Finance and Operations data tables.
2. Wait up to 15 minutes for Microsoft Sentinel to ingest the logs to the logs table in the workspace.
3. Query the `FinanceOperationsActivity_CL` table in the Microsoft Sentinel workspace under **Logs**.
4. Check that the table shows new logs that reflect the activities you executed in step 1 of this procedure.

    ![Screenshot of viewing a new Finance and Operations incident in Microsoft Sentinel.](media/deploy-dynamics-365-finance-operations-solution/query-finance-operations-table.png)