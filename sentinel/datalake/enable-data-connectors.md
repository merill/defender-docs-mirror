---
layout: Conceptual
title: Asset data in Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/enable-data-connectors
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
description: Asset data in security data lake
author: mberdugo
ms.topic: concept-article
ms.date: 2026-05-13T00:00:00.0000000Z
ms.author: monaberdugo
ms.collection: ms-security
ai-usage: ai-assisted
locale: en-us
document_id: 80f3afbb-53c2-bed3-69df-ed6d2c0dda70
document_version_independent_id: 672ce8fd-a6d0-7892-1687-71b466ff20a6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/enable-data-connectors.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/enable-data-connectors
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/enable-data-connectors.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 14a3de11-10e5-eb09-1ae6-883fae49e3dd
---

# Asset data in Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn

Asset data in cybersecurity refers to an organization’s physical and digital entities such as computers, identities, software, cloud services, and networks. It shows what exists so you know what must be protected. Microsoft Sentinel’s data lake adds powerful value by storing this asset data in a scalable, cost-efficient way that supports long-term retention, advanced analytics, and AI-driven threat detection. With unified visibility across systems and flexible data management, Sentinel lake helps security teams understand their environment, spot unusual activity, and respond to threats.

## How is asset data ingestion enabled in Sentinel data lake?

- When you onboard to Sentinel lake, asset data is automatically ingested if you have appropriate permissions. For more information, see Required permissions for asset sources.
- If you don't have sufficient permissions, asset tables are created but no data is ingested. Manually enable asset data ingestion as follows:

    1. Go to the Microsoft Sentinel workspace in the Azure portal.
    2. Navigate to the **Data connectors** page.
    3. Find the relevant asset data source connector.
    4. Select the connector and follow the prompts to enable ingestion.
- Asset data is ingested into the Microsoft Sentinel data lake tier only. After onboarding, asset data, it can take up to 24 hours to arrive in the lake.
- Asset data is retained for 30 days by default. Retention can be expanded for up to 12 years. For more information on managing table retention, see [Table Management documentation](../manage-table-tiers-retention).

## Billing considerations

- Customers incur charges for asset data ingestion.
- Customers incur charges for asset data retention.

Asset data snapshots are taken once every 24 hours.

Since asset data ingestion is enabled by default when onboarding to Sentinel data lake, it’s important to understand the foundational role of asset Sentinel data connectors that facilitate asset data ingestion. These data connectors are responsible for bringing asset-related data into Sentinel data lake and are bundled within their respective Sentinel Solution packages. You can discover and manage these solutions through the Content Hub.

## Required permissions for asset sources

The following table describes the various asset data sources and their data connectors:

