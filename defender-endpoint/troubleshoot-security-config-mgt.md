---
layout: Conceptual
title: Troubleshoot onboarding issues related to Security Management for Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-security-config-mgt
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot issues that might arise during the onboarding of devices using Security Management for Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: troubleshooting
ms.subservice: onboard
ms.date: 2024-06-12T00:00:00.0000000Z
locale: en-us
document_id: 72b5dafc-79ab-8c4d-4bd1-7f065629a7fb
document_version_independent_id: 72b5dafc-79ab-8c4d-4bd1-7f065629a7fb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-security-config-mgt.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-security-config-mgt
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-security-config-mgt.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: ce4d0441-b726-cca6-5830-104409758588
---

# Troubleshoot onboarding issues related to Security Management for Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Security Management for Microsoft Defender for Endpoint is a capability for devices that aren't managed by Microsoft Intune to receive security configurations.

- For more information on Security Management for Microsoft Defender for Endpoint, see [Manage Microsoft Defender for Endpoint on devices with Microsoft Intune](/en-us/intune/intune-service/protect/mde-security-integration).
- For Security Management for Microsoft Defender for Endpoint onboarding instructions, see [Microsoft Defender for Endpoint Security Configuration Management](/en-us/intune/intune-service/protect/mde-security-integration).
- For more information about the client analyzer, see [Troubleshoot sensor health using Microsoft Defender for Endpoint Client Analyzer](overview-client-analyzer).

## Run Microsoft Defender for Endpoint Client Analyzer on Windows

Consider running the Client Analyzer on endpoints that are failing to complete the Security Management for Microsoft Defender for Endpoint onboarding flow. For more information about the client analyzer, see [Troubleshoot sensor health using Microsoft Defender for Endpoint Client Analyzer](overview-client-analyzer).

The Client Analyzer output file (MDE Client Analyzer Results.htm) can provide key troubleshooting information:

