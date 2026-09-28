---
layout: Conceptual
title: Authentication architecture for GCP connectors - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/authentication-architecture-google-cloud
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
description: Learn how Microsoft Defender for Cloud authenticates to Google Cloud using federated identity, short-lived tokens, and workload identity federation.
ms.topic: concept-article
ms.date: 2026-02-11T00:00:00.0000000Z
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 3f256c0b-6f1a-faec-069b-e8b87d7c3a9d
document_version_independent_id: f52d2122-86e1-cb61-1213-8d6ed328f2d8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/authentication-architecture-google-cloud.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/authentication-architecture-google-cloud
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/authentication-architecture-google-cloud.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: f03bbef3-ad06-0642-b04b-c9298e2549e4
---

# Authentication architecture for GCP connectors - Microsoft Defender for Cloud | Microsoft Learn

When you connect a Google Cloud Platform (GCP) project or organization to Microsoft Defender for Cloud, the service uses federated authentication to securely access GCP APIs without storing long-lived credentials.

Authentication is performed by exchanging short-lived tokens between Microsoft Entra ID and Google Cloud Security Token Service (STS), allowing Defender for Cloud to impersonate a GCP service account with scoped permissions.

This article explains the authentication resources created during onboarding and how the federated trust model works.

## Authentication resources created in GCP

When you onboard a GCP project or organization to Defender for Cloud, a GCloud template is used to create the authentication resources required to establish trust between Microsoft Entra ID and Google Cloud.

These resources include:

- Workload identity pool and providers
- Service accounts and policy bindings

These resources enable Defender for Cloud to authenticate to GCP and access the required APIs for discovery, posture assessment, and security analysis.

## Identity provider model

Defender for Cloud authenticates to GCP using workload identity federation.

A workload identity provider is configured in GCP to trust tokens issued by Microsoft Entra ID. This trust allows Defender for Cloud to exchange Microsoft Entra tokens for Google STS tokens and impersonate a GCP service account.

The service account permissions are scoped to the connected project or organization and are limited to the access required by the enabled Defender plans.

## Cross-cloud authentication flow

The following diagram shows how Defender for Cloud authenticates to GCP using federated identity and token exchange.

[![Diagram showing the Defender for Cloud GCP connector authentication process using federated identity and token exchange.](media/concept-authentication-architecture-gcp/authentication-process.png)](media/concept-authentication-architecture-gcp/authentication-process.png#lightbox)

The authentication process works as follows:

1. Microsoft Defender for Cloud's CSPM service acquires a Microsoft Entra token. Microsoft Entra ID signs the token using the RS256 algorithm. The token is valid for one hour.
2. The Microsoft Entra token is exchanged with Google's Security Token Service (STS).
3. Google STS validates the token with the workload identity provider. Audience validation is performed, and the token is signed. A Google STS token is then returned to Defender for Cloud.
4. Defender for Cloud uses the Google STS token to impersonate the service account. The service account credentials are used to scan the GCP project or organization.

## Service account impersonation and access scope

After authentication completes, Defender for Cloud operates using impersonated service account credentials.

- Service account access is limited to the GCP resources that were onboarded. If you onboarded a single project, access is restricted to that project. If you onboarded a GCP organization, access is scoped to the projects included in that organization.
- Policy bindings restrict access to only the connected resources.
- Permissions granted to the service account determine which security signals Defender for Cloud can collect.

This model ensures least-privilege access while enabling continuous security assessment.