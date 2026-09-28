---
layout: Conceptual
title: Fetch Microsoft Defender XDR incidents - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/fetch-incidents
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to fetch Microsoft Defender XDR incidents from a customer tenant
ms.service: defender-xdr
ms.author: edbaynash
author: EdB-MSFT
ms.localizationpriority: medium
ms.collection:
- m65-security-compliance
- tier3
- must-keep
ms.topic: reference
ms.custom: api
ms.date: 2021-10-25T00:00:00.0000000Z
locale: en-us
document_id: 1b627fbd-fd7f-2017-3abe-ee1aa0e1d5f9
document_version_independent_id: 1b627fbd-fd7f-2017-3abe-ee1aa0e1d5f9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/fetch-incidents.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fetch-incidents
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/fetch-incidents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 56a15725-e70d-613e-32fb-b4affb770222
---

# Fetch Microsoft Defender XDR incidents - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender for Endpoint](/en-us/defender-endpoint/microsoft-defender-endpoint)
- [Microsoft Defender XDR](microsoft-365-defender)

Note

**Try our new APIs using MS Graph security API**. Find out more at: [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/en-us/graph/api/resources/security-api-overview).

Note

This action is taken by the MSSP.

There are two ways you can fetch alerts:

- Using the SIEM method
- Using APIs

## Fetch incidents into your SIEM

To fetch incidents into your SIEM system, you'll need to take the following steps:

- Step 1: Create a third-party application
- Step 2: Get access and refresh tokens from your customer's tenant
- Step 3: allow your application on Microsoft Defender

### Step 1: Create an application in Microsoft Entra ID

You'll need to create an application and grant it permissions to fetch alerts from your customer's Microsoft Defender tenant.

1. Sign in to the [Microsoft Entra admin center](https://aad.portal.azure.com/).
2. Select **Microsoft Entra ID** &gt; **App registrations**.
3. Click **New registration**.
4. Specify the following values:

    - Name: &lt;Tenant\_name&gt; SIEM MSSP Connector (replace Tenant\_name with the tenant display name)
    - Supported account types: Account in this organizational directory only
    - Redirect URI: Select Web and type `https://<domain_name>/SiemMsspConnector`(replace &lt;domain\_name&gt; with the tenant name)
5. Click **Register**. The application is displayed in the list of applications you own.
6. Select the application, then click **Overview**.
7. Copy the value from the **Application (client) ID** field to a safe place, you will need this in the next step.
8. Select **Certificate & secrets** in the new application panel.
9. Click **New client secret**.

    - Description: Enter a description for the key.
    - Expires: Select **In 1 year**
10. Click **Add**, copy the value of the client secret to a safe place, you will need this in the next step.

### Step 2: Get access and refresh tokens from your customer's tenant

This section guides you on how to use a PowerShell script to get the tokens from your customer's tenant. This script uses the application from the previous step to get the access and refresh tokens using the OAuth Authorization Code Flow.

After providing your credentials, you'll need to grant consent to the application so that the application is provisioned in the customer's tenant.

1. Create a new folder and name it: `MsspTokensAcquisition`.
2. Download the [LoginBrowser.psm1 module](https://github.com/shawntabrizi/Microsoft-Authentication-with-PowerShell-and-MSAL/blob/master/Authorization%20Code%20Grant%20Flow/LoginBrowser.psm1) and save it in the `MsspTokensAcquisition` folder.

    Note

    In line 30, replace `authorzationUrl` with `authorizationUrl`.
3. Create a file with the following content and save it with the name `MsspTokensAcquisition.ps1` in the folder:

    ```powershell
    param (
        [Parameter(Mandatory=$true)][string]$clientId,
        [Parameter(Mandatory=$true)][string]$secret,
        [Parameter(Mandatory=$true)][string]$tenantId
    )
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
    
    # Load our Login Browser Function
    Import-Module .\LoginBrowser.psm1
    
    # Configuration parameters
    $login = "https://login.microsoftonline.com"
    $redirectUri = "https://SiemMsspConnector"
    $resourceId = "https://graph.windows.net"
    
    Write-Host 'Prompt the user for his credentials, to get an authorization code'
    $authorizationUrl = ("{0}/{1}/oauth2/authorize?prompt=select_account&response_type=code&client_id={2}&redirect_uri={3}&resource={4}" -f
                        $login, $tenantId, $clientId, $redirectUri, $resourceId)
    Write-Host "authorzationUrl: $authorizationUrl"
    
    # Fake a proper endpoint for the Redirect URI
    $code = LoginBrowser $authorizationUrl $redirectUri
    
    # Acquire token using the authorization code
    
    $Body = @{
        grant_type = 'authorization_code'
        client_id = $clientId
        code = $code
        redirect_uri = $redirectUri
        resource = $resourceId
        client_secret = $secret
    }
    
    $tokenEndpoint = "$login/$tenantId/oauth2/token?"
    $Response = Invoke-RestMethod -Method Post -Uri $tokenEndpoint -Body $Body
    $token = $Response.access_token
    $refreshToken= $Response.refresh_token
    
    Write-Host " ----------------------------------- TOKEN ---------------------------------- "
    Write-Host $token
    
    Write-Host " ----------------------------------- REFRESH TOKEN ---------------------------------- "
    Write-Host $refreshToken
    ```
4. Open an elevated PowerShell command prompt in the `MsspTokensAcquisition` folder.
5. Run the following command: `Set-ExecutionPolicy -ExecutionPolicy Bypass`
6. Enter the following commands: `.\MsspTokensAcquisition.ps1 -clientId <client_id> -secret <app_key> -tenantId <customer_tenant_id>`

    - Replace &lt;client\_id&gt; with the **Application (client) ID** you got from the previous step.
    - Replace &lt;app\_key&gt; with the **Client Secret** you created from the previous step.
    - Replace &lt;customer\_tenant\_id&gt; with your customer's **Tenant ID**.
7. You'll be asked to provide your credentials and consent. Ignore the page redirect.
8. In the PowerShell window, you'll receive an access token and a refresh token. Save the refresh token to configure your SIEM connector.

### Step 3: Allow your application on Microsoft Defender

You'll need to allow the application you created in Microsoft Defender.

You'll need to have **Manage portal system settings** permission to allow the application. Otherwise, you'll need to request your customer to allow the application for you.

1. Go to `https://security.microsoft.com?tid=<customer_tenant_id>` (replace &lt;customer\_tenant\_id&gt; with the customer's tenant ID.
2. Click **Settings** &gt; **Endpoints** &gt; **APIs** &gt; **SIEM**.
3. Select the **MSSP** tab.
4. Enter the **Application ID** from the first step and your **Tenant ID**.
5. Click **Authorize application**.

You can now download the relevant configuration file for your SIEM and connect to the Microsoft Defender XDR API. For more information, see, [Pull alerts to your SIEM tools](/en-us/defender-endpoint/configure-siem).

- In the ArcSight configuration file / Splunk Authentication Properties file, write your application key manually by setting the secret value.
- Instead of acquiring a refresh token in the portal, use the script from the previous step to acquire a refresh token (or acquire it by other means).

## Fetch alerts from MSSP customer's tenant using APIs

For information on how to fetch alerts using REST API, see [Pull alerts using REST API](/en-us/defender-endpoint/configure-siem).