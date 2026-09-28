---
layout: Conceptual
title: Recommendation methods and properties - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/recommendation
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Retrieves the top recent alerts.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom: api
ms.date: 2025-11-13T00:00:00.0000000Z
locale: en-us
document_id: 9113f264-a254-441c-7c80-9f1512046de4
document_version_independent_id: 9113f264-a254-441c-7c80-9f1512046de4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/recommendation.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/recommendation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/recommendation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: 0e0f1d30-25c2-54c1-1cf5-52ce28153dcd
---

# Recommendation methods and properties - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Properties

| Property | Type | Description |
| --- | --- | --- |
| id | String | Recommendation ID |
| productName | String | Related software name |
| recommendationName | String | Recommendation name |
| Weaknesses | Long | Number of discovered vulnerabilities |
| Vendor | String | Related vendor name |
| recommendedVersion | String | Recommended version |
| recommendedProgram | String | Recommended program |
| recommendedVendor | String | Recommended vendor |
| recommendationCategory | String | Recommendation category. Possible values are: `Accounts`, `Application`, `Network`, `OS`, `SecurityControls` |
| subCategory | String | Recommendation subcategory |
| severityScore | Double | Potential impact of the configuration to the organization's Microsoft Secure Score for Devices (1-10) |
| publicExploit | Boolean | Public exploit is available |
| activeAlert | Boolean | Active alert is associated with this recommendation |
| associatedThreats | String collection | Threat analytics report is associated with this recommendation |
| remediationType | String | Remediation type. Possible values are: `ConfigurationChange`,`Update`,`Upgrade`,`Uninstall` |
| Status | Enum | Recommendation exception status. Possible values are: `Active` and `Exception` |
| configScoreImpact | Double | Microsoft Secure Score for Devices impact |
| exposureImpact | Double | Exposure score impact |
| totalMachineCount | Long | Number of installed devices |
| exposedMachinesCount | Long | Number of installed devices that are exposed to vulnerabilities |
| nonProductivityImpactedAssets | Long | Number of devices that aren't affected |
| relatedComponent | String | Related software component |
| exposedCriticalDevices | Numeric | The sum of critical devices in all levels of criticality except "not critical" for a particular recommendation |