---
layout: Conceptual
title: Prerequisites and support in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/prerequisites
author: dlanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Review the prerequisites for Microsoft Security Exposure Management.
ms.topic: overview
ms.date: 2026-06-18T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
ai-usage: ai-assisted
locale: en-us
document_id: bf5e44c1-6d2b-ec90-a76e-4b409899c7c0
document_version_independent_id: bf5e44c1-6d2b-ec90-a76e-4b409899c7c0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/prerequisites.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: prerequisites
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/prerequisites.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 95a8e714-49b3-d2e4-66c3-dde20ef916b7
---

# Prerequisites and support in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

This article describes the requirements and prerequisites for using Microsoft Security Exposure Management in the unified Microsoft Defender portal.

## Portal access and setup

Microsoft Security Exposure Management is integrated into the Microsoft Defender XDR portal at https://security.microsoft.com. There's no separate installation required - all Exposure Management features are accessible through the **Exposure Management** section in the unified portal.

### Licensing requirements

Microsoft Security Exposure Management features are available with the following license plans:

- Microsoft 365 E5
- Microsoft 365 E3 with certain add-ons
- Microsoft Defender suite licenses
- Other qualifying licenses as specified in the integration and licensing documentation

### Environmental requirements

The following products must be enabled to get full value from the dashboard:

- **Defender for Cloud** with CSPM (Cloud Security Posture Management) capabilities enabled.
- **Microsoft Defender Vulnerability Management (MDVM)** — standalone or as part of Defender for Endpoint P2.

### External data connectors (Preview)

External data connectors are currently in public preview with separate consumption-based pricing. During the preview phase, use of data connectors is free. Once generally available, there will be consumption-based costs for each non-Microsoft data connector based on the number of assets retrieved from connected security tools.

### Regional and tenant requirements

Microsoft Security Exposure Management is available in Public Cloud only. It's not available in national/sovereign clouds (US Gov, China Gov, or other sovereign clouds).

All data is processed within the Microsoft Defender XDR portal infrastructure. Ensure your tenant meets the standard requirements for Defender portal access.

## Permissions

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## Manage permissions with Microsoft Defender unified role-based access control (RBAC)

[Microsoft Defender unified role-based access control(RBAC)](/en-us/defender-xdr/manage-rbac) allows you to create custom roles with specific permissions for Exposure Management. These permissions are located under the **Security posture** category in Defender unified RBAC permissions model and are named:

- **Exposure Management (read)** for read-only access
- **Exposure Management (manage)** for access to manage Exposure Management experiences

For more sensitive actions in Exposure Management, users need the **Core security settings (manage)** permission that is located under the **Authorization and settings** category.

To access Exposure Management data and actions, a custom role in Defender unified RBAC with any of the permissions mentioned here, shall be assigned to the **Microsoft Security Exposure Management** data source.

To learn more about using Microsoft Defender unified RBAC to manage your Secure Score permissions, see [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac). For the full list of available permissions and their descriptions, see [Permissions in Microsoft Defender unified RBAC](/en-us/defender-xdr/custom-permissions-details).

The following table highlights what a user can access or perform with each of the permissions:

