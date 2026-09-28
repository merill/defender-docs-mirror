---
layout: Conceptual
title: Onboard Non-Azure Servers with Defender for Endpoint - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/onboard-machines-with-defender-for-endpoint
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
description: Learn how to connect your non-Azure machines directly to Microsoft Defender for Cloud with Microsoft Defender for Endpoint.
ms.topic: quickstart
ms.date: 2026-06-17T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 83692c99-fa1a-4cfc-f334-c43aaea4b3d9
document_version_independent_id: 7ec06c35-846b-5f11-33f7-01fc5e6039be
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/onboard-machines-with-defender-for-endpoint.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/onboard-machines-with-defender-for-endpoint
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/onboard-machines-with-defender-for-endpoint.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 301d6f11-4fa0-764c-d257-a94d471374b3
---

# Onboard Non-Azure Servers with Defender for Endpoint - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud lets you onboard on-premises and multicloud servers through Microsoft Defender for Endpoint. This setup protects non-Azure machines without the need for any additional agents and shows all servers, Azure and non-Azure, in one unified security view.

Note

To connect your non-Azure machines via Azure Arc, see [Connect your non-Azure machines to Microsoft Defender for Cloud with Azure Arc](quickstart-onboard-machines).

## How it works

Direct onboarding is a native integration between Defender for Endpoint and Defender for Cloud. When enabled, non-Azure servers with Defender for Endpoint appear in Defender for Cloud under the selected subscription.

Defender for Cloud uses the selected subscription for licensing, billing, alerts, and security insights. This subscription doesn’t support Azure management capabilities such as Azure Policy or Guest Configuration. Use other tools to manage security settings, such as antivirus policies, attack surface reduction rules, and updates.

### Manage security settings

| Server type | Management options |
| --- | --- |
| **Windows Server** | [Defender for Endpoint security settings management](/en-us/defender-endpoint/mde-security-settings-management)[Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/defender-advanced-threat-protection)[Group Policy](/en-us/defender-endpoint/use-group-policy-microsoft-defender-antivirus)[PowerShell](/en-us/powershell/module/defender/)[WMI](/en-us/defender-endpoint/use-wmi-microsoft-defender-antivirus) |
| **Linux Server** | [Defender for Endpoint security settings management](/en-us/defender-endpoint/mde-security-settings-management)[Configure security settings in Defender for Endpoint on Linux](/en-us/defender-endpoint/linux-preferences) |

## Availability

This capability is **generally available (GA)** and supports on-premises servers and multicloud VMs.

Supported operating systems include all Windows Server and Linux server versions supported by Defender for Endpoint. For OS-specific requirements, see:

- [Supported Windows Server versions](/en-us/defender-endpoint/minimum-requirements#windows-versions-supported-by-defender-for-endpoint)
- [Supported Linux server versions](/en-us/defender-endpoint/mde-linux-prerequisites#system-requirements)

This capability works with both:

- **Defender for Servers Plan 1 (P1)**
- **Defender for Servers Plan 2 (P2)** (with limitations)

## Enable direct onboarding

When you enable direct onboarding, Defender for Cloud applies the setting to both existing and new servers onboarded to Defender for Endpoint in the same Microsoft Entra tenant. After you enable it, your servers appear under the selected subscription, and their alerts, vulnerability data, and inventory integrate with Defender for Cloud.

Before you begin:

Important

If you have both Microsoft Defender for Endpoint for Servers licenses and Defender for Servers enabled, request the billing discount to avoid double billing. For steps, see [Can I get a discount if I already have a Microsoft Defender for Endpoint license?](faq-defender-for-servers#can-i-get-a-discount-if-i-already-have-a-microsoft-defender-for-endpoint-license-).

- Make sure you have the required permissions:
    - **Subscription Owner** permissions on the subscription you select for onboarding.
    - **Microsoft Entra Security Administrator** (or higher) permissions on the tenant.
- Review the current limitations

### Enable in the Defender for Cloud portal

To enable direct onboarding in the Defender for Cloud portal:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Defender for Cloud**.
3. Go to **Environment settings** &gt; **Direct onboarding**.
4. Toggle direct onboarding to **On**.
5. Select the subscription you want to use for servers onboarded through Defender for Endpoint.
6. Select **Save**.

[![Screenshot showing the Direct onboarding toggle in Defender for Cloud portal.](media/onboard-machines-with-defender-for-endpoint/direct-onboarding-subscription.png)](media/onboard-machines-with-defender-for-endpoint/direct-onboarding-subscription.png#lightbox)

Non-Azure servers might take up to 24 hours to appear in the selected subscription.

### Deploy Defender for Endpoint on your servers

Deploy the Defender for Endpoint agent the same way on Windows and Linux servers, with or without direct onboarding. See [Onboard servers to Defender for Endpoint](/en-us/defender-endpoint/onboard-server) for more information.

## Current limitations

- **Plan support** – Direct onboarding provides all Defender for Servers Plan 1 features. Some Defender for Servers Plan 2 features still require Azure Arc. If you enable Plan 2, directly onboarded servers gain Plan 1 + [Defender Vulnerability Management](/en-us/defender-vulnerability-management/defender-vulnerability-management-capabilities) features.
- **Multicloud support** – Direct onboarding supports AWS and GCP VMs using the Defender for Endpoint agent. However, if you also connect your AWS or GCP account to Defender for Servers via multicloud connectors, we still recommend using Azure Arc.
- **Simultaneous onboarding** – Defender for Cloud automatically correlates servers onboarded through multiple methods. Older Defender for Endpoint agent versions might limit this behavior and, in rare cases, cause duplicate billing. Ensure agents meet or exceed these minimum versions:

    | Operating System | Minimum agent version |
    | --- | --- |
    | Windows Server 2019 and later | 10.8555 |
    | Windows Server 2016 or Windows 2012 R2 ([modern, unified solution](/en-us/defender-endpoint/onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2)) | 10.8560 |
    | Linux (AMD64) | 30.101.23052.009 |
    | Linux (ARM64) | 30.101.25022.004 |