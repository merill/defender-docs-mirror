---
layout: Conceptual
title: Submit an App Catalog update request - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/submit-app-catalog-update-request
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Learn how app owners and nonapp owners can submit update requests for apps in the Defender for Cloud Apps catalog.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: bcdcb9e8-c933-6622-5259-09c0cd92fbf5
document_version_independent_id: bcdcb9e8-c933-6622-5259-09c0cd92fbf5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/submit-app-catalog-update-request.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: submit-app-catalog-update-request
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/submit-app-catalog-update-request.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: c3c4060e-201b-b9a6-90ec-e60c16dc0683
---

# Submit an App Catalog update request - Microsoft Defender for Cloud Apps | Microsoft Learn

To keep the Microsoft Defender for Cloud Apps (MDA) catalog accurate, use the submission method that fits your role and the type of update you need. App owners can submit updates through a self-attestation questionnaire, while other users can request risk score changes or suggest catalog corrections. This article explains each submission path and what to expect during processing.

## Submit updates as an app owner or verified vendor

If you're a verified app vendor or developer, complete the [Self-Attestation Questionnaire](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR4CRHM-U7CtKpJma_QJAnSlUMEpLQzBaQ1hWNDMxUEhRNFI3Q0FZUkdWRC4u) to:

- Add a new app to the catalog.
- Update risk attributes.

**While we review your request:**

- If the app isn’t in the catalog, you can [add it as a custom app](cloud-discovery-custom-apps) in Cloud Discovery to monitor its usage in your environment.
- If the app is listed but its risk score doesn’t reflect your organization’s security posture, you can manually [override the app’s risk score](risk-score#override-the-risk-score).

## Request updates as a nonowner

Even if you're not the app owner, you can help improve the app catalog's accuracy:

- You can [request a risk score update](risk-score#customize-the-risk-score) for apps in use by your organization.
- You can [suggest a change to the cloud app catalog](risk-score#suggest-a-change-to-the-cloud-app-catalog) if you find a new app in your environment that hasn't been scored by Defender for Cloud Apps, or if you want to request a review for a new risk factor, a score update, or outdated app data.

## Validation and processing timeline

We thoroughly validate all catalog update requests to ensure accuracy and relevance. All app catalog requests must meet these criteria:

- The submitted domain must map to a known application.
- The app must qualify as a SaaS product.
- The request must include complete and verifiable information.

After we validate and accept your request, the standard turnaround time for a catalog update is approximately seven weeks.

## Submit other catalog update requests

For general inquiries, metadata corrections, or requests other than self-attestation submissions or risk score updates, [open a support ticket](/en-us/defender-cloud-apps/support-and-ts).

Note

We review support tickets individually. They aren’t a fast track for catalog updates, but they help us find edge cases or routing issues.