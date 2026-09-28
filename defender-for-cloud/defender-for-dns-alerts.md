---
layout: Conceptual
title: Respond to Microsoft Defender for DNS alerts - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-dns-alerts
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
description: Learn best practices for responding to alerts that indicate security risks in DNS services.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 8bdea38b-ebff-071a-c584-2cb6bb6f6b72
document_version_independent_id: 1103af3c-106c-cbcc-519b-c9f041c6400d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-dns-alerts.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-dns-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-dns-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: f475f8e5-4dbe-0643-a053-d3131d174507
---

# Respond to Microsoft Defender for DNS alerts - Microsoft Defender for Cloud | Microsoft Learn

Use this article to investigate suspicious DNS activity, confirm whether it is expected, and mitigate potentially compromised resources.

## Investigate and respond to DNS alerts

Important

- As of August 1, 2023, customers with an existing subscription to Defender for DNS can continue to use the service as a standalone plan.
- For new subscriptions, alerts about suspicious DNS activity are included as part of Defender for Servers Plan 2 (P2).
- There's no change to the protection scope: Defender for DNS continues to protect all Azure resources connected to Azure's default DNS resolvers. The change affects how DNS protection is billed and bundled, not what resources are covered.

When you receive a security alert about suspicious activity in DNS transactions, investigate and respond by using the steps in this article. Even if you're familiar with the application or user that triggered the alert, verify the situation around every alert.

## Contact resource owner

Depending on the alert, the resource owner may be the user, application, or service that triggered the alert. The resource owner is typically the person or team responsible for the resource that generated the alert.

1. Contact the resource owner to determine whether the behavior was expected or intentional.
2. If the activity is expected, dismiss the alert.
3. If the activity is unexpected, treat the resource as potentially compromised and follow the mitigation steps in Mitigate the alert.

## Mitigate the alert

If the resource owner confirms that the activity is unexpected, mitigate the alert as soon as possible to prevent further damage.

1. Isolate the resource from the network to prevent lateral movement (an attacker moving from one compromised system to other systems).
2. Run a full antimalware scan on the resource, following any resulting remediation advice.
3. Review installed and running software on the resource, removing any unknown or unwanted packages.
4. Revert the machine to a known good state, reinstalling the operating system if required, and restore software from a verified malware-free source.
5. Resolve any Microsoft Defender for Cloud recommendations for the machine, remediating highlighted security issues to prevent future breaches.