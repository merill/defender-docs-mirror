---
layout: Conceptual
title: Ingest Microsoft Defender for Cloud alerts into Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-defender-for-cloud
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
description: Connect Microsoft Defender for Cloud alerts to Microsoft Sentinel using subscription-based or tenant-based connectors, and configure alert synchronization between the services.
ms.author: guywild
author: guywi-ms
ms.reviewer: idpelleg
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 0553cf81-6976-c1c2-9d21-5776f381c9ed
document_version_independent_id: bbc33ec4-5fad-53cb-679b-e59d4a99a3dd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-defender-for-cloud.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-defender-for-cloud
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-defender-for-cloud.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 585d5628-2e65-ab0a-a554-0cd118165099
---

# Ingest Microsoft Defender for Cloud alerts into Microsoft Sentinel | Microsoft Learn

[Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/)'s integrated cloud workload protections allow you to detect and quickly respond to threats across hybrid and multicloud workloads. The **Microsoft Defender for Cloud** connector allows you to ingest [security alerts from Defender for Cloud](/en-us/azure/defender-for-cloud/alerts-reference) into Microsoft Sentinel, so you can view, analyze, and respond to Defender alerts, and the incidents they generate, in a broader organizational threat context.

[Microsoft Defender for Cloud Defender plans](/en-us/azure/defender-for-cloud/defender-for-cloud-introduction#protect-cloud-workloads) are enabled per subscription. While Microsoft Sentinel's legacy connector for Defender for Cloud Apps is also configured per subscription, the **Tenant-based Microsoft Defender for Cloud** connector, in preview, allows you to collect Defender for Cloud alerts over your entire tenant without having to enable each subscription separately. The tenant-based connector also works with [Defender for Cloud's integration with Microsoft Defender XDR](ingest-defender-for-cloud-incidents) to ensure that all of your Defender for Cloud alerts are fully included in any incidents you receive through [Microsoft Defender XDR incident integration](microsoft-365-defender-sentinel-integration).

- **Alert synchronization**:

    - When you connect Microsoft Defender for Cloud to Microsoft Sentinel, the status of security alerts that get ingested into Microsoft Sentinel is synchronized between the two services. So, for example, when an alert is closed in Defender for Cloud, that alert displays as closed in Microsoft Sentinel as well.
    - Changing the status of an alert in Defender for Cloud won't affect the status of any Microsoft Sentinel **incidents** that contain the Microsoft Sentinel alert, only that of the alert itself.
- **Bi-directional alert synchronization**: Enabling **bi-directional sync** automatically syncs the status of original security alerts with that of the Microsoft Sentinel incidents that contain those alerts. So, for example, when a Microsoft Sentinel incident containing a security alerts is closed, the corresponding original alert is closed in Microsoft Defender for Cloud automatically.

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

Note

The connector does not support syncing alerts from subscriptions owned by other tenants, even when Lighthouse is enabled for those tenants.

## Prerequisites

- You must be using Microsoft Sentinel in the Azure portal. When you onboard Microsoft Sentinel to the Defender portal, Defender for Cloud alerts are already ingested into Microsoft Defender XDR, and the **Tenant-based Microsoft Defender for Cloud (Preview)** data connector isn't listed in the **Data connectors** page in the Defender portal. For more information, see [Microsoft Sentinel in the Microsoft Defender portal](microsoft-sentinel-defender-portal).

    If you've onboarded Microsoft Sentinel to the Defender portal, you'll still want to install the **Microsoft Defender for Cloud** solution to use built-in security content with Microsoft Sentinel.

    If you're using Microsoft Sentinel in the Defender portal without Microsoft Defender XDR, this procedure is still relevant for you.
- You must have the following roles and permissions:

    - You must have read and write permissions on your Microsoft Sentinel workspace.
    - You must have the **Contributor** or **Owner** role on the subscription you want to connect to Microsoft Sentinel.
    - To enable bi-directional sync, you must have the **Contributor** or **Security Admin** role on the relevant subscription.
- You'll need to enable at least one plan within Microsoft Defender for Cloud for each subscription where you want to enable the connector. To enable Microsoft Defender plans on a subscription, you must have the **Security Admin** role for that subscription.
- You'll need the `SecurityInsights` resource provider to be registered for each subscription where you want to enable the connector. Review the guidance on the [resource provider registration status](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider) and the ways to register the `SecurityInsights` resource provider.

## Connect to Microsoft Defender for Cloud

To connect Microsoft Defender for Cloud to Microsoft Sentinel and start ingesting security alerts, follow these steps:

1. In Microsoft Sentinel, install the solution for **Microsoft Defender for Cloud** from the **Content Hub**. For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy).
2. Select **Configuration &gt; Data connectors**.
3. From the **Data connectors** page, select either the **Subscription-based Microsoft Defender for Cloud (Legacy)** or the **Tenant-based Microsoft Defender for Cloud (Preview)** connector, and then select **Open connector page**.
4. Under **Configuration**, you'll see a list of the subscriptions in your tenant, and the status of their connection to Microsoft Defender for Cloud. Select the **Status** toggle next to each subscription whose alerts you want to stream into Microsoft Sentinel. If you want to connect several subscriptions at once, mark the check boxes next to the relevant subscriptions and then select the **Connect** button on the bar above the list.

    - The check boxes and **Connect** toggles are active only on the subscriptions for which you have the required permissions.
    - The **Connect** button is active only if at least one subscription's check box has been marked.
