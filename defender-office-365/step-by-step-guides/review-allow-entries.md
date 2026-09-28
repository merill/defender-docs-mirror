---
layout: Conceptual
title: Review and Remove Unnecessary Allowlist Entries with Advanced Hunting in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/review-allow-entries
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Steps and sample queries for advanced hunting to start reviewing your security configuration and removing unnecessary allowlist entries.
ms.service: defender-office-365
ms.author: chrisda
author: MSFTBen
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 3fbbe8c9-1944-d9ef-e622-79a26130cccc
document_version_independent_id: 3fbbe8c9-1944-d9ef-e622-79a26130cccc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/review-allow-entries.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/review-allow-entries
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/review-allow-entries.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: f60ab7d0-b9fc-bba3-b59c-46baea1927b8
---

# Review and Remove Unnecessary Allowlist Entries with Advanced Hunting in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Allowlists let Microsoft 365 organizations with cloud mailboxes ignore signals that an email is malicious. Vendors often ask for IPs, domains, and sender addresses to be overridden when it isn't needed. Attackers exploit these gaps, so unused allowlist entries are a serious security risk. This guide shows you how to use advanced hunting to find these overrides and remove them.

## Prerequisites

Before you run these queries, make sure you meet the following prerequisites:

- Microsoft Defender for Office 365 Plan 2 (Included in E5 plans, or trial available at aka.ms/trymdo)
- Sufficient permissions (Security reader role)
- 5-10 minutes to do the following procedures.

## Common steps for all the below queries

Use the following steps to run each query in this section.

1. [Sign in to the security portal and navigate to advanced hunting](https://security.microsoft.com/advanced-hunting)
2. Enter the KQL query into the query box, and press **Run Query**.
3. In the results, select the **NetworkMessageId** link for an email to open a flyout. The flyout shows the email entity page. Select the **analysis** tab to see details such as the transport rules that the email matched.
4. The results can also be exported by pressing **Export** for manipulation / analysis offline.

Tip

Changing **OrgLevelAction** to **UserLevelAction** will allow you to search for email warnings that were overridden by users rather than administrators, and can also be a useful insight.

## Override analysis queries

The following queries help you identify different types of unnecessary overrides. Each query filters the **EmailEvents** table by the **OrgLevelAction** field, which indicates an organization-level override action applied to a message.

### Top override source

Use the following query to find where the most unnecessary overrides are located. It looks for emails that were overridden without any detection that needed an override.

```kusto
EmailEvents
| where OrgLevelAction == "Allow"
| summarize count() by OrgLevelPolicy, ThreatTypes
```

### Top overridden threat type

Use the following DetectionMethods query to find the most overridden threat types. It looks for emails that had the detected threat overridden. Because DMARC and Spoof detections indicate email authentication issues, fixing those issues can remove the *need* for the override.

```kusto
EmailEvents
| where OrgLevelAction == "Allow" and ThreatTypes != ""
|summarize count() by DetectionMethods
```

### Top overridden IPs

The following IP summary query looks for emails that were overridden by IP, without any detection that called for an override.

```kusto
EmailEvents
| where OrgLevelAction == "Allow" and ThreatTypes == ""
|summarize count() by SenderIPv4
| top 10 by count_
```

### Top overridden domains

The following domain summary query looks for emails that were overridden by sending domain without any detection that called for an override. **(Change to SenderMailFromDomain to check the 5321.MailFrom)**

```kusto
EmailEvents
| where OrgLevelAction == "Allow" and ThreatTypes == ""
|summarize count() by SenderFromDomain
| top 10 by count_
```

### Top overridden senders

The following sender address query looks for emails that were overridden by sending address without any detection that requires an override. **(Change to SenderMailFromAddress to check the 5321.MailFrom)**

```kusto
EmailEvents
| where OrgLevelAction == "Allow" and ThreatTypes == ""
|summarize count() by SenderFromAddress
| top 10 by count_
```