| Permission name | Actions |
| --- | --- |
| **Exposure Management (read)** | Access to all Exposure Management experiences and read access to all available data |
| **Exposure Management (manage)** | In addition to the read access, the user can set initiative target score and edit metric values, as long as the user has access to all Defender for Endpoint [device groups](/en-us/microsoft-365/security//defender-endpoint/machine-groups). |
| **Core security settings (manage)** | Connect or change vendor to the External Attack Surface Management initiative |

For full Microsoft Security Exposure Management access, user roles need access to all Defender for Endpoint [device groups](/en-us/microsoft-365/security//defender-endpoint/machine-groups). Users with restricted access to some of the organization's device groups can:

- Access global exposure insights data.
- View affected assets under metrics, recommendations, events, and initiatives history only within their scope.
- View devices in attack paths that are within their scope.
- Access the Security Exposure Management attack surface map and advanced hunting schemas (ExposureGraphNodes and ExposureGraphEdges) for the device groups they have access to.

Note

Access with manage permissions to **Critical asset management**, under **System&gt; Settings&gt; Microsoft Defender XDR** requires users to have access to all Defender for Endpoint device groups.

## Access with Microsoft Entra ID roles

An alternative to managing access with Microsoft Defender unified RBAC permissions, access to Microsoft Security Exposure Management data and actions is also possible with [Microsoft Entra ID Roles](/en-us/entra/identity/role-based-access-control/custom-overview). You need a tenant with at least one Global Admin or Security Admin to create a Security Exposure Management workspace.

For full access, users need one of the following Microsoft Entra ID roles:

- **Global Admin** (read and write permissions)
- **Security Admin** (read and write permissions)
- **Security Operator** (read and limited write permissions)
- **Global Reader** (read permissions)
- **Security Reader** (read permissions)
- **Service Support** Administrator (read permissions)
- **User Administrator** (read permissions)
- **Helpdesk Administrator** (read permissions)
- **Exchange Administrator** (read and write permissions)
- **SharePoint Administrator** (read and write permissions)

Permission levels are summarized in the table.

| Action | Global Admin | Global Reader | Security Admin | Security Operator | Security Reader |
| --- | --- | --- | --- | --- | --- |
| **Grant permissions to others** | ✔ | - | - | - | - |
| **Onboard your organization to the Microsoft Defender External Attack Surface Management (EASM) initiative** | ✔ | ✔ | ✔ | ✔ | ✔ |
| **Mark initiative as a favorite** | ✔ | ✔ | ✔ | ✔ | ✔ |
| **Set initiative target score** | ✔ | - | ✔ | - | - |
| **View general initiatives** | ✔ | ✔ | ✔ | ✔ | ✔ |
| **Share metric/Recommendations** | ✔ | ✔ | ✔ | ✔ | ✔ |
| **Edit metric weight** | ✔ | - | ✔ | - | - |
| **Export metric (PDF)** | ✔ | ✔ | ✔ | ✔ | ✔ |
| **View metrics** | ✔ | ✔ | ✔ | ✔ | ✔ |
| **Export assets (metric/recommendation)** | ✔ | ✔ | ✔ | ✔ | ✔ |
| **Manage recommendations** | ✔ | - | ✔ | - | - |
| **View recommendations** | ✔ | ✔ | ✔ | ✔ | ✔ |
| **Export events** | ✔ | ✔ | ✔ | ✔ | ✔ |
| **Change criticality level** | ✔ | - | ✔ | ✔ | - |
| **Set critical asset rule** | ✔ | - | ✔ | - | - |
| **Create criticality rule** | ✔ | - | ✔ | - | - |
| **Turn criticality rule on/off** | ✔ | - | ✔ | ✔ | - |
| **Run a query on exposure graph data** | ✔ | ✔ | ✔ | ✔ | ✔ |
| **Configure data connectors** | ✔ |  | ✔ | ✔ |  |
| **View data connectors** | ✔ | ✔ | ✔ | ✔ | ✔ |

## Browser requirements

You can access Security Exposure Management in the Microsoft Defender portal using Microsoft Edge, Internet Explorer 11, or any HTML 5 compliant web browser.

## Critical asset classification

- Before you start, learn about [critical asset management](critical-asset-management) in Security Exposure Management.
- [Review required permissions](prerequisites#permissions) for working with the critical assets.
- When classifying critical assets, we support devices running version 10.3740.XXXX of the Defender for Endpoint sensor or later. We recommended running a more recent sensor version, as listed on the Defender for Endpoint [What's New page](/en-us/defender-endpoint/windows-whatsnew).

    You can check which sensor version a device is running as follows:

    - On a specific device, browse to the MsSense.exe file in C:\Program Files\Windows Defender Advanced Threat Protection. Right-click the file, and select **Properties**. On the **Details** tab, check the file version.
    - For multiple devices, it's easier to run an [advanced hunting Kusto query](/en-us/defender-xdr/advanced-hunting-query-language) to check device sensor versions, as follows:

        `DeviceInfo | project DeviceName, ClientVersion`

## Data freshness, retention, and related functionality

We currently ingest and process supported data from first-party Microsoft products, making it available within the enterprise exposure graph and applicable Microsoft Security Exposure Management experiences built on top of graph data within 72 hours of its production at the source product.

Microsoft product data is retained for no less than 14 days in the enterprise exposure graph and/or Microsoft Security Exposure Management. Only the latest data snapshot received from Microsoft products is retained; we do not store historical data.

Some enterprise exposure graph and/or Microsoft Security Exposure Management experiences data is available for querying via Advanced Hunting and is subject to Advanced Hunting service limitations.

We reserve the right to modify some or all of these parameters in the future, including:

- Data ingestion frequency and freshness: We might increase the current 72-hour latency (decrease the frequency of data ingestion) for some or all Microsoft data sources.
- Data retention period: We might decrease the current 14-day data retention period.
- Service features and functionality: We might alter, limit, or discontinue specific features, capabilities, or functionalities of the service built on top of the enterprise exposure graph and/or Microsoft Security Exposure Management data.
- Data query limits: We might impose limitations on the number, frequency, or type of data queries that can be performed against enterprise exposure graph or Microsoft Security Exposure Management data.

We will make reasonable efforts to provide advance notice of any significant changes to the service. However, you acknowledge and agree that you are solely responsible for monitoring any such notifications.

## Getting support

To get support, select the Help question mark icon in the Microsoft Security toolbar.

![Screenshot of the Microsoft Defender security portal Help button in the portal header bar.](media/microsoft-defender-portal-header.png)

You can also engage with the [Microsoft Tech community](https://techcommunity.microsoft.com/).