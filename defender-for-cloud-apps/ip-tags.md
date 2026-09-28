---
layout: Conceptual
title: Work with IP ranges and tags - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/ip-tags
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Learn how to define IP address ranges, assign categories and custom tags, use built-in cloud and threat-intelligence tags, and override geolocation data in Microsoft Defender for Cloud Apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 033975a6-7c48-d479-8de9-70515e4a029e
document_version_independent_id: 033975a6-7c48-d479-8de9-70515e4a029e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/ip-tags.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ip-tags
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/ip-tags.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 776ed3a8-6b22-3272-5cf7-d081e1112cf8
---

# Work with IP ranges and tags - Microsoft Defender for Cloud Apps | Microsoft Learn

To easily identify known IP addresses, such as your physical office IP addresses, you need to set IP address ranges. IP address ranges allow you to tag, categorize, and customize the way logs and alerts are displayed and investigated. Each group of IP ranges can be categorized based on a preset list of IP categories. You're also able to create custom IP tags for your IP ranges. Additionally, you can override public geolocation information based on your internal network knowledge. Both IPv4 and IPv6 are supported.

Defender for Cloud Apps comes preconfigured with built-in IP ranges for popular cloud providers such as Azure and Microsoft 365. Additionally, we have built-in tagging based on Microsoft threat intelligence including anonymous proxy, Botnet, and Tor. You can see the full list of built-in IP tags in the drop-down on the IP address ranges page.

Note

- To use these built-in tags as part of a search, refer to the tag IDs in the Defender for Cloud Apps API documentation.
- You can add IP ranges in bulk by creating a script using the [IP address ranges API](api-data-enrichment).
- You can't add IP ranges with overlapping IP addresses.
- To view the API documentation, go to [API documentation](api-introduction).

Built-in IP address tags and custom IP tags are considered hierarchically. Custom IP tags take precedence over built-in IP tags. For instance, if an IP address is tagged as **Risky** based on threat intelligence but there's a custom IP tag that identifies it as **Corporate**, the custom category and tags take precedence.

## Create an IP address range

In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **System**, select **IP address ranges**. Select **Add IP address range** to add IP address ranges and set the following fields:

1. **Name** your IP range. The name doesn't appear in the activities log. It's only used to manage your IP range.
2. Enter each **IP address range** you want to configure. You can add as many IP addresses and subnets as you want using network prefix notation (also known as CIDR notation), for example 192.168.1.0/32 for IPv4 or 2001:db8::/32 for IPv6.
3. **Categories** are used to easily recognize activities from important IP addresses in your logs and alerts. Categories are available in the portal. However, they typically require user configuration to determine which IP addresses are included in each category. The exception to this configuration is the **Risky** category, which includes three IP tags: Anonymous proxy, Botnet, and Tor.

    The following categories are available:

    - **Administrative**: These IPs should be all the IP addresses used by your admins.
    - **Cloud provider**: These IPs should be the IP addresses used by your cloud provider. Apply this category if your cloud provider isn't automatically identified.
    - **Corporate**: These IPs should be all the public IP addresses of your internal network, your branch offices, and your Wi-Fi roaming addresses.
    - **Risky**: These IPs should be any IP addresses that you consider risky. They can include suspicious IP addresses you've seen in the past, IP addresses in your competitors' networks, and so on. It is suggested to be cautious with applying automatic governance actions only based on risky IP, since there are some cases when IPs that serve malicious actors are also being in use by legitimate employees, hence our recommendation is to examine each case by itself.
    - **VPN**: These IPs should be any IP addresses you use for remote workers. By using this category, you can avoid raising [impossible travel](anomaly-detection-policy#impossible-travel) alerts when employees connect from their home locations via the corporate VPN.

    To include the IP range in a category, select a category from the **Categories** drop-down menu.
4. To **Tag** the activities from these IP addresses enter a tag. Entering a word into the box creates the tag. After you create a tag, you can add that tag to additional IP ranges by selecting the tag from the existing tags list. You can add more than one IP tag for each range. IP tags can be used when building policies. Along with IP tags you configure, Defender for Cloud Apps has built-in tags that aren't configurable. You can see the list of built-in IP tags under the [IP tags filter](activity-filters#ip-address-insights).

    Note

    - IP tags are added to the activity without overriding data.
    - Multiple tags can be applied on the same IP range.
5. To **Override registered ISP** or **Override the location** or for these addresses, select the relevant checkbox. For example, if you have an IP address that is considered publicly to be in Ireland, but you know the IP is in the US. You'll override the location for that IP address range. Or if you don't want an IP address range to be associated with a registered ISP, you can override the registered ISP.
6. When you're done, select **Create**.

    ![Screenshot showing the dialog to create a new IP address range in Defender for Cloud Apps.](media/newipaddress-range.png)