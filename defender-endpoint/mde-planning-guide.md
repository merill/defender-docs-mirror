---
layout: Conceptual
title: Get started with your Microsoft Defender for Endpoint deployment - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mde-planning-guide
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to get started with the deploy, setup, licensing validation, tenant configuration, network configuration stages.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365solution-endpointprotect
- m365solution-scenario
- highpri
- tier1
- essentials-get-started
ms.custom:
- admindeeplinkDEFENDER
- sfi-ga-nochange
ms.topic: get-started
ms.subservice: onboard
ms.date: 2025-06-19T00:00:00.0000000Z
locale: en-us
document_id: b22f40ca-4e77-9e6e-8989-c01ab167e43b
document_version_independent_id: b22f40ca-4e77-9e6e-8989-c01ab167e43b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mde-planning-guide.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mde-planning-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mde-planning-guide.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 7c6c0a14-bcf7-e0d8-7ced-d067e9e96a5a
---

# Get started with your Microsoft Defender for Endpoint deployment - Microsoft Defender for Endpoint | Microsoft Learn

Tip

As a companion to this article, see our [Microsoft Defender for Endpoint setup guide](https://go.microsoft.com/fwlink/p/?linkid=2268087) to review best practices and learn about essential tools such as attack surface reduction and next-generation protection. For a customized experience based on your environment, you can access the Defender for [Endpoint automated setup guide](https://go.microsoft.com/fwlink/p/?linkid=2268088) in the Microsoft 365 admin center.

Maximize available security capabilities and better protect your enterprise from cyber threats by deploying Microsoft Defender for Endpoint and onboarding your devices. Onboarding your devices enables you to identify and stop threats quickly, prioritize risks, and evolve your defenses across operating systems and network devices.

This guide provides five steps to help deploy Defender for Endpoint as your multi-platform endpoint protection solution. It helps you choose the best deployment tool, onboard devices, and configure capabilities. Each step corresponds to a separate article.

The steps to deploy Defender for Endpoint are:

[![The deployment steps](/en-us/defender/media/defender-endpoint/onboard-mde.png)](/en-us/defender/media/defender-endpoint/onboard-mde.png#lightbox)

1. [Step 1 - Set up Microsoft Defender for Endpoint deployment](production-deployment): This step focuses on getting your environment ready for deployment.
2. [Step 2 - Assign roles and permissions](prepare-deployment): Identify and assign roles and permissions to view and manage Defender for Endpoint.
3. [Step 3 - Identify your architecture and choose your deployment method](deployment-strategy): Identify your architecture and the deployment method that best suits your organization.
4. [Step 4 - Onboard devices](onboarding): Assess and onboard your devices to Defender for Endpoint.
5. [Step 5 - Configure capabilities](onboard-configure): You're now ready to configure Defender for Endpoint security capabilities to protect your devices.

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

## Requirements

Here's a list of prerequisites required to deploy Defender for Endpoint:

- You're a Security Administrator
- Your environment meets the [minimum requirements](minimum-requirements)
- You have a full inventory of your environment. The following table provides a starting point to gather information and ensure that stakeholders understand your environment. The inventory helps identify potential dependencies and/or changes required in technologies or processes.

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

| What | Description |
| --- | --- |
| Endpoint count | Total count of endpoints by operating system. |
| Server count | Total count of Servers by operating system version. |
| Management engine | Management engine name and version (for example, System Center Configuration Manager Current Branch 1803). |
| CDOC distribution | High level CDOC structure (for example, Tier 1 outsourced to Contoso, Tier 2 and Tier 3 in-house distributed across Europe and Asia). |
| Security information and event (SIEM) | SIEM technology in use. |