---
layout: Conceptual
title: Unified Connectors Platform for Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/unified-connector
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
description: Learn about the Unified Connectors Platform that simplifies connector management across Microsoft security products including Microsoft Sentinel, Defender for Cloud, and Defender for Identity.
ms.author: monaberdugo
author: mberdugo
contributors: 
ms.topic: concept-article
ms.date: 2025-08-10T00:00:00.0000000Z
ms.custom: references_regions
locale: en-us
document_id: a48f4935-c23a-3427-446d-6a06b31c0d2e
document_version_independent_id: 7d0bead9-5ab8-1654-28af-f99c487fef71
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/unified-connector.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/unified-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/unified-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: ec7d5d03-84d0-2495-f9eb-2895b74a6506
---

# Unified Connectors Platform for Microsoft Sentinel | Microsoft Learn

The Unified connectors platform enables you to connect once to an external product that provides value in multiple Microsoft security products. This platform simplifies the connector management experience across Microsoft security products.

Unified connectors provide the following benefits:

- Connect and collect the data once for use with multiple Microsoft security products
- Centralized Management
- Enhanced Security: Credentials stored once
- Cost Reduction: Reduced API calls and data duplication

## Unified services

The unified connectors platform provides unified services shared by all security products to allow consistent development and user experience. These services include:

### Unified collector service

Multiple Microsoft Security products often collect the same data from the same external source for different scenarios. For example, Okta Single Sign On system logs are collected every five minutes both by Microsoft Sentinel and Defender for Identity users. This duplication and inefficiency can cause customers to exceed their API rate limit due to the quotas imposed by Okta.

The unified collector is applied to two or more Microsoft Security products connecting to the same external source and having similar data collection needs. It collects the data once for all products as shown in the following diagram:

![Diagram showing Okta data flowing into the unified collector and from there to Microsoft Sentinel, MDI, and Microsoft security exposure management.](media/unified-connector/unified-connector-structure.png)

### Consistent single management across all security products

Users can manage all their connectors in one place through the Unified Security Experience (USX) portal.

### One time authentication

When configuring a unified connector, you enter your credentials for the external product only once. Your credentials are stored and managed in a unified credentials service serving all applicable connections to this product. This enhances security of credentials management along with usability.

### Unified health service

All health issues are stored to a shared health table that is accessible to all users through [Advanced Hunting](/en-us/defender-xdr/advanced-hunting-microsoft-defender).

[![Screenshot of Okta connector with health information on the right side.](media/unified-connector/unified-health.png)](media/unified-connector/unified-health-focus.png#lightbox)

### Integration with Microsoft data lake

The platform allows integration with data lake, including enabling data federation.

### Lifecycle management

Unified connectors are preinstalled with the latest version where possible, minimizing the need for manual updates.

## Supported products

The Unified Connectors Platform currently supports connectors serving the following Microsoft security products:

- Microsoft Sentinel
- Microsoft Defender for Identity

Currently, Defender for Cloud Apps and Microsoft Security Exposure Management aren't supported and these customers should continue using their current connectors.

## Supported connectors

Currently, the Unified Connectors Platform is available in preview for Okta single sign-on connectors shared by [Microsoft Sentinel](unified-connector-integration) and [Microsoft Defender for Identity](/en-us/defender-for-identity/okta-integration).

## Data connectors gallery

The available unified connectors are shown in the [Data connectors Gallery](https://security.microsoft.com/sentinel/unified-connector)**Catalog** tab.

![Screenshot of catalog tab in connectors gallery.](media/unified-connector/connectors-gallery.png)

You can see all the available unified connectors in this tab. There are also links to other product specific connectors galleries. The connectors column of the table shows you how many connector instances this connector currently has. The table also shows who supports the connector and who the provider is.

The **My Connectors** tab shows the connectors that are currently configured. The **Unified connectors** tab shows the unified connectors that are available to you, while the Microsoft Sentinel tab shows connectors that are available only to Sentinel as they appear in the content hub.

![Screenshot of my connectors tab in connectors gallery.](media/unified-connector/connector-info.png)

Under the Unified connectors tab, you can select a connector to see and manage its health information.

Connector health information available in the **My Connectors** tab includes:

- **Name**: The name of the connector.
- **Status**: The status of the connector, such as *OK*, *Warning*, or *Error*.
- **Audit details**: Created and updated information.
- **Workspace**: The workspace to which the connector is connected.
- **Table**: The table that is used by the connector.
- **Last health messages**: The latest error messages.

The Sentinel tab shows the connectors that are available only to Sentinel as the appear in the content hub.

## Considerations and limitations

- Billing for Connectors data is managed separately for each individual Microsoft security product, in accordance with its use cases and benefits.
- The unified connectors feature isn't supported for tenants in the United Arab Emirates region.
- Unified connectors are the preferred way to create a connection. If you already have an Okta connector, you can disconnect it and install a unified connector so that you only collect the system logs once. We don't recommend having both a unified connector and a product specific connector for the same data source.
- Currently, for Sentinel, unified connectors aren't part of solutions and can't be discovered through content hub.
- Currently the unified connectors platform doesn't allow self-service development for third parties.