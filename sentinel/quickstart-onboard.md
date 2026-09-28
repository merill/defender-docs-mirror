---
layout: Conceptual
title: Onboard to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/quickstart-onboard
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
description: In this quickstart, you enable Microsoft Sentinel, and set up data connectors to monitor and protect your environment.
ms.author: guywild
author: guywi-ms
ms.reviewer: soulisabag
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: references_regions, mode-other, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: bacad1e2-c50b-0d73-4055-9820778939c1
document_version_independent_id: afbc5d98-2415-321c-72ae-8b23f0e0f5f2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/quickstart-onboard.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/quickstart-onboard
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/quickstart-onboard.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 78a9c34b-0f03-7f32-5fc6-eb6946768ae3
---

# Onboard to Microsoft Sentinel | Microsoft Learn

In this quickstart, you'll enable Microsoft Sentinel and install a solution from the content hub. Then, you'll set up a data connector to start ingesting data into Microsoft Sentinel. Before you begin, make sure you meet the prerequisites, including an active Azure subscription and the required permissions.

Microsoft Sentinel comes with many data connectors for Microsoft products such as the Microsoft Defender XDR service-to-service connector. You can also enable built-in connectors for non-Microsoft products such as Syslog or Common Event Format (CEF). For this quickstart, you'll use the Azure Activity data connector that's available in the Azure Activity solution for Microsoft Sentinel.

To onboard to Microsoft Sentinel by using the API, see the latest supported version of [Sentinel Onboarding States](/en-us/rest/api/securityinsights/sentinel-onboarding-states).

## Prerequisites

- **Active Azure Subscription**: If you don't have one, create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.
- **Permissions**:

    - To enable Microsoft Sentinel, you need **contributor** permissions to the subscription in which the Microsoft Sentinel workspace resides.
    - To use Microsoft Sentinel, you need either **Microsoft Sentinel Contributor** or **Microsoft Sentinel Reader** permissions on the resource group that the workspace belongs to.
    - To install or manage solutions in the content hub, you need the **Microsoft Sentinel Contributor** role on the resource group that the workspace belongs to.
    - If you are a new Microsoft Sentinel customer and have permissions of a subscription [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) or a [User access administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator), your workspace is automatically onboarded to the Defender portal. Users of such workspaces use [Microsoft Sentinel in the Defender portal](microsoft-sentinel-defender-portal) only.
