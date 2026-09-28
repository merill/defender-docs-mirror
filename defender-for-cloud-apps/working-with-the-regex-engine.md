---
layout: Conceptual
title: Work with the regular expression engine in Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/working-with-the-regex-engine
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
description: Use regular expressions in Microsoft Defender for Cloud Apps policies to match text patterns, understand syntax limitations, and refine content inspection conditions.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a5c286ac-6784-bd4e-b465-58e528509a4b
document_version_independent_id: a5c286ac-6784-bd4e-b465-58e528509a4b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/working-with-the-regex-engine.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: working-with-the-regex-engine
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/working-with-the-regex-engine.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8b896464-3b7d-4e1f-84b0-9bb45aeb5f64
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1d2d671-9549-46e8-918c-24349120dbf5
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: a617c4d8-8dc8-821c-2cab-11b9675fe2fd
---

# Work with the regular expression engine in Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn

Important

File policies retire on January 6, 2027. To maintain file-based data protection, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

Microsoft Defender for Cloud Apps supports regular expressions (RegEx) for pattern matching in content inspection and file policies. This article covers the supported RegEx syntax, known limitations, and provides examples to help you build effective expressions for your policies.

## Regular expressions in Defender for Cloud Apps

The Microsoft Defender for Cloud Apps content inspection policies use RegEx for pattern matching. Content inspection may be applied as part of file policies.

### Testing regular expressions

To test regular expressions, you can use the following websites:

- [RegexPal regular expression tester](https://www.regexpal.com/) - Make sure you select **Case insensitive**.
- [Regex101 regular expression tester](https://regex101.com/) - Provides detailed analysis of the RegEx.

### Limitations of regular expressions in Defender for Cloud Apps

The following limitations are imposed on custom regular expressions:

- The search is always case-insensitive
- Allowed quantifiers: {n,m} where n, m &lt; 10
- All groups must be non-capturing, for example: (?:xxx)

    Instead of (group) use (?:group)
- Disallowed quantifiers: \*, +, {n,}

    Instead of \* use {0,9}

    Instead of + use {1,9}
- Disallowed back-references: \&lt;number&gt; or \k&lt;name&gt;

### Regular expression examples

The following table gives you example expressions and if they would match or not.

| Regular expression | Data | Matches |
| --- | --- | --- |
| `Colou?r (?:black&#124;blue&#124;white)` | Color black Color white Color red | Yes Yes No |
| `[a-z0-9]{1,9}@[a-z0-9]{1,9}\\.[a-z]{2,}` | Some1@abc.com user@host.org@bad.com | Yes Yes No |
| `20\d{2}-(?:0[1-9]|1[0-2])-(?:[0-2][0-9]|30|31)` | 2015-12-31 2015-01-09 1999-12-31 | Yes Yes No |
| `d.n't\s{0,10}c.r.` | Don't care D!n'tcor0 Doesn't care | Yes Yes No |