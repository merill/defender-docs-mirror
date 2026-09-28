---
layout: Conceptual
title: Microsoft Sentinel Solution for MS Business Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/business-applications/solution-overview
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
description: Learn about the Microsoft Sentinel solution for MS Business Apps, including Microsoft Power Platform, Microsoft Dynamics 365 Customer Engagement, and Microsoft Dynamics 365 Finance and Operations.
ms.author: monaberdugo
author: mberdugo
ms.topic: overview
ms.date: 2024-11-13T00:00:00.0000000Z
locale: en-us
document_id: 43ea359b-e965-719e-4e92-6e0171ed9c2f
document_version_independent_id: 865c4970-1e85-cad2-320b-bdbef4ee49be
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/business-applications/solution-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/business-applications/solution-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/business-applications/solution-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e6f942e8-55a7-4c86-b8e3-7456508ea850
- https://authoring-docs-microsoft.poolparty.biz/devrel/410e33a0-5420-48ba-a8e2-7fb3dc6a9163
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f1834696-48d6-470d-966b-6ee418881596
- https://authoring-docs-microsoft.poolparty.biz/devrel/437f62ae-23a5-4ffc-9ff2-ac42acc41d76
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: ccfdcb6b-6c59-17d7-53a7-2b15ce8d36b1
---

# Microsoft Sentinel Solution for MS Business Apps | Microsoft Learn

The Microsoft Sentinel solution for Microsoft Business Apps helps you monitor and protect your Microsoft Power Platform, Microsoft Dynamics 365 Customer Engagement, and Microsoft Dynamics 365 Finance and Operations. environments. It provides security insights and threat detection by collecting audit and activity logs to detect threats, suspicious activities, illegitimate activities, and more.

- [Microsoft Power Platform](/en-us/power-platform/) is a suite of applications, connectors, and a data platform (Dataverse) that provides a rapid application development environment to build custom apps for your business needs. Power Platform enables users to analyze data, build solutions, automate processes, and create virtual agents.
- [Microsoft Dynamics 365 Customer Engagement](/en-us/dynamics365/customerengagement/) is a cloud-based suite of customer relationship management (CRM) applications designed to streamline and automate business processes across sales, customer service, field service, project service automation, and marketing
- [Microsoft Dynamics 365 for Finance and Operations](/en-us/dynamics365/finance) is a comprehensive Enterprise Resource Planning (ERP) solution that combines financial and operational capabilities to help businesses manage their day-to-day operations. It offers a range of features that enable businesses to streamline workflows, automate tasks, and gain insights into operational performance.

## Securing Power Platform and Microsoft Dynamics 365 Customer Engagement activities

The Microsoft Sentinel solution for Microsoft Business Apps helps you secure your Power Platform by allowing you to:

- Monitor and detect suspicious or malicious activities in your Power Platform environment
- Monitor and secure your Dynamics 365 Customer Engagement environment, which uses the Microsoft Dataverse common data store known as .

The solution collects activity logs from different Power Platform components and inventory data, and analyzes those activity logs to detect threats and suspicious activities, such as:

- Power Apps execution from unauthorized geographies
- Suspicious data destruction by Power Apps
- Mass deletion of Power Apps
- Phishing attacks made possible through Power Apps
- Power Automate flows activity by departing employees
- Suspicious and anomalous activities in Microsoft Dataverse

## Securing Dynamics 365 for Finance and Operations activities

Finance and operations applications enable important business processes like finance, procurement, operations, and supply chain. They store and process sensitive business data, like payments, orders, account receivables, and suppliers, and might be administered by nonsecurity savvy administrators and used by both internal and external users.

The Microsoft Sentinel solution for Microsoft Business apps helps you secure your Dynamics 365 Finance and Operations environment by providing:

- **Visibility to user activities**, like user logins and sign-ins, Create, Read, Update, Delete (CRUD) activities, configurations changes, or activities by external applications and APIs.
- **The ability to detect suspicious or illegitimate activities**, like suspicious logins, illegitimate changes of settings and user permissions, data exfiltration, or bypassing of SOD policies.
- **The ability to investigate and respond to related incidents**, like limiting user access, notifying business admins, or rolling back changes.

## Data connectors

The Microsoft Sentinel solution for Microsoft Business Apps includes the following data connectors:

| Connector name | Data collected | Log Analytics tables |
| --- | --- | --- |
| Microsoft Power Platform Admin Activity | Power Platform administrator activity logs includes the following workloads: - Power Apps- Power Pages- Power Platform Connectors- Power Platform DLPFor more information, see [View Power Platform administrative logs using auditing solutions in Microsoft Purview (preview)](/en-us/power-platform/admin/admin-activity-logging). | PowerPlatformAdminActivity |
| Microsoft Dataverse | Dataverse and model-driven apps activity logging (including Dynamics 365 Customer Engagement) For more information, see [Microsoft Dataverse and model-driven apps activity logging](/en-us/power-platform/admin/enable-use-comprehensive-auditing).If you use the data connector for Dynamics 365, migrate to the data connector for Microsoft Dataverse. This data connector replaces the legacy data connector for Dynamics 365 and supports data collection rules. | DataverseActivity |
| Dynamics 365 F&O | Dynamics 365 Finance and Operations admin activities and audit logsBusiness process and application activity logs | FinanceOperationsActivity\_CL |

## Analytics rules

The Microsoft Sentinel solution for Microsoft Business Apps includes the analytics rules to help you detect threats and suspicious activities in your Power Platform and Dynamics 365 Finance and Operations environments. The rules are based on best practices and industry standards, and are designed to help you identify and respond to security incidents.

- **Analytics rules for Power Platform and Microsoft Dynamics 365 Customer Engagement** cover activities like Power Apps being run from unauthorized geographies, suspicious data destruction by Power Apps, mass deletion of Power Apps, and more.
- **Analytics rules for Dynamics 365 Finance and Operations** cover suspicious activities like changes in bank account details, multiple user account updates or deletions, suspicious sign-in events, changes to workload identities, and more.

## Hunting queries

The Microsoft Sentinel solution for Microsoft Business Apps includes Hunting Queries, enabling the SOC to proactively uncover potential threats and suspicious activities by applying advanced hunting techniques to analyze available data.

## Playbooks

The Microsoft Sentinel solution for Microsoft Business Apps includes Playbooks, which are integral to Sentinel's SOAR capabilities. These playbooks enable automated security responses for Dynamics and Power Platform, streamlining workflows and improving collaboration between SOC analysts and Business Applications experts.

## Workbooks

The Microsoft Sentinel solution for Microsoft Business Apps includes workbooks designed to present security data visually, making it easier to detect anomalies and uncover patterns through interactive visualizations.

## Parsers

The Microsoft Sentinel solution for Microsoft Business Apps includes parsers that that are used to access data from the raw data tables from Power Platform. Parsers ensure that the correct data is returned with a consistent schema. When available, we recommend that you use the parsers instead of directly querying the inventory tables and watchlists.