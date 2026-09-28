---
layout: Conceptual
title: Defender CLI setup for agentic code security - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/defender-cli-authentication
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Set up Defender CLI authentication to run agentic code scans locally or in CI/CD pipelines.
ms.topic: how-to
ms.date: 2026-08-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: c05948b4-3e80-9652-475e-2778229c159b
document_version_independent_id: c05948b4-3e80-9652-475e-2778229c159b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/defender-cli-authentication.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-cli-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/defender-cli-authentication.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/089c8ba6-d135-43ff-bfaf-b8197fb72fb9
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/32516e21-6665-416f-be21-413febe47d91
platformId: 6f41e8ec-90cd-5279-aaed-818c06e8136b
---

# Defender CLI setup for agentic code security - Microsoft Security Exposure Management | Microsoft Learn

Use Defender CLI authentication to run agentic code scans locally or in CI/CD pipelines.

## Authentication options

Agentic code security supports two Defender CLI authentication methods:

- **App-based authentication**: Use this option for CI/CD pipelines and other non-interactive automation.
- **Interactive authentication**: Use this option for local terminal scans by signed-in users.

## Required permissions

The permissions you need depend on your authentication method. For information about assigning Defender unified RBAC permissions, see [Assign permissions to users using Defender RBAC](ai-code-security-onboarding#assign-permissions-to-users-using-defender-rbac).

| Authentication method | Required permissions |
| --- | --- |
| App-based authentication | **Application Administrator** role in Microsoft Entra ID to register the app and add API permissions. **Global Administrator** role to grant admin consent. The app registration requires the **AIScan.enabled** permission to run AI scans and **AIScan.Upload** to upload scan results. |
| Interactive authentication | **Security Administrator** role in Microsoft Entra ID. In Microsoft Defender unified RBAC, assign the permissions required to run scans, upload scan results, and view or manage scan results. |

## Install the Microsoft Defender Code enterprise application if required

This step is needed for both authentication methods. The script installs the Microsoft Defender Code first-party app on your tenant and grants admin consent for users running the CLI locally.

Note

For customers with an E5 license, the Microsoft Defender Code app is automatically provisioned during MDASH onboarding. Running this script isn't required. If your tenant doesn't have an E5 license, complete the following steps.

1. Install Azure CLI if it isn't already installed.

    ```powershell
    winget install -e --id Microsoft.AzureCLI
    ```
2. Copy the admin consent script and save it as `Grant-DefenderAdminConsent.ps1`. For more information, see [Microsoft Defender Code admin consent script](microsoft-defender-code-admin-consent-script).
3. Run the saved script with your tenant ID.

    ```powershell
    ./Grant-DefenderAdminConsent.ps1 -TenantId <tenant-id>
    ```
4. Complete the Azure sign-in flow. Copy the code shown in Azure CLI and sign in with the redirected URL.
5. Verify that the application was installed:

    1. In Microsoft Entra ID, go to **Overview**.
    2. Search your tenant for **Microsoft Defender Code**.
    3. Confirm that the application appears under **Enterprise applications**.

## Use app-based authentication

Use app-based authentication to run Defender CLI scans in CI/CD pipelines.

### Prerequisites

- **Application Administrator** role in Microsoft Entra ID.
- **Global Administrator** role available to approve the required permissions.
- Permission to view the app registration's tenant ID and client ID, and to create or retrieve a client secret.
- Azure CLI installed.

### Create a Microsoft Entra app

1. Sign in to the Azure portal.
2. Search for and select **App registrations**.
3. Select **New registration**.
4. Enter a name for your application, and then select **Register**.

### Add API permissions

1. In the new app registration, expand **Manage** in the left navigation pane.
2. Select **API permissions** &gt; **Add a permission**.
3. Select **APIs my organization uses**.
4. Search for and select **Microsoft Defender Code**.
5. Select **Application permissions**.
6. Add the permissions you need:
    - To allow users to run AI scans, select **AIScan.enabled**.
    - To allow users to upload AI scan results to Defender, select **AIScan.Upload**.
7. Select **Add permissions**.

Note

The **AIScan.View** role currently doesn't affect permissions.

### Grant admin consent

A Global Administrator must grant consent for the permissions. If the **Grant admin consent** button isn't available, you don't have the Global Administrator role.

1. On the **API permissions** page, select **Grant admin consent**.
2. Confirm when prompted.

### Add a client secret

1. In your app registration, select **Certificates & secrets** &gt; **New client secret**.
2. Enter a description and expiration date, and then select **Add**.
3. Store the secret value in a secure location. You can't view it again after you leave the page.
4. Record the **Application (client) ID** and **Directory (tenant) ID** from the app registration **Overview** page.

### Configure credentials for CI/CD

To configure Defender CLI in a pipeline, add the following values as encrypted secrets in your CI/CD platform, then expose them as environment variables in the workflow or pipeline job that runs the scan:

```bash
DEFENDER_ASPM_TENANT_ID
DEFENDER_ASPM_CLIENT_ID
DEFENDER_ASPM_CLIENT_SECRET
```

To find `DEFENDER_ASPM_TENANT_ID` and `DEFENDER_ASPM_CLIENT_ID`, open the app registration in Microsoft Entra ID and copy the **Directory (tenant) ID** and **Application (client) ID** values from the **Overview** page.

To get `DEFENDER_ASPM_CLIENT_SECRET`, create a new client secret in the same app registration, copy the secret value immediately after it's created, and store it securely in your pipeline secret store.

Important

Don't commit this secret to source control or include it in workflow logs. Rotate secrets regularly and replace them before they expire to avoid pipeline failures.

## Use interactive authentication

Use this approach to let users authenticate with their Defender credentials for local Defender CLI scans. You can also use app-based authentication instead.

### Prerequisites

Before you can run the Defender CLI commands, make sure your account has been assigned at least one of the following permissions:

- At least **Security Administrator** role in Microsoft Entra ID.
- Required permissions assigned in Microsoft Defender unified RBAC. For more information, see [Assign permissions to users using Defender RBAC](ai-code-security-onboarding#assign-permissions-to-users-using-defender-rbac).

### Set the tenant environment variable

Set the tenant ID used for Defender interactive authentication in your shell as an environment variable before you sign in. This ensures Azure CLI requests the device login against the correct Microsoft Entra tenant.

```bash
DEFENDER_DFD_TENANT_ID=<tenant-id>
```

### Sign in with Azure CLI

Run the following command to start a device code sign-in flow for Defender interactive authentication. The scope value requests the Defender interactive login permission, and the command allows sign-in even when no Azure subscription is associated with the account.

```bash
az login \
  --tenant <DEFENDER_DFD_TENANT_ID> \
  --scope c2fd607e-fe6e-41bd-ae58-08e2f24014aa/Defender.InteractiveLogin \
  --allow-no-subscriptions \
  --use-device-code
```

### Complete the device code sign-in

1. Copy the device code shown in the console, then open the device login page in your browser.
2. Sign in with an account that has access to the specified tenant.
3. Paste the device code when prompted and complete the authentication flow.
4. Return to the console and wait for the Azure CLI session to complete.