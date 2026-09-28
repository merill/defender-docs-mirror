---
layout: Conceptual
title: Step 2. Perform a SOC integration readiness assessment using the Zero Trust Framework - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/integrate-microsoft-365-defender-secops-readiness
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: The basics of performing a SOC integration readiness assessment using the Zero Trust Framework when integrating Microsoft Defender XDR into your security operations.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- msftsolution-secops
- tier2
ms.topic: how-to
ms.date: 2026-06-15T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 41ede7e7-57c6-7ca0-172f-805017d2de4c
document_version_independent_id: 41ede7e7-57c6-7ca0-172f-805017d2de4c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/integrate-microsoft-365-defender-secops-readiness.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: integrate-microsoft-365-defender-secops-readiness
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/integrate-microsoft-365-defender-secops-readiness.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: d83dab2d-3da6-ff3f-00e3-d9ed1acd75e6
---

# Step 2. Perform a SOC integration readiness assessment using the Zero Trust Framework - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- Microsoft Defender XDR

To prepare for Microsoft Defender XDR adoption, organizations should assess readiness using a [Zero Trust approach](/en-us/security/zero-trust/). Adoption can help you determine the requirements needed for deploying Microsoft Defender XDR using modern industry-leading practices, while evaluating Microsoft Defender XDR's capabilities against your environment.

The Zero Trust approach is based on a strong foundation of protections and includes key areas such as identity, endpoints (devices), data, apps, infrastructure, and networking. The Readiness Assessment team determines the areas where a foundational requirement for enabling Microsoft Defender XDR hasn't yet been met and what needs remediation.

The following list provides some examples of things that must be remediated in order for the SOC to fully optimize processes in the SOC:

- **Identity:** Legacy on-premises Active Directory Domain Services (AD DS) domains, no MFA plan, no inventory of privileged accounts, and others.
- **Endpoints (devices):** Large number of legacy operating systems, limited device inventory, and others.
- **Data and apps:** Lack of data governance standards, or no inventory of custom apps that won't integrate.
- **Infrastructure:** Large number of unsanctioned SaaS licenses, no container security, and others.
- **Networking:** Performance issues due to low bandwidth, flat network, wireless security issues, and others.

Use the guidance in [turning on Microsoft Defender XDR](m365d-enable) to capture the baseline set of configuration requirements. Capturing the baseline configuration requirements helps determine remediation activities the SOC teams have to carry out to effectively develop use cases.

For next steps, see [Plan for Microsoft Defender XDR integration with your SOC catalog of services](integrate-microsoft-365-defender-secops-services) and [Use Microsoft Defender XDR incident response in your SOC](integrate-microsoft-365-defender-secops-use-cases).