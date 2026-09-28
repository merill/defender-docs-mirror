---
layout: Conceptual
title: Onboard Docker Hub registries to Microsoft Defender for Containers - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-enable-external-registry-for-docker-hub
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
description: Connect your Docker Hub organization to Defender for Containers for vulnerability scanning by creating a dedicated user account and access token.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: e841804a-1786-cda7-4782-2396da5d919d
document_version_independent_id: b47fc6b1-a740-1d15-3a69-bb87f1930d87
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-containers-enable-external-registry-for-docker-hub.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-containers-enable-external-registry-for-docker-hub
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-containers-enable-external-registry-for-docker-hub.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 9dd5ad1f-eea6-8b0d-0a61-2105a961bbda
---

# Onboard Docker Hub registries to Microsoft Defender for Containers - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Containers connects to your Docker Hub organization to assess vulnerabilities in container images. Before you start, make sure you meet the prerequisites.

To connect Docker Hub to Defender for Containers, you need to:

- Create a dedicated user in your Docker Hub organization with access to all organization registries.
- Generate an access token for the Docker Hub dedicated user.
- Supply the Docker Hub dedicated user name and access token when configuring the Defender for Cloud Docker Hub connector.

## Before you begin

Make sure you have these prerequisites:

- You own a Docker Hub organization account and have permissions to create and manage users at the organization scope.
- You created a dedicated user with your organization email account (for example, `mdc_user@contoso.com`) for Defender for Cloud connectivity only.

## Create a user in Docker Hub

To create a user in Docker Hub:

1. Verify that you can create and manage users in your Docker Hub organization.
2. Invite the dedicated user via email to access all repositories in your organization as an "Editor".

    [![Screenshot of select an invite member.](media/defender-for-containers-enable-external-registry-for-docker-hub/docker-hub-invite-member.png)](media/defender-for-containers-enable-external-registry-for-docker-hub/docker-hub-invite-member.png#lightbox)

    [![Screenshot of invite a member.](media/defender-for-containers-enable-external-registry-for-docker-hub/docker-hub-invite-editor-type-reduced.png)](media/defender-for-containers-enable-external-registry-for-docker-hub/docker-hub-invite-editor-type.png#lightbox)

    Note

    While the Editor privilege allows a user to modify Docker Hub registries, the access token created will allow Defender for Cloud read-only access.
3. An email is sent to the dedicated user with a link to verify the email address. Select the verify link in the email and complete the process of creating a Docker Hub dedicated user.

## Create an access token for the dedicated Docker Hub user

To create an access token for the dedicated Docker Hub user:

1. Sign in to Docker Hub as the dedicated user.
2. Generate an access token with **Read-Only** permissions.
3. Save the access token and the Docker Hub user name to use when configuring the Defender for Cloud Docker Hub connector.
4. Continue with [configure the Defender for Cloud Docker Hub connector](agentless-vulnerability-assessment-docker-hub#onboard-docker-hub-to-defender-for-cloud).

[![Screenshot of create an access token.](media/defender-for-containers-enable-external-registry-for-docker-hub/docker-hub-create-access-token.png)](media/defender-for-containers-enable-external-registry-for-docker-hub/docker-hub-create-access-token.png#lightbox)

[![Screenshot of view an access token.](media/defender-for-containers-enable-external-registry-for-docker-hub/docker-hub-access-token-text.png)](media/defender-for-containers-enable-external-registry-for-docker-hub/docker-hub-access-token-text.png#lightbox)