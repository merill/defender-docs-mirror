---
layout: Conceptual
title: Get started with Microsoft Defender Experts for cloud workloads - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-servers-get-started
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Set up Microsoft Defender Experts for Servers by onboarding cloud resources, granting permissions, configuring notifications, and preparing your environment in the Defender portal.
ms.service: defender-experts-for-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-security
- tier1
- essentials-get-started
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-dex
- msecd-doc-authoring-1012
search.appverid: met150
ms.date: 2026-06-16T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: b70aa369-d470-f873-dee8-446c4f46af5e
document_version_independent_id: b70aa369-d470-f873-dee8-446c4f46af5e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-servers-get-started.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-servers-get-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-servers-get-started.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a68c96c1-9077-b11c-88d3-1853c672413f
---

# Get started with Microsoft Defender Experts for cloud workloads - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender Experts for Servers](defender-experts-servers-overview)

Set up Defender Experts for Servers in the Microsoft Defender portal by onboarding cloud resources, granting permissions, configuring notifications, and preparing your environment.

## Review pricing information

Defender Experts for Servers uses **pay-as-you-go consumption meter**. For more information on pricing, review the [Microsoft Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/) or contact your Microsoft representative.

## Prerequisites

Before you begin, confirm the following:

- [Defender for Servers Plan 1 or Plan 2](/en-us/azure/defender-for-cloud/defender-for-servers-overview) enabled in Microsoft Defender for Cloud
- Microsoft Entra ID Plan 2

Ensure you have at least a **Security Administrator** role assigned in the Microsoft Defender portal to onboard your cloud workloads.

## Complete the onboarding steps

Complete these steps to onboard your cloud workloads to the Defender Experts service.

### Select the cloud resources to onboard

Choose which cloud resource types you want Defender Experts to cover. The Defender Experts service is enabled at the tenant level.

Note

Defender Experts only supports managed cloud security for Microsoft Defender for Servers.

To select your coverage options:

1. In the Microsoft Defender portal, go to **Settings** &gt; **Defender Experts** &gt; **Cloud workloads**.
2. Under supported cloud coverage options, select **Defender Experts for Servers**.

    [![Screenshot of the Defender Experts settings page in the Defender portal, with the Defender Experts for Servers option highlighted.](media/get-started-dex-servers/defender-experts-servers-select.png)](media/get-started-dex-servers/defender-experts-servers-select.png#lightbox)
3. Select **Save**.

    - If you're an existing Defender Experts MDR customer, no additional action is needed (the provisioning script, permissions, and setup steps don't apply), and server coverage starts immediately.
    - If you're a new Defender Experts customer, saving your selection opens the Defender Experts onboarding wizard.
4. Select **Continue** to proceed with the onboarding wizard to complete the following steps, or select **Cancel** to go back.

### Run the provisioning script

To start your managed cloud security service, download and run a signed PowerShell script on any managed device by using PowerShell 7 or in Azure Cloud Shell. This script provisions and registers the necessary first-party applications that Defender Experts relies on to securely access and manage your environment.

Note

To perform this onboarding step, ensure you're assigned *at least* an **Application Admin** role.

To run the provisioning script:

1. In the Defender Experts onboarding wizard, under **Service set up**, download a copy of the signed PowerShell script and run it on a local device by using PowerShell 7 or in Azure Cloud Shell.

    [![Screenshot of Defender Experts onboarding wizard showing Run provisioning script step with Download script and Validate buttons.](media/get-started-dex-servers/defender-experts-servers-script.png)](media/get-started-dex-servers/defender-experts-servers-script.png#lightbox)
2. After you run the script, it might take some time to process. Don't close the wizard while the script processes. You can select **Validate** to check connector access and verify that the required components are provisioned.

### Grant permissions to experts

Defender Experts for Servers requires **Service provider access** that experts use to sign in to your tenant and deliver services based on assigned security roles. For more information, see [Cross-tenant access overview](/en-us/entra/external-id/cross-tenant-access-overview).

Grant experts one or both of the following permissions:

- **Investigate incidents and guide my responses** (default): Experts proactively monitor and investigate incidents and guide you through response actions. (Access level: Security Reader)
- **Respond directly to active threats** (recommended): Experts contain and remediate active threats immediately while investigating, reducing the threat's impact and improving response efficiency. (Access level: Security Operator)

To grant permissions:

1. In the onboarding wizard, under **Permissions**, choose one or more access levels to grant to the experts.

    [![Screenshot of Defender Experts onboarding Permission step with Investigate incidents and Respond directly to active threats options.](media/get-started-dex-servers/defender-experts-servers-permissions.png)](media/get-started-dex-servers/defender-experts-servers-permissions.png#lightbox)
2. Select **Next** to continue.

### Finish the setup and prepare your environment

To finish the setup:

1. Continue with the onboarding wizard to set up the following configurations:

    - [Notification contacts](defender-experts-mdr-get-started#tell-us-who-to-contact-for-important-matters)
    - [Microsoft Teams notifications](defender-experts-mdr-get-started#receive-managed-response-notifications-and-updates-in-microsoft-teams)
2. Review and submit settings. The onboarding wizard finishes its initial setup.

## After you complete the onboarding steps

After you onboard your cloud workloads, take note of the following information:

- **Billing:**Billing starts when you finish onboarding.
    - View your bill in **Microsoft Cost Management**. For more information, see [What is Microsoft Cost Management](/en-us/azure/cost-management-billing/costs/overview-cost-management).
    - At the end of your billing cycle, look for **Microsoft Defender Experts for Servers costs**.
- **Endpoint protection:** The Microsoft Defender for Endpoint extension is automatically installed on all supported devices connected to Microsoft Defender for Cloud. Ensure that automatic provisioning of the Defender for Endpoint sensor is enabled.

## Turn off Defender Experts for Servers service

To disable the service, [contact your Service Delivery Expert](defender-experts-mdr-communication).

Note

Charges continue until the service is fully turned off within 48 hours.