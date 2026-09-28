---
layout: Conceptual
title: View your Microsoft Defender Vulnerability Management dashboard in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-view-tvm-dashboard
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use your Microsoft Defender Vulnerability Management dashboard to see important items to address in Defender for Business.
author: chrisda
ms.author: chrisda
ms.topic: concept-article
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2025-09-11T00:00:00.0000000Z
ms.reviewer: nehabha
ms.collection:
- SMB
- m365-security
- tier1
ms.custom: intro-get-started
locale: en-us
document_id: 58a03fb4-1e1d-33ec-8526-468e2f305d96
document_version_independent_id: 58a03fb4-1e1d-33ec-8526-468e2f305d96
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-view-tvm-dashboard.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-view-tvm-dashboard
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-view-tvm-dashboard.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: cade0aef-4965-b19f-3f08-e0f5e73ad459
---

# View your Microsoft Defender Vulnerability Management dashboard in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

Defender for Business includes a vulnerability management dashboard that is designed to save your security team time and effort. In addition to providing an exposure score, that dashboard enables you to view information about exposed devices and see relevant security recommendations. You can use your Defender Vulnerability Management dashboard to:

- View your exposure score, which is associated with devices in your company.
- View your top security recommendations. For example:
    - Address impaired communications with devices.
    - Turn on firewall protection.
    - Update Microsoft Defender Antivirus definitions.
- View remediation activities, such as any files that were sent to quarantine, or vulnerabilities found on devices.

## Vulnerability management features and capabilities

Vulnerability management features and capabilities in Microsoft Defender for Business include:

- **Dashboard**: Provides information about vulnerabilities, exposure, and recommendations. You can see recent remediation activities, exposed devices, and ways to improve your company's overall security. Each card in the dashboard includes a link to more detailed information or to a page where you can take a recommended action.

    [![Screenshot of Microsoft Defender Vulnerability Management Dashboard.](media/mdb-mdvm-dashboard.png)](media/mdb-mdvm-dashboard.png#lightbox)
- **Recommendations**: Lists current security recommendations and related threat information to review and consider. When you select an item in the list, a flyout panel opens with more details about threats and actions you can take.
- **Remediation**: Lists any remediation actions and their status. Remediation activities can include sending a file to quarantine, stopping a process from running, and blocking a detected threat from running. Remediation activities can also include updating a device, running an antivirus scan, and more.

    [![Screenshot of Microsoft Defender Vulnerability Management-Remediation.](media/mdb-mdvm-remediation.png)](media/mdb-mdvm-remediation.png#lightbox)
- **Inventories**: Lists software and apps currently in use in your organization. You see browsers, operating systems, and other software on devices, along with identified weaknesses and threats.
- **Weaknesses**: Lists vulnerabilities along with the number of exposed devices in your organization. If you see "0" in the Exposed devices column, you don't have to take any immediate action. However, you can learn more about each vulnerability listed on this page. Select an item to learn more about it and what you can do to mitigate the potential threat to your company.

    [![Screenshot of Microsoft Defender Vulnerability Management-Weaknesses.](media/mdb-mdvm-weakness-details.png)](media/mdb-mdvm-weakness-details.png#lightbox)
- **Event timeline**: Lists vulnerabilities that affect your organization in a timeline view.

[Learn more about Microsoft Defender Vulnerability Management](/en-us/defender-vulnerability-management/defender-vulnerability-management).