---
layout: FAQ
title: Common questions -  regulatory compliance questions - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/faq-regulatory-compliance
summary: ''
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Frequently asked general questions about regulatory compliance
services: defender-for-cloud
ms.topic: faq
ms.date: 2025-05-18T00:00:00.0000000Z
locale: en-us
document_id: bc7e5cc2-006f-1f0a-cced-fc6925e70cfe
document_version_independent_id: f5cdbd4c-9297-96f8-5567-15fad0930927
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/faq-regulatory-compliance.yml
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: faq
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/faq-regulatory-compliance
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/faq-regulatory-compliance.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 53f00ad1-b89d-b3f8-2d83-edcce5b06e61
---

# Common questions -  regulatory compliance questions - Microsoft Defender for Cloud | Microsoft Learn

## How do I know which benchmark or standard to use?

[Microsoft cloud security benchmark (MCSB)](/en-us/security/benchmark/azure/introduction) is the canonical set of security recommendations and best practices defined by Microsoft, aligned with common compliance control frameworks including [CIS Control Framework](https://www.cisecurity.org/benchmark/azure/), [NIST SP 800-53](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final) and PCI-DSS. MCSB is a comprehensive cloud agnostic set of security principles designed to recommend the most up-to-date technical guidelines for Azure along with other clouds such as AWS and GCP. We recommend MCSB to customers who want to maximize their security posture and align their compliance status with industry standards.

The [CIS Benchmark](https://www.cisecurity.org/benchmark/azure/) is authored by an independent entity - Center for Internet Security (CIS) - and contains recommendations on a subset of core Azure services. We work with CIS to try to ensure that their recommendations are up to date with the latest enhancements in Azure, but they're sometimes delayed and can become outdated. Nonetheless, some customers like to use this objective, third-party assessment from CIS as their initial and primary security baseline.

Since we've released the Microsoft cloud security benchmark, many customers have chosen to migrate to it as a replacement for CIS benchmarks.

## What standards are supported in the compliance dashboard?

By default, the regulatory compliance dashboard shows you the Microsoft cloud security benchmark. The Microsoft cloud security benchmark is the Microsoft-authored guidelines for security, and compliance best practices based on common compliance frameworks. Learn more in the [Microsoft cloud security benchmark introduction](/en-us/azure/security/benchmarks/introduction).

To track your compliance with any other standard, you'll need to explicitly add them to your dashboard.

For a list of available regulatory standards, see [What regulatory compliance standards are available in Defender for Cloud](assign-regulatory-compliance-standards).

**AWS**: When users onboard, every AWS account has the AWS Foundational Security Best Practices assigned. This is the AWS-specific guideline for security and compliance best practices based on common compliance frameworks.

Users that have one Defender bundle enabled can enable other standards.

To add regulatory compliance standards on AWS accounts:

1. Navigate to **Environment settings**.
2. Select the relevant account.
3. Select **Standards**.
4. Select **Add** and choose **Standard**.
5. Choose a standard from the drop-down menu.
6. Select **Save**.

    [![Screenshot of adding regulatory compliance standard to AWS account.](media/update-regulatory-compliance-packages/add-aws-regulatory-compliance.png)](media/update-regulatory-compliance-packages/add-aws-regulatory-compliance.png#lightbox)

More standards will be added to the dashboard and included in the information on [Customize the set of standards in your regulatory compliance dashboard](assign-regulatory-compliance-standards).

## Why do some controls appear grayed out?

For each compliance standard in the dashboard, there's a list of the standard's controls. For the applicable controls, you can view the details of passing and failing assessments.

Some controls are grayed out. These controls don't have any Defender for Cloud assessments associated with them. Some might be procedure or process-related, and so can't be verified by Defender for Cloud. Some don't have any automated policies or assessments implemented yet, but will have in the future. And some controls might be the platform's responsibility as explained in [Shared responsibility in the cloud](/en-us/azure/security/fundamentals/shared-responsibility).

## How can I remove a built-in standard, like PCI-DSS, ISO 27001, or SOC2 TSP from the dashboard?

To customize the regulatory compliance dashboard, and focus only on the standards that are applicable to you, you can remove any of the displayed regulatory standards that aren't relevant to your organization. To remove a standard, follow the instructions in [Remove a standard from your dashboard](assign-regulatory-compliance-standards).

## I made the suggested changes based on the recommendation, but it isn't being reflected in the dashboard?

After you take action to resolve recommendations, wait 12 hours to see the changes to your compliance data. Assessments are run approximately every 12 hours, so you'll see the effect on your compliance data only after the assessments run.

## What permissions do I need to access the compliance dashboard?

To access all compliance data in your tenant, you need to have at least a **Reader** level of permissions on the applicable scope of your tenant, or all relevant subscriptions.

The minimum set of roles for accessing the dashboard and managing standards is **Resource Policy Contributor** and **Security Admin**.

## The regulatory compliance dashboard isn't loading for me

To use the regulatory compliance dashboard, Defender for Cloud must be enabled at the subscription level. If the dashboard isn't loading correctly, try the following steps:

1. Clear your browser's cache.
2. Try a different browser.
3. Try opening the dashboard from a different network location.

## How can I view a report of passing and failing controls per standard in my dashboard?

On the main dashboard, you can see a report of passing and failing controls for (1) the 'top 4' lowest compliance standards in the dashboard. To see all the passing/failing controls status, select (2) **Show all *x*** (where x is the number of standards you're tracking). A context plane displays the compliance status for every one of your tracked standards.

![Summary section of the regulatory compliance dashboard.](media/regulatory-compliance-dashboard/summaries-of-compliance-standards.png)

## How can I download a report with compliance data in a format other than PDF?

When you select **Download report**, select the standard and the format (PDF or CSV). The resulting report will reflect the current set of subscriptions you've selected in the portal's filter.

- The PDF report shows a summary status for the standard you selected
- The CSV report provides detailed results per resource, as it relates to policies associated with each control

Currently, there's no support for downloading a report for a custom policy; only for the supplied regulatory standards.

## How can I create exceptions for some of the policies in the regulatory compliance dashboard?

For MCSB recommendations that are included in the secure score, you can create exemptions for one or more resources directly in the portal as explained in [Exempting resources and recommendations from your secure score](exempt-resource).

For other recommendations, you can create an exemption directly in the recommendation itself, by following the instructions in [Azure Policy exemption structure](/en-us/azure/governance/policy/concepts/exemption-structure).

## What Microsoft Defender plans or licenses do I need to use the regulatory compliance dashboard?

If you've got *any* of the Microsoft Defender plans (except for Defender for Servers Plan 1) enabled on *any* of your Azure resources, you can access Defender for Cloud's regulatory compliance dashboard and all of its data and features.

Note

For Defender for Servers you'll get regulatory compliance only for plan 2. Plan 1 doesn't include regulatory compliance.