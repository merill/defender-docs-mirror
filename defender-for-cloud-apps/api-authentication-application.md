---
layout: Conceptual
title: Access with application context - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-authentication-application
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Learn how to design a web app to get programmatic access to Defender for Cloud Apps without a user.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
ms.custom: sfi-image-nochange
locale: en-us
document_id: 0298588e-4ba3-7e51-75ff-c454c45c89a0
document_version_independent_id: 0298588e-4ba3-7e51-75ff-c454c45c89a0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-authentication-application.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-authentication-application
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-authentication-application.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0e848536-d1a8-6245-4035-afd8c6f5a50a
---

# Access with application context - Microsoft Defender for Cloud Apps | Microsoft Learn

This page describes how to create an application to get programmatic access to Defender for Cloud Apps without a user. If you need programmatic access to Defender for Cloud Apps on behalf of a user, see [Get access with user context](api-authentication-user). If you aren't sure which access you need, see the [Managing API tokens](api-authentication) page.

Microsoft Defender for Cloud Apps exposes much of its data and actions through a set of programmatic APIs. Those APIs help you automate work flows and innovate based on Defender for Cloud Apps capabilities. The API access requires OAuth2.0 authentication. For more information, see [OAuth 2.0 Authorization Code Flow](/en-us/azure/active-directory/develop/active-directory-v2-protocols-oauth-code).

In general, you need to take the following steps to use the APIs:

- Create a Microsoft Entra application.
- Get an access token using this application.
- Use the token to access Defender for Cloud Apps API.

This article explains how to create a Microsoft Entra application, get an access token to Microsoft Defender for Cloud Apps, and validate the token.

## Create an app for Defender for Cloud Apps

