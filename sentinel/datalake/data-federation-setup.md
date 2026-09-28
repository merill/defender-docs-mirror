---
layout: Conceptual
title: Set Up Federated Data Connectors in Microsoft Sentinel Data Lake - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/data-federation-setup
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
description: Learn how to configure federated data connectors for Azure Databricks, ADLS Gen 2, and Microsoft Fabric in Microsoft Sentinel data lake.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: amyhari
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: ms-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 38642446-abfb-1302-0a70-8ea31df29f35
document_version_independent_id: 365fc0b1-b992-cff4-7fa8-7e21d32d63dd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/data-federation-setup.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/data-federation-setup
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/data-federation-setup.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f488294d-f483-456e-94e3-755f933b811b
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/5c1f3bfc-fced-4ad1-b4e6-b7200832734d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/02662057-0b9b-40f4-a3c7-537125b6d283
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/5017978e-5a12-4c31-bdfd-1880eb1a780b
platformId: cdc55d4b-eea0-74a3-a538-a3ac7a27158b
---

# Set Up Federated Data Connectors in Microsoft Sentinel Data Lake - Microsoft Security | Microsoft Learn

This article explains how to configure federated data connectors to enable querying of external data sources from the Microsoft Sentinel data lake. You can federate with Azure Databricks, Azure Data Lake Storage (ADLS) Gen 2, and Microsoft Fabric. The article walks through creating a service principal, storing credentials in Azure Key Vault, and setting up a connector instance for each supported data source. Use this guide if you're a security administrator who needs to bring external data into Microsoft Sentinel for investigation and analysis.

## Prerequisites

Before setting up data federation, ensure you meet the following requirements:

- **Sentinel data lake onboarding**: Your tenant must be onboarded to the Sentinel data lake. For more information, see [Onboard to Microsoft Sentinel data lake](sentinel-lake-onboard-defender).
- **Public accessibility**: The external source must be publicly accessible. Private endpoints aren't currently supported.
- **Service principal**: A service principal with appropriate permissions in the data source you want to connect with is required for Azure Databricks and Azure Data Lake Storage Gen2 sources. For more information, see [Microsoft Entra ID app registrations](/en-us/entra/identity-platform/quickstart-register-app).
- **Azure Key Vault**: An Azure Key Vault configured with the Service principal client secret is required. The Microsoft Sentinel application identity needs permissions assigned to the key vault. For more information on configuring Azure Key vaults, see [Azure Key Vaults](/en-us/azure/key-vault/general/basic-concepts).
- **Microsoft Sentinel permissions**: **Data (manage)** permissions on System tables to configure a data federation connector. For more information, see [Roles and permissions in the Microsoft Sentinel platform](/en-us/azure/sentinel/roles).

## Create a service principal

For Azure Databricks and ADLS Gen 2 federation, you need a service principal with access credentials stored in Azure Key Vault. You can use an existing service principal or use the following steps to create a new service principal.

1. **Create a Microsoft Entra ID application registration**:

    1. In the Azure portal, navigate to **Microsoft Entra ID** &gt; **App registrations**.
    2. Select **New registration**.
    3. Enter a name for the application.
    4. Leave the redirect URI empty (not required for this scenario).
    5. Select **Register**.
2. **Create a client secret**:

    1. In your app registration, go to **Certificates & secrets**.
    2. Select **New client secret**.
    3. Enter a description and select an expiration period.
    4. Select **Add**.
    5. Copy the client secret value immediately because you can't retrieve it later. You need this value when you store the secret in Azure Key Vault.
3. **Note the application details**:

    - Application (client) ID
    - Object ID
    - Directory (tenant) ID

For more information on creating service principals, see [Microsoft Entra ID app registrations](/en-us/entra/identity-platform/quickstart-register-app).

## Create an Azure Key Vault and store credentials

You can use an existing Azure Key Vault and follow the steps below to configure Key Vault access, or create a new Key Vault using the following steps:

1. **Create an Azure Key Vault**:

    1. In the Azure portal, create a new Azure Key Vault.
    2. Use the **Azure role-based access control (recommended)** permission model.
    3. Enable soft delete and purge protection settings for the key vault.
    4. Note the Key Vault URI after creation.
