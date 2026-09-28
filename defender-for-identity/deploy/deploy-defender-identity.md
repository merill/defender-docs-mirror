---
layout: Conceptual
title: Deploy Microsoft Defender for Identity sensors - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/deploy-defender-identity
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how to deploy Microsoft Defender for Identity sensors on domain controllers and identity servers. Choose the right sensor version for your environment.
ms.date: 2026-09-10T00:00:00.0000000Z
ms.topic: overview
ms.custom: msecd-doc-authoring-1015
ms.reviewer: rlitinsky
ai-usage: ai-assisted
locale: en-us
document_id: 036630b3-2132-8260-6d75-a7d14389893a
document_version_independent_id: 036630b3-2132-8260-6d75-a7d14389893a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/deploy-defender-identity.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/deploy-defender-identity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/deploy-defender-identity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: 38073ffd-893f-40cf-08b0-5025b9b627a8
---

# Deploy Microsoft Defender for Identity sensors - Microsoft Defender for Identity | Microsoft Learn

Microsoft Defender for Identity sensors collect signals from your on-premises identity infrastructure. Defender for Identity uses these signals to detect threats such as privilege escalation and high-risk lateral movement. It also reports identity security issues, such as unconstrained Kerberos delegation, so your security team can correct them.

Install Defender for Identity sensors on all domain controllers, including read-only domain controllers (RODCs). Also install sensors on Active Directory Federation Services (AD FS), Active Directory Certificate Services (AD CS), and Microsoft Entra Connect servers that aren't domain controllers. Use the table in this article to select the sensor version.

## Select your deployment method

The sensor version you deploy depends on the server role and operating system. Use the following table to select the appropriate deployment for each server in your environment.

For eligible domain controllers running Windows Server 2019 or later, sensor v3.x supports onboarding with or without Microsoft Defender for Endpoint deployment. Other eligible identity-role servers require Defender for Endpoint onboarding.

![Diagram of sensor deployment: use sensor v3.x on supported servers running Windows Server 2019 or later, and v2.x on earlier versions.](media/deploy-defender-identity/sensor-deployment-decision.png)

| Server configuration | Server operating system | Recommended deployment | Onboarding options |
| --- | --- | --- | --- |
| Any supported server type | Windows Server 2019 or later with the July 2026 or later cumulative update | [Defender for Identity sensor v3.x](deploy-sensor-v3) | For servers onboarded to Defender for Endpoint, activate sensor v3.x directly. For domain controllers that aren't onboarded to Defender for Endpoint, use the sensor v3.x onboarding package. AD FS, AD CS, and Microsoft Entra Connect servers must be onboarded to Defender for Endpoint before activation. |
| Any supported server type | Windows Server 2016 or earlier | [Defender for Identity sensor v2.x](prerequisites-sensor-version-2) | [Install the sensor v2.x package](install-sensor). |

Defender for Identity supports sensor v3.x and sensor v2.x in the same workspace. For example, you might deploy sensor v3.x on servers running Windows Server 2019 or later and sensor v2.x on servers running Windows Server 2016 or earlier.

