---
layout: Conceptual
title: Prepare to deploy Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/production-deployment
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to set up the deployment for Microsoft Defender for Endpoint.
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
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1016
ms.topic: how-to
ms.subservice: onboard
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 68fc48f8-fa8b-1227-ed98-2cd8477b4cbc
document_version_independent_id: 68fc48f8-fa8b-1227-ed98-2cd8477b4cbc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/production-deployment.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: production-deployment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/production-deployment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: f2d80f5f-eee4-8912-f734-7af76dfa2f6e
---

# Prepare to deploy Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

The first step when deploying Microsoft Defender for Endpoint is to set up your Defender for Endpoint environment.

In this Microsoft Defender for Endpoint deployment guide, you're guided through the steps on:

- Licensing validation
- Tenant configuration
- Network configuration

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

This Defender for Endpoint deployment guide covers only deployments that use Microsoft Configuration Manager. Defender for Endpoint supports the use of other onboarding tools but this deployment guide doesn't cover those onboarding-tool scenarios. For more information, see [Identify Defender for Endpoint architecture and deployment method](deployment-strategy).

Tip

As a companion to this article, see our [Microsoft Defender for Endpoint setup guide](https://go.microsoft.com/fwlink/p/?linkid=2268087) to review best practices and learn about essential tools such as attack surface reduction and next-generation protection. For a customized experience based on your environment, you can access the Defender for [Endpoint automated setup guide](https://go.microsoft.com/fwlink/p/?linkid=2268088) in the Microsoft 365 admin center.

## Check your license state

Checking the license state and whether the license was properly provisioned can be done through the Microsoft 365 admin center or through the **Microsoft Azure portal**.

- In the [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/), in the navigation pane, expand **Billing**, and then select **Your products**.
- In the [Microsoft Azure portal](https://portal.azure.com/#home), under **Manage Microsoft Entra ID**, select **View**. Then, under **Manage**, select **Licenses**.

## Validate your Cloud Solution Provider setup

If you're a Cloud Service Provider (CSP) partner managing a customer tenant, you can check which licenses are provisioned and verify their state through the Microsoft 365 admin center.

1. From the **Partner portal**, select **Administer services** &gt; **Office 365**.
2. Selecting the **Partner portal** link opens the **Admin on behalf** option and gives you access to the customer admin center.

    [![The Office 365 admin portal](media/atp-o365-admin-portal-customer.png)](media/atp-o365-admin-portal-customer.png#lightbox)

## Configure your tenant settings

To provision Defender for Endpoint in your tenant, follow these steps:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. In the navigation pane, select any of the following items:

    - Under **Assets**, select **Devices**.
    - Under **Endpoints**, select an item, such as **Dashboard** or **Endpoint security policies**.

## Review data center location requirements

Microsoft Defender for Endpoint stores and process data in the [same location as used by Microsoft Defender XDR](/en-us/defender-xdr/m365d-enable). If Microsoft Defender XDR hasn't been turned on yet, onboarding to Defender for Endpoint also turns on Defender XDR, and a new data center location is automatically selected based on the location of active Microsoft 365 security services. The selected data center location is shown in the Microsoft Defender portal.

## Configure network access for deployment

Ensure devices can connect to the Defender for Endpoint cloud services. The use of a proxy is recommended. See the following articles to configure your network:

1. [Configure your network environment to ensure connectivity with Defender for Endpoint service](configure-environment).
2. [Configure your devices to connect to the Defender for Endpoint service using a proxy](configure-proxy-internet).
3. [Verify client connectivity to Microsoft Defender for Endpoint service URLs](verify-connectivity).

In environments that restrict outbound URL-based filtering, you might want to allow traffic to specific IP addresses. Not all services are accessible through specific IP addresses, and you need to evaluate how to address this potential issue in your environment. For example, you might need to download updates to a central location and then distribute them. For more information, see [Configure connectivity using static IP ranges](configure-device-connectivity#option-2-configure-connectivity-using-static-ip-ranges).