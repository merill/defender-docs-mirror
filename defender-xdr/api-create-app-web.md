---
layout: Conceptual
title: Create an app to access Microsoft Defender XDR without a user - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/api-create-app-web
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to create an app to access Microsoft Defender XDR without a user.
ms.service: defender-xdr
ms.author: edbaynash
author: EdB-MSFT
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.custom: api
ms.date: 2025-04-18T00:00:00.0000000Z
locale: en-us
document_id: 79577d8b-22df-3ca1-7a29-4f1c9791c43a
document_version_independent_id: 79577d8b-22df-3ca1-7a29-4f1c9791c43a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/api-create-app-web.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-create-app-web
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/api-create-app-web.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: d8b3e48a-2d96-2acb-320e-9078288ab245
---

# Create an app to access Microsoft Defender XDR without a user - Microsoft Defender XDR | Microsoft Learn

Important

Some information relates to prereleased product which may be substantially modified before its general availability. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Create an application to get programmatic access to Microsoft Defender without a defined user—for example, if you're creating a daemon or background service.

If you need programmatic access to Microsoft Defender on behalf of one or more users, see [Create an app to access Microsoft Defender APIs on behalf of a user](api-create-app-user-context) and [Create an app with partner access to Microsoft Defender APIs](api-partner-access). If you're not sure which kind of access you need, see [Get started](api-access).

Microsoft Defender exposes much of its data and actions through a set of programmatic APIs. Those APIs help you automate workflows and make use of Microsoft Defender's capabilities. This API access requires OAuth2.0 authentication. For more information, see [OAuth 2.0 Authorization Code Flow](/en-us/azure/active-directory/develop/active-directory-v2-protocols-oauth-code).

In general, you need to take the following steps to use these APIs:

- Create a Microsoft Entra application.
- Get an access token using this application.
- Use the token to access Microsoft Defender API.

This article explains how to:

- Create a Microsoft Entra application
- Get an access token to Microsoft Defender
- Validate the token.

## Create an app