| Data Source | Tables | Permission | Data Connector Solution |
| --- | --- | --- | --- |
| **Azure Resource Graph (ARG)** | [ARGResources](asset-data-tables#argresources)[ARGResourceContainers](asset-data-tables#argresourcecontainers)[ARGAuthorizationResources](asset-data-tables#argauthorizationresources) | Subscription Owner | Azure Resource Graph |
| **Microsoft Entra ID** | [EntraApplications](asset-data-tables#entraapplications)[EntraGroupMemberships](asset-data-tables#entragroupmemberships)[EntraGroups](asset-data-tables#entragroups)[EntraMembers](asset-data-tables#entramembers)[EntraOrganizations](asset-data-tables#entraorganizations)[EntraServicePrincipals](asset-data-tables#entraserviceprincipals)[EntraUsers](asset-data-tables#entrausers) | None | Microsoft Entra ID Asset |

Note

Certain data connectors, including but not limited to asset connectors, contribute to the construction of data risk graphs in Purview. If these graphs are active, disabling the associated connectors interrupts their generation. Connector descriptions indicate if they're involved in building data risk graphs.

### Expand Azure Resource Graph connector coverage

The Azure Resource Graph connector ingests only the Azure resources that can be read by its managed identity. When you enable the connector, its managed identity is granted the **Reader** role only on the subscriptions where you have the **Owner** role. Most users don't have **Owner** access across every subscription in the tenant, so the connector often ingests a partial view of your Azure estate, which limits coverage.

To expand coverage after the connector is enabled, a user with higher-level permissions must assign the **Reader** role to the connector's managed identity. This user should have tenant root privileges, be a Global Administrator with elevated tenant-level access, or have User Access Administrator or Owner permissions at a higher scope. The user must find the managed identity associated with the connector in the Azure portal and assign the Reader role at the broadest scope you want ingested. For example, assigning at the tenant root management group level allows the connector to read resources across all subscriptions in the tenant, while assigning at a specific management group or subscription level limits the scope accordingly.

Follow these steps to assign the Reader role to the Azure Resource Graph connector's managed identity:

1. In the Azure portal, locate the managed identity that the connector created. The identity's name is `msg-resources-` followed by an alphanumeric ID that depends on the version, for example `msg-resources-b05e`.
2. Select a scope that covers the resources you want ingested:

    - **Tenant root management group** to cover all subscriptions in the tenant.
    - A specific **management group** to cover a subset of subscriptions.
    - One or more individual **subscriptions**.

    [![Screenshot of the Tenant Root Group overview page in the Azure portal.](media/enable-data-connectors/azure-resource-graph-scope-management-group.png)](media/enable-data-connectors/azure-resource-graph-scope-management-group.png#lightbox)
3. Select **Access control (IAM)**.
4. Select **+ Add** &gt; **Add role assignment**.

    [![Screenshot of the Access control (IAM) page with the Add role assignment menu item highlighted.](media/enable-data-connectors/azure-resource-graph-add-role-assignment.png)](media/enable-data-connectors/azure-resource-graph-add-role-assignment.png#lightbox)
5. Assign the **Reader** role to the connector's managed identity. For step-by-step guidance, see [Assign Azure roles using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal) and, when assigning at the tenant root, [Elevate access to manage all Azure subscriptions and management groups](/en-us/azure/role-based-access-control/elevate-access-global-admin).

    [![Screenshot of the Add role assignment page with the Reader role selected.](media/enable-data-connectors/azure-resource-graph-select-reader-role.png)](media/enable-data-connectors/azure-resource-graph-select-reader-role.png#lightbox)

After the assignment propagates, the next ingestion cycle picks up the additional resources. It can take up to 24 hours for the new data to appear in the lake.

## Prerequisites

To manage asset data connectors, you need to meet the following prerequisites:

- Ensure you have the necessary [access and permissions](../roles#roles-and-permissions-for-the-microsoft-sentinel-data-lake) to Microsoft Sentinel, as specified *Permissions* column of the previous table.
- Search for the relevant solution containing the data connector in the Content Hub. Content Hub can be found under the **Microsoft Sentinel** menu **Content Management** &gt; **Content Hub**. Install the solution if not already installed.

[![Screenshot of Sentinel Defender data connectors page with the Azure Resource Graph data connector displayed.](media/enable-data-connectors/data-connectors.png)](media/enable-data-connectors/data-connectors.png#lightbox)

## Configure and Manage

Access the connector page in one of the following ways:

- From the installed solution:

    - Select **Manage**
    - Select the connector and then **Open connector page**
- From the Connector gallery:

    - The Connector gallery can be found under the **Microsoft Sentinel** menu **Configuration** &gt; **Data connectors**

To edit the table retention period, select on the three dots (…) to the right of the table name in the table manage grid. Select a retention period for up to 12 years. When asset data connector shows a *Connected* status, the toggle button text shows *Disconnect*. This indicates that ingestion is enabled. To disable the ingestion, select the *Disconnect* button. Once disconnected, the connector status shows *Disconnected* and the button text toggles to *Connect*.

[![Screenshot of asset home page with connect button.](media/enable-data-connectors/disconnect.png)](media/enable-data-connectors/disconnect.png#lightbox)

## Use asset data to enrich activity data

Asset data adds valuable context and insights that might not be evident from activity logs alone. For example, when investigating risky sign-ins in the `SigninLogs` table, you can enhance the analysis by joining it with the `EntraUsers` table to include user-specific attributes such as department and hire date. This extra context helps security teams better understand user behavior and assess potential threats more accurately.

```kql
SigninLogs
| where IsRisky == true
| join kind=leftouter (
   EntraUsers
   | summarize arg_max(TimeGenerated, userPrincipalName, department, employeeHireDate) by userPrincipalName
) on $left.UserPrincipalName == $right.userPrincipalName
| project Identity, UserPrincipalName, IsRisky, IPAddress, department, employeeHireDate
```

## Execute KQL queries on asset data

To execute KQL queries on asset data in the Sentinel data lake, ensure that you are querying within the correct workspace scope. Follow these steps:

1. Navigate to the **Microsoft Sentinel** menu **Data lake exploration** &gt; **KQL queries**
2. Select the **Selected workspace** button.

    ![Screenshot of the KQL queries information bar showing a button to select the workspace.](media/enable-data-connectors/select-workspace.png)
3. Ensure that the *System tables* workspace is selected.

    ![Screenshot of the KQL queries information bar showing the System tables workspace selected.](media/enable-data-connectors/workspace-scope.png)

Asset data tables are shown under the Asset category:

[![Screenshot of the KQL queries table picker showing asset data tables under the Asset category.](media/enable-data-connectors/kql-queries.png)](media/enable-data-connectors/kql-queries.png#lightbox)