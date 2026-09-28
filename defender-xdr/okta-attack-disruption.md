---
layout: Conceptual
title: Enable attack disruption actions in Okta with Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/okta-attack-disruption
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Configure the Okta integration with Microsoft Defender for Identity to enable Microsoft Defender XDR automatic attack disruption actions in your Okta environment.
ms.service: defender-xdr
ms.author: monaberdugo
author: mberdugo
ms.localizationpriority: medium
ms.reviewer: Ofer Shreiber
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 11cf3078-3515-94bd-e014-2c02bef7376f
document_version_independent_id: 11cf3078-3515-94bd-e014-2c02bef7376f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/okta-attack-disruption.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: okta-attack-disruption
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/okta-attack-disruption.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 0146102d-9025-d20d-40e9-20d63f5bb99b
---

# Enable attack disruption actions in Okta with Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Microsoft Defender XDR's [automatic attack disruption](automatic-attack-disruption) capabilities can help protect your Okta-managed identities by automatically responding to threats. When an identity managed by Okta is compromised, Defender XDR can take remediation actions directly in Okta to contain the attack, limit lateral movement, and reduce overall impact.

This article describes how to set up the Okta integration in Microsoft Defender for Identity to enable attack disruption actions in your Okta environment. Before you begin, review the prerequisites to ensure your Okta and Microsoft environments are properly configured.

## Prerequisites

Make sure you meet these requirements:

### Okta requirements

You need an Okta account with admin access. You also need a developer or enterprise license.

### Microsoft requirements

Complete these steps before you continue:

- Connect your Microsoft Sentinel analytic workspace to the unified security operations portal.
- Deploy and enable the Okta connector for Microsoft Sentinel.

Note

During public preview, only the Okta single sign-in connector is supported.

## Step 1: Create the Okta integration

To create the integration from an Okta account with admin privileges, follow these steps:

1. [Find your Okta domain](https://developer.okta.com/docs/guides/find-your-domain/main/#find-your-okta-domain)
2. [Create an Okta API key](https://help.okta.com/en-us/content/topics/security/api.htm#create-okta-api-token)

    - Provide a friendly name for your token
    - Make sure to keep the generated token value to be used later when creating the integration profile in the Defender portal.

Note

This token is a secret that allows connecting to your Okta environment and performing actions. Don't share its value or save it in any visible or public location.

## Step 2: Create the integration from the Defender portal

To create the integration in the Defender portal, follow these steps:

1. Log in to the [Defender portal](https://security.microsoft.com/)
2. Navigate **Microsoft Sentinel** -&gt; **Configuration** -&gt; **Automation**.
3. In the **Integrations profiles** tab, select **+Create** to create a new integration.

    ![Screenshot of the Integrations profile tab in the Automation page with the Create button highlighted.](media/okta-attack-disruption/create-new-integration.png)
4. Fill in the following values, then select **Create**:

    1. **Integration name**
    2. **Description**
    3. **Base API URL**: Enter your full Okta domain starting with `https://`
    4. **Authentication method**: Select API Key

        1. **API key name**
        2. **API key**: Enter `SSWS <API-Key>`, replacing `<API-Key>` with the value of the API token you generated in Okta. There should be a space between `SSWS` and your API Key. For more information, see the [Okta documentation for API Key usage](https://developer.okta.com/docs/reference/core-okta-api/#authentication)
        3. **API key identifier**: Leave empty
        4. Enable the **Send SPI key in header** switch.

    [![Screenshot of the integration details form with fields for Integration name, Description, Base API URL, and Authentication method.](media/okta-attack-disruption/integration-details.png)](media/okta-attack-disruption/integration-details.png#lightbox)