1. Sign in to [Azure](https://portal.azure.com).
2. Navigate to **Microsoft Entra ID** &gt; **App registrations** &gt; **New registration**.

    [![The New registration tab in the Microsoft Defender portal](/en-us/defender/media/atp-azure-new-app2.png)](/en-us/defender/media/atp-azure-new-app2.png#lightbox)
3. In the form, choose a name for your application, then select **Register**.
4. On your application page, select **API Permissions** &gt; **Add permission** &gt; **APIs my organization uses** &gt;, type **Microsoft Threat Protection**, and select **Microsoft Threat Protection**. Your app can now access Microsoft Defender XDR.

    Your app can now access Microsoft Defender.

    Tip

    *Microsoft Threat Protection* is a former name for Microsoft Defender XDR, and doesn't appear in the original list. You need to start writing its name in the text box to see it appear.

    [![The organization's APIs usage tab in the Microsoft Defender portal](/en-us/defender/media/apis-in-my-org-tab.PNG)](/en-us/defender/media/apis-in-my-org-tab.PNG#lightbox)
5. Select **Application permissions**. Choose the relevant permissions for your scenario (for example, **Incident.Read.All**), and then select **Add permissions**.

    [![The application permission pane in the Microsoft Defender portal](/en-us/defender/media/request-api-permissions.PNG)](/en-us/defender/media/request-api-permissions.PNG#lightbox)

    Note

    You need to select the relevant permissions for your scenario. *Read all incidents* is just an example. To determine which permission you need, check the **Permissions** section in the API you want to call.

    For instance, to [run advanced queries](api-advanced-hunting), select the 'Run advanced queries' permission; to [isolate a device](/en-us/windows/security/threat-protection/microsoft-defender-atp/isolate-machine), select the 'Isolate machine' permission.
6. Select **Grant admin consent**. Every time you add a permission, you must select **Grant admin consent** for it to take effect.

    [![The consent grant-related pane in the Microsoft Defender portal](/en-us/defender/media/grant-consent.PNG)](/en-us/defender/media/grant-consent.PNG#lightbox)
7. To add a secret to the application, select **Certificates & secrets**, add a description to the secret, then select **Add**.

    Tip

    After you select **Add**, select **copy the generated secret value**. You won't be able to retrieve the secret value after you leave.

    [![The create app pane in the Microsoft Defender portal](/en-us/defender/media/defender-endpoint/webapp-create-key2.png)](/en-us/defender/media/defender-endpoint/webapp-create-key2.png#lightbox)
8. Record your application ID and your tenant ID somewhere safe. They're listed under **Overview** on your application page.

    [![The Overview pane in the Microsoft Defender portal](/en-us/defender/media/app-and-tenant-ids.png)](/en-us/defender/media/app-and-tenant-ids.png#lightbox)
9. **For Microsoft Defender partners only**: [Follow these instructions](api-partner-access) for partner access through the Microsoft Defender XDR APIs, set your app to be multitenant, so it can be available in all tenants once you receive admin consent. Partner access is **required** for third-party apps—for example, if you create an app that is intended to run in multiple customers' tenants. It is **not required** if you create a service that you want to run in your tenant only, like an application for your own use that only interacts with your own data. To set your app to be multitenant:

    - Go to **Authentication**, and add https://portal.azure.com as the **Redirect URI**.
    - On the bottom of the page, under **Supported account types**, select the **Accounts in any organizational directory** application consent for your multitenant app.

    Since your application interacts with Microsoft Defender XDR on behalf of your users, it needs to be approved for every tenant on which you intend to use it.

    The Active Directory administrator for each tenant needs to select the consent link and approve your app.

    The consent link has the following structure:

    ```http
    https://login.microsoftonline.com/common/oauth2/authorize?prompt=consent&client_id=<00000000-0000-0000-0000-000000000000>&response_type=code&sso_reload=true
    ```

    The digits `00000000-0000-0000-0000-000000000000` should be replaced with your Application ID.

**Done!** You've successfully registered an application! See the following examples for token acquisition and validation.

## Get an access token

For more information on Microsoft Entra tokens, see the [Microsoft Entra tutorial](/en-us/azure/active-directory/develop/active-directory-v2-protocols-oauth-client-creds).

Important

Although the examples in this section encourage you to paste in secret values for testing purposes, you should **never hardcode secrets** into an application running in production. A third party could use your secret to access resources. You can help keep your app's secrets secure by using [Azure Key Vault](/en-us/azure/key-vault/general/about-keys-secrets-certificates). For a practical example of how you can protect your app, see [Manage secrets in your server apps with Azure Key Vault](/en-us/training/modules/manage-secrets-with-azure-key-vault/).

### Get an access token using PowerShell

```PowerShell
# This code gets the application context token and saves it to a file named "Latest-token.txt" under the current directory.

$tenantId = '' # Paste your directory (tenant) ID here
$clientId = '' # Paste your application (client) ID here
$appSecret = '' # Paste your own app secret here to test, then store it in a safe place, such as the Azure Key Vault!

$resourceAppIdUri = 'https://api.security.microsoft.com'
$oAuthUri = "https://login.windows.net/$tenantId/oauth2/token"

$authBody = [Ordered] @{
    resource = $resourceAppIdUri
    client_id = $clientId
    client_secret = $appSecret
    grant_type = 'client_credentials'
}

$authResponse = Invoke-RestMethod -Method Post -Uri $oAuthUri -Body $authBody -ErrorAction Stop
$token = $authResponse.access_token

Out-File -FilePath "./Latest-token.txt" -InputObject $token

return $token
```

### Get an access token using C#

Note

The following code was tested with Nuget Microsoft.Identity.Client 3.19.8.

Important

The [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) NuGet package and Azure AD Authentication Library (ADAL) were deprecated. No new features were added since June 30, 2020. We strongly encourage you to upgrade, see the [migration guide](/en-us/azure/active-directory/develop/msal-migration) for more details.

1. Create a new console application.
2. Install NuGet [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client/).
3. Add the following line:

    ```C
    using Microsoft.Identity.Client;
    ```
4. Copy and paste the following code into your app (don't forget to update the three variables: `tenantId`, `clientId`, `appSecret`):

    ```C
    csharp
    string tenantId = "00000000-0000-0000-0000-000000000000"; // Paste your own tenant ID here
    string appId = "11111111-1111-1111-1111-111111111111"; // Paste your own app ID here
    string appSecret = "22222222-2222-2222-2222-222222222222"; // Paste your own app secret here for a test, and then store it in a safe place! 
    const string authority = https://login.microsoftonline.com;
    const string audience = https://api.securitycenter.microsoft.com;
    
    IConfidentialClientApplication myApp = ConfidentialClientApplicationBuilder.Create(appId).WithClientSecret(appSecret).WithAuthority($"{authority}/{tenantId}").Build();
    
    List<string> scopes = new List<string>() { $"{audience}/.default" };
    
    AuthenticationResult authResult = myApp.AcquireTokenForClient(scopes).ExecuteAsync().GetAwaiter().GetResult();
    
    string token = authResult.AccessToken;
    ```

### Get an access token using Python

```Python
import json
import urllib.request
import urllib.parse

tenantId = '' # Paste your directory (tenant) ID here
clientId = '' # Paste your application (client) ID here
appSecret = '' # Paste your own app secret here to test, then store it in a safe place, such as the Azure Key Vault!

url = "https://login.windows.net/%s/oauth2/token" % (tenantId)

resourceAppIdUri = 'https://api.security.microsoft.com'

body = {
    'resource' : resourceAppIdUri,
    'client_id' : clientId,
    'client_secret' : appSecret,
    'grant_type' : 'client_credentials'
}

data = urllib.parse.urlencode(body).encode("utf-8")

req = urllib.request.Request(url, data)
response = urllib.request.urlopen(req)
jsonResponse = json.loads(response.read())
aadToken = jsonResponse["access_token"]
```

### Get an access token using curl

Note

Curl is pre-installed on Windows 10, versions 1803 and later. For other versions of Windows, download and install the tool directly from the [official curl website](https://curl.haxx.se/windows/).

1. Open a command prompt, and set CLIENT\_ID to your Azure application ID.
2. Set CLIENT\_SECRET to your Azure application secret.
3. Set TENANT\_ID to the Azure tenant ID of the customer that wants to use your app to access Microsoft Defender.
4. Run the following command:

    ```bash
    curl -i -X POST -H "Content-Type:application/x-www-form-urlencoded" -d "grant_type=client_credentials" -d "client_id=%CLIENT_ID%" -d "scope=https://api.security.microsoft.com/.default" -d "client_secret=%CLIENT_SECRET%" "https://login.microsoftonline.com/%TENANT_ID%/oauth2/v2.0/token" -k
    ```

    A successful response looks like this:

    ```bash
    {"token_type":"Bearer","expires_in":3599,"ext_expires_in":0,"access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIn <truncated> aWReH7P0s0tjTBX8wGWqJUdDA"}
    ```

## Validate the token

1. Copy and paste the token into the [JSON web token validator website, JWT,](https://jwt.ms) to decode it.
2. Make sure that the *roles* claim within the decoded token contains the desired permissions.

    In the following image, you can see a decoded token acquired from an app, with `Incidents.Read.All`, `Incidents.ReadWrite.All`, and `AdvancedHunting.Read.All` permissions:

    [![The Decoded token pane in the Microsoft Defender portal](/en-us/defender/media/defender-endpoint/webapp-decoded-token.png)](/en-us/defender/media/defender-endpoint/webapp-decoded-token.png#lightbox)

## Use the token to access the Microsoft Defender XDR API

1. Choose the API you want to use (incidents, or advanced hunting). For more information, see [Supported Microsoft Defender APIs](api-supported).
2. In the HTTP-based request you're about to send, set the authorization header to `"Bearer" <token>`, *Bearer* being the authorization scheme, and *token* being your validated token.
3. The token expires within one hour. You can send more than one request during this time with the same token.

The following example shows how to send a request to get a list of incidents **using C#**.

```C
    var httpClient = new HttpClient();
    var request = new HttpRequestMessage(HttpMethod.Get, "https://api.security.microsoft.com/api/incidents");

    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", token);

    var response = httpClient.SendAsync(request).GetAwaiter().GetResult();
```