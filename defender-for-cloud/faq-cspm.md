---
layout: FAQ
title: Common questions - cloud security posture management (CSPM) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/faq-cspm
summary: >
  <p>One of Microsoft Defender for Cloud's main pillars for cloud security is Cloud Security Posture Management (CSPM). CSPM provides you with hardening guidance that helps you efficiently and effectively improve your security. CSPM also gives you visibility into your current security situation.</p>
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodekek
ms.service: defender-for-cloud
description: Frequently asked questions about cloud security posture management (CSPM) for Microsoft Defender for Cloud.
ms.topic: faq
ms.date: 2025-05-18T00:00:00.0000000Z
locale: en-us
document_id: d0256b73-ed3d-c071-2c29-ebd31c6152da
document_version_independent_id: 553a61a7-2186-c353-b0c5-3f421753574d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/faq-cspm.yml
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: faq
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/faq-cspm
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/faq-cspm.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: baadc530-e236-0f05-7f0a-08ff6be049f6
---

# Common questions - cloud security posture management (CSPM) - Microsoft Defender for Cloud | Microsoft Learn

One of Microsoft Defender for Cloud's main pillars for cloud security is Cloud Security Posture Management (CSPM). CSPM provides you with hardening guidance that helps you efficiently and effectively improve your security. CSPM also gives you visibility into your current security situation.

## If I address only three out of four recommendations in a security control, will my secure score change?

No. It doesn't change until you remediate all of the recommendations for a single resource. To get the maximum score for a control, you must remediate all recommendations for all resources.

## If a security control offers me zero points towards my secure score, should I ignore it?

In some cases, you'll see a control max score greater than zero, but the impact is zero. When the incremental score for fixing resources is negligible, it's rounded to zero. Don't ignore these recommendations because they still bring security improvements. The only exception is the "Additional Best Practice" control. Remediating these recommendations doesn't increase your score, but it enhances your overall security.

## How does scanning affect the instances?

Since the scanning process is an out-of-band analysis of snapshots, it doesn't impact the actual workloads and isn't visible by the guest operating system.

## How does scanning affect the account/subscription?

The scanning process has minimal footprint on your accounts and subscriptions.

| Cloud provider | Changes |
| --- | --- |
| Azure | - Adds a "VM Scanner Operator" role assignment- Adds a "vmScanners" resource with the relevant configurations used to manage the scanning process |
| AWS | - Adds role assignment- Adds authorized audience to OpenIDConnect provider- Snapshots are created next to the scanned volumes, in the same account, during the scan (typically for a few minutes) |
| GCP | - Adds a role assignment |

## What is the Virtual Machine (VM) scan freshness?

Each VM is scanned every 24 hours.

## Can I calculate the secure score at the resource group level?

Secure score is calculated per Azure subscription, AWS account, or GCP project. You can also view the secure score within the management scope such as Azure management group, AWS management account, or GCP organization. There's no secure score per resource group.