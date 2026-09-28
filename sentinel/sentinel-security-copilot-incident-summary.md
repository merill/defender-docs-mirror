---
layout: Conceptual
title: Summarize Microsoft Sentinel incidents with Security Copilot | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sentinel-security-copilot-incident-summary
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
description: Learn about Microsoft Sentinel's incident summarization capabilities in Security Copilot.
ms.collection: usx-security
ms.pagetype: security
ms.author: guywild
author: guywi-ms
ms.reviewer: idpelleg
ms.localizationpriority: medium
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 9c2c9efb-2e83-2bfc-2fad-4dfd82a8bc49
document_version_independent_id: 230ae326-f0ad-cfde-63dc-275784ceb0fe
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sentinel-security-copilot-incident-summary.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/sentinel-security-copilot-incident-summary
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sentinel-security-copilot-incident-summary.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 219c6333-d338-ca1a-dbee-ac7b15b0711a
---

# Summarize Microsoft Sentinel incidents with Security Copilot | Microsoft Learn

Microsoft Sentinel applies the capabilities of [Security Copilot](/en-us/security-copilot/microsoft-security-copilot) in the Azure portal to create enriched summaries of incidents, providing a comprehensive overview of security incidents by consolidating information from multiple alerts. The Copilot incident summary feature enhances incident response efficiency by offering a clear summary that helps your security operations teams quickly understand the scope and impact of an incident. The incident summary provides a structured overview, including timelines, assets involved, and indicators of compromise, along with enrichments like user risk, device risk, and watchlist matching. These incident summaries suggest an investigation path for your analysts to assess the scope and impact of an attack. For more information, see [Navigate, triage, and manage Microsoft Sentinel incidents in the Azure portal](incident-navigate-triage).

If you onboarded Microsoft Sentinel to the Defender portal, you can move directly to the same incident in the Defender portal and follow the guided investigation procedures in the Defender portal. For more information, see [Triage and investigate incidents with guided responses from Security Copilot in Microsoft Defender](/en-us/defender-xdr/security-copilot-m365d-guided-response).

This guide outlines what to expect and how to access the summarizing capability of Copilot in Microsoft Sentinel, including information on providing feedback.

Important

The Copilot incident summary feature for Microsoft Sentinel is currently in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Prerequisites

If you're new to Security Copilot, you should familiarize yourself with it by reading these articles:

- [What is Microsoft Security Copilot?](/en-us/security-copilot/microsoft-security-copilot)
- [Microsoft Security Copilot experiences](/en-us/security-copilot/experiences-security-copilot)
- [Get started with Microsoft Security Copilot](/en-us/security-copilot/get-started-security-copilot)
- [Understand authentication in Microsoft Security Copilot](/en-us/security-copilot/authentication)
- [Prompting in Microsoft Security Copilot](/en-us/security-copilot/prompting-security-copilot)

## Security Copilot integration with Microsoft Sentinel

The incident summary capability is available in Microsoft Sentinel in the Azure portal for customers who have provisioned access to Security Copilot.

The incident summary capability is also available in the Defender portal, and in the Security Copilot standalone experience through the Microsoft Sentinel plugins. Know more about [preinstalled plugins in Security Copilot](/en-us/security-copilot/manage-plugins#preinstalled-plugins).

## Key features of incident summarization

Incidents containing up to 100 alerts can be summarized into one incident summary. An incident summary, depending on the availability of the data, includes the following:

- The time and date when an attack started.
- The entity or asset where the attack started.
- A summary of timelines of how the attack unfolded.
- The assets involved in the attack.
- Indicators of compromise (IoCs).
- Names of [threat actors](/en-us/defender-xdr/microsoft-threat-actor-naming) involved.
- User risk and criticality.
- Device risk and criticality.
- Watchlist matches.

Copilot automatically generates an incident summary when you open the incident's page. The incident summary appears at the top of the details pane of the incident page, before the description.

[![Screenshot that shows the Copilot-generated incident summary on the details pane of the Microsoft Sentinel incident page.](media/sentinel-security-copilot-incident-summary/copilot-sentinel-incident-summary.png)](media/sentinel-security-copilot-incident-summary/copilot-sentinel-incident-summary.png#lightbox)

Select **Show more** to expand the summary to see its complete content.

![Screenshot that shows the expanded incident summary.](media/sentinel-security-copilot-incident-summary/copilot-sentinel-incident-summary-expanded.png)

Tip

You can navigate to a file, IP, or URL page from the Copilot results pane by clicking on the evidence in the results.

Review the summary and use the information to guide your investigation and response to the incident.