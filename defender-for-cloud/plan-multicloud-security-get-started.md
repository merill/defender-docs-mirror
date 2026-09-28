---
layout: Conceptual
title: Start to Plan Multicloud Protection in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-multicloud-security-get-started
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
description: Learn about designing a solution for securing and protecting your multicloud environment with Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 1925c8ac-44cd-9c89-46f8-2c9766e4b6dc
document_version_independent_id: 0734c260-c640-1a52-6b6a-75f699adfaf8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-multicloud-security-get-started.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-multicloud-security-get-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-multicloud-security-get-started.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 2551047d-ee5f-f5ab-fcd1-2e3a7f2733a1
---

# Start to Plan Multicloud Protection in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

This article provides guidance to design a solution to secure and protect a multicloud environment with Microsoft Defender for Cloud. Cloud solution and infrastructure architects, security architects and analysts, and others can use this guidance in designing a multicloud security solution.

As you capture your functional and technical requirements, the articles in this guide provide an overview of multicloud capabilities, planning guidance, and prerequisites.

Follow the multicloud security planning guides in order. The articles build on each other to help you make design decisions.

## What should I get from this guide?

Use this guide as you design Cloud Security Posture Management (CSPM) solutions to identify and remediate security misconfigurations. Design Cloud Workload Protection Platform (CWPP) solutions for protecting workloads such as servers, databases, and containers, for multicloud environments. After you read the articles in this guide, you should have answers to the following questions:

- What questions should I ask and answer as I design my multicloud solution?
- What steps do I need to complete to design a solution?
- What technologies and capabilities are available to me?
- What trade-offs do I need to consider?

## Multicloud protection challenges

When organizations span multiple cloud providers, it becomes increasingly complex to centralize security and for security teams to work in multiple environments with multiple vendors.

Defender for Cloud helps you to protect your multicloud environment by strengthening your security posture and protecting your workloads. Defender for Cloud provides a single dashboard to manage protection for all environments.

[![Diagram that shows multicloud protection with Defender for Cloud.](media/planning-multicloud-security/get-started.png)](media/planning-multicloud-security/get-started.png#lightbox)

## Before you begin

Before working through these articles, you should have a basic understanding of Azure, Defender for Cloud, Azure Arc, and your multicloud AWS/GCP environment.