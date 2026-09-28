---
layout: Conceptual
title: Authentication architecture for AWS connectors - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-authentication-architecture-aws
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
description: Learn how Microsoft Defender for Cloud authenticates to AWS using short-lived credentials, federated trust, and role-based access controls.
ms.topic: concept-article
ms.date: 2025-11-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 1675a4c6-befc-87eb-baa8-6f08b5414ffe
document_version_independent_id: d3ce8bea-69dc-5b33-3cc0-45280995fe93
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/concept-authentication-architecture-aws.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/concept-authentication-architecture-aws
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/concept-authentication-architecture-aws.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 4316ed2f-a731-d1ce-1f9d-e9e40a7f7d59
---

# Authentication architecture for AWS connectors - Microsoft Defender for Cloud | Microsoft Learn

When you connect an AWS account to Microsoft Defender for Cloud, the service uses federated authentication to securely call AWS APIs without storing long-lived credentials. Temporary access is granted through AWS Security Token Service (STS), using short-lived credentials exchanged through a cross-cloud trust relationship.

This article explains how that trust is established and how short-lived credentials are used to access AWS resources securely.

## Authentication resources created in AWS

During onboarding, the CloudFormation template creates the authentication components that Defender for Cloud requires to establish trust between Microsoft Entra ID and AWS. These typically include:

- An **OpenID Connect identity provider** bound to a Microsoft-managed Microsoft Entra application
- One or more **IAM roles** that Defender for Cloud can assume through web identity federation

Depending on the Defender plan you enable, additional AWS resources might be created as part of the onboarding process.

## Identity provider model

Defender for Cloud authenticates to AWS using OIDC federation with a Microsoft-managed Microsoft Entra application. As a SaaS service, it operates independently of customer-managed identity providers and does not use identities from a customer’s Entra tenant to request federated AWS credentials.

The authentication resources created during onboarding establish the trust relationship required for Defender for Cloud to obtain short-lived AWS credentials through web identity federation.

## Cross-cloud authentication flow

The following diagram shows how Defender for Cloud authenticates to AWS by exchanging Microsoft Entra tokens for short-lived AWS credentials.

[![Diagram showing Microsoft Defender for Cloud obtaining a token from Microsoft Entra ID, which AWS validates and exchanges for temporary security credentials.](media/concept-authentication-architecture-aws/architecture-authentication-across-clouds.png)](media/concept-authentication-architecture-aws/architecture-authentication-across-clouds.png#lightbox)

## Role trust relationships

The IAM role defined by the CloudFormation template includes a trust policy that allows Defender for Cloud to assume the role through web identity federation. AWS only accepts tokens that satisfy this trust policy, which prevents unauthorized principals from assuming the same role.

The permissions granted to Defender for Cloud are controlled separately by the IAM policies attached to each role. These policies can be scoped to follow your organization’s least-privilege requirements, as long as the minimum permissions required for the selected Defender plans are included.

[![Screenshot of the AWS CloudFormation identity provider entry created during onboarding.](media/concept-authentication-architecture-aws/configure-access-roles.png)](media/concept-authentication-architecture-aws/configure-access-roles.png#lightbox)

## Token validation conditions

Before AWS issues temporary credentials, it performs several checks:

- **Audience validation** ensures that the expected application is requesting access.
- **Token signature validation** verifies that Microsoft Entra ID signed the token.
- **Certificate thumbprint validation** confirms that the signer matches the trusted identity provider.
- **Role-level conditions** restrict which federated identities can assume the role and prevent other Microsoft identities from using the same role.

AWS grants access only when all validation rules succeed.