- **Microsoft Sentinel is a paid service**: Review the [Microsoft Sentinel pricing options](https://go.microsoft.com/fwlink/?linkid=2104058) and the [Microsoft Sentinel pricing page](https://azure.microsoft.com/pricing/details/azure-sentinel/).
- Before deploying Microsoft Sentinel to a production environment, review the [predeployment activities and prerequisites for deploying Microsoft Sentinel](prerequisites).

## Create a Log Analytics workspace

Microsoft Sentinel must be added to a workspace. If you already have a Log Analytics workspace, skip to Add Microsoft Sentinel to your Log Analytics workspace. If you don't already have a Log Analytics workspace, create one by using the following procedure in this section. For a more detailed explanation, see [Create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace). For more information about Log Analytics workspaces, see [Designing your Azure Monitor Logs deployment](/en-us/azure/azure-monitor/logs/workspace-design).

Your Log Analytics workspace might have a [default 30-day retention period under legacy pricing tiers](/en-us/azure/azure-monitor/logs/cost-logs#legacy-pricing-tiers). To make sure that you can use all Microsoft Sentinel functionality and features, raise the retention to 90 days. [Configure data retention and archive policies in Azure Monitor Logs](/en-us/azure/azure-monitor/logs/data-retention-configure).

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Sentinel**.![Screenshot of searching for and selecting Microsoft Sentinel from the Azure portal.](media/quickstart-onboard/search-sentinel.png)
3. Select **Create**. ![Screenshot of selecting Create to start creating a new Log Analytics workspace.](media/quickstart-onboard/log-analytics-workspace-create.png)
4. Select **Create a new workspace**. ![Screenshot of selecting Create a new workspace.](media/quickstart-onboard/log-analytics-workspace-create-a-new-workspace.png)
5. Under **Subscription** &gt; **Resource group**, select **Create new**. Enter a name for your resource group and select **OK**. ![Screenshot of creating a Log Analytics workspace screen. Under Subscription and resource group, Create New is selected.](media/quickstart-onboard/log-analytics-workspace-resource-group-create-new-with-name-both-selected.png)
6. Give the workspace a name and select a region, then select **Review + Create**. (See [Log Analytics regional availability](https://azure.microsoft.com/regions/services/).)
7. After validation has passed, select **Create**. Wait until your deployment is complete.

## Add Microsoft Sentinel to your Log Analytics workspace

To add Microsoft Sentinel to an existing Log Analytics workspace, perform the following steps:

1. From the [Azure portal](https://portal.azure.com/), search for and select **Microsoft Sentinel**.
2. Select **Create**. ![Screenshot of selecting Create to create a new Log Analytics workspace.](media/quickstart-onboard/log-analytics-workspace-create.png)
3. Select the workspace you want to use and select **Add**. You can run Microsoft Sentinel on more than one workspace, but data is isolated to a single workspace.

    - The default workspaces created by Microsoft Defender for Cloud aren't shown in the list. You can't install Microsoft Sentinel on these workspaces.
    - Once deployed on a workspace, Microsoft Sentinel **doesn't support** moving that workspace to another resource group or subscription.

Note

If your workspace isn't automatically onboarded to the Defender portal, we recommend onboarding for a unified experience in managing security operations (SecOps) across both Microsoft Sentinel and other Microsoft security services. For more information, see [Onboard Microsoft Sentinel to the Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard).

If your workspace is automatically onboarded, or if you decide to onboard your workspace now, you can continue with Install a solution from the content hub and Set up the data connector from the Defender portal. If this is your first time using the Defender portal, there will be a delay of a few minutes while the process completes.

## Access Microsoft Sentinel in the Defender portal

To access Microsoft Sentinel in the Defender portal:

1. Sign into the [Defender portal](https://security.microsoft.com).

    The first time you access the Defender portal, it'll take some time to provision your tenant.
2. Once provisioned, you'll see **Microsoft Sentinel** available in the navigation pane, with Microsoft Sentinel nodes nested within. For example:

    ![Screenshot of Microsoft Sentinel in the Defender portal.](media/quickstart-onboard/defender-portal-initial-view.png)
3. Scroll down in the navigation pane, and select **Settings &gt; Microsoft Sentinel &gt; Workspaces** to view the workspaces onboarded to the Defender portal and available to you.

The Defender portal supports multiple workspaces, with one workspace acting as the primary workspace per tenant. For more information, see [Multiple Microsoft Sentinel workspaces in the Defender portal](workspaces-defender-portal) and [Microsoft Defender multitenant management](/en-us/defender-xdr/mto-overview).

## Install a solution from the content hub

The content hub in Microsoft Sentinel is the centralized location to discover and manage out-of-the-box content including data connectors. For this quickstart, install the solution for Azure Activity.

1. In Microsoft Sentinel, browse to the **Content hub** page, and find and select the **Azure Activity** solution.

# [Defender portal](#tab/defender-portal)
![Screenshot of the content hub in the Defender portal with the solution for Azure Activity selected.](media/quickstart-onboard/content-hub-azure-activity-defender.png)

# [Azure portal](#tab/azure-portal)
![Screenshot of the content hub in the Azure portal with the solution for Azure Activity selected.](media/quickstart-onboard/content-hub-azure-activity.png)

---
2. On the solution details pane on the side, select **Install**.

## Set up the Azure Activity data connector

Microsoft Sentinel ingests data from services and apps by connecting to the service and forwarding the events and logs to Microsoft Sentinel. For this quickstart, install the data connector to forward data for Azure Activity to Microsoft Sentinel.

1. In Microsoft Sentinel, select **Configuration** &gt; **Data connectors** and search for and select the **Azure Activity** data connector.
2. In the connector details pane, select **Open connector page**. Use the instructions on the **Azure Activity** connector page to set up the data connector.

    1. Select **Launch Azure Policy Assignment Wizard**.
    2. On the **Basics** tab, set the **Scope** to the subscription and resource group that has activity to send to Microsoft Sentinel. For example, select the subscription that contains your Microsoft Sentinel instance.
    3. Select the **Parameters** tab, and set the **Primary Log Analytics workspace**. This should be the workspace where Microsoft Sentinel is installed.
    4. Select **Review + create** and **Create**.

## Generate activity data

Let's generate some activity data by enabling a rule that was included in the Azure Activity solution for Microsoft Sentinel. This step also shows you how to manage content in the content hub.

1. In Microsoft Sentinel, select **Content hub** and search for and select **Suspicious Resource deployment** rule template in the **Azure Activity** solution.
2. In the details pane, select **Create rule** to create a new rule using the **Analytics rule wizard**.
3. In the **Analytics rule wizard - Create a new Scheduled rule** page, change the **Status** to **Enabled**.

    On the **General**, **Set rule logic**, **Incident settings**, and **Automated response** tabs, leave the default values as they are.
4. On the **Review and create** tab, select **Create**.

## View data ingested into Microsoft Sentinel

Now that you've enabled the Azure Activity data connector and generated some activity data let's view the activity data added to the workspace.

1. In Microsoft Sentinel, select **Configuration** &gt; **Data connectors** and search for and select the **Azure Activity** data connector.
2. In the connector details pane, select **Open connector page**.
3. Review the **Status** of the data connector. It should be **Connected**.

    ![Screenshot of data connector for Azure Activity with the status showing as connected.](media/quickstart-onboard/azure-activity-connected-status.png)
4. Select a tab to continue, depending on which portal you're using:

# [Defender portal](#tab/defender-portal)
1. Select **Go to log analytics** to open the **Advanced hunting** page.
    2. On the top of the pane, next to the **New query** tab, select the **+** to add a new query tab.
    3. Run the following query to view the activity date ingested into the workspace:

        ```kusto
        AzureActivity
        ```

For example:

![Screenshot of the AzureActivity query in the Logs page of the Defender portal.](media/quickstart-onboard/content-hub-azure-activity-defender.png)

# [Azure portal](#tab/azure-portal)
1. Select **Go to query** to open the **Logs** page in the Azure portal.
    2. On the top of the pane, next to the **New query 1** tab, select the **+** to add a new query tab.
    3. On the side, switch from **Simple mode** to **KQL mode**, and run the following query to view the activity date ingested into the workspace:

        ```kusto
        AzureActivity
        ```

For example:

![Screenshot of the AzureActivity query in the Logs page of the Azure portal.](media/quickstart-onboard/azure-activity-logs-query.png)

---

## Summary

In this quickstart, you enabled Microsoft Sentinel and installed a solution from the content hub. Then, you set up a data connector to start ingesting data into Microsoft Sentinel. You also verified that data is being ingested by viewing the data in the workspace.

If you're a new customer who's been automatically onboarded to the Defender portal, your users will access Microsoft Sentinel in the Defender portal only. As you use the Microsoft Sentinel documentation, make sure to select the Defender portal version of the documentation.