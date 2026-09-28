---
layout: Conceptual
title: Guide to build and publish Microsoft Sentinel SIEM solutions | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/isv/sentinel-integration-guide
breadcrumb_path: ../breadcrumb/toc.json
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
description: This article walks you through the entire lifecycle of how to build and publish solutions to Microsoft Sentinel.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: jesko
ms.topic: concept-article
ms.date: 2026-06-29T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: fa6e0697-1566-04ac-bd21-a6c5129cfd34
document_version_independent_id: 37ed03f9-6382-d86d-e677-e636e5075c96
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/isv/sentinel-integration-guide.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/isv/sentinel-integration-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/isv/sentinel-integration-guide.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: d582e4e9-6c2c-b495-d91b-1c3eedab4cec
---

# Guide to build and publish Microsoft Sentinel SIEM solutions | Microsoft Learn

Microsoft Sentinel SIEM includes a range of capabilities that partners can use to create impactful solutions they can publish through Sentinel SIEM Content Hub. By building on top of Sentinel, partners can enable new scenarios that use security data and analytics capabilities to help customers detect and respond to threats.

This article provides an overview of the lifecycle of building and publishing Microsoft Sentinel SIEM solutions, from learning about Sentinel and planning your solution, to building, testing, and publishing it to customers. Each section includes links to more detailed documentation to help you through each step of the process.

