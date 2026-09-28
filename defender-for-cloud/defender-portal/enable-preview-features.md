---
layout: Conceptual
title: Enable preview features in the Defender portal - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-portal/enable-preview-features
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to enable preview features for Microsoft Defender for Cloud in the Defender portal, including prerequisites, steps, and what to expect.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: fbcbbc90-9b56-c286-c30a-6189fc2b3bea
document_version_independent_id: 8b253bb4-95e6-52b0-f403-6a7ac9bea738
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-portal/enable-preview-features.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: ../toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-portal/enable-preview-features
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-portal/enable-preview-features.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 2b3d018d-60ec-38e0-20f1-def4422b0d90
---

# Enable preview features in the Defender portal - Microsoft Defender for Cloud | Microsoft Learn

Defender for Cloud expansion to the Defender portal is in preview phase and aligns to the general preview feature guidelines and support: [Microsoft Defender XDR preview features](/en-us/defender-xdr/preview)

Note

Enabling preview features in Defender portal does not impact Defender for Cloud in the Azure portal, they live side by side.

## Prerequisites

Defender for Cloud with at least one paid plan is eligible to experience the Defender for Cloud preview capabilities in the Defender portal.

Accounts must have one of the following Entra ID roles:

- Global Administrator
- Security Administrator

## How to enable

In the Microsoft Defender portal, navigate to **Settings** &gt; **Microsoft Defender XDR** &gt; **General** &gt; **Preview features**, and select to turn on preview features.

Ensure both "Microsoft Defender XDR" and "Microsoft Defender for Cloud" options are selected.

## What happens after you enable preview features

After you enable preview features, expect the following changes:

- Preview features may take up to 24 hours to turn on.
- Enabling preview features introduces new security recommendations in preview in the Azure portal.
- Once preview features are enabled, find Defender for Cloud in the left menu under **Cloud security**.