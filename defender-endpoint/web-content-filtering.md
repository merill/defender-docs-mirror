---
layout: Conceptual
title: Web content filtering in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/web-content-filtering
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use web content filtering in Microsoft Defender for Endpoint to track and regulate access to websites based on their content categories.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.reviewer: ericlaw
ms.localizationpriority: medium
ms.date: 2026-09-21T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
- mde-asr
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1015
ms.topic: how-to
ms.subservice: asr
ai-usage: ai-assisted
locale: en-us
document_id: a49219ec-b35a-6411-30d5-fb91ec78dbd2
document_version_independent_id: a49219ec-b35a-6411-30d5-fb91ec78dbd2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/web-content-filtering.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: web-content-filtering
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/web-content-filtering.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: 3f38cb39-c23f-f0bd-0c83-859859de86a3
---

# Web content filtering in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Web content filtering is part of [web protection](web-protection-overview) in Microsoft Defender for Endpoint and Microsoft Defender for Business. Use web content filtering to track and regulate access to websites based on their content categories. Websites that aren't malicious might still be unsuitable because of compliance requirements, bandwidth usage, or other concerns.

Web content filtering provides the following benefits:

- Block access to website categories on managed devices, whether users are on your network or away.
- Review blocks and web usage in centralized reports.
- In Defender for Endpoint, assign different policies to [device groups](rbac).
- In Defender for Business, define one web content filtering policy that applies to all users.

Configure policies for device groups to block selected categories. Blocking a category prevents users on devices in those groups from accessing URLs associated with the category. URLs in categories that you don't block are audited. Users can access audited URLs without disruption, and you can use the access statistics to make informed policy decisions. Users receive a notification when a webpage tries to load a blocked resource.

On Windows, Microsoft Defender SmartScreen enforces web content filtering in Microsoft Edge and in Internet Explorer 11 on operating systems where it remains supported. Network protection enforces web content filtering in Google Chrome, Mozilla Firefox, Brave, and Opera. On macOS and Linux, network protection enforces web content filtering in supported browsers. For all requirements, see Prerequisites.

## Prerequisites

Make sure your environment meets the following requirements:

