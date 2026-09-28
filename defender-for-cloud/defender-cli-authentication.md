---
layout: Conceptual
title: Defender for Cloud CLI Authentication - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-cli-authentication
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
description: Learn how to securely integrate Azure DevOps with Microsoft Defender for Cloud using connector-based authentication. Simplify token management and enhance security.
ms.date: 2025-11-06T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: 7f8e6c35-04e3-d301-db41-0c50febad6a1
document_version_independent_id: 2b8032e5-bff4-4d5c-e363-2a3ced3041ba
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-cli-authentication.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-cli-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-cli-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
platformId: 70aed085-accf-f7b8-4c14-aa6ccdede9aa
---

# Defender for Cloud CLI Authentication - Microsoft Defender for Cloud | Microsoft Learn

Defender for Cloud CLI supports two authentication methods to align with enterprise security practices: connector-based authentication for Azure DevOps and GitHub, which handles authentication automatically, and token-based authentication, which provides flexibility across different build systems and local environments.

## Connector Based (ADO and GitHub)

Connector‑based authentication integrates Azure DevOps and GitHub directly with Microsoft Defender for Cloud through a secure connector. Once the connection is established, authentication is managed automatically, removing the need to store or inject tokens in your pipelines. This method is the preferred authentication method for Azure DevOps and GitHub. Learn how to create a connector:

- [Learn how to create an ADO connector](quickstart-onboard-devops)
- [Learn how to create a GitHub connector](quickstart-onboard-github)

## Token Based

Token‑based authentication allows security admins to generate tokens in the Microsoft Defender for Cloud portal and configure them as environment variables in CI/CD pipelines or local terminals. This method provides flexibility across different build systems and ensures secure, scoped access without embedding credentials in scripts.

1. Sign in to the Azure portal and open Microsoft Defender for Cloud.
2. Navigate to **Management ▸ Environment settings ▸ Integrations**.

    ![Screenshot of the Environment settings Integrations page showing available integration options.](media/cli-cicd/env-settings-integrations.png)
3. Select **+ Add integration ▸ DevOps Ingestion (Preview)**

    ![Screenshot of the Add integration menu with DevOps Ingestion (Preview) option highlighted.](media/cli-cicd/new-devops-ingestion.png)
4. Enter an application name.

    1. Choose the tenant to store the secret.
    2. Set an expiration date, and enable the token.
    3. Select **Save**.

    ![Screenshot of the Add DevOps Ingestion form with application name, tenant, expiration, and token settings.](media/cli-cicd/add-devops-ingestion.png)![Screenshot of the completed DevOps ingestion configuration showing generated client and secret values.](media/cli-cicd/devops-ingestion-created.png)
5. After saving, copy the Client ID, Client Secret, and Tenant ID. You can't retrieve them again.

    ![Screenshot of the success confirmation panel displaying Client ID, Client Secret, and Tenant ID.](media/cli-cicd/devops-ingestion-created-success.png)