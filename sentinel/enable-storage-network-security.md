---
layout: Conceptual
title: Enable Network Security for Azure Storage Blob Connectors | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/enable-storage-network-security
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
description: Learn how to enable network security for Azure Storage connector resources. Follow step-by-step instructions to secure your storage accounts with Network Security Perimeters.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: krishsa
ms.date: 2026-07-01T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 138afdf3-528a-a250-ff20-01445726651a
document_version_independent_id: d3d8f93b-bff3-effd-9bc1-405af4c90dce
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/enable-storage-network-security.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/enable-storage-network-security
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/enable-storage-network-security.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/467aaae1-e916-4fcd-a463-5b27f9d4745c
- https://authoring-docs-microsoft.poolparty.biz/devrel/de8ce683-cbe1-461b-bae7-77db0888ec6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fbd4eef5-2258-406b-95d3-2c68fa333b20
- https://authoring-docs-microsoft.poolparty.biz/devrel/a06cf482-4ca9-4582-a142-bcf842258d42
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 4bf87bae-2b9e-106c-cd5c-b1983ea909f1
---

# Enable Network Security for Azure Storage Blob Connectors | Microsoft Learn

## Overview

This article provides step-by-step instructions on how to enable network security on the storage resources integrated with your Azure Storage connector. Azure network security perimeter (NSP) is an Azure-native feature that creates a logical isolation boundary for your PaaS resources. By associating resources like storage accounts or databases with an NSP, you can centrally manage network access using a simplified rule set. For more information, see [Network security perimeter concepts](/en-us/azure/private-link/network-security-perimeter-concepts).

## Prerequisites

Before you begin, you must have the following Azure Storage connector resources already deployed and configured:

- **Azure Storage account**: The storage account integrated with your Azure Storage connector.
- **Azure Storage queue**: The queue that receives blob creation event notifications.
- **Event Grid system topic**: The system topic on the storage account that streams blob creation events to the storage queue.

If you haven't created these resources yet, see [Set up your Azure Storage Connector to stream logs to Microsoft Sentinel](setup-azure-storage-connector).

To complete this setup, ensure you have the following permissions:

- Subscription Owner or Contributor to create network security perimeter resources.
- Storage Account Contributor to associate the storage account with the NSP.
- Storage Account User Access Administrator or Owner to assign RBAC roles to the Event Grid managed identity.
- Event Grid Contributor to enable managed identity and manage event subscriptions.

## Enable Network Security

To enable network security on the storage resources integrated with your Azure Storage connector, create a Network Security Perimeter (NSP), associate the storage account with it, and configure the rules to allow traffic from Event Grid and other required sources while blocking unauthorized access. Use the following steps to complete the Network Security Perimeter configuration for the storage account.

### Create a Network Security Perimeter

To create a Network Security Perimeter in the Azure portal, perform the following steps:

