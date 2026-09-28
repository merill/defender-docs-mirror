---
layout: Conceptual
title: Protect your Virtual Machines (VMs) with Microsoft Defender for Servers - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/tutorial-protect-resources
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
description: This tutorial shows you how to configure a just-in-time VM access policy and an application control policy.
ms.topic: tutorial
ms.custom: mvc
ms.date: 2026-04-19T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 41df458a-1471-22b1-a7ef-e363d5d65ad9
document_version_independent_id: c3ebb8a5-f8e4-21c9-0885-08db80e5a02e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/tutorial-protect-resources.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/tutorial-protect-resources
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/tutorial-protect-resources.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
platformId: 094b11fd-dd6c-b064-2b26-83ae2a98bddc
---

# Protect your Virtual Machines (VMs) with Microsoft Defender for Servers - Microsoft Defender for Cloud | Microsoft Learn

Defender for Servers in Microsoft Defender for Cloud, limits your exposure to threats by using access and application controls to block malicious activity. Just-in-time (JIT) virtual machine (VM) access reduces your exposure to attacks by enabling you to deny persistent access to VMs. Instead, you provide controlled and audited access to VMs only when needed. Defender for Cloud uses machine learning to analyze the processes running in the VM and helps you apply allowlist rules using this intelligence.

In this tutorial you'll learn how to:

- Configure a just-in-time VM access policy
- Configure an application control policy

## Prerequisites

To step through the features covered in this tutorial, you must have Defender for Cloud's enhanced security features enabled. A free trial is available. To upgrade, see [Enable enhanced protections](connect-azure-subscription).

## Manage VM access

JIT VM access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks while providing easy access to connect to VMs when needed.

Management ports don't need to be open always. They only need to be open while you're connected to the VM, for example to perform management or maintenance tasks. When just-in-time is enabled, Defender for Cloud uses Network Security Group (NSG) rules, which restrict access to management ports so they can't be targeted by attackers.

Follow the guidance in [Secure your management ports with just-in-time access](just-in-time-access-usage).