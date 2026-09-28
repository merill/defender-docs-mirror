---
layout: Conceptual
title: Microsoft Defender Experts for Servers overview - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-servers-overview
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about Microsoft Defender Experts for Servers, a managed detection and response service for on-premises and multicloud server workloads.
ms.service: defender-experts-for-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-security
- tier1
- essentials-overview
ms.topic: concept-article
ms.custom:
- cx-ti
- cx-dex
- msecd-doc-authoring-1012
search.appverid: met150
ms.date: 2026-05-18T00:00:00.0000000Z
locale: en-us
document_id: f0a8ac5d-8de7-4d1b-6d5e-108c39ffa447
document_version_independent_id: f0a8ac5d-8de7-4d1b-6d5e-108c39ffa447
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-servers-overview.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-servers-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-servers-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: c364e282-8f5b-d3f9-47c1-807a53909960
---

# Microsoft Defender Experts for Servers overview - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/defender-for-cloud-introduction)

Important

Microsoft Defender Experts for Servers is sold separately from other Microsoft Defender products and uses **pay-as-you-go consumption meter**. If you're interested in purchasing Defender Experts for Servers, contact your Microsoft account representative. [Learn more about Microsoft Defender for Cloud pricing](https://azure.microsoft.com/pricing/details/defender-for-cloud/).

Note

Any incident response services offered by Defender Experts ares offered under the Defender Experts Service Terms.

**Microsoft Defender Experts for Servers** is a managed extended detection and response service that provides expert-driven coverage for on-premises and multicloud servers protected by [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/defender-for-cloud-introduction). It combines automation and Microsoft's security analyst expertise to help you detect and respond to threats targeting your server infrastructure across Microsoft Azure, Amazon Web Services (AWS), and Google Cloud Platform (GCP).

Defender Experts for Servers augments your security operation center (SOC) with threat intelligence and dedicated analyst support to help you:

- **Focus on incidents that matter.** Experts prioritize incidents and alerts related to your server workloads, reduce alert fatigue, and drive SOC efficiency for your team.
- **Manage response your way.** Experts provide actionable, step-by-step guidance to respond to incidents, with the option to act on your behalf.
- **Access expertise when you need it.** Extend your team's capacity with access to Defender Experts for assistance on an investigation.
- **Stay ahead of emerging threats.** Experts proactively hunt for emerging threats in your server environment, informed by unparalleled threat intelligence and visibility.

## Prerequisites and licensing

Defender Experts for Servers is a standalone service that you can purchase independently. It doesn't require a [Microsoft Defender Experts MDR](defender-experts-mdr-overview) enrollment. You can purchase and use this service independently.

If your organization also has Defender Experts MDR, the two services complement each other. Defender Experts MDR covers your broader Microsoft Defender environment (endpoints, email, identity, and cloud apps), while Defender Experts for Servers provides dedicated coverage for your server infrastructure protected by Defender for Cloud.

To get started with this Defender Experts for Servers, you need the following items:

- **Defender for Servers Plan 1 or Plan 2** in Microsoft Defender for Cloud must be enabled.
- Microsoft Entra ID P2

Depending on the coverage you're looking for, you can enable the Defender for Servers plan for an Azure subscription, AWS account, or GCP project.

For more information, see [Before you begin using Defender Experts](defender-experts-mdr-prerequisites)

## Service capabilities

Defender Experts for Servers delivers managed security operations for your server workloads through a combination of automation and human expertise. The service includes the following capabilities:

- **Managed detection and response:** Expert analysts manage your server-related incidents in the Microsoft Defender incident queue, handle triage and investigation on your behalf, and partner with your team to take action or guide you through response. For details, see [Managed detection and response](defender-experts-mdr-managed-response).
- **Proactive threat hunting:**[Microsoft Defender Experts Hunting - Servers](defender-experts-hunting-overview) is built in to extend your team's threat hunting capabilities and prioritize significant threats targeting your servers.

    Note

    Defender Experts Hunting - Servers is also available as a standalone service offering. For more information, contact your Microsoft account representative.
- **Ask Defender Experts:** Select [Ask Defender Experts](defender-experts-hunting-ask-experts) in the Microsoft Defender portal to get expert advice about threats your organization is facing.
- **Live dashboards and reports:** Get a transparent view of operations on your behalf and noise-free, actionable insights into what matters for you, coupled with detailed analytics. For details, see [Defender Experts reports](defender-experts-mdr-reports).
- **Third-party network signal enrichment:** Enrich your Defender Experts experience with third-party network signals from Palo Alto Networks, Fortinet, and Zscaler to gain a more comprehensive view of an attack's path. For details, see [Third-party network signal enrichment](defender-experts-mdr-third-party-enrichment).

## Server and cloud workload coverage

Defender Experts for Servers covers **all** servers in your tenant that have [Defender for Servers](/en-us/azure/defender-for-cloud/defender-for-servers-overview) protection enabled in Defender for Cloud. This coverage includes multicloud servers across Azure, AWS, and GCP, provided that Defender for Endpoint is installed on the servers.

All Defender for Servers Plan 1 and Plan 2 alerts are in scope. [DNS alerts](/en-us/azure/defender-for-cloud/alerts-dns) are excluded from coverage due to limited data available for investigation.