2. **Configure Key Vault access**:

    1. Assign the **Key Vault Secrets User** role to the Microsoft Sentinel platform's managed identity. The identity is prefixed with `msg-resources-`.
    2. If you're using access policies for Key Vaults instead of Azure role-based access control, provide the permissions for Get and List for Secret Management Operations.
3. **Store the client secret in Key Vault**:

    1. In your Key Vault, go to **Secrets** &gt; **Generate/Import**.
    2. Create a new secret containing the service principal's client secret.
    3. Note the secret name. It's used when configuring the data federation connector instance.

For more information on configuring Azure Key vaults, see [Azure Key Vaults](/en-us/azure/key-vault/general/basic-concepts).

## View and manage federated data connectors in the Defender portal

Federated connectors are managed on the Data connectors page in Microsoft Sentinel on the Defender portal.

1. Navigate to **Microsoft Sentinel** &gt; **Configuration** &gt; **Data connectors**.
2. Under **Data federation**, select **Catalog** to view the available federated connectors.

    The catalog page displays:

    - Available federation connector types
    - Number of configured instances for each connector
    - Publisher and support information

    [![Screenshot showing the data federation catalog with available connectors.](media/data-federation-setup/federation-catalog.png)](media/data-federation-setup/federation-catalog.png#lightbox)
3. Select **My connectors page** to view all configured connector instances. The page lists your tenant's data federation connector instances along with their display name, version, status, and support provider.
4. Select each instance to view details, edit configurations, or delete the instance.

[![Screenshot showing the My connectors page with configured federation instances.](media/data-federation-setup/my-connectors.png)](media/data-federation-setup/my-connectors.png#lightbox)

## Create a connector instance

The process for creating a connector instance varies depending on whether you're connecting to Microsoft Fabric, Azure Data Lake Storage Gen 2, or Azure Databricks. Follow the instructions for your specific data source type.

# [Microsoft Fabric](#tab/fabric)
Use the following steps to create a federated connector instance for Microsoft Fabric.

#### Create a Microsoft Fabric connector instance

Before configuring the Fabric connector instance, you must set up permissions within the Microsoft Fabric environment to allow Microsoft Sentinel to access the data.

- Configure the admin settings within Microsoft Fabric so that the tenant is enabled for External data sharing, For more information, see [Create an external data share](/en-us/fabric/governance/external-data-sharing-create).
- Configure the admin settings within Microsoft Fabric so that the setting is enabled for **Service principals can call Fabric public APIs**. For more information, see [Service principals can call Fabric public APIs](/en-us/fabric/admin/service-admin-portal-developer#service-principals-can-call-fabric-public-apis).
- Add the Sentinel platform identity, prefixed with `msg-resources-` as a Workspace Member on the Lakehouse from which you want to federate tables. For more information, see [Give access to workspaces](/en-us/fabric/fundamentals/give-access-workspaces).

To configure the Fabric connector instance:

1. On the **Data federation** &gt; **Catalog** page, select the **Microsoft Fabric** row.
2. In the side panel, select **Connect a connector**.
3. Enter the following information:

    | Field | Description |
    | --- | --- |
    | **Instance name** | A friendly name for this connector instance. This instance name is appended to the tables represented in the lake from this instance. |
    | **Fabric workspace ID** | ID of the Fabric workspace to federate. When you navigate to the Fabric workspace or Lakehouse, the workspace ID is in the URL after `/groups/` |
    | **Lakehouse table ID** | ID of the Fabric Lakehouse table to federate. When you navigate to the Fabric lakehouse, the lakehouse ID is shown in the URL after `/lakehouses/`. |
4. Select **Next**.

    [![Screenshot of the Microsoft Fabric connection details form.](media/data-federation-setup/fabric-connection-details.png)](media/data-federation-setup/fabric-connection-details.png#lightbox)
5. Select the tables you want to federate.
6. Select **Next**.
7. Review the federation target configuration.
8. Select **Connect** to create the connection instance.

# [Azure Data Lake Storage Gen 2](#tab/adls)
Use the following steps to create a federated connector instance for Azure Data Lake Storage (ADLS) Gen 2.

#### Create an ADLS Gen 2 connector instance

Before creating the connector, prepare your storage account:

1. If you're creating a new storage account, ensure the **Hierarchical namespaces** setting is enabled.
2. Assign the **Storage Blob Data Reader** role to the service principal you created earlier. For more information on granting access through the Azure portal, see [Assign Azure roles using the Azure portal - Azure RBAC](/en-us/azure/role-based-access-control/role-assignments-portal).
3. On the **Data federation** &gt; **Catalog** page, select **Azure Data Lake Storage**.
4. Select **Connect a connector**.
5. Configure the following name and connection details:

    | Field | Description |
    | --- | --- |
    | **Instance name** | A friendly name for this connector instance. The instance name is appended to the table names in the lake. |
    | **Application (client) ID** | GUID of the service principal with access to the Key Vault and the target data source. |
    | **Azure Key Vault URI** | URI of the Key Vault containing the authentication secret for the service principal. |
    | **Secret name** | Name of the secret in Key Vault containing the service principal client secret |
    | **Azure Data Lake Storage URL** | URL of the ADLS Gen 2 endpoint (must be publicly accessible) |
6. Select **Next** to continue.

    [![Screenshot of the ADLS Gen 2 connection details form.](media/data-federation-setup/adls-connection-details.png)](media/data-federation-setup/adls-connection-details.png#lightbox)
7. Select the tables you want to federate from your ADLS Gen 2 storage account.
8. Browse the available tables in your ADLS Gen 2 storage.
9. Select at least one table to federate.
10. Select **Next** to continue.

    [![Screenshot showing table selection for ADLS Gen 2 federation.](media/data-federation-setup/adls-select-tables.png)](media/data-federation-setup/adls-select-tables.png#lightbox)
11. Once you have selected the tables, review the configuration settings.
12. Select **Connect** to create the connector instance.
13. If you need to make changes, select **Back** to return to previous steps.

    [![Screenshot of the ADLS Gen 2 configuration review page.](media/data-federation-setup/adls-review.png)](media/data-federation-setup/adls-review.png#lightbox)

Select **Connect**, to complete the setup for the ADLS Gen 2 connector instance. The wizard closes and the instance count for Azure Data Lake Storage Gen2 increases.

# [Azure Databricks](#tab/databricks)
Use the following steps to create a federated connector instance for Azure Databricks.

#### Prepare the Azure Databricks environment

Before creating the connector, configure access in your Databricks environment as follows:

1. In Azure Databricks, select the catalog you want to connect to from Microsoft Sentinel data lake.
2. Select the gear icon for the catalog and select **Metastore**.
3. In your metastore details page, set **External data access** to **Enabled**.
4. In the catalog that you're federating with, select **Permissions** and then select **Grant**.
5. Search for the service principal you created earlier.
6. Grant the service principal the **Data Reader** privilege preset, and select **External Use Schema** permission and select **Confirm**.
7. In the top right of your Azure Databricks screen, select your account and select **Settings**.
8. Under **Identity and access**, select the **Manage** button next to **Service principals**.
9. Select Add service principal
10. Use the Service principal box to select an existing principal.
11. Select the service principal you created earlier and select Add.

#### Create the Azure Databricks connector instance

Follow these steps to create the Azure Databricks connector instance in the Defender portal:

1. On the **Data federation** &gt; **Catalog** page, select the **Azure Databricks** row.
2. In the side panel, select **Connect a connector**.
3. Enter the following details:

    | Field | Description |
    | --- | --- |
    | **Instance name** | A friendly name for this connector instance |
    | **Principal ID** | GUID of the service principal with Key Vault access |
    | **Azure Key Vault URI** | URI of the Key Vault containing the authentication secret |
    | **Secret name** | Name of the secret in Key Vault containing the Databricks connection information |
    | **Databricks URL** | URL of the Azure Databricks instance (must be publicly accessible) |
    | **Catalog name** | Name of the catalog in Azure Databricks to federate |
    | **Schema name** | Name of the schema in Azure Databricks to federate |

    [![Screenshot of the Azure Databricks connection details form.](media/data-federation-setup/databricks-connection-details.png)](media/data-federation-setup/databricks-connection-details.png#lightbox)
4. Select **Next**.
5. Select the tables you want to federate from your Azure Databricks instance.
6. Select **Next** to continue.

    [![Screenshot showing table selection for Azure Databricks federation.](media/data-federation-setup/databricks-select-tables.png)](media/data-federation-setup/databricks-select-tables.png#lightbox)
7. Review the configuration settings.
8. Select **Connect** to create the connector instance.
9. If you need to make changes, select **Back** to return to previous steps.

[![Screenshot of the Azure Databricks configuration review page.](media/data-federation-setup/databricks-review.png)](media/data-federation-setup/databricks-review.png#lightbox)

After selecting **Connect**, the wizard closes and the instance count for Databricks increases.

---

## Verify tables from your connector instance

After creating a connector instance check that the tables you federated are available in Microsoft Sentinel.

1. Navigate to **Microsoft Sentinel &gt; Configuration &gt; Tables**.
2. Filter by Type **Federated** to see all federated tables.
3. Search by your connector instance name.
4. Tables from your connector instance are listed with their name followed by `_instance name`. For example if your data connector instance name was `GlobalHRData` and your table was called `hrlogs`, your table name is shown as `hrlogs_GlobalHRData`.
5. Select a table from the list to open the details panel.
6. Select the **Overview** tab to see the table type and federation provider.
7. Select the **Data source** tab to see the connector instance data provider and source product for the table. Selecting the connector instance name takes you to that instance in **My Connectors** within **Data Connectors**.
8. Select the **Schema** tab to see the table schema.
9. On the **Schema** tab, select **Refresh** to refresh the table schema associated with the federated table.

[![Screenshot showing the federated table schema.](media/data-federation-setup/verify-tables.png)](media/data-federation-setup/verify-tables.png#lightbox)

## Manage connector instances

To modify or delete a connector instance:

1. Navigate to **Data federation** &gt; **My connectors page**.
2. Select the connector instance you want to manage.
3. In the details panel, use the available options to:
    - Edit connection settings
    - Add or remove federated tables
    - Delete the connector instance

Note

Microsoft Fabric connection instances don't support editing. You can create a new federated connection to add more tables, or you can delete the Fabric connection instance and recreate it with the same instance name and a different set of tables selected.

[![Screenshot showing the My Connectors page.](media/data-federation-setup/my-connectors.png)](media/data-federation-setup/my-connectors.png#lightbox)

## Troubleshooting

Use the following checks to diagnose common issues with federated data connector setup and operation.

### Connection fails

- Verify the Sentinel platform managed identity prefixed by `msg-resources-` has the correct permissions on Azure Key Vault.
- If your connection source is Azure Databricks or Azure Data Lake Storage Gen2, ensure the Key Vault secret contains the correct client secret for your service principal.
- If your connection source is Azure Databricks, confirm the target uses hybrid workspace type and that external data access has been enabled for the workspace.
- The Key Vault networking must be set to **Allow public access from all networks** during the connector configuration, which is the default configuration of Key Vault. It can be changed after connector creation or editing.
- Confirm the external data source is publicly accessible.
- Check that the service principal has appropriate permissions on the target data source for Azure Databricks and ADLS.
- If the target data source is Fabric, check that the `msg-resources-` prefixed identity for Microsoft Sentinel was granted permission as Workspace Member.
- Check to ensure you don't have more than 100 connection instances.

Note

ADLS and Azure Databricks use one connection instance per federated connection. Fabric may use more instances per federated connection. For Fabric, each lakehouse schema in your federated connection counts against the 100-instance limit.

### Tables don't appear

- Verify the service principal has read access to the target tables for ADLS and Azure Databricks, and the service principal is in the same tenant as these data sources.
- Verify the target tables are in delta parquet format.
- For Databricks, ensure you granted both the built-in Data Reader privilege preset plus the External Use Schema permission to the service principal.
- For ADLS Gen 2, confirm the Storage Blob Data Reader role is assigned to the service principal.

### Query performance issues

- Consider the size of data being queried from external sources.
- Optimize queries to filter data early.
- Check network connectivity between Sentinel and the external source.