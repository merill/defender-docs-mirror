---
layout: Conceptual
title: Hello World for Microsoft Defender XDR REST API - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/api-hello-world
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to create an app and use a token to access the Microsoft Defender XDR APIs
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
document_id: abcae5a0-1985-3e3e-6af3-a33093df9a0d
document_version_independent_id: abcae5a0-1985-3e3e-6af3-a33093df9a0d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/api-hello-world.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-hello-world
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/api-hello-world.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 66f2e878-f9fd-1944-4c7b-dec513c6063c
---

# Hello World for Microsoft Defender XDR REST API - Microsoft Defender XDR | Microsoft Learn

Important

Some information relates to prereleased product which may be substantially modified before its general availability. Microsoft makes no warranties, express or implied, with respect to the information provided here.

## Get incidents using a simple PowerShell script

It should take 5 to 10 minutes to complete this project. This time estimate includes registering the application, and applying the code from the PowerShell sample script.

### Register an app in Microsoft Entra ID

1. Sign in to [Azure](https://portal.azure.com).
2. Navigate to **Microsoft Entra ID** &gt; **App registrations** &gt; **New registration**.

    [![The New registration section in the Microsoft Defender portal](/en-us/defender/media/atp-azure-new-app2.png)](/en-us/defender/media/atp-azure-new-app2.png#lightbox)
3. In the registration form, choose a name for your application, then select **Register**. Selecting a redirect URI is optional. You don't need one to complete this example.
4. On your application page, select **API Permissions** &gt; **Add permission** &gt; **APIs my organization uses** &gt;, type **Microsoft Threat Protection**, and select **Microsoft Threat Protection**. Your app can now access Microsoft Defender XDR.

    Tip

    *Microsoft Threat Protection* is a former name for Microsoft Defender XDR, and doesn't appear in the original list. You need to start writing its name in the text box to see it appear. [![The section of APIs usage in the Microsoft Defender portal](/en-us/defender/media/apis-in-my-org-tab.PNG)](/en-us/defender/media/apis-in-my-org-tab.PNG#lightbox)

    - Choose **Application permissions** &gt; **Incident.Read.All** and select **Add permissions**.

        [![An application's permissions pane in the Microsoft Defender portal](/en-us/defender/media/request-api-permissions.PNG)](/en-us/defender/media/request-api-permissions.PNG#lightbox)
5. Select **Grant admin consent**. Every time you add a permission, you must select **Grant admin consent** for it to take effect.

    [![ The Grant admin consent section in the Microsoft Defender portal](/en-us/defender/media/grant-consent.PNG)](/en-us/defender/media/grant-consent.PNG#lightbox)
6. Add a secret to the application. Select **Certificates & secrets**, add a description to the secret, then select **Add**.

    Tip

    After you select **Add**, select **copy the generated secret value**. You won't be able to retrieve the secret value after you leave.

    [![ The add secret section in the Microsoft Defender portal](/en-us/defender/media/webapp-create-key2.png)](/en-us/defender/media/webapp-create-key2.png#lightbox)
7. Record your application ID and your tenant ID somewhere safe. They're listed under **Overview** on your application page.

    [![The Overview section in the Microsoft Defender portal](/en-us/defender/media/app-and-tenant-ids.png)](/en-us/defender/media/app-and-tenant-ids.png#lightbox)

### Get a token using the app and use the token to access the API

For more information on Microsoft Entra tokens, see the [Microsoft Entra tutorial](/en-us/azure/active-directory/develop/active-directory-v2-protocols-oauth-client-creds).

Important

Although the example in this demo app encourages you to paste in your secret value for testing purposes, you should **never hardcode secrets** into an application running in production. A third party could use your secret to access resources. You can help keep your app's secrets secure by using [Azure Key Vault](/en-us/azure/key-vault/general/about-keys-secrets-certificates). For a practical example of how you can protect your app, see [Manage secrets in your server apps with Azure Key Vault](/en-us/training/modules/manage-secrets-with-azure-key-vault/).

1. Copy the following script and paste it into your favorite text editor. Save as **Get-Token.ps1**. You can also run the code as-is in PowerShell ISE, but you need save it because we need to run it again when we use the incident-fetching script in the next section.

    This script generates a token and save it in the working folder under the name, *Latest-token.txt*.

    ```PowerShell
    # This script gets the app context token and saves it to a file named "Latest-token.txt" under the current directory.
    # Paste in your tenant ID, client ID and app secret (App key).
    
    $tenantId = '' # Paste your directory (tenant) ID here
    $clientId = '' # Paste your application (client) ID here
    $appSecret = '' # # Paste your own app secret here to test, then store it in a safe place!
    
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

#### Validate the token

1. Copy and paste the token you received into [JWT](https://jwt.ms) to decode it.
2. *JWT* stands for *JSON Web Token*. The decoded token contains several of JSON-formatted items or claims. Make sure that the *roles* claim within the decoded token contains the desired permissions.

    In the following image, you can see a decoded token acquired from an app, with `Incidents.Read.All`, `Incidents.ReadWrite.All`, and `AdvancedHunting.Read.All` permissions:

    [![The Decoded Token section in the Microsoft Defender portal](/en-us/defender/media/api-jwt-ms.png)](/en-us/defender/media/api-jwt-ms.png#lightbox)

### Get a list of recent incidents

The following script uses **Get-Token.ps1** to access the API. It then retrieves a list of incidents that were last updated within the past 48 hours, and saves the list as a JSON file.

Important

Save this script in the same folder you saved **Get-Token.ps1**.

```PowerShell
# This script returns incidents last updated within the past 48 hours.

$token = ./Get-Token.ps1

# Get incidents from the past 48 hours.
# The script may appear to fail if you don't have any incidents in that time frame.
$dateTime = (Get-Date).ToUniversalTime().AddHours(-48).ToString("o")

# This URL contains the type of query and the time filter we created above.
# Note that `$filter` does not refer to a local variable in our script --
# it's actually an OData operator and part of the API's syntax.
$url = "https://api.security.microsoft.com/api/incidents`?`$filter=lastUpdateTime+ge+$dateTime"

# Set the webrequest headers
$headers = @{
    'Content-Type' = 'application/json'
    'Accept' = 'application/json'
    'Authorization' = "Bearer $token"
}

# Send the request and get the results.
$response = Invoke-WebRequest -Method Get -Uri $url -Headers $headers -ErrorAction Stop

# Extract the incidents from the results.
$incidents =  ($response | ConvertFrom-Json).value | ConvertTo-Json -Depth 99

# Get a string containing the execution time. We concatenate that string to the name 
# of the output file to avoid overwriting the file on consecutive runs of the script.
$dateTimeForFileName = Get-Date -Format o | foreach {$_ -replace ":", "."}

# Save the result as json
$outputJsonPath = "./Latest Incidents $dateTimeForFileName.json"

Out-File -FilePath $outputJsonPath -InputObject $incidents
```

You're all done! You've successfully:

- Created and registered an application.
- Granted permission for that application to read alerts.
- Connected to the API.
- Used a PowerShell script to return incidents updated in the past 48 hours.