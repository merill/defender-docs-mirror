---
layout: Conceptual
title: Unified identity security recommendations (Preview) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/identity-security/identity-security-recommendations
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn which identity sources and applications are covered by security recommendations in Microsoft Defender, including Active Directory, SaaS apps, and non-Microsoft identity providers.
ms.author: abbyweisberg
author: AbbyMSFT
ms.reviewer: maelgami
ms.date: 2026-03-17T00:00:00.0000000Z
ms.topic: concept-article
ms.service: defender-xdr
ms.custom: msecd-doc-authoring-106
ai-usage: ai-assisted
locale: en-us
document_id: 7cca7c27-977a-9c5e-a8b0-708a50f6a71d
document_version_independent_id: 7cca7c27-977a-9c5e-a8b0-708a50f6a71d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/identity-security/identity-security-recommendations.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-security/identity-security-recommendations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/identity-security/identity-security-recommendations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a16cfd5a-0543-ca27-ce4f-a5fa566003de
---

# Unified identity security recommendations (Preview) - Microsoft Defender XDR | Microsoft Learn

Microsoft Defender provides security recommendations that help you identify and fix configuration weaknesses across your identity sources. These recommendations cover Active Directory, SaaS applications, and non-Microsoft identity providers (IdPs), and they appear in [Microsoft Security Exposure Management](/en-us/security-exposure-management/microsoft-security-exposure-management) and [Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score).

Security recommendations come from two capabilities:

- **Identity security posture management (ISPM)**: Provides recommendations for Active Directory and non-Microsoft identity providers. For information about how to view and act on these recommendations, see [Identity security initiative (Preview)](/en-us/defender-for-identity/identity-security-initiative).
- **SaaS security posture management (SSPM)**: Provides recommendations for SaaS application configurations. For information about how SSPM works and how to turn on recommendations, see [SaaS security posture management](/en-us/defender-cloud-apps/posture-overview).

## Supported identity sources

The following sections list the identity sources and applications that currently have security recommendations in Microsoft Defender.

### Active Directory

Microsoft Defender for Identity provides security recommendations for on-premises Active Directory environments. For the full list of recommendations, see [Security posture assessments](/en-us/defender-for-identity/security-assessment).

### SaaS applications

Microsoft Defender for Cloud Apps provides security recommendations for SaaS application configurations through SSPM. For information about connecting apps and turning on recommendations, see [SaaS security posture management](/en-us/defender-cloud-apps/posture-overview).

Security recommendations are available for the following SaaS applications:

- All Microsoft apps
- Atlassian
- Citrix ShareFile
- DocuSign
- Dropbox
- GitHub
- Google Workspace
- NetDocuments
- Salesforce
- ServiceNow
- Workplace by Meta
- Zendesk
- Zoom

### Non-Microsoft identity providers

Security recommendations are available for the following non-Microsoft identity providers:

- Okta
- PingOne
- CyberArk (Preview)
- SailPoint (Preview)