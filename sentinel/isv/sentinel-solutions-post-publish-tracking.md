---
layout: Conceptual
title: Microsoft Sentinel Solution Lifecycle in Partner Center | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/isv/sentinel-solutions-post-publish-tracking
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
description: Track your Microsoft Sentinel solution through each publishing phase in Partner Center—from automated validation to live availability in the content hub.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: rmoriarty
ms.topic: concept-article
ms.date: 2026-06-16T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1012
locale: en-us
document_id: 74a8994b-19be-f440-dad7-d656575065a4
document_version_independent_id: d37c124c-f241-cee2-b021-a24e121546a0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/isv/sentinel-solutions-post-publish-tracking.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/isv/sentinel-solutions-post-publish-tracking
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/isv/sentinel-solutions-post-publish-tracking.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: de5f1c21-de84-1f28-7fca-6e134a84acd3
---

# Microsoft Sentinel Solution Lifecycle in Partner Center | Microsoft Learn

After your Microsoft Sentinel solution is published, it goes through a series of validation checks before it becomes live in the Content Hub, Azure Marketplace, and Microsoft Security Store.

Note

Within Partner Center, your solution is referred to as an offer. The terms are used interchangeably in this article.

If you haven't created an offer yet, see [Publish solutions to Microsoft Sentinel](/en-us/azure/sentinel/publish-sentinel-solutions).

## Automated validation phase

The first step in the publishing process is a set of automated validations to ensure that the offer is set up correctly and can be provisioned successfully. This step can take 1–2 hours. Fix any issues before the offer proceeds to the next stage.

After the offer is published, Partner Center notifies the owner of your developer account by email. Notifications also appear under Action Center in Partner Center. You can also add users with a developer or manager role to receive notifications. For more information, see [Action Center Overview](/en-us/partner-center/action-center/action-center-overview) and [Notifications](/en-us/partner-center/marketplace-offers/review-publish-offer#notifications).

## Preview creation

During the preview creation phase, Partner Center creates a version of your offer that only the preview audience you specified can access. The preview version of your offer isn't available to anyone outside the preview audience until you make the offer live in the Publisher approval phase. Don't use the preview audience settings to share the offer with people outside your organization. Use the Private Offer option instead. At this point, your offer isn't fully tested and validated and isn't ready for external distribution.

## Publisher approval

You receive an email once the offer is created. At this point, you can review and approve your offer. You can also refresh the Offer overview page in your browser to see if your offer has reached the Publisher approval phase. If it has reached the Publisher approval phase, the **Go live** button and preview links are available. Validate all aspects of your solution in the preview phase before you make the offer live.

[![Screenshot of the Go live button activated view in Partner Center.](media/sentinel-solutions-post-publish-tracking/partner-go-live-button.png)](media/sentinel-solutions-post-publish-tracking/partner-go-live-button.png#lightbox)

## Certification

Offers submitted to the commercial marketplace must be certified before being published. Offers undergo a series of rigorous automated and manual validations. To learn more, see [commercial marketplace certification policies](/en-us/legal/marketplace/certification-policies). As part of the manual validations, checks include:

- Publisher business eligibility
- Content validations, such as appropriate title, well-written descriptions, quality screenshots
- Technical validations, such as malware scanning, package analysis, and test deployments

If your offer fails any checks, or if you aren't eligible to submit that type of offer, Partner Center sends a certification failure report to your email address. The errors also appear in Action Center in Partner Center. The report contains descriptions of any policies that failed, and review notes. Review the report, address any issues, update your offer as needed, and resubmit using the [commercial marketplace portal](https://go.microsoft.com/fwlink/?linkid=2165935) in Partner Center. You can resubmit as many times as needed until passing certification.

If there are certification failures, you can select **View certification link** to review the issues.

[![Screenshot of errors during certification phase in Partner Center.](media/sentinel-solutions-post-publish-tracking/partner-certification-failures.png)](media/sentinel-solutions-post-publish-tracking/partner-certification-failures.png#lightbox)

## Publishing

In the Publishing step, a series of final validation checks run to ensure the live offer is configured just like the preview version. After these validation checks are complete, your offer is live in the marketplace. Select the Azure Marketplace link under the Publish step to see the published solution in Azure Marketplace.

[![Screenshot of the final validations during publish phase in Partner Center.](media/sentinel-solutions-post-publish-tracking/partner-publish-view.png)](media/sentinel-solutions-post-publish-tracking/partner-publish-view.png#lightbox)

## Solution availability in Sentinel content hub

After the solution is published in Azure Marketplace, the solution is available in the Microsoft Sentinel content hub within 3–5 days. If you published your solution over the weekend, your solution is available by Tuesday. After your solution syncs to Microsoft Sentinel, customers can find it in the Microsoft Sentinel content hub, Azure Marketplace, and Microsoft Security Store. They can install, configure, monitor, and uninstall it from Microsoft Sentinel in the Microsoft Defender portal.

[![Screenshot of the Microsoft Sentinel content hub showing a published solution available to customers.](media/sentinel-solutions-post-publish-tracking/partner-solution-content-hub.png)](media/sentinel-solutions-post-publish-tracking/partner-solution-content-hub.png#lightbox)