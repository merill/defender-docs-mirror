---
layout: Conceptual
title: Set up Azure Resources to Export Security Alerts to IBM QRadar and Splunk - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/export-to-splunk-or-qradar
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to configure the required Azure resources in the Azure portal to stream security alerts to IBM QRadar and Splunk.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: f3507cc9-407f-b66d-3283-a0c25cee7ce3
document_version_independent_id: 0dc171eb-4d01-d14a-93f5-c043fbbe4397
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/export-to-splunk-or-qradar.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/export-to-splunk-or-qradar
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/export-to-splunk-or-qradar.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
platformId: 65de6c9e-cf05-67fd-4368-fa7f5407b468
---

# Set up Azure Resources to Export Security Alerts to IBM QRadar and Splunk - Microsoft Defender for Cloud | Microsoft Learn

To stream Microsoft Defender for Cloud security alerts to IBM QRadar and Splunk, set up resources in Azure, such as Azure Event Hubs and Microsoft Entra ID. Use these instructions to configure these resources in the Azure portal. You can also configure them by using a PowerShell script. Before you configure the Azure resources for exporting alerts to QRadar and Splunk, review [Stream alerts to QRadar and Splunk](export-to-siem#stream-alerts-to-qradar-and-splunk).

To configure the Azure resources for QRadar and Splunk in the Azure portal:

## Step 1: Create an Event Hubs namespace and event hub with send permissions

Create an Event Hubs namespace, an event hub, and a shared access policy with send permissions.

1. In the [Event Hubs service](/en-us/azure/event-hubs/event-hubs-create), create an Event Hubs namespace:

    1. Select **Create**.
    2. Enter the details of the namespace, select **Review + create**, and select **Create**.

    [![Screenshot of creating an Event Hubs namespace in Microsoft Event Hubs.](media/export-to-siem/create-event-hub-namespace.png)](media/export-to-siem/create-event-hub-namespace.png#lightbox)
2. Create an event hub:

    1. In the namespace that you create, select **+ Event Hub**.
    2. Enter the details of the event hub, and select **Review + create**, and select **Create**.
3. Create a shared access policy.

    1. In the Event Hubs menu, select the Event Hubs namespace you created.
    2. In the Event Hubs namespace menu, select **Event Hubs**.
    3. Select the event hub that you created.
    4. In the event hub menu, select **Shared access policies**.
    5. Select **Add**, enter a unique policy name, and select **Send**.
    6. Select **Create** to create the policy.

    [![Screenshot of creating a shared policy in Microsoft Event Hubs.](media/export-to-siem/create-shared-access-policy.png)](media/export-to-siem/create-shared-access-policy.png#lightbox)

## Step 2: For streaming to QRadar SIEM - Create a Listen policy

If you're streaming to QRadar, create a Listen policy on the same event hub.

1. Select **Add**, enter a unique policy name, and select **Listen**.
2. Select **Create** to create the policy.
3. After the listen policy is created, copy the **Connection string primary key** and save it to use later.

    [![Screenshot of creating a listen policy in Microsoft Event Hubs.](media/export-to-siem/create-shared-listen-policy.png)](media/export-to-siem/create-shared-listen-policy.png#lightbox)

## Step 3: Create a consumer group, then copy and save the name to use in the SIEM platform

Create a consumer group for your event hub and save its name for later use when you configure your SIEM platform.

1. In the **Entities** section of the Event Hubs event hub menu, select **Event Hubs** and then select the event hub you created.

    [![Screenshot of opening the event hub Microsoft Event Hubs.](media/export-to-siem/open-event-hub.png)](media/export-to-siem/open-event-hub.png#lightbox)
2. Select **Consumer group**.

## Step 4: Enable continuous export for the scope of the alerts

Use Azure Policy to enable continuous export of security alerts to your event hub.

Tip

If you assign this policy at the tenant (root management group) level, it automatically streams alerts from any *new* subscription created under that tenant.

1. In the Azure search box, search for *policy* and go to the Policy.
2. In the Policy menu, select **Definitions**.
3. Search for *deploy export* and select the **Deploy export to Event Hub for Microsoft Defender for Cloud data** built-in policy.
4. Select **Assign**.
5. Define the basic policy options:

    1. In **Scope**, select **...** to choose where the policy applies.
    2. Find the root management group for tenant scope, management group, subscription, or resource group. Then select **Select**.

        - You need tenant-level permissions to select the root management group.
    3. (Optional) In **Exclusions**, select subscriptions to exclude from the export.
    4. Enter an assignment name.
    5. Make sure policy enforcement is enabled.

    [![Screenshot of assignment for the export policy.](media/export-to-siem/create-export-policy.png)](media/export-to-siem/create-export-policy.png#lightbox)
6. In the policy parameters:

    1. Enter the resource group where the automation resource is saved.
    2. Select the resource group location.
    3. Select **...** next to **Event Hub details** and enter these details:

        - Subscription.
        - The Event Hubs namespace you created.
        - The event hub you created.
        - In **authorizationrules**, select the shared access policy you created for sending alerts.

    [![Screenshot of parameters for the export policy.](media/export-to-siem/create-export-policy-parameters.png)](media/export-to-siem/create-export-policy-parameters.png#lightbox)
7. Select **Review and Create**, then select **Create** to finish defining continuous export to Event Hubs.

    - When you activate this policy at the tenant (root management group) level, it streams alerts from any **new** subscription created under that tenant.

## Step 5: **For streaming alerts to QRadar SIEM** - Create a storage account

To stream alerts to QRadar, create a storage account that QRadar uses to consume events.

1. Go to the Azure portal, select **Create a resource**, and select **Storage account**. If that option isn't shown, search for "storage account".
2. Select **Create**.
3. Enter the details for the storage account, select **Review and Create**, and then **Create**.

    [![Screenshot of creating storage account.](media/export-to-siem/create-storage-account.png)](media/export-to-siem/create-storage-account.png#lightbox)
4. After you create your storage account and go to the resource, in the menu select **Access Keys**.
5. Select **Show keys** to see the keys, and copy the connection string of Key 1.

    [![Screenshot of copying storage account key.](media/export-to-siem/copy-storage-account-key.png)](media/export-to-siem/copy-storage-account-key.png#lightbox)

## Step 6: For streaming alerts to Splunk SIEM - Create a Microsoft Entra application

If you're streaming alerts to Splunk, register a Microsoft Entra application that Splunk uses to authenticate with the event hub.

1. In the menu search box, search for *Microsoft Entra ID* and go to Microsoft Entra ID.
2. Go to the Azure portal, select **Create a resource**, and select **Microsoft Entra ID**. If that option isn't shown, search for *active directory*.
3. In the menu, select **App registrations**.
4. Select **New registration**.
5. Enter a unique name for the application and select **Register**.

    [![Screenshot of registering application.](media/export-to-siem/register-application.png)](media/export-to-siem/register-application.png#lightbox)
6. Copy and save the **Application (client) ID** and **Directory (tenant) ID**.
7. Create the client secret for the application:

    1. In the menu, go to **Certificates & secrets**.
    2. Create a password for the application to prove its identity when requesting a token:
    3. Select **New client secret**.
    4. Enter a short description, choose the expiration time of the secret, and select **Add**.

    [![Screenshot of creating client secret.](media/export-to-siem/create-client-secret.png)](media/export-to-siem/create-client-secret.png#lightbox)
8. After the client secret is created, copy the secret **Value** and save it for later use together with the **Application (client) ID** and **Directory (tenant) ID**.

## Step 7: For streaming alerts to Splunk SIEM - Allow Microsoft Entra ID to read from the event hub

Grant your Microsoft Entra application the Data Receiver role on the Event Hubs namespace so Splunk can read events.

1. Go to the Event Hubs namespace you created.
2. In the menu, go to **Access control**.
3. Select **Add** and select **Add role assignment**.
4. Select **Add role assignment**.

    [![Screenshot of adding a role assignment.](media/export-to-siem/add-role-assignment.png)](media/export-to-siem/add-role-assignment.png#lightbox)
5. In the **Roles** tab, search for **Azure Event Hubs Data Receiver**.
6. Select **Next**.
7. Select **Select Members**.
8. Search for the Microsoft Entra application you registered in Step 6. Select it.
9. Select **Close**.

Your Azure resources are now configured to stream security alerts to your SIEM platform.