1. In the Microsoft Entra admin center, register a new application. For more information, see [Quickstart: Register an application with the Microsoft Entra admin center](/en-us/azure/active-directory/develop/quickstart-register-app).
2. To enable your app to access Defender for Cloud Apps and assign it **'Read all alerts'** permission, on your application page, select **API Permissions** &gt; **Add permission** &gt; **APIs my organization uses** &gt;, type **Microsoft Cloud App Security**, and then select **Microsoft Cloud App Security**.

    Note

    *Microsoft Cloud App Security* doesn't appear in the original list. Start writing its name in the text box to see it appear. Make sure to type this name, even though the product is now called Defender for Cloud Apps.

    [![Screenshot showing how to configure API permissions for your application.](media/api-authentication-application/add-app-permissions.png)](media/api-authentication-application/add-app-permissions.png#lightbox)
3. Select **Application permissions** &gt; **Investigation.Read**, and then select **Add permissions**.

    [![Screenshot that shows which API permissions to request for your application.](media/api-authentication-application/request-permissions.png)](media/api-authentication-application/request-permissions.png#lightbox)
4. You need to select the relevant permissions. **Investigation.Read** is only an example. For other permission scopes, see Supported permission scopes
5. To determine which permission you need, look at the **Permissions** section in the API you're interested to call.
6. Select **Grant admin consent**.

    Note

    Every time you add a permission, you must select **Grant admin consent** for the new permission to take effect.

    [![Screenshot that shows the option to grant admin consent.](media/api-authentication-application/grant-consent.png)](media/api-authentication-application/grant-consent.png#lightbox)
7. To add a secret to the application, select **Certificates & secrets**, select **New client secret**. Add a description to the secret, and then select **Add**.

    Note

    After you select **Add**, select **copy the generated secret value**. You won't be able to retrieve this value after you leave.

    [![Screenshot that shows how to create an app key.](media/api-authentication-application/webapp-create-key2.png)](media/api-authentication-application/webapp-create-key2.png#lightbox)
8. Write down your application ID and your tenant ID. On your application page, go to **Overview** and copy the **Application (client) ID** and the **Directory (tenant) ID**.

    [![Screenshot that shows the created app ID.](media/api-authentication-application/app-and-tenant-ids.png)](media/api-authentication-application/app-and-tenant-ids.png#lightbox)
9. **For Microsoft Defender for Cloud Apps Partners only**. Set your app to be multitenant (available in all tenants after consent). This is **required** for third-party apps (for example, if you create an app that is intended to run in multiple customers' tenant). This is **not required** if you create a service that you want to run in your tenant only (for example, if you create an application for your own usage that will only interact with your own data). To set your app to be multitenant:

    - Go to **Authentication**, and add `https://portal.azure.com` as the **Redirect URI**.
    - On the bottom of the page, under **Supported account types**, select the **Accounts in any organizational directory** application consent for your multitenant app.

    You need your application to be approved in each tenant where you intend to use it. This is because your application interacts Defender for Cloud Apps on behalf of your customer.

    You (or your customer if you're writing a third-party app) need to select the consent link and approve your app. The consent should be done with a user who has administrative privileges in Active Directory.

    The consent link is formed as follows:

    ```url
    https://login.microsoftonline.com/common/oauth2/authorize?prompt=consent&client_id=00000000-0000-0000-0000-000000000000&response_type=code&sso_reload=true
    ```

    Where 00000000-0000-0000-0000-000000000000 is replaced with your application ID.

**Done!** You've successfully registered an application! See examples below for token acquisition and validation.

## Supported permission scopes

| Permission name | Description | Supported actions |
| --- | --- | --- |
| Investigation.read | Perform all supported actions on activities and alerts except closing alerts.View IP ranges but not add, update, or delete.Perform all entities actions. | Activities list, fetch, feedbackAlerts list, fetch, mark as read/unreadEntities list, fetch, fetch treeSubnet list |
| Investigation.manage | Perform all investigation.read actions in addition to managing alerts and IP ranges. | Activities list, fetch, feedbackAlerts list, fetch, mark as read/unread, closeEntities list, fetch, fetch treeSubnet list, create/update/delete |
| Discovery.read | Perform all supported actions on activities and alerts except closing alerts.List discovery reports and categories. | Alerts list, fetch, mark as read/unreadDiscovery list reports, list report categories |
| Discovery.manage | Discovery.read permissionsClose alerts, upload discovery files, and generate block scripts | Alerts list, fetch, mark as read/unread, closeDiscovery list reports, list report categoriesDiscovery file upload, generate block script |
| Settings.read | List IP ranges. | Subnet list |
| Settings.manage | List and manage IP ranges. | Subnet list, create/update/delete |

## Get an access token

For more information on Microsoft Entra tokens, see the [Microsoft Entra tutorial](/en-us/azure/active-directory/develop/active-directory-v2-protocols-oauth-client-creds).

### Use PowerShell

```powershell
# This script acquires the App Context Token and stores it in the variable $token for later use in the script.
# Paste your Tenant ID, App ID, and App Secret (App key) into the indicated quotes below.

$tenantId = '' ### Paste your tenant ID here
$appId = '' ### Paste your Application ID here
$appSecret = '' ### Paste your Application key here

$resourceAppIdUri = '05a65629-4c1b-48c1-a78b-804c4abdd4af'
$oAuthUri = "https://login.microsoftonline.com/$TenantId/oauth2/token"
$authBody = [Ordered] @{
    resource = "$resourceAppIdUri"
    client_id = "$appId"
    client_secret = "$appSecret"
    grant_type = 'client_credentials'
}
$authResponse = Invoke-RestMethod -Method Post -Uri $oAuthUri -Body $authBody -ErrorAction Stop
$token = $authResponse.access_token
```

### Use C#

The following code was tested with NuGet Microsoft.Identity.Client 4.47.2.

1. Create a new console application.
2. Install NuGet [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client/).
3. Add the following:

    ```text
    using Microsoft.Identity.Client;
    ```
4. Copy and paste the following code in your app (don't forget to update the three variables: `tenantId, appId, appSecret`):

    ```c
    string tenantId = "00000000-0000-0000-0000-000000000000"; // Paste your own tenant ID here
    string appId = "00001111-aaaa-2222-bbbb-3333cccc4444"; // Paste your own app ID here
    string appSecret = "22222222-2222-2222-2222-222222222222"; // Paste your own app secret here for a test, and then store it in a safe place!
    const string authority = "https://login.microsoftonline.com";
    const string audience = "05a65629-4c1b-48c1-a78b-804c4abdd4af";
    
    IConfidentialClientApplication myApp = ConfidentialClientApplicationBuilder.Create(appId).WithClientSecret(appSecret).WithAuthority($"{authority}/{tenantId}").Build();
    
    List scopes = new List() { $"{audience}/.default" };
    
    AuthenticationResult authResult = myApp.AcquireTokenForClient(scopes).ExecuteAsync().GetAwaiter().GetResult();
    
    string token = authResult.AccessToken;
    ```

### Use Python

See [Microsoft Authentication Library (MSAL) for Python](https://github.com/AzureAD/microsoft-authentication-library-for-python).

### Use Curl

Note

The following procedure assumes that Curl for Windows is already installed on your computer.

1. Open a command prompt, and set CLIENT\_ID to your Azure application ID.
2. Set CLIENT\_SECRET to your Azure application secret.
3. Set TENANT\_ID to the Azure tenant ID of the customer that wants to use your app to access Defender for Cloud Apps.
4. Run the following command:

    ```curl
    curl -i -X POST -H "Content-Type:application/x-www-form-urlencoded" -d "grant_type=client_credentials" -d "client_id=%CLIENT_ID%" -d "scope=05a65629-4c1b-48c1-a78b-804c4abdd4af/.default" -d "client_secret=%CLIENT_SECRET%" "https://login.microsoftonline.com/%TENANT_ID%/oauth2/v2.0/token" -k
    ```

    You get an answer in the following form:

    ```output
    {"token_type":"Bearer","expires_in":3599,"ext_expires_in":0,"access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIn <truncated> aWReH7P0s0tjTBX8wGWqJUdDA"}
    ```

## Validate the token

Ensure that you got the correct token:

1. Copy and paste the token you got in the previous step into [JWT](https://jwt.ms) in order to decode it.
2. Validate that you get a 'roles' claim with the desired permissions.
3. In the following image, you can see a decoded token acquired from an app with permissions to all Microsoft Defender for Cloud Apps roles:

    ![Screenshot that shows the decoded token.](media/api-authentication-application/webapp-decoded-token.png)

## Use the token to access Microsoft Defender for Cloud Apps API

1. Choose the API you want to use. For more information, see [Defender for Cloud Apps APIs](api-introduction).
2. Set the authorization header in the http request you send to "Bearer {token}" (Bearer is the authorization scheme).
3. The expiration time of the token is one hour. You can send more than one request with the same token.

    The following is an example of sending a request to get a list of alerts **using C#**:

    ```C
        var httpClient = new HttpClient();
    
        var request = new HttpRequestMessage(HttpMethod.Get, "https://portal.cloudappsecurity.com/cas/api/v1/alerts/");
    
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", token);
    
        var response = httpClient.SendAsync(request).GetAwaiter().GetResult();
    
        // Do something useful with the response
    ```