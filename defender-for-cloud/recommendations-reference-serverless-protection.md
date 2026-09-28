---
layout: Conceptual
title: Serverless protection recommendations - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/recommendations-reference-serverless-protection
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
description: This article lists the Microsoft Defender for Cloud security recommendations for serverless protection.
ms.topic: reference
ms.date: 2026-05-25T00:00:00.0000000Z
ms.custom: generated
ai-usage: ai-assisted
locale: en-us
document_id: 57a2dfc2-78ef-359f-1d11-70dead79c9e0
document_version_independent_id: 50739d3f-d8ca-7997-cc43-ddc235d911ea
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/recommendations-reference-serverless-protection.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/recommendations-reference-serverless-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/recommendations-reference-serverless-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: ff201327-a6d5-c56a-791b-4a0d959a88c5
---

# Serverless protection recommendations - Microsoft Defender for Cloud | Microsoft Learn

This article lists all the security recommendations you might see issued by the Microsoft Defender for Cloud plan - Defender Cloud Security Posture Management (CSPM) for serverless protection.

The recommendations that appear in your environment are based on the resources that you're protecting and on your customized configuration. You can [see the recommendations in the portal](https://portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/5) that apply to your resources.

To learn about actions that you can take in response to these recommendations, see [Remediate recommendations in Defender for Cloud](implement-security-recommendations).

Tip

If a recommendation's description says *No related policy*, usually it's because that recommendation is dependent on a different recommendation and *its* policy.

For example, the recommendation *Endpoint protection health failures should be remediated* relies on the recommendation that checks whether an endpoint protection solution is even installed (*Endpoint protection solution should be installed*). The underlying recommendation *does* have a policy. Limiting the policies to only the foundational recommendation simplifies policy management.

## Serverless protection recommendations

### Authentication should be enabled on Azure Functions

**Description**: Defender for Cloud identified that authentication isn't enabled for your Azure Functions App, and at least one HTTP triggered function is set to 'anonymous'. This authentication poses a risk of unauthorized access to a Function. Add an Identity provider for the Function app or change the authentication type of the function itself to prevent this risk. (No related policy)

**Severity**: High

### Authentication should be enabled on Lambda Function URLs

**Description**: Defender for Cloud identified that authentication isn't enabled for one or more Lambda Function URLs. Publicly accessible Lambda Function URLs without authentication pose a risk of unauthorized access and potential abuse. Enforcing AWS IAM authentication on Lambda Function URLs helps mitigate these risks. (No related policy)

**Severity**: High

### Code Signing should be enabled on Lambda

**Description**: Defender for Cloud has identified that code signing isn't enabled on Lambda, which poses a risk of unauthorized modifications to the Lambda function code. Enabling code signing ensures the integrity and authenticity of the code, preventing such modifications. (No related policy)

**Severity**: High

### Lambda function should be configured with automatic runtime version updates

**Description**: Defender for Cloud identified that the Lambda function isn't using an automatic runtime version update. This poses a risk of exposure to outdated runtime versions with vulnerabilities. Using automatic updates keeping runtime up to date and ensures the function benefits from the latest security patches and improvements. (No related policy)

**Severity**: Medium

### Lambda function should implement Reserved Concurrency to prevent resource exhaustion

**Description**: Defender for Cloud identified that the Lambda function is using an outdated layer version. This poses a risk of exposure to known vulnerabilities. Keeping layers up to date ensures the function benefits from the latest security patches and improvements. (No related policy)

**Severity**: Medium

### Overly permissive permissions shouldn't be configured on Function App, Web App, or Logic App

**Description**: Defender for Cloud identified that the Function App, Web App, or Logic App Identity has overly permissive permissions. By restricting permissions, you can ensure that only necessary access is granted, reducing the risk of unauthorized access and potential security breaches. (No related policy)

**Severity**: High

### Restricted network access should be configured on Internet exposed Function app

**Description**: Defender for Cloud identified that the Function App is exposed to the internet without any restrictions. By restricting network access, you can ensure that only allowed networks can access the Functionapp. If the function doesn't require public network access, set 'Public Network Access' setting to 'disabled' or 'Enabled from selected virtual networks and IP addresses'. This action restricts the network access, reducing exposure to unauthorized access and protecting your application from potential threats. (No related policy)

**Severity**: High

### Security mechanism should be used on lambda function API Gateway

**Description**: Defender for Cloud identified that authentication isn't enabled for lambda function API Gateway. This poses a risk of unauthorized access and potential abuse of the function endpoints. Enforcing authentication can help mitigate these risks. (No related policy)

**Severity**: High