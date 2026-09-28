---
layout: Conceptual
title: CI/CD example for Defender CLI - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/defender-cli-cicd
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Sample GitHub Actions workflow for running agentic code scans with Defender CLI in a CI/CD pipeline.
ms.topic: how-to
ms.date: 2026-06-01T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 8ceb6ea0-ba88-e081-520f-e5efd1f5d6bb
document_version_independent_id: 8ceb6ea0-ba88-e081-520f-e5efd1f5d6bb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/defender-cli-cicd.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-cli-cicd
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/defender-cli-cicd.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
platformId: 86ff7126-caf6-3480-4aa9-aaef472eafb5
---

# CI/CD example for Defender CLI - Microsoft Security Exposure Management | Microsoft Learn

This sample GitHub Actions workflow downloads Defender CLI at runtime, passes credentials as environment variables, and runs both a file system scan and an AI scan submission. Use it as a baseline and adapt the trigger, path scope, and secret names to match your repository standards.

Important

Don't commit credential values to source control or include them in workflow logs. Rotate secrets regularly and replace them before they expire to avoid pipeline failures.

For instructions on obtaining the required credentials and configuring them as pipeline secrets, see [Configure credentials for CI/CD](defender-cli-authentication#configure-credentials-for-cicd).

```yaml
name: Defender ASPM scan
on: [workflow_dispatch]

permissions:
  contents: read
  id-token: write
  security-events: write

jobs:
  scan:
    runs-on: ubuntu-latest
    env:
      DEFENDER_ASPM_TENANT_ID:     ${{ secrets.DEFENDER_ASPM_TENANT_ID }}
      DEFENDER_ASPM_CLIENT_ID:     ${{ secrets.DEFENDER_ASPM_CLIENT_ID }}
      DEFENDER_ASPM_CLIENT_SECRET: ${{ secrets.DEFENDER_ASPM_CLIENT_SECRET }}
    steps:
      - uses: actions/checkout@v4
      - name: Download Defender CLI
        run: |
          curl -fL -o defender \
            "https://cli.dfd.security.azure.net/public/v2/latest/Defender_linux-x64"
          chmod +x defender
      - run: ./defender scan fs .                            # will run filesystem scans: open source dependencies, secrets, IaC misconfigurations, etc.
      - run: ./defender scan ai-scan ai submit .             # runs MDASH
```