1. In the Azure portal, search for *Network Security Perimeters*
2. Select **Create**.
3. Select a **Subscription** and **Resource group**.
4. Enter **Name**, for example `storageblob-connectors-nsp`
5. Select a **Region**. The region must be the same region as the storage account.
6. Enter a **Profile name** or accept the default. The profile defines the set of rules that are applied to associated resources. You can have multiple profiles within a single NSP to apply different rules to different resources if required.
7. Select **Review + create**, then select **Create**.

    [![A screenshot showing the creation of a Network Security Perimeter in the Azure portal.](media/enable-storage-network-security/create-network-security-perimeter.png)](media/enable-storage-network-security/create-network-security-perimeter.png#lightbox)

### Associate the Storage Account with the Network Security Perimeter

To associate the storage account with the Network Security Perimeter, perform the following steps:

1. Open your newly created Network Security Perimeter resource in the Azure portal.
2. Select **Profiles**, then select the profile name you used when creating the NSP resource.
3. Select **Associated resources**.
4. Select **Add**.
5. Search for and add your storage account, then select **Select**.
6. Select **Associate**.

The access mode is set to **Transition** by default, allowing you to validate the configuration before enforcing restrictions.

[![A screenshot showing how to associate a storage account with the Network Security Perimeter in the Azure portal.](media/enable-storage-network-security/associate-resources.png)](media/enable-storage-network-security/associate-resources.png#lightbox)

### Enable System-Assigned Identity on Event Grid System Topic

To enable a system-assigned managed identity on the Event Grid system topic, perform the following steps:

1. From your storage account, navigate to the **Events** tab.
2. Select the **System Topic** used to stream blob creation events to the storage queue.

    [![A screenshot showing the Event tab for Storage Accounts in the Azure portal.](media/enable-storage-network-security/select-event-system-topic.png)](media/enable-storage-network-security/select-event-system-topic.png#lightbox)
3. Select **Identity**.
4. On the **System assigned** tab, set the **Status** to **On**.
5. Select **Save**, then copy the managed identity's **Object ID**. You need this Object ID when assigning the **Storage Queue Data Message Sender** role in the next section.

    [![A screenshot showing the creation of a managed identity for an Event Grid System Topic in the Azure portal.](media/enable-storage-network-security/create-system-assigned-identity.png)](media/enable-storage-network-security/create-system-assigned-identity.png#lightbox)

### Grant RBAC permissions on the Storage Queue

To grant the Event Grid system topic managed identity permission to send messages to the storage queue, perform the following steps:

1. Navigate to your **Storage Account**.
2. Select **Access Control (IAM)**.
3. Select **Add**.
4. Search for and select the **Storage Queue Data Message Sender** role (scope: the storage account).
5. Select the **Members** tab and then **Select members**.
6. In the **Select members** pane, paste the Object ID of the system-assigned managed identity for the Event Grid system topic.
7. Select the managed identity and then select **Select**.
8. Select **Review + assign** to complete the role assignment. [![A screenshot showing the assignment of the Storage Queue Data Message Sender role to a managed identity in the Azure portal.](media/enable-storage-network-security/add-role-assignment.png)](media/enable-storage-network-security/add-role-assignment.png#lightbox)

### Enable Managed Identity on the event subscription

To enable managed identity on the event subscription, perform the following steps:

1. Open the **Event Grid System Topic**.
2. Select the event subscription that targets the queue.
3. Select the **Additional settings** tab.
4. Set **Managed identity type** to **System-assigned**.
5. Select **Save**.
6. Review the Event Grid subscription metrics to validate messages are successfully published to the storage queue after this update.

[![A screenshot showing the enabling of managed identity for an Event Grid subscription in the Azure portal.](media/enable-storage-network-security/set-additional-features.png)](media/enable-storage-network-security/set-additional-features.png#lightbox)

### Configure Inbound Access rules on the Network Security Perimeter profile

The following rules are required to allow Event Grid to deliver messages to the storage account while blocking unauthorized access. Depending on the system sending data to the storage account or accessing the storage resources, you may need to add additional inbound rules. Review your scenario and traffic patterns to determine whether you need only the required Event Grid rules or additional inbound NSP rules, and allow time for rule propagation.

#### Rule 1: Allow the Subscription (Event Grid Delivery)

Event Grid delivery doesn't originate from fixed public IPs. The NSP validates delivery using subscription identity.

1. Navigate to Network Security Perimeter and select your NSP.
2. Select **Profiles** and then select the profile associated with your storage account.
3. Select **Inbound access rules** and then select **Add**.

    [![A screenshot showing the Inbound access rules page in the Azure portal.](media/enable-storage-network-security/inbound-access-rules.png)](media/enable-storage-network-security/inbound-access-rules.png#lightbox)
4. Enter a **Rule name**; for example, `Allow-Subscription`.
5. Select *Subscription* from the **Source type** drop-down.
6. Select your subscription from the **Allowed Sources** drop-down.
7. Select **Add** to create the rule.

    [![A screenshot showing the creation of an inbound access rule to allow a subscription in the Azure portal.](media/enable-storage-network-security/add-inbound-rule.png)](media/enable-storage-network-security/add-inbound-rule.png#lightbox)

Note

Rules can take a few minutes to appear in the list after creation.

#### Rule 2: Allow Scuba service IP ranges

Create an inbound rule that allows the Scuba service IP ranges required for this scenario.

1. Create a second **Inbound access rules**.
2. Enter a **Rule name**; for example, `Allow-Scuba`.
3. Select **IP address ranges** from the **Source type** drop-down.
4. Open the [Download Azure service tags JSON files](/en-us/azure/virtual-network/service-tags-overview#discover-service-tags-by-using-downloadable-json-files) page.
5. Select your cloud; for example, **Azure Public**.
6. Select the **Download** button and open the downloaded file to get the list of IP ranges.
7. Find the `Scuba` service tag and copy the associated IPv4 ranges.

    Important

    Remove the quotes from the IP ranges and ensure that there's no trailing comma on the last entry before pasting them into the **Allowed Sources** field. Service tag ranges update over time; refresh regularly to keep rules current.
8. Paste the IPv4 ranges into the **Allowed Sources** field after removing any quotes and trailing commas.
9. Select **Add** to create the rule.

    [![A screenshot showing a part of the ServiceTags_Public.json file with the Scuba service tag and IPv4 ranges highlighted.](media/enable-storage-network-security/scuba-ipv4-addresses.png)](media/enable-storage-network-security/scuba-ipv4-addresses.png#lightbox)

### Validate and enforce

After configuring the rules, monitor the diagnostic logs for the Network Security Perimeter to validate that legitimate traffic is allowed and there are no disruptions. Once you have confirmed that the rules are correctly allowing necessary traffic, you can switch from Transition mode to Enforced mode to block unauthorized access.

#### Transition mode

Enable Network Security Perimeter diagnostic logs and review collected telemetry to validate communication patterns before enforcement. For more information, see [Diagnostic logs for Network Security Perimeter](/en-us/azure/private-link/network-security-perimeter-diagnostic-logs).

#### Apply Enforcement mode

Once validation is successful, set the access mode to **Enforced** as follows:

1. From the Network Security Perimeter page, under **Settings**, select **Associated resources**.
2. Select the storage account.
3. Select **Change access mode**.
4. Select **Enforced** and then **Save**.

    [![A screenshot showing how to change the access mode of a storage account associated with a Network Security Perimeter in the Azure portal.](media/enable-storage-network-security/change-access-mode.png)](media/enable-storage-network-security/change-access-mode.png#lightbox)

### Post-enforcement validation

After you set the NSP access mode to **Enforced**, monitor the environment closely for any blocked traffic that may indicate misconfigurations. Validate the Event Grid configuration isn't impacted by reviewing the Event Grid system topic subscription metrics.

Use the diagnostic logs to investigate and resolve any issues that arise. Review the metrics on the storage account (queue ingress and errors) and Event Grid (delivery success) to validate for any errors. Roll back to Transition Mode if you experience any disruption and repeat investigation using the diagnostic logs.

#### Set Secured by Perimeter on the Storage Account (Optional)

Setting the storage account to **Secured by Perimeter** ensures that all traffic to the storage account is evaluated against the Network Security Perimeter rules and blocks public network access.

1. Navigate to your **Storage Account**.
2. Under **Security + networking**, select **Networking**.
3. Under **Public network access**, select **Manage**.
4. Set **Secured by Perimeter (Most restricted)**.
5. Select **Save**.

[![A screenshot showing how to set a storage account to 'Secured by Perimeter' in the Azure portal.](media/enable-storage-network-security/set-storage-networking.png)](media/enable-storage-network-security/set-storage-networking.png#lightbox)