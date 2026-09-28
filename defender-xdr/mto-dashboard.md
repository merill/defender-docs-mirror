---
layout: Conceptual
title: Vulnerability management in multitenant management - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/mto-dashboard
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the capabilities of the vulnerability management dashboard in multitenant management in Microsoft Defender XDR
ms.service: defender-xdr
author: guywi-ms
ms.author: guywild
ms.collection:
- m365-security
- highpri
- tier1
ms.topic: concept-article
ms.date: 2023-09-01T00:00:00.0000000Z
locale: en-us
document_id: 5a534235-dd43-80c7-494a-09adba00ddbd
document_version_independent_id: 5a534235-dd43-80c7-494a-09adba00ddbd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/mto-dashboard.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mto-dashboard
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/mto-dashboard.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 0b4ffc17-ddd3-4ed5-bcfd-0c6f71030cec
---

# Vulnerability management in multitenant management - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender XDR](/en-us/defender-xdr/microsoft-365-defender)

## Microsoft Defender Vulnerability Management dashboard

You can use the Defender Vulnerability Management dashboard in multi-tenant management to view aggregated and summarized information across all tenants, such as:

- Your exposure score and exposure level for devices across all tenants.
- Your most exposed tenants along with details of the number of weaknesses, exposed devices, and available recommendations for each tenant.

    [![Screenshot of the defender vulnerability management dashboard in multi-tenant management in Microsoft Defender XDR](media/mto-dashboard/mto-mdvm-dashboard.png)](media/mto-dashboard/mto-mdvm-dashboard.png#lightbox)

The Defender Vulnerability Management dashboard in multi-tenant management provides the following information across all the tenants you have access to:

| Area | Description |
| --- | --- |
| **Organization Exposure score** | See the current state of your organization's device exposure to threats and vulnerabilities across all tenants. |
| **Most exposed tenants** | Real time visibility into the tenants with the highest current exposure level. |
| **Tenants with the largest increase in exposure** | Identify tenants with the largest increase in exposure over the last 30 days. |
| **Device exposure distribution** | See how many devices are exposed based on their exposure level, across all tenants. Select a section in the doughnut chart to see the number of exposed devices at each level. |
| **Tenant exposure distribution** | View a summary of exposed tenants aggregated by exposure level. |

## Tenant vulnerability details

The **Tenants page** under **Vulnerability management** includes vulnerability information for all tenants, and at a tenant-specific level, such as exposed devices, security recommendations, weaknesses, and critical CVEs.

[![Screenshot of multi-tenant vulnerability management in Microsoft Defender XDR](media/mto-dashboard/mto-multi-tenant-view.png)](media/mto-dashboard/mto-multi-tenant-view.png#lightbox)

At the top of the page, you can view the number of tenants and the aggregate number of:

- Exposed devices
- Critical CVEs
- High severity CVEs
- Security recommendations

Select a tenant name to navigate to the Defender Vulnerability Management dashboard for that tenant in the [Microsoft Defender XDR](https://security.microsoft.com/machines) portal.

For more information, see [Microsoft Defender Vulnerability Management dashboard](/en-us/defender-vulnerability-management/tvm-dashboard-insights).