[![Diagram that shows high-level phases for the Microsoft Sentinel SIEM solution lifecycle from learn through go-to-market.](media/sentinel-integration-guide/sentinel-integration-timeline.png)](media/sentinel-integration-guide/sentinel-integration-timeline.png#lightbox)

## Prerequisites

Before you create and publish a SIEM solution to Azure Commercial Marketplace, join the Microsoft Cloud Partner Program and create an account in Partner Center. See the following resources for more information:

- Join the [Microsoft Cloud Partner Program](https://partner.microsoft.com/).
- Create a [Commercial Marketplace account](/en-us/partner-center/marketplace/create-account) in Partner Center.

## Learn about Microsoft Sentinel

To get started, learn about Microsoft Sentinel, identify the data and functionality you want to create, and find the resources to help you learn about the different capabilities that will help you build solutions that keep your customers secure.

| Step | Description |
| --- | --- |
| **Learn about Sentinel** | Microsoft Sentinel SIEM is a scalable, cloud-native security information and event management (SIEM) application that delivers an intelligent and comprehensive solution for SIEM and security orchestration, automation, and response (SOAR). It provides cyberthreat detection, investigation, response, and proactive hunting, with a bird's-eye view across your enterprise. For more information, see:[What is Microsoft Sentinel?](/en-us/azure/sentinel/overview) |
| **Identify what to build** | The most important step to a successful integration is deciding which types of content to include in your solution. Explore the following resources to understand Microsoft Sentinel.  For more information, see:[Technology Integration Scenarios with Microsoft Sentinel](siem-components-to-include)[Building Microsoft Sentinel Integrations - Part 1: Onboarding](https://www.youtube.com/watch?v=eK5bmKhy2iI)[Decide which components to include in your solution](siem-components-to-include) |
| **Review the docs** | There's a rich collection of documentation to support with your journey. Here are some key resources to get you started.  For more information, see:[Guide to understand Microsoft Sentinel solution repository in GitHub](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions)[Guide to understand ASIM (Advanced Security Information Model) Schema](/en-us/azure/sentinel/normalization-content)[Guide to understand Kusto query language](/en-us/archive/blogs/msdn/ben/getting-started-with-the-kusto-query-language) |
| **Become a Cloud Partner and create a Publisher Account** | Microsoft Sentinel solutions are published on the Azure Commercial Marketplace. To publish to the marketplace, join the cloud partner program.  For more information, see:[Guide to understand Microsoft commercial marketplace](/en-us/partner-center/marketplace-offers/overview)[Guide to create a commercial marketplace account in Microsoft Partner Center](/en-us/partner-center/account-settings/create-account)[Join ISV Success program](https://www.microsoft.com/isv/offer-benefits)[Sign up for Microsoft for Startups program, if applicable](https://www.microsoft.com/startups) |

## Build your solution

Once you have a good understanding of Microsoft Sentinel and the solution you want to building, follow these steps:

| Step | Description |
| --- | --- |
| **Provisioning environment** | To help you get started with building and testing your solution, we recommend you sign up for an Azure Free Trial and a Microsoft Sentinel Free Trial.  For more information, see:[Sign up for an Azure Free Trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)[Then sign up for a Microsoft Sentinel Free Trial (Scroll down to 'Free trial')](https://azure.microsoft.com/pricing/details/microsoft-sentinel/) |
| **Complete the training lab** | We highly recommend the training lab to get fully ramped up with Microsoft Sentinel. This lab provides hands-on practical experience for product features, capabilities, and scenarios.  For more information, see:[Complete the Microsoft Sentinel Training Lab](/en-us/azure/sentinel/skill-up-resources) |
| **Build a connector** | Microsoft Sentinel is built on data. Most solutions start with bringing the data from a customer's environment into Microsoft Sentinel. To understand how to build a connector, refer to the following resources.  For more information, see:[Develop a SIEM solution for Microsoft Sentinel](develop-siem-solutions-overview)[Build custom connectors with AI in Microsoft Sentinel](create-custom-connector-builder-agent)[Create a pull codeless connector for Microsoft Sentinel](create-codeless-connector)[Webinar: Creating Data Connectors](https://www.youtube.com/watch?v=wXCh17rgtLU) |
| **Build your SIEM content** | In addition to data, your solution can offer a rich array of other components to help customers get the most out of your data. For example, you can offer detections, workbooks, playbooks, and hunting queries to make your offering readily usable by customers.  For more information, see:[Microsoft Sentinel components and patterns](siem-components-to-include) |
| **Security, privacy and compliance** | For details on Secure Future Initiative (SFI) requirements, see https://aka.ms/securefutureinitiativeFollow the Security Development Lifecycle (SDL) practices for:- Threat modeling- Secure configuration- Dependency hygiene- Penetration testing in coordination with your security team - Use only approved tools for vulnerability tracking and patch management. For more information, see [Microsoft Security Development Lifecycle](https://www.microsoft.com/securityengineering/sdl/) |

## Test your solution

Once the solution is built you need to package and test your solution. Once you have tested you will validate your solution locally and then submit a pull request (PR), address feedback as needed, and have your PR approved and merged.

| Step | Description |
| --- | --- |
| **Package and test your SIEM solution** | Once your solution is built, package it and test it to ensure that it meets SIEM solution quality standards and is ready for publishing. For more information, see [Develop a SIEM solution for Microsoft Sentinel](develop-siem-solutions-overview) and [Microsoft Sentinel SIEM solution quality guidelines](sentinel-siem-solution-quality-guidance). |
| **Run local validation** | Run validation scripts against your packaged solution to check whether your solution passes CI validation checks before you submit a PR. For more information, see [Local validation scripts](https://github.com/Azure/Azure-Sentinel/tree/master/.script/local-validation). |
| **Open a GitHub pull request** | Raise a pull request (PR) in the Microsoft Sentinel solutions repository so the Microsoft Sentinel engineering staff can review it and provide feedback. |
| **Resolve technical feedback, merge PR, and generate package** | The Microsoft Sentinel engineering staff reviews your solution and provides feedback. After you address all technical feedback, the engineering staff merges the pull request into the main branch and generates the final package that you submit with your offer. For more information, see [Develop SIEM solutions](develop-siem-solutions-overview). |

## Publish

Once your solution is built, tested, and certified, you can publish it to the Azure Commercial Marketplace. This section provides guidance on how to publish your solution.

| Step | Description |
| --- | --- |
| **Create an offer** | Once you have a solution package, you're ready to create an offer in the Security Store or Marketplace.  For more information, see:[Publish Solutions to Microsoft Sentinel](/en-us/azure/sentinel/publish-sentinel-solutions) |
| **Test Offer Preview** | We create a version of your offer that is accessible only to the preview audience you specified. Creating a preview offer ensures that specific audiences test your solution before your solution is broadly shared with all customers. We recommend keeping your solution in preview for at least four weeks to gather feedback from customers and address any issues that arise.  For more information, see:[Microsoft Sentinel Solution Lifecycle in Partner Center](sentinel-solutions-post-publish-tracking) |
| **Fix certification issues** | Offers submitted to the commercial marketplace must be certified before being published. If your offer fails any of the checks or if you aren't eligible to submit an offer of that type, a certification failure report is sent to your email address. The errors also show up within Action Center in Partner Center. For more information, see [Certification issues](sentinel-solutions-post-publish-tracking#certification). After the issues are fixed, you can resubmit the offer for certification. This triggers the review process again and once the offer passes certification. Your solution is published to the marketplace and available for customers in Microsoft Sentinel content hub within two working days. |
| **Make the offer broadly available** | Ensure that you validate all aspects of your solution in the test offer preview phase before you make the offer live.For more information, see:[Publisher approval](sentinel-solutions-post-publish-tracking#publisher-approval) |

## Go to Market (GTM)

After your solution is in preview for at least four weeks and you address any issues that customers encounter, you can make your solution generally available to all customers.

| Step | Description |
| --- | --- |
| **Remove preview flag** | After the preview period, you can remove the preview flag from your offer to make it generally available to all customers. |
| **Listen for customer feedback** | Continue to monitor feedback and support requests as your solution gains traction. |
| **Enhance solution** | Based on customer feedback, you might need to enhance your solution to meet customer needs. Customer feedback might require the addition of new features, improving performance, or addressing any issues that customers encounter. |

Microsoft offers the following programs to help partners approach Microsoft customers:

- [Microsoft Partner Network (MPN)](https://partner.microsoft.com/): The primary program for partnering with Microsoft is the Microsoft Partner Network. Membership in MPN is required to become an Azure Marketplace publisher, which is where all Microsoft Sentinel solutions are published.
- [Azure Marketplace](https://azure.microsoft.com/marketplace/): Microsoft Sentinel solutions are delivered via Azure Marketplace, where customers discover and deploy both Microsoft and partner-supplied Azure integrations.

    Microsoft Sentinel solutions are one of many types of offers found in Marketplace. You can also find solution offerings embedded in [Microsoft Sentinel content hub](../sentinel-solutions-catalog).
- [Microsoft Intelligent Security Association (MISA)](https://www.microsoft.com/security/partnerships/intelligent-security-association). MISA helps Microsoft Security partners create awareness about partner-created integrations with Microsoft customers and improve discoverability for Microsoft Security product integrations.

    Joining the MISA program requires a nomination from a participating Microsoft Security product team. Building any of the following integrations can qualify partners for nomination:

    - A Microsoft Sentinel data connector and associated content, such as workbooks, sample queries, and analytics rules.
    - Published Logic Apps connector and Microsoft Sentinel playbooks.
    - API integrations, on a case-by-case basis.

To request a MISA nomination review or ask questions, contact `AzureSentinelPartner@microsoft.com`.