- **Subscription**: Your subscription must include one of the following plans:
    - [Windows 10/11 Enterprise E5](/en-us/windows/deployment/deploy-enterprise-licenses)
    - [Microsoft 365 E5](https://www.microsoft.com/microsoft-365/enterprise/e5?activetab=pivot%3aoverviewtab)
    - Microsoft 365 A5
    - Microsoft Defender Suite
    - [Microsoft 365 E3](https://www.microsoft.com/microsoft-365/enterprise/e3?activetab=pivot%3aoverviewtab)
    - [Microsoft Defender for Endpoint Plan 1 or Plan 2](/en-us/defender-xdr/eval-defender-endpoint-overview)
    - [Microsoft Defender for Business](/en-us/defender-business/mdb-overview)
    - [Microsoft 365 Business Premium](https://www.microsoft.com/microsoft-365/business/microsoft-365-business-premium)
- **Portal access and permissions**: You must have access to the [Microsoft Defender portal](https://security.microsoft.com)and permissions for the tasks you perform:
    - [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac):
        - View policies and reports: **Security operations \ Security data \ Security data basics (read)**.
        - Create, update, or delete policies and allow indicators: **Security operations \ Security data \ Response (manage)**.
        - Turn on web content filtering: **Authorization and settings \ Security settings \ Core security settings (manage)**.
    - [Defender for Endpoint RBAC](user-roles), for organizations that haven't enabled unified RBAC:
        - View policies and reports: **View data \ Security operations**.
        - Create, update, or delete policies and allow indicators: **Active remediation actions \ Security operations**.
        - Turn on web content filtering: **Manage security settings in Security Center**.
    - Assign the role to the device groups that the administrator manages.
- **Operating system**: Devices must run one of the following operating systems:
    - Windows 11, Windows 10 version 1607 (August 2016) or later, or Windows Server 2019 or later, with the [latest Microsoft Defender Antivirus updates](microsoft-defender-antivirus-updates)
    - A macOS version supported by [network protection for macOS](network-protection-macos)
    - A Linux version supported by [network protection for Linux](network-protection-linux)
- **Browser**: Devices must use Microsoft Edge, Google Chrome, Mozilla Firefox, Brave, or Opera. Internet Explorer 11 is supported only on operating systems where it remains a supported Windows component.
- **Protection configuration**:
    - On Windows, enable [Microsoft Defender SmartScreen](/en-us/windows/security/operating-system-security/virus-and-threat-protection/microsoft-defender-smartscreen/) for Microsoft Edge.
    - On Windows, enable [network protection](network-protection) in block mode for supported non-Microsoft browsers.
    - On macOS and Linux, enable network protection in block mode for all supported browsers, including Microsoft Edge.

## Web content filtering data storage and privacy

For information about how Defender for Endpoint stores, processes, and protects web content filtering data, see [Microsoft Defender for Endpoint data storage and privacy](data-storage-privacy).

## Precedence for multiple active policies

Applying multiple different web content filtering policies to the same device results in applying the more restrictive policy for each category. Consider the following scenario:

- **Policy 1**: blocks categories 1 and 2 and audits the rest
- **Policy 2**: blocks categories 3 and 4 and audits the rest

The result is that categories 1 through 4 are all blocked, as illustrated in the following diagram:

![Diagram showing block mode taking precedence over audit mode for web content filtering policies.](media/web-content-filtering-policies-mode-precedence.png)

## Turn on web content filtering

On the **Optional features** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/integration, verify the **Web content filtering** setting is ![](media/toggle-on.png)**On**. If necessary, slide the toggle to ![](media/toggle-on.png)**On**, and then select **Save preferences**.

## Create a web content filtering policy

Web content filtering policies specify which of the following parent and child categories to block for each device group:

- **Adult content**:
    - **Cults**: Sites related to groups or movements whose members demonstrate passion for a belief system different from commonly accepted beliefs.
    - **Gambling**: Online gambling and sites that promote gambling.
    - **Nudity**: Sites that provide full-frontal or partially nude images or videos, typically in an artistic form, and might allow the download or sale of these materials.
    - **Pornography/Sexually explicit**: Sites that contain sexually explicit content or other sexually oriented material.
    - **Sex education**: Sites that discuss sex and sexuality, including human reproduction, contraception, prevention of sexually transmitted infections, and sexual health.
    - **Tasteless**: Sites with content that might be unsuitable for children or inappropriate in a workplace but isn't necessarily violent or pornographic.
    - **Violence**: Sites that display or promote violence against humans or animals.
- **High bandwidth**:
    - **Download sites**: Sites whose primary purpose is downloading media or software.
    - **Image sharing**: Sites primarily used to find or share photos, including sites with social features.
    - **Peer-to-peer**: Sites that host peer-to-peer (P2P) software or facilitate P2P file sharing.
    - **Streaming media & downloads**: Sites primarily used to distribute, find, watch, or listen to streaming media.
- **Legal liability**:
    - **Child abuse images**: Sites that include child abuse content.
    - **Criminal activity**: Sites that instruct, advise on, or promote illegal activities.
    - **Hacking**: Sites that provide resources for illegal or questionable uses of software or hardware, including cracked copyrighted material.
    - **Hate & intolerance**: Sites that promote aggressive, degrading, or abusive opinions about groups identified by characteristics such as race, religion, gender, age, nationality, disability, economic situation, sexual orientation, or lifestyle.
    - **Illegal drug**: Sites that sell illegal or controlled substances, promote substance abuse, or sell related paraphernalia.
    - **Illegal software**: Sites that contain or promote malware, spyware, botnets, phishing scams, piracy, or copyright theft.
    - **School cheating**: Sites related to plagiarism or school cheating.
    - **Self-harm**: Sites that promote self-harm, including cyberbullying sites that contain abusive or threatening messages.
    - **Weapons**: Sites that sell weapons or advocate their use, including guns, knives, and ammunition.
- **Leisure**:
    - **Chat**: Sites primarily used as web-based chat rooms.
    - **Games**: Sites related to video or computer games, including sites that host games or provide gaming information.
    - **Instant messaging**: Sites used to download or access instant messaging software.
    - **Professional network**: Sites that provide professional networking services.
    - **Social networking**: Sites that provide social networking services.
    - **Web-based email**: Sites that provide web-based email services.
- **Uncategorized**:
    - **Newly registered domains**: Sites registered in the past 30 days that haven't been assigned to another category.
    - **Parked domains**: Sites that have no content or are reserved for later use.

Note

**Uncategorized** contains only newly registered domains and parked domains. It doesn't include every site that falls outside the other categories.

*Remote proxy sites* are categorized as **Illegal software** because they can route traffic to any destination, including unwanted, malicious, or illegal content. To override a category block for a specific site, create an allow indicator.

### Create a policy

Note

- There might be up to 2 hours of latency between the time a policy is created and when it's enforced on the device.
- You can deploy a policy without selecting any categories to block. This action creates an audit-only policy to help you understand user behavior before creating a block policy.
- If you're removing a policy or changing device groups at the same time, there could be a delay in policy deployment.
- Blocking the **Uncategorized** category could lead to unexpected and undesired results.

To create a web content filtering policy, follow these steps:

1. On the **Web content filtering** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/web_content_filtering_policy, select ![](media/defender-portal-icon-create.png)**Add policy**.
2. The **Add policy** wizard opens. On the **General** page, specify a unique, descriptive name for the policy, and then select **Next**.
3. On the **Blocked categories** page, select one or more web content categories to block, and then select **Next**.
4. On the **Scope** page, select the device groups to which the policy applies. The default value for **Machine groups** is **Select all**. Select **Next**.

    Tip

    If you're using Microsoft 365 Business Premium or Microsoft Defender for Business, the web content filtering policy is applied to all users by default. Scoping doesn't apply.
5. On the **Summary** page, review your settings. Select **Back** to make changes, or select **Submit** to create the policy.

## End-user experience

In supported non-Microsoft browsers, network protection displays a system notification when it blocks a connection. Microsoft Edge provides an in-browser block page.

Beginning with Microsoft Edge version 124, the following page appears for all web content filtering blocks.

[![Screenshot of notification that content is blocked.](media/wcf-content-blocked.jpg)](media/wcf-content-blocked.jpg#lightbox)

### Allow specific websites

To override a web content filtering category block for a specific site, create a [custom allow indicator](indicator-ip-domain). Allow indicators take precedence over web content filtering policies.

To define an allow indicator, follow these steps:

1. On the **Indicators** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/custom_ti_indicators, select the **URLs/Domains** tab, and then select ![](media/defender-portal-icon-create.png)**Add item**.
2. The **Add indicator** wizard opens. On the **Indicator** tab, enter the following information:

    - **URL/Domain**
    - **Title**: Enter a unique, descriptive name.
    - **Expires on (UTC)**: Select **Never** (default) or **Custom** to enter an expiration date.

    In the **Statistics** section, you can select **Show statistics** to understand the effects of adding this custom indicator.

    When you're finished on the **Indicator** page, select **Next**.
3. On the **Action** page, select **Allow**, and then select **Next**.
4. On the **Organizational scope** page, select a device group scope. The default value is **All devices in my organization**. Select **Next**.
5. On the **Summary** page, review your settings. Select **Back** to make changes, or select **Submit** to create the indicator.

### Dispute categories

If you encounter a domain that has been incorrectly categorized, you can dispute the category directly in the Microsoft Defender portal.

On the **Web protection** page in the Microsoft Defender portal at https://security.microsoft.com/reports/webprotection, select **Web content filtering categories details**, and then select the **Domains** tab. Find the domain, select the ellipsis (**...**), and then select **Dispute category**.

In the pane that opens, select the priority and provide details, such as the suggested category. Select **Submit**. Microsoft reviews the request within one business day. To unblock the domain while the request is reviewed, create a [custom allow indicator](indicator-ip-domain).

## Monitor web content filtering reports

On the **Web protection** page in the Microsoft Defender portal at https://security.microsoft.com/reports/webprotection, review the cards for web content filtering and web threat protection. The following cards summarize web content filtering activity.

### Web activity by category

The **Web activity by category** card lists the parent categories with the largest increase or decrease in access attempts. Review activity for the last 30 days, 3 months, or 6 months. Select a category to view details.

In the first 30 days of using web content filtering, your organization might not have enough data to display the Web activity by category card.

[![Screenshot of the Web activity by category card showing category access trends.](media/web-activity-by-category600.png)](media/web-activity-by-category600.png#lightbox)

### Web content filtering summary card

The **Web content filtering summary** card displays the distribution of blocked access attempts across the different parent web content categories. Select one of the colored bars to view more information about a specific parent web category.

[![Screenshot of the Web content filtering summary card showing blocked access attempts by category.](media/web-content-filtering-summary.png)](media/web-content-filtering-summary.png#lightbox)

### Web activity summary card

The **Web activity summary** card displays the total number of requests for web content across all URLs.

[![Screenshot of the Web activity summary card showing total requests for web content.](media/web-activity-summary.png)](media/web-activity-summary.png#lightbox)

### View card details

To open **Report details** for a card, select a table row or a bar in the chart. The details include statistics for web content categories, domains, and device groups.

[![Screenshot of Web protection report details showing web categories, domains, and device groups.](media/web-protection-report-details.png)](media/web-protection-report-details.png#lightbox)

- **Web categories**: Lists the web content categories that have had access attempts in your organization. Select a specific category to open a summary flyout.
- **Domains**: Lists the web domains that have been accessed or blocked in your organization.
- **Device groups**: Lists all device groups that generated web activity in your organization.

Use the time range filter at the top left of the page to select a time period. You can also filter the information or customize the columns. Select a row to open a flyout pane with even more information about the selected item.

## Known issues and limitations

- Web content filtering identifies supported browsers by process name. It doesn't work when a local proxy application, such as Fiddler, masks the originating process name. Web content filtering also doesn't work in isolated browser sessions, such as Microsoft Defender Application Guard.
- Web content filtering uses network protection in non-Microsoft browsers. Blocking in these browsers requires the [browser configuration for content inspection](network-protection#required-browser-configuration). For HTTPS traffic, full URL paths can be blocked only in Microsoft Edge. To block certain web applications in other browsers, you might need to create a custom block indicator for the application's sign-in domain. The indicator might also block other services that use the same domain.
- Web content filtering classifies billions of URLs, but new sites might not be categorized immediately. A site's content and category can also change. For more control over access to a site, create a custom indicator to allow or block it.
- If you use Microsoft 365 Business Premium or Microsoft Defender for Business, you can define only one web content filtering policy for your environment.