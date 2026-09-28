---
layout: Conceptual
title: Integrate your SIEM tools with Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/configure-siem-defender
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Integrate supported SIEM tools with Microsoft Defender XDR by using REST APIs and connectors to pull incidents and stream event data.
ms.service: defender-xdr
ms.author: edbaynash
author: EdB-MSFT
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: ef872857-0ad6-6670-ec60-239438313309
document_version_independent_id: ef872857-0ad6-6670-ec60-239438313309
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/configure-siem-defender.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-siem-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/configure-siem-defender.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 3226388a-e1a3-56da-1486-b742663c815c
---

# Integrate your SIEM tools with Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

This article describes how to integrate supported security information and event management (SIEM) tools with Microsoft Defender XDR. You can pull incidents through the REST API or stream event data through Azure Event Hubs to platforms such as Splunk, ArcSight, Elastic, and IBM QRadar.

## Use SIEM tools to pull Microsoft Defender incidents and streaming event data

Note

- [Microsoft Defender Incidents](incident-queue) consists of collections of correlated alerts and their evidence.
- [Microsoft Defender Streaming API](streaming-api) streams event data from Microsoft Defender to event hubs or Azure storage accounts.

Microsoft Defender supports security information and event management (SIEM) tools ingesting information from your enterprise tenant in Microsoft Entra ID using the OAuth 2.0 authentication protocol for a registered Microsoft Entra application representing the specific SIEM solution or connector installed in your environment.

For more information, see:

- [Microsoft Defender APIs license and terms of use](/en-us/legal/microsoft-365/api-terms)
- [Access the Microsoft Defender APIs](api-access)
- [Hello World example](api-hello-world)
- [Get access with application context](api-create-app-web)

There are two primary models to ingest security information:

1. Ingesting Microsoft Defender XDR incidents and their contained alerts from a REST API in Azure.
2. Ingesting streaming event data either through Azure Event Hubs or Azure Storage Accounts.

Microsoft Defender currently supports the following SIEM solution integrations:

- Ingesting incidents from the incidents REST API
- Ingesting streaming event data via Event Hubs

## Ingesting incidents from the incidents REST API

The following SIEM solutions support ingesting Microsoft Defender XDR incidents and their contained alerts from the incidents REST API.

### Incident schema

For more information on Microsoft Defender incident properties including contained alert and evidence entities metadata, see [Schema mapping](api-list-incidents#schema-mapping).

### Ingest incidents into Splunk

Using the new, fully supported Splunk Add-on for Microsoft Security that supports:

- Ingesting incidents that contain alerts from the following products, which are mapped onto Splunk's Common Information Model (CIM), a standard schema for normalizing event data:

    - Microsoft Defender
    - Microsoft Defender for Endpoint
    - Microsoft Defender for Identity and Microsoft Entra ID Protection
    - Microsoft Defender for Cloud Apps
- Ingesting Defender for Endpoint alerts (from the Defender for Endpoint's Azure endpoint) and updating these alerts
- Support for updating Microsoft Defender Incidents and/or Microsoft Defender for Endpoint Alerts and the respective dashboards has moved to the Microsoft 365 App for Splunk.

For more information on:

- The Splunk Add-on for Microsoft Security, see the [Microsoft Security Add-on on Splunkbase](https://splunkbase.splunk.com/app/6207/#/overview)
- The Microsoft 365 App for Splunk, see the [Microsoft 365 App on Splunkbase](https://splunkbase.splunk.com/app/3786/)

### Ingest incidents into Micro Focus ArcSight

The new SmartConnector for Microsoft Defender XDR ingests incidents into ArcSight and maps the incident data onto its Common Event Framework (CEF).

For more information on the new ArcSight SmartConnector for Microsoft Defender XDR, see [ArcSight Product Documentation](https://www.microfocus.com/documentation/arcsight/arcsight-smartconnectors-8.4/microsoft-365-defender/index.html).

The SmartConnector replaces the previous FlexConnector for Microsoft Defender for Endpoint, which is now retired.

### Ingest incidents into Elastic

Elastic Security combines SIEM threat detection features with endpoint prevention and response capabilities in one solution.

The Elastic integration for Microsoft Defender XDR and Defender for Endpoint enables organizations to leverage incidents and alerts from Defender within Elastic Security to perform investigations and incident response. Elastic correlates this data with other data sources, including cloud, network, and endpoint sources using robust detection rules to find threats quickly.

For more information on the Elastic connector, see: [Microsoft M365 Defender | Elastic docs](https://docs.elastic.co/integrations/m365_defender)

## Ingesting streaming event data via Event Hubs

For streaming event data integrations, you must first stream events from your Microsoft Entra tenant to your Event Hubs or Azure Storage Account. For more information, see [Microsoft Defender XDR Streaming API](streaming-api).

For more information on the event types supported by the Streaming API, see [Microsoft Defender XDR supported streaming event types](supported-event-types).

### Stream event data to Splunk

Use the Splunk Add-on for Microsoft Cloud Services to ingest events from Azure Event Hubs.

For more information on the Splunk Add-on for Microsoft Cloud Services, see the [Microsoft Cloud Services Add-on on Splunkbase](https://splunkbase.splunk.com/app/3110/).

### Stream event data to IBM QRadar

Use the new IBM QRadar Microsoft Defender XDR Device Support Module (DSM) that calls the [Microsoft Defender Streaming API](streaming-api) that allows ingesting streaming event data from Microsoft Defender products via Event Hubs or Azure Storage Account. For more information on supported event types, see [Supported event types](supported-event-types).

### Stream event data to Elastic

For more information on the Elastic streaming API integration, see [Microsoft M365 Defender | Elastic docs](https://docs.elastic.co/integrations/m365_defender).