---
layout: Conceptual
title: Microsoft Defender for DNS - the benefits and features - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-dns-introduction
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
description: Learn about the benefits and features of Microsoft Defender for DNS.
ms.date: 2025-08-20T00:00:00.0000000Z
ms.topic: overview
ai-usage: ai-assisted
locale: en-us
document_id: 2b341237-00b2-c2ba-b4b5-849c3279121d
document_version_independent_id: dd704c7d-6d65-3e96-8c0b-a30ecfb2cae8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-dns-introduction.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-dns-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-dns-introduction.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: fa0f5bdb-5000-386e-8f80-c123c199032f
---

# Microsoft Defender for DNS - the benefits and features - Microsoft Defender for Cloud | Microsoft Learn

Important

- As of August 1, 2023, customers with an existing subscription to Defender for DNS can continue to use the service as a standalone plan.
- For new subscriptions, alerts about suspicious DNS activity are included as part of Defender for Servers Plan 2 (P2).
- There's no change to the protection scope: Defender for DNS continues to protect all Azure resources connected to Azure's default DNS resolvers. The change affects how DNS protection is billed and bundled, not what resources are covered.

Microsoft Defender for DNS provides an additional layer of protection for all Azure resources that use Azure DNS's Azure-provided name resolution capability.

From within Azure DNS, Defender for DNS monitors the queries from these resources and detects suspicious activities without the need for any extra agents.

## Support

**Microsoft Defender for DNS** is billed as shown on the [pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

Review Defender for DNS [cloud availability](support-matrix-defender-for-cloud).

## What are the benefits of Microsoft Defender for DNS?

Microsoft Defender for DNS detects suspicious and anomalous activities such as:

- **Data exfiltration** from your Azure resources using DNS tunneling
- **Malware** communicating with command and control servers
- **DNS attacks** - communication with malicious DNS resolvers
- **Communication with domains used for malicious activities** such as phishing and crypto mining

A full list of the alerts provided by Microsoft Defender for DNS is on the [alerts reference page](alerts-dns).

## Dependencies

Microsoft Defender for DNS doesn't use any agents.