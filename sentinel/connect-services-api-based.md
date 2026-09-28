---
layout: Conceptual
title: Connect Microsoft Sentinel to other Microsoft services with an API-based data connector | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-services-api-based
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
description: Learn the common setup concepts, connection methods, and requirements for API-based Microsoft service data connectors in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: ofshezaf
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 0f5f49e9-7a07-0cc9-23a4-1e37915804d3
document_version_independent_id: 567d1972-d7cd-bacf-1fd1-5a307bd5d364
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-services-api-based.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-services-api-based
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-services-api-based.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 2b389380-def9-a982-0b84-83b3ddd18eea
---

# Connect Microsoft Sentinel to other Microsoft services with an API-based data connector | Microsoft Learn

This article describes how to make API-based connections to Microsoft Sentinel. Microsoft Sentinel uses the Azure foundation to provide built-in, service-to-service support for data ingestion from many Azure and Microsoft 365 services, Amazon Web Services, and various Windows Server services. There are a few different methods through which API-based connections to Microsoft Sentinel are made.

The following requirements and steps apply to Microsoft Sentinel API-based data connectors.

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

## Prerequisites

Before you connect a service, make sure you meet the following prerequisites:

- You must have read and write permissions on the Log Analytics workspace.
- You must have a Security administrator role on your Microsoft Sentinel workspace's tenant, or the equivalent permissions.
- Data connector specific requirements:

    | Data connector | Licensing, costs, and other prerequisites |
    | --- | --- |
    | Microsoft Entra ID Protection | - [Microsoft Entra ID P2 subscription](https://azure.microsoft.com/pricing/details/active-directory/) - Other charges may apply |
    | Dynamics 365 | - [Microsoft Dynamics 365 production license](/en-us/office365/servicedescriptions/microsoft-dynamics-365-online-service-description). Not available for sandbox environments.- At least one user assigned a Microsoft/Office 365 [E1 or greater](/en-us/power-platform/admin/enable-use-comprehensive-auditing#requirements) license. - Audit logging enabled in [Microsoft Purview](/en-us/purview/purview). See [Turn auditing on or off](/en-us/purview/audit-log-enable-disable). - Audit logging enabled in your Microsoft Dataverse environment. See [Microsoft Dataverse and model-driven apps activity logging](/en-us/power-platform/admin/enable-use-comprehensive-auditing). - Other charges may apply. |
    | Microsoft Defender for Cloud Apps | For Cloud Discovery logs, [enable Microsoft Sentinel as your SIEM in Microsoft Defender for Cloud Apps](/en-us/cloud-app-security/siem-sentinel) |
    | Microsoft Defender for Endpoint | Valid license for [Microsoft Defender for Endpoint deployment](/en-us/microsoft-365/security/defender-endpoint/production-deployment) |
    | Microsoft Defender for Office 365 | Valid license for [Office 365 ATP Plan 2](/en-us/microsoft-365/security/office-365-security/office-365-atp#office-365-atp-plan-1-and-plan-2) |
    | Microsoft 365 | - Your Microsoft 365 deployment must be on the same tenant as your Microsoft Sentinel workspace.- Other charges may apply. |
    | Microsoft Power BI | - Your Office 365 deployment must be on the same tenant as your Microsoft Sentinel workspace.- Other charges may apply. |
    | Microsoft Purview Information Protection | - Your Office 365 deployment must be on the same tenant as your Microsoft Sentinel workspace.- Other charges may apply. |
    | Microsoft Purview Insider Risk Management (IRM) | - Valid subscription for Microsoft 365 E5/A5/G5, or their accompanying Compliance or IRM add-ons.- [Microsoft Purview Insider Risk Management](/en-us/microsoft-365/compliance/insider-risk-management) fully onboarded, and [IRM policies](/en-us/microsoft-365/compliance/insider-risk-management-policies) defined and producing alerts.- [Insider Risk Management settings for exporting alerts](/en-us/microsoft-365/compliance/insider-risk-management-settings#export-alerts-preview) configured to enable the export of IRM alerts to the Office 365 Management Activity API in order to receive the alerts through the Microsoft Sentinel connector. |

## Connect to Microsoft services via API-based connectors

To connect a Microsoft service by using an API-based connector, complete the following steps:

1. From the Microsoft Sentinel navigation menu, select **Data connectors**.
2. Select your service from the data connectors gallery, and then select **Open Connector Page** on the preview pane.
3. Select **Connect** to start streaming events and/or alerts from your service into Microsoft Sentinel.
4. If on the connector page there is a section titled **Create incidents - recommended!**, select **Enable** if you want to automatically create incidents from alerts.

You can find and query the data for each service using the table names listed under each connector's section on the [Data connectors reference](data-connectors-reference) page. For example, Microsoft Entra ID Protection data appears in the [Microsoft Entra ID Protection connector](data-connectors-reference#microsoft-entra-id-protection) section of that reference.