If your organization requires [VPN integration](../vpn-integration) or [syslog notifications](../notifications#configure-syslog-notifications), use the v2.x sensor on the applicable domain controllers. These features aren't supported by the v3.x sensor.

Important

If any of your sensors are v3.x, select **Automatically use the sensor's local system account** for all sensors. The v3.x sensors don't use gMSA accounts configured for v2.x sensors; they always use the local system account. For more information, see [Sensor v3.x service account requirements](deploy-sensor-v3#service-account-requirements).

Before you activate the Defender for Identity sensor v3.x, note that v3.x:

- Supports onboarding through Defender for Endpoint. Eligible domain controllers can instead use the sensor v3.x onboarding package.
- Doesn't support VPN integration.
- Doesn't support [syslog notifications](../notifications#configure-syslog-notifications).
- Has limitations working with Azure ExpressRoute. For more information, see [Azure ExpressRoute for Microsoft 365](/en-us/microsoft-365/enterprise/azure-expressroute).

## Review the Sensor management tab

The **Sensor management** tab displays deployed sensors and servers discovered in Device Inventory. Each server's onboarding status shows whether the server is eligible for sensor v3.x and what action to take.

### Review action cards

Action cards summarize servers and sensors that need attention. Select a card to open a pane with more information and available actions.

| Action card | What the pane presents | Available actions |
| --- | --- | --- |
| **Domain controllers ready for activation** | Eligible domain controllers that are onboarded to Microsoft Defender for Endpoint and ready for sensor v3.x activation. | To automatically activate eligible domain controllers, select **Enable automatic activation**. On the **Advanced features** page, turn on **Automatic sensor v3.x activation**. To review the servers instead, select **Show in table**. |
| **Domain controllers ready for manual onboarding** | Eligible domain controllers that aren't onboarded to Microsoft Defender for Endpoint or that run Windows Server 2016 or earlier. | Select **Download onboarding package** to choose the applicable manual sensor deployment package. |
| **Servers ready for migration** | Eligible servers that are ready to migrate from sensor v2.x to sensor v3.x. | Select **Show in table** to filter the server list to servers that are **Ready for migration**. Start migration by selecting servers in the filtered table. |
| **AD CS, AD FS, or Entra Connect servers ready for activation** | Eligible AD FS, AD CS, or Microsoft Entra Connect servers that are onboarded to Microsoft Defender for Endpoint and ready for sensor v3.x activation. | Select **Show in table** to review the servers. Select an eligible server, and then select **Activate**. |
| **AD CS, AD FS, or Entra Connect servers ready for manual onboarding** | Eligible AD FS, AD CS, or Microsoft Entra Connect servers that aren't onboarded to Microsoft Defender for Endpoint or that run Windows Server 2016 or earlier. | Select **Download onboarding package** to choose the applicable manual sensor deployment package. |
| **Sensors not healthy** | Sensors with open health issues that require attention. | Select **Show in table** to filter the sensor list to unhealthy sensors, or select **Go to health page** to review the health issues. |

The **Onboarding status** column uses the following values:

| Onboarding status | Next steps |
| --- | --- |
| Onboarded | The Defender for Identity sensor is deployed on the server. |
| Activate sensor | The server is ready for sensor v3.x activation. [Activate the v3.x sensor](activate-sensor#activate-the-defender-for-identity-sensor). |
| Manually onboard | The server requires manual sensor deployment. Choose the appropriate deployment method. |
| Upgrade to the latest Windows Update | The server doesn't meet the operating system requirements for sensor v3.x. Install the latest Windows updates before activation. |

Note

The table combines deployed sensors with servers discovered through Device Inventory. A server without a deployed sensor must be onboarded to Microsoft Defender for Endpoint to appear as a server row. Servers that aren't onboarded to Defender for Endpoint can appear in the manual onboarding action cards.

## Choose a deployment flow

Choose the sensor deployment flow that matches the server configuration:

- If the server is onboarded to Microsoft Defender for Endpoint, [activate sensor v3.x from the Sensor management tab](activate-sensor#activate-the-defender-for-identity-sensor).
- If an eligible domain controller isn't onboarded to Defender for Endpoint, [download and run the sensor v3.x onboarding package](activate-sensor#onboard-the-domain-controller-preview).
- If the server already runs sensor v2.x, [migrate the sensor to v3.x](migrate-to-sensor-v3).
- If the server supports sensor v2.x only, [install sensor v2.x](install-sensor).

## Deployment steps for sensor v3.x

Follow these steps to deploy sensor v3.x on eligible servers running Windows Server 2019 or later:

1. [Verify prerequisites](deploy-sensor-v3#before-you-activate).
2. [Activate the sensor](activate-sensor).
3. [Configure Windows event auditing](configure-windows-event-collection#configure-defender-for-identity-to-collect-windows-events-automatically).
4. [Configure RPC auditing](deploy-sensor-v3#configure-rpc-auditing).
5. [Validate deployment](test-sensor).

## Deployment steps for sensor v2.x

Follow these steps to deploy the sensor v2.x on supported servers running Windows Server 2016 or earlier:

1. [Verify prerequisites](prerequisites-sensor-version-2).
2. [Plan capacity](capacity-planning).
3. [Configure connectivity](configure-proxy).
4. [Install the sensor](install-sensor).
5. [Configure the sensor](configure-sensor-settings).
6. [Configure Windows event auditing](configure-windows-event-collection#configure-windows-event-collection-manually).
7. [Configure Directory Service accounts](directory-service-accounts).
8. [Configure for AD FS, AD CS, or Entra Connect (if applicable)](active-directory-federation-services).
9. [Validate deployment](test-sensor).