---
layout: FAQ
title: Common questions - permissions - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/faq-permissions
summary: ''
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
description: This FAQ answers questions about permissions in Microsoft Defender for Cloud, a product that helps you prevent, detect, and respond to threats.
services: defender-for-cloud
ms.topic: faq
ms.date: 2025-05-18T00:00:00.0000000Z
locale: en-us
document_id: 20f1e25e-c7e8-c92d-991e-2b424527e680
document_version_independent_id: d9cf5dd6-94d0-d87e-9d1a-a6b48b5d5058
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/faq-permissions.yml
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: faq
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/faq-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/faq-permissions.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 8a3d4b10-76e4-b277-9a80-e4f19cd5eb67
---

# Common questions - permissions - Microsoft Defender for Cloud | Microsoft Learn

## How do permissions work in Microsoft Defender for Cloud?

Microsoft Defender for Cloud uses [Azure role-based access control (Azure RBAC)](/en-us/azure/role-based-access-control/role-assignments-portal), which provides [built-in roles](/en-us/azure/role-based-access-control/built-in-roles) that can be assigned to users, groups, and services in Azure.

Defender for Cloud assesses the configuration of your resources to identify security issues and vulnerabilities. In Defender for Cloud, you only see information related to a resource when you're assigned the role of Owner, Contributor, or Reader for the subscription or resource group that a resource belongs to.

See [Permissions in Microsoft Defender for Cloud](permissions) to learn more about roles and allowed actions in Defender for Cloud.

## Who can modify a security policy?

To modify a security policy, you must be a Security Admin or an Owner or Contributor of that subscription.

To learn how to configure a security policy, see [Setting security policies in Microsoft Defender for Cloud](tutorial-security-policy).

## What is the minimum SAS policy permissions required when exporting data to Azure Event Hubs?

**Send** is the minimum SAS policy permissions required. For step-by-step instructions, see **Step 1: Create an Event Hubs namespace and event hub with send permissions** in [this article](export-to-splunk-or-qradar#step-1-create-an-event-hubs-namespace-and-event-hub-with-send-permissions).