5. To enable bi-directional sync on a subscription, locate the subscription in the list, and choose **Enabled** from the drop-down list in the **Bi-directional sync** column. To enable bi-directional sync on several subscriptions at once, mark their check boxes and select the **Enable bi-directional sync** button on the bar above the list.

    - The check boxes and drop-down lists are active only on the subscriptions for which you have the required permissions.
    - The **Enable bi-directional sync** button is active only if at least one subscription's check box has been marked.
6. In the **Microsoft Defender plans** column of the list, you can see if Microsoft Defender plans are enabled on your subscription, which is a connector prerequisite.

    The value for each subscription in this column is either blank, meaning no Defender plans are enabled, **All enabled**, or **Some enabled**. Subscriptions whose value is **Some enabled** also have an **Enable all** link you can select, that takes you to your Microsoft Defender for Cloud configuration dashboard for that subscription, where you can choose Defender plans to enable.

    The **Enable Microsoft Defender for all subscriptions** link button on the bar above the list takes you to your Microsoft Defender for Cloud Getting Started page, where you can choose on which subscriptions to enable Microsoft Defender for Cloud altogether. For example:

    ![Screenshot of Microsoft Defender for Cloud connector configuration.](media/connect-defender-for-cloud/azure-defender-config.png)
7. You can select whether you want the alerts from Microsoft Defender for Cloud to automatically generate incidents in Microsoft Sentinel. Under **Create incidents**, select **Enabled** to turn on the default analytics rule that automatically [creates incidents from alerts](create-incidents-from-alerts). You can then edit this rule under **Analytics**, in the **Active rules** tab.

    Tip

    When configuring [custom analytics rules](detect-threats-custom) for alerts from Microsoft Defender for Cloud, consider the alert severity to avoid opening incidents for informational alerts.

    Informational alerts in Microsoft Defender for Cloud don't represent a security risk on their own, and are relevant only in the context of an existing, open incident. For more information, see [Security alerts and incidents in Microsoft Defender for Cloud](/en-us/azure/security-center/security-center-alerts-overview).

## Find and analyze your data

Security alerts are stored in the *SecurityAlert* table in your Log Analytics workspace. To query Defender for Cloud security alerts in Log Analytics, use the following Kusto query to retrieve alerts where the product name is Azure Security Center:

```kusto
SecurityAlert 
| where ProductName == "Azure Security Center"
```

Alert synchronization *in both directions* can take a few minutes. Changes in the status of alerts might not be displayed immediately.

On the **Microsoft Defender for Cloud** connector page in Microsoft Sentinel, select the **Next steps** tab for sample queries, analytics rule templates, and recommended workbooks.