- Verify that the device OS is in scope for Security Management for Microsoft Defender for Endpoint onboarding flow in **General Device Details** section
- Verify that the device appears in Microsoft Entra ID in **Device Configuration Management Details**

    [![The client analyzer results](media/client-analyzer-results.png)](media/client-analyzer-results.png#lightbox)

In the **Detailed Results** section of the report, the Client Analyzer also provides actionable guidance.

Tip

Make sure the Detailed Results section of the report does not include any "Errors", and make sure to review all "Warning" messages.

## General troubleshooting

If you weren't able to identify the onboarded device in Microsoft Entra ID or in the Intune admin center, and didn't receive an error during the enrollment, checking the registry key `Computer\\HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\SenseCM\\EnrollmentStatus` can provide additional troubleshooting information.

[![The page displaying the enrollment status](media/enrollment-status.png)](media/enrollment-status.png#lightbox)

The following table lists errors and directions on what to try/check in order to address the error. Note that the list of errors isn't complete and is based on typical/common errors encountered by customers in the past:

| Error Code | Enrollment Status | Administrator Actions |
| --- | --- | --- |
| `5-7`, `9`, `11-12`, `26-33` | General error | The device was successfully onboarded to Microsoft Defender for Endpoint. However, there was an error in the security configuration management flow. This could be due to the device not meeting [prerequisites for Microsoft Defender for Endpoint management channel](/en-us/intune/intune-service/protect/mde-security-integration). Running the [MDE Client Analyzer (preview)](https://aka.ms/MDEClientAnalyzerPreview) on the device can help identify the root cause of the issue. If this doesn't help, contact support. |
| `8`, `44` | Microsoft Intune Configuration issue | The device was successfully onboarded to Microsoft Defender for Endpoint. However, Microsoft Intune hasn't been configured through the Admin Center to allow Microsoft Defender for Endpoint Security Configuration. Make sure the [Microsoft Intune tenant is configured and the feature is turned on](/en-us/intune/intune-service/protect/mde-security-integration#configure-your-tenant-to-support-microsoft-defender-for-endpoint-security-configuration-management). |
| `13-14`,`20`,`24`,`25` | Connectivity issue | The device was successfully onboarded to Microsoft Defender for Endpoint. However, there was an error in the security configuration management flow, which could be due to a connectivity issue. Verify that the [Microsoft Entra ID and Microsoft Intune endpoints](/en-us/intune/intune-service/protect/mde-security-integration#connectivity-requirements) are opened in your firewall. |
| `10`,`42` | General Hybrid join failure | The device was successfully onboarded to Microsoft Defender for Endpoint. However, there was an error in the security configuration management flow and the OS failed to perform hybrid join. Use [Troubleshoot Microsoft Entra hybrid joined devices](/en-us/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current) for troubleshooting OS-level hybrid join failures. |
| `15` | Tenant mismatch | The device was successfully onboarded to Microsoft Defender for Endpoint. However, there was an error in the security configuration management flow because your Microsoft Defender for Endpoint tenant ID doesn't match your Microsoft Entra tenant ID. Make sure that the Microsoft Entra tenant ID from your Defender for Endpoint tenant matches the tenant ID in the SCP entry of your domain. For more details, [Troubleshoot onboarding issues related to Security Management for Microsoft Defender for Endpoint](troubleshoot-security-config-mgt). |
| `16`,`17` | Hybrid error - Service Connection Point | The device was successfully onboarded to Microsoft Defender for Endpoint. However, Service Connection Point (SCP) record isn't configured correctly and the device couldn't be joined to Microsoft Entra ID. This could be due to the SCP being configured to join Enterprise DRS. Make sure the SCP record points to Microsoft Entra ID and SCP is configured following best practices. For more information, see [Configure a service connection point](/en-us/azure/active-directory/devices/hybrid-azuread-join-manual#configure-a-service-connection-point). |
| `18` | Certificate error | The device was successfully onboarded to Microsoft Defender for Endpoint. However, there was an error in the security configuration management flow due to a device certificate error. The device certificate belongs to a different tenant. Verify that best practices are followed when creating [trusted certificate profiles](/en-us/intune/intune-service/protect/certificates-trusted-root#create-trusted-certificate-profiles). |
| `36` , `37` | Microsoft Entra Connect misconfiguration | The device was successfully onboarded to Microsoft Defender for Endpoint. However, there was an error in the security configuration management flow due to a misconfiguration in Microsoft Entra Connect. To identify what is preventing the device from registering to Microsoft Entra ID, consider running the [Device Registration Troubleshooter Tool](https://github.com/Azure-Samples/DSRegTool). For Windows Server 2012 R2, run the [dedicated troubleshooting instructions](/en-us/azure/active-directory/devices/troubleshoot-hybrid-join-windows-legacy). |
| `38`,`41` | DNS error | The device was successfully onboarded to Microsoft Defender for Endpoint. However, there was an error in the security configuration management flow due to a DNS error. Check the internet connection and/or DNS settings on the device. The invalid DNS settings might be on the workstation's side. Active Directory requires you to use domain DNS to work properly (and not the router's address). For more information, see [Troubleshoot onboarding issues related to Security Management for Microsoft Defender for Endpoint](troubleshoot-security-config-mgt). |
| `40` | Clock sync issue | The device was successfully onboarded to Microsoft Defender for Endpoint. However, there was an error in the security configuration management flow. Verify that the clock is set correctly and is synced on the device where the error occurs. |
| `43` | MDE and ConfigMgr | The device is managed using Configuration Manager and Microsoft Defender for Endpoint. Controlling policies through both channels may cause conflicts and undesired results. To avoid this, endpoint security policies should be isolated to a single control plane. |
| `2` | Device is not enrolled and has never been enrolled | The device was successfully onboarded to Microsoft Defender for Endpoint. However, it is not enrolled to be managed by Defender for Endpoint. For more information, see [Configure Microsoft Defender for Endpoint](/en-us/intune/intune-service/protect/mde-security-integration?pivots=mdssc-preview). |
| `4` | Device is managed by SCCM Agent | The device was successfully onboarded to Microsoft Defender for Endpoint. However, it is configured to be managed by SCCM. In order for the machine to be managed by MDE go to Settings &gt; Endpoints &gt; Configuration Management &gt; Enforcement Scope and turn off the "Manage Security setting using Configuration Manager" toggle. For more information on co-existence with Configuration Manager, see [Defender for Endpoint integration with Configuration Manager](/en-us/intune/intune-service/protect/mde-security-integration#co-existence-with-microsoft-endpoint-configuration-manager). |

## Related topic

- [Manage Microsoft Defender for Endpoint on devices with Microsoft Intune](/en-us/intune/intune-service/protect/mde-security-integration)