---
layout: Conceptual
title: Use Direct onboarding for on-premises servers - Microsoft Defender for Cloud | Microsoft Learn
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
description: Associate existing endpoint-protected servers with Defender for Servers and review the affected population.
ms.topic: how-to
ms.date: 2026-10-20T00:00:00.0000000Z
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
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/beac614b-f66d-40ed-a947-3996de709333
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/9da05372-4706-43ec-a899-f436adab380d
platformId: 301d6f11-4fa0-764c-d257-a94d471374b3
---

# Use Direct onboarding for on-premises servers - Microsoft Defender for Cloud | Microsoft Learn

Use this procedure only when you choose to associate eligible servers already reporting to Defender for Endpoint with Defender for Servers through an Azure subscription. Direct onboarding doesn't install the endpoint agent and isn't required to continue using an existing Defender for Endpoint deployment.

Note

To connect your non-Azure machines via Azure Arc, see [Connect on-premises servers to Defender for Servers](quickstart-onboard-machines).

## Who is affected

Important

The setting applies to existing and future eligible non-Azure servers onboarded to Defender for Endpoint in the same Microsoft Entra tenant. You can't select individual servers or limit it to a pilot group.

Review the full affected population before enabling the setting, including servers with an existing Azure Arc connection.

## Prerequisites

- Servers meet [Defender for Endpoint requirements](/en-us/defender-endpoint/minimum-requirements) and report healthy telemetry.
- The selected Azure subscription and Defender for Endpoint use the same Microsoft Entra tenant.
- You have the **Owner** role on the selected Azure subscription and the **Security Administrator** role or a higher-privileged role in Microsoft Entra ID.
- Required features are available through this connection. Review feature limits before choosing a plan.

Important

If you have both Microsoft Defender for Endpoint for Servers licenses and Defender for Servers enabled, request the billing discount to avoid double billing. For steps, see [Can I get a discount if I already have a Microsoft Defender for Endpoint license?](faq-defender-for-servers#can-i-get-a-discount-if-i-already-have-a-microsoft-defender-for-endpoint-license-)

## Configure Direct onboarding

To enable Direct onboarding in the Azure portal:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Defender for Cloud**.
3. Go to **Environment settings** &gt; **Direct onboarding**.
4. Set **Direct onboarding** to **On**.
5. Select the subscription you want to use for servers onboarded through Defender for Endpoint.
6. Select **Save**.

[![Screenshot showing the Direct onboarding toggle in Defender for Cloud portal.](media/onboard-machines-with-defender-for-endpoint/direct-onboarding-subscription.png)](media/onboard-machines-with-defender-for-endpoint/direct-onboarding-subscription.png#lightbox)

Non-Azure servers might take up to 24 hours to appear in the selected subscription.

## Verify Direct onboarding

1. In Defender for Cloud, confirm that representative affected servers appear under the selected subscription with the intended plan.
2. Check endpoint health separately using the [onboarding checks](/en-us/defender-endpoint/onboard-server#verify-onboarding).
3. Check for duplicate records. Keep the endpoint agent current; older versions can interfere with correlation when a server uses multiple connection methods.

The following minimum agent versions help Defender for Cloud correlate servers that use multiple connection methods:

| Operating system | Minimum agent version |
| --- | --- |
| Windows Server 2019 and later | 10.8555 |
| Windows Server 2016 or Windows Server 2012 R2 ([modern, unified solution](/en-us/defender-endpoint/onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2)) | 10.8560 |
| Linux (AMD64) | 30.101.23052.009 |
| Linux (ARM64) | 30.101.25022.004 |

## Feature limits

Direct onboarding supports Defender for Servers Plan 1 and a subset of Plan 2 capabilities. Some Plan 2 features still require Azure Arc. Review [plan feature requirements](defender-for-servers-overview#plan-protection-features) for your workloads.

Direct onboarding supports AWS and GCP VMs using the Defender for Endpoint agent. If you also connect the AWS or GCP account through a multicloud connector, use Azure Arc to access Arc-dependent capabilities.

Direct onboarding doesn't provide Azure management capabilities such as Azure Policy or Guest Configuration. Continue to manage endpoint settings through your existing supported tools.

### Manage security settings

| Server type | Management options |
| --- | --- |
| **Windows Server** | [Defender for Endpoint security settings management](/en-us/defender-endpoint/mde-security-settings-management)[Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/defender-advanced-threat-protection)[Group Policy](/en-us/defender-endpoint/use-group-policy-microsoft-defender-antivirus)[PowerShell](/en-us/powershell/module/defender/)[WMI](/en-us/defender-endpoint/use-wmi-microsoft-defender-antivirus) |
| **Linux Server** | [Defender for Endpoint security settings management](/en-us/defender-endpoint/mde-security-settings-management)[Configure security settings in Defender for Endpoint on Linux](/en-us/defender-endpoint/linux-preferences) |