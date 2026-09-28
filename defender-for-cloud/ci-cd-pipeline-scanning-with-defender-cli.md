---
layout: Conceptual
title: CI/CD in pipeline-scanning with Defender for Cloud CLI - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/ci-cd-pipeline-scanning-with-defender-cli
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
description: Learn how to integrate Microsoft Defender for Cloud CLI into your CI/CD workflows for automated security scanning and standards-based SARIF output.
ms.date: 2025-11-06T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: 7a669134-3dfe-9119-9bb1-bcb8b1136f55
document_version_independent_id: 69f6bed3-78b4-da66-4c69-51e799f71fcb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/ci-cd-pipeline-scanning-with-defender-cli.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/ci-cd-pipeline-scanning-with-defender-cli
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/ci-cd-pipeline-scanning-with-defender-cli.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 1e3a0c72-be5c-8a56-ad70-3428b8b00f83
---

# CI/CD in pipeline-scanning with Defender for Cloud CLI - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud Command‑Line Interface (Defender for Cloud CLI) lets you embed security scanning directly in your continuous integration and continuous deployment (CI/CD) workflows. The CLI orchestrates security scanners and can run locally for developers.

## Key capabilities

- Container‑image vulnerability assessment and automatic ingestion into Cloud Security Explorer.
- Unified, cross‑platform CLI that works with any CI/CD tools.
- Standards‑based SARIF output that integrates with pull‑request annotations and quality gates.
- Token‑based authentication scoped to a single Azure subscription for granular control or Azure DevOps Connector authentication.

## Prerequisites

- An Azure Subscription with Defender for Cloud onboarded. If you don't already have an Azure account, [create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Defender CSPM enabled.
- One of the following CI/CD pipeline tools: Azure Pipelines, GitHub Actions, Jenkins, BitBucket Pipelines, GitLab, Google Cloud Build, Bamboo, CircleCI, Travis CI, TeamCity, Oracle DevOps services, or AWS CodeBuild.
- Windows or Linux/WSL terminal for local desktop scans.
- Security Admin permission to create the client ID and secret tokens if using token‑based authentication, or an Azure DevOps or GitHub connector established if using connector‑based authentication.

## Authentication setup

Defender for Cloud CLI supports two authentication methods to align with enterprise security practices. Connector-based authentication is currently available and the preferred method of authentication for Azure DevOps and GitHub.

1. [Connector-based authentication](defender-cli-authentication#connector-based-ado-and-github)
2. [Token‑based authentication](defender-cli-authentication#token-based)

## Configure your CI/CD pipeline

Choose the configuration example that matches your CI/CD platform and authentication method.

### Azure DevOps (Connector-based authentication)

```yaml
- task: MicrosoftDefenderCLI@2
    inputs:
      command: 'run'
      scanType: 'image'
      imageName: $(ImageName)
      break: false
```

### GitHub (Token-based authentication)

```yaml
- name: Download Defender for Cloud CLI
  run: |
    curl -L -o defender "https://aka.ms/defender-cli_linux-x64" && chmod +x defender
- name: Run Defender for Cloud CLI Scan (Built)
  run: |
    #replace image-name with the Container image built      
    ./defender scan image '${{ image-name }}'
  continue-on-error: true
  env:
    DEFENDER_TENANT_ID: ${{ secrets.DEFENDER_TENANT_ID }}
    DEFENDER_CLIENT_ID: ${{ secrets.DEFENDER_CLIENT_ID }}
    DEFENDER_CLIENT_SECRET: ${{ secrets.DEFENDER_CLIENT_SECRET }}
```

### Jenkins (Token-based authentication)

```groovy
environment {
  DEFENDER_TENANT_ID=credentials('defender-tenant-id')
  DEFENDER_CLIENT_ID=credentials('defender-client-id')
  DEFENDER_CLIENT_SECRET=credentials('defender-client-secret')
} 

stage('Download & Run Defender for Cloud CLI') {
  steps {
    script {
      node {
        sh 'curl -L -o defender "https://aka.ms/defender-cli_linux-x64"'
        sh 'chmod +x defender'
        sh './defender scan image ${IMAGE_NAME}'
      }
    }
  }
}
```