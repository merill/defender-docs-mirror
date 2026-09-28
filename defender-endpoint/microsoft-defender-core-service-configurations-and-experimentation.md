---
layout: Conceptual
title: Microsoft Defender Core service configurations and experimentation - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-core-service-configurations-and-experimentation
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Understand the interaction between Microsoft Defender Core Service and the Experimentation and Configuration Service (ECS).
ms.service: defender-endpoint
author: paulinbar
ms.author: painbar
ms.reviewer: yongrhee
ms.localizationpriority: medium
ms.date: 2024-07-19T00:00:00.0000000Z
ms.topic: troubleshooting
ms.subservice: ngp
ms.collection:
- m365-security
- tier3
- mde-ngp
locale: en-us
document_id: e980034a-4a96-6a2e-2f67-6e342c8fb1d5
document_version_independent_id: e980034a-4a96-6a2e-2f67-6e342c8fb1d5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-defender-core-service-configurations-and-experimentation.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-core-service-configurations-and-experimentation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-defender-core-service-configurations-and-experimentation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 839b16ec-6185-2821-cb2f-d4c5328ae7e7
---

# Microsoft Defender Core service configurations and experimentation - Microsoft Defender for Endpoint | Microsoft Learn

This article describes the interaction between Microsoft Defender Core Service and the Experimentation and Configuration Service (ECS). Microsoft Defender Core Service is a part of Microsoft Defender Antivirus and communicates with ECS to request and receive different kinds of payloads. These payloads include configurations, feature rollouts, and experiments.

Caution

If you disable communications with the service, this will affect Microsoft's ability to respond to a severe bug in a timely manner.

Important

Make sure clients can access the following URLs so payloads can be received:

Enterprise customers should allow the following URLs:

- `*.events.data.microsoft.com`
- `*.endpoint.security.microsoft.com`
- `*.ecs.office.com`

Enterprise U.S. Government customers should allow the following URLs:

- `*.events.data.microsoft.com`
- `*.endpoint.security.microsoft.us (GCC-H & DoD)`
- `*.gccmod.ecs.office.com (GCC-M)`
- `*.config.ecs.gov.teams.microsoft.us (GCC-H)`
- `*.config.ecs.dod.teams.microsoft.us (DoD)`

Note

The information in this article applies to Microsoft Defender Antivirus platform update version [4.18.24030](microsoft-defender-antivirus-updates) or later.

## Configurations

Configurations are the payload meant to ensure product health, security, and privacy compliance, and are intended to have the same value for all the users (based on platforms and channels.) This could be to enable a feature flag for a domain action, and can also be used to disable a feature flag in the event of a bug.

## Controlled feature rollout

Controlled feature rollout (CFR) is a procedure for slowly increasing the size of the user group that receives a feature. By distributing a new feature to a randomly selected subset of the user population, it's possible to compare user feedback to an equally sized control group without the feature to measure the impact of the feature.

## Experiments

Currently, Microsoft Defender Core service doesn't do any experimental testing. Development is carried out via the [Gradual Rollout process](manage-gradual-rollout#microsoft-gradual-rollout-model). If this changes, an announcement will be posted in the [Message Center](/en-us/microsoft-365/admin/manage/message-center).