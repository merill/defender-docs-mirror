---
layout: Conceptual
title: Microsoft Sentinel Content and Solutions Overview | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sentinel-solutions
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Discover Microsoft Sentinel content and solutions, including data connectors and analysis tools, to enhance your security operations. Learn more today.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: tbeerthuis
ms.topic: overview
ms.date: 2025-05-27T00:00:00.0000000Z
locale: en-us
document_id: 3f45082a-fa8f-d565-f244-604baf93264d
document_version_independent_id: f3951f94-0fe6-1868-784e-e2a39652ce4c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sentinel-solutions.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/sentinel-solutions
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sentinel-solutions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 65788f9c-b73a-ded5-3900-5d656e6f8539
---

# Microsoft Sentinel Content and Solutions Overview | Microsoft Learn

Microsoft Sentinel content includes Security Information and Event Management (SIEM) solution components that help you ingest data, monitor, alert, and respond to security threats. This article explains the types of content and solutions in Microsoft Sentinel and how they help your security operations.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Supported content

Content is available in the Microsoft Sentinel **Content hub**, and includes the following types:

| Content type | Description |
| --- | --- |
| **[Analytics rules](detect-threats-built-in)** | Create alerts that point to relevant SOC actions through incidents. |
| **[Data connectors](connect-data-sources)** | Ingest logs from different sources into Microsoft Sentinel. |
| **[Hunting queries](hunting)** | Help SOC teams proactively hunt for threats in Microsoft Sentinel. |
| **[Parsers](normalization-about-parsers)** | Format and transform logs into [Advanced Security Information Model (ASIM)](normalization) formats for use across different content types and scenarios. |
| **[Playbooks and Azure Logic Apps custom connectors](automate-responses-with-playbooks)** | Automate investigation, remediation, and response scenarios in Microsoft Sentinel. |
| **[Watchlists](watchlists)** | Ingest specific data for better threat detection and less alert fatigue. |
| **[Workbooks](get-visibility)** | Monitor, visualize, and interact with data in Microsoft Sentinel to see meaningful insights. |
| **[Summary rule templates](summary-rules#deploy-pre-built-summary-rule-templates)** | Deploy tested, prebuilt rules that optimize costs and improve query performance by aggregating insights from incoming verbose logs. |

The **Content hub** delivers these content types as *solutions* and *standalone* items. *Solutions* are packages of Microsoft Sentinel content or Microsoft Sentinel API integrations that support an end-to-end product, domain, or industry vertical scenario in Microsoft Sentinel.

Customize out-of-the-box (OOTB) content for your needs, or create your own solution to share with others in the community. For more information, see the [Microsoft Sentinel Solutions Build Guide](https://aka.ms/sentinelsolutionsbuildguide) for authoring and publishing solutions.

## Discover and manage content in Microsoft Sentinel

Use the Microsoft Sentinel **Content hub** to centrally find and install out-of-the-box (OOTB) content.

The Microsoft Sentinel **Content hub** lets you find content in the product, deploy it in a single step, and enable end-to-end product, domain, or vertical OOTB solutions and content in Microsoft Sentinel.

- Filter by categories and other parameters, or use text search, to find the content that works best for your organization.

    The **Content hub** also shows the support model for each piece of content. Some content is maintained by Microsoft, and others are maintained by partners or the community.
- Manage updates for out-of-the-box content in the **Content hub**. For custom content, manage updates from the **Repositories** page. For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy).
- Customize out-of-the-box content for your needs, or create custom content, including analytics rules, hunting queries, workbooks, and more.

    Manage your custom content directly in your Microsoft Sentinel workspace by using the Microsoft Sentinel API or from your source control repository. For more information, see [Microsoft Sentinel API](/en-us/rest/api/securityinsights/) and [Deploy custom content from your repository](ci-cd).

### Why use Microsoft Sentinel solutions?

Microsoft Sentinel solutions are packaged integrations that deliver end-to-end product value for one or more domains or vertical scenarios in the **Content hub**.

The solutions experience, powered by [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace), helps you find and deploy the content you want. For more information about authoring and publishing solutions in the Azure Marketplace, see the [Microsoft Sentinel Solutions Build Guide](https://aka.ms/sentinelsolutionsbuildguide).

- **Packaged content** is a collection of one or more components of Microsoft Sentinel content.
- **Integrations** include services or tools built using Microsoft Sentinel or Azure Log Analytics APIs that support integrations between Azure and existing customer applications, or move data, queries, and more from those applications into Microsoft Sentinel.

Use solutions to install packages of out-of-the-box (OOTB) content in a single step. The content is often ready to use immediately. Providers and partners use Sentinel solutions to add value to their customers' investments by delivering combined product, domain, or vertical value.

Use the **Content hub** to centrally find and deploy solutions and OOTB content based on your scenario.

For more information, see:

- [Centrally discover and deploy Microsoft Sentinel out-of-the-box content and solutions](sentinel-solutions-deploy)
- Microsoft Sentinel solutions catalog in the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps?filters=solution-templates&amp;page=1&amp;search=sentinel)
- [Microsoft Sentinel catalog](sentinel-solutions-catalog)

## Categories for Microsoft Sentinel out-of-the-box content and solutions

Microsoft Sentinel out-of-the-box content fits into one or more of these categories. In the **Content hub**, select the categories you want to view to change the content shown. You find community-delivered items in the **Content hub** as standalone content or solutions.

### Domain categories

| Category name | Description |
| --- | --- |
| **Application** | Web, server-based, SaaS, database, communications, or productivity service |
| **Cloud Provider** | Cloud service |
| **Cloud Security** | Cloud security service |
| **Compliance** | Compliance product, services, and protocols |
| **DevOps** | Development operations tools and services |
| **Identity** | Identity service providers and integrations |
| **Internet of Things (IoT)** | IoT, operational technology (OT) devices, and infrastructure, industrial control services |
| **IT Operations** | Products and services managing IT |
| **Migration** | Migration enablement products and services |
| **Networking** | Network products, services, and tools |
| **Platform** | Microsoft Sentinel generic or framework components, Cloud infrastructure, and platform |
| **Security** | General security products |
| **Security - 0-day Vulnerability** | Specialized solutions for zero-day vulnerability attacks |
| **Security - Automation (SOAR)** | Security automations, SOAR (Security Operations and Automated Responses), security operations, and incident response products and services. |
| **Security - Cloud Security** | CASB (Cloud Access Service Broker), CWPP (cloud workload protection platforms), CSPM (cloud security posture management), and other cloud security products and services |
| **Security - Information Protection** | Information protection and document protection products and services |
| **Security - Insider Threat** | Insider threat and user and entity behavioral analytics (UEBA) for security products and services |
| **Security - Network** | Security network devices, firewall, NDR (network detection and response), NIDP (network intrusion and detection prevention), and network packet capture |
| **Security - Others** | Other security products and services with no other clear category |
| **Security - Threat Intelligence** | Threat intelligence platforms, feeds, products, and services |
| **Security - Threat Protection** | Threat protection, email protection, extended detection and response (XDR), and endpoint protection products and services |
| **Security - Vulnerability Management** | Vulnerability management products and services |
| **Storage** | File stores and file sharing products and services |
| **Training and Tutorials** | Training, tutorials, and onboarding assets |
| **User Behavior (UEBA)** | User behavior analytics products and services |

### Industry vertical categories

| Category name | Description |
| --- | --- |
| **Aeronautics** | Products, services, and content specific for the aeronautics industry |
| **Education** | Products, services, and content specific for the education industry |
| **Finance** | Products, services, and content specific for the finance industry |
| **Healthcare** | Products, services, and content specific for the healthcare industry |
| **Manufacturing** | Products, services, and content specific for the manufacturing industry |
| **Retail** | Products, services, and content specific for the retail industry |
| **Software** | Products, services, and content specific for the software industry |

## Support models for Microsoft Sentinel out-of-the-box content and solutions

Microsoft and other organizations author Microsoft Sentinel out-of-the-box content and solutions. Each piece of out-of-the-box content or solution has one of the following support types:

| Support model | Description |
| --- | --- |
| **Microsoft-supported** | Applies to: - Content or solutions where Microsoft is the data provider, where relevant, and author.  - Some Microsoft-authored content or solutions for non-Microsoft data sources.  Microsoft supports and maintains content or solutions in this support model in accordance with [Microsoft Azure Support Plans](https://azure.microsoft.com/support/options/#overview). Partners or the community support content or solutions authored by any party other than Microsoft. |
| **Partner-supported** | Applies to content or solutions authored by parties other than Microsoft.  The partner company provides support or maintenance for these pieces of content or solutions. The partner company can be an independent software vendor, a managed service provider (MSP or MSSP), a systems integrator (SI), or any organization whose contact information is provided on the Microsoft Sentinel page for the selected content or solutions. For any issues with a partner-supported solution, contact the specified support contact. |
| **Community-supported** | Applies to content or solutions authored by Microsoft or partner developers without listed contacts for support and maintenance in Microsoft Sentinel. For questions or issues with these solutions, [file an issue](https://github.com/Azure/Azure-Sentinel/issues/new/choose) in the [Microsoft Sentinel GitHub community](https://aka.ms/threathunters). |

## Content sources for Microsoft Sentinel content and solutions

Each piece of content or solution has one of the following content sources:

| Content source | Description |
| --- | --- |
| **Solution** | Solutions deployed by the **Content hub** that support lifecycle management. |
| **Standalone** | Standalone content deployed by the **Content hub** that is automatically kept up to date. |
| **Custom** | Content or solutions you customize in your workspace. |
| **Repositories** | Content or solutions from a repository connected to your workspace. |