---
layout: Conceptual
title: Submit files for analysis by Microsoft - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/submission-guide
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to submit files to Microsoft for malware analysis, how to track your submissions, and dispute detections.
ms.service: defender-xdr
author: poliveria
ms.author: pauloliveria
ms.reviewer: 
ms.collection:
- m365-security
- tier2
ms.topic: faq
ms.date: 2024-05-10T00:00:00.0000000Z
locale: en-us
document_id: 8693c798-6079-7fb6-3084-ecadbd003442
document_version_independent_id: 8693c798-6079-7fb6-3084-ecadbd003442
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/submission-guide.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: submission-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/submission-guide.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: d7483888-e655-ae0f-07e7-20db831c7141
---

# Submit files for analysis by Microsoft - Microsoft Defender XDR | Microsoft Learn

If you have a file that you suspect might be malware or is being incorrectly detected, you can submit it to us for analysis. This page has answers to some common questions about submitting a file for analysis.

Tip

If your organization's subscription includes [Microsoft Defender for Endpoint Plan 2](/en-us/defender-endpoint/microsoft-defender-endpoint), [Microsoft Defender for Office 365 Plan 2](/en-us/defender-office-365/mdo-about), or [Microsoft Defender XDR](/en-us/defender-xdr/microsoft-365-defender), you can use the [new unified submissions portal](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/unified-submissions-in-microsoft-365-defender-now-generally/ba-p/3270770). To learn more, see [Submit files in Microsoft Defender for Endpoint](/en-us/defender-endpoint/admin-submissions-mde).

## How do I submit a file to Microsoft for analysis?

Important

Starting May 20, 2024, [file submissions](https://www.microsoft.com/en-us/wdsi/filesubmission) will be transitioning to a new [Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id). If your tenant requires admin consent to continue accessing this service, refer to [Overview of user and admin consent](/en-us/entra/identity/enterprise-apps/user-admin-consent-overview) and grant access to app ID: 6ba09155-cb24-475b-b24f-b4e28fc74365 with graph permissions for Directory.Read.All and User.Read.

### Send a malware file

You can send files that you think might be malware or files that were incorrectly detected through the [sample submission portal](https://www.microsoft.com/wdsi/filesubmission).

You can complete a quick analysis by providing detailed information about the product you were using and what you were doing when you found the file.

After you sign in, you'll be able to track your submissions.

Note

You can use the Microsoft Security Intelligence submission feature even if you don't have Microsoft Defender for Endpoint Plan 2 or Microsoft Defender for Office Plan 2.

### Submit a suspected email attachment

Use the [Microsoft Defender portal](https://security.microsoft.com/) to submit suspected email attachments to Microsoft for review. For more information, see [Submit a suspected email attachment to Microsoft](/en-us/defender-office-365/submissions-admin).

### Submit a file or file hash

Use the unified submissions feature in Microsoft Defender for Endpoint to submit files and file hashes to Microsoft for review. For more information, see [Submit files in Microsoft Defender for Endpoint](/en-us/defender-endpoint/admin-submissions-mde).

## Can I send a sample by email?

No, we only accept submissions through our [sample submission portal](https://www.microsoft.com/wdsi/filesubmission).

## Can I submit a sample without signing in?

No. If you're an enterprise customer, you need to sign in so that we can prioritize your submission appropriately. If you're currently experiencing a virus outbreak or security-related incident, you should contact your designated Microsoft support professional or go to [Microsoft Support](https://support.microsoft.com/) for immediate assistance.

## What is the Software Assurance ID (SAID)?

The [Software Assurance ID (SAID)](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx) is for enterprise customers to track support entitlements. The submission portal accepts and retains SAID information and allows customers with valid SAIDs to make higher priority submissions.

### How do I dispute the detection of my program?

[Submit the file](https://www.microsoft.com/wdsi/filesubmission) in question as a software developer. Wait until your submission has a final determination.

If you're not satisfied with our determination of the submission, use the developer contact form provided with the submission results to reach Microsoft. We'll use the information you provide to investigate further if necessary.

We encourage all software vendors and developers to read about [how Microsoft identifies malware and unwanted software](criteria).

## How do I track or view past sample submissions?

You can track your submissions through the [submission history page](https://www.microsoft.com/wdsi/submissionhistory).

## What does the submission status mean?

Each submission is shown to be in one of the following status types:

- Submitted—the file has been received
- In progress—an analyst has started checking the file
- Closed—a final determination has been given by an analyst

You can see the status of any files you submit to us on the [submission history page](https://www.microsoft.com/wdsi/submissionhistory).

## How does Microsoft prioritize submissions

Processing submissions take dedicated analyst resource. Because we regularly receive a large number of submissions, we handle them based on a priority. The following factors affect how we prioritize submissions:

- Prevalent files with the potential to impact large numbers of computers are prioritized.
- Authenticated customers, especially enterprise customers with valid [Software Assurance IDs (SAIDs)](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx), are given priority.
- Submissions flagged as high priority by SAID holders are given immediate attention.

Your submission is immediately scanned by our systems to give you the latest determination even before an analyst starts handling your case. Note that the same file may have already been processed by an analyst. To check for updates to the determination, select rescan on the submission details page.