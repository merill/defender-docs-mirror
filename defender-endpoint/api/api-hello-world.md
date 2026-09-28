---
layout: Conceptual
title: Hello World for Microsoft Defender for Endpoint API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/api-hello-world
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Create a practice 'Hello world'-style API call to the Microsoft Defender for Endpoint API.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom:
- api
- sfi-image-nochange
ms.date: 2026-01-08T00:00:00.0000000Z
locale: en-us
document_id: 49248f86-86ec-d5a5-492f-796bd2373de6
document_version_independent_id: 49248f86-86ec-d5a5-492f-796bd2373de6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/api-hello-world.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/api-hello-world
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/api-hello-world.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: caa34783-75c2-32b0-cdd9-a5c029139d3b
---

# Hello World for Microsoft Defender for Endpoint API - Microsoft Defender for Endpoint | Microsoft Learn

Note

If you're a US Government customer, use the URIs listed in [Microsoft Defender for Endpoint for US Government customers](/en-us/defender-endpoint/gov#api).

Tip

For better performance, instead of using api.security.microsoft.com, use a server closer to your geolocation:

- us.api.security.microsoft.com
- eu.api.security.microsoft.com
- uk.api.security.microsoft.com
- au.api.security.microsoft.com
- swa.api.security.microsoft.com
- ina.api.security.microsoft.com
- aea.api.security.microsoft.com

## Get Alerts using a simple PowerShell script

### How long it takes to go through this example?

It only takes 5 minutes done in two steps:

- Application registration
- Use examples: only requires copy/paste of a short PowerShell script

### Do I need a permission to connect?

For the Application registration stage, you must have an appropriate role assigned in your Microsoft Entra tenant. For more details about roles, see [Permission options](../user-roles#permission-options).

### Step 1 - Create an App in Microsoft Entra ID

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Entra ID** &gt; **App registrations** &gt; **New registration**.

    [![The App registrations option under the Manage pane in the Microsoft Entra admin center](../media/atp-azure-new-app2.png)](../media/atp-azure-new-app2.png#lightbox)
3. In the registration form, choose a name for your application and then select **Register**.
4. Allow your Application to access Defender for Endpoint and assign it **'Read all alerts'** permission:

    - On your application page, select **API Permissions** &gt; **Add permission** &gt; **APIs my organization uses** &gt; type **WindowsDefenderATP** and select **WindowsDefenderATP**.

        Note

        WindowsDefenderATP does not appear in the original list. You need to start writing its name in the text box to see it appear.

        [![The API permissions option under the Manage pane in the Microsoft Entra admin center](../media/add-permission.png)](../media/add-permission.png#lightbox)
    - Choose **Application permissions** &gt; **Alert.Read.All**, and then select **Add permissions**.

        [![The permission type and settings panes in the Request API permissions page](../media/application-permissions.png)](../media/application-permissions.png#lightbox)

        Important

        You need to select the relevant permissions. **Read All Alerts** is only an example.

        For example:

        - To [run advanced queries](run-advanced-query-api), select 'Run advanced queries' permission.
        - To [isolate a machine](isolate-machine), select 'Isolate machine' permission.
        - To determine which permission you need, see the **Permissions** section in the API you're interested to call.
5. Select **Grant consent**.

    Note

    Every time you add permission, you must click on **Grant consent** for the new permission to take effect.

    [![The grant permission consent option in the Microsoft Entra admin center](../media/grant-consent.png)](../media/grant-consent.png#lightbox)
6. Add a secret to the application.

    Select **Certificates & secrets**, add description to the secret and select **Add**.

    Important

    After click Add, **copy the generated secret value**. You won't be able to retrieve after you leave!

    [![The Certificates &amp; secrets menu item in the Manage pane in the Microsoft Entra admin center](../media/webapp-create-key2.png)](../media/webapp-create-key2.png#lightbox)
7. Write down your application ID and your tenant ID.

    On your application page, go to **Overview** and copy the following:

    [![The application details pane under the Overview menu item in the Microsoft Entra admin center](../media/app-and-tenant-ids.png)](../media/app-and-tenant-ids.png#lightbox)

Done! You've successfully registered an application!

### Step 2 - Get a token using the App and use this token to access the API

Tip

Some Microsoft Defender for Endpoint APIs continue to require access tokens issued for the legacy resource `https://api.securitycenter.microsoft.com`. If the token audience doesn't match the resource expected by the API, requests fail with `403 Forbidden`, even if the API endpoint uses `https://api.security.microsoft.com`. Use `https://api.securitycenter.microsoft.com` as the resource or scope when acquiring tokens.

Copy the following script to PowerShell ISE or to a text editor, and save it as `Get-Token.ps1`. Running this script generates a token and saves it in the working folder under the name `Latest-token.txt`.

```powershell
# This code gets the application context token and saves it to a file named "Latest-token.txt" in the current directory.

$tenantId = '' ### Paste your tenant ID here
$appId = '' ### Paste your Application (client) ID here
$appSecret = '' ### Paste your Application secret (App key) here to test, and then store it in a safe place!

$resourceAppIdUri = 'https://api.securitycenter.microsoft.com/'
$oAuthUri = "https://login.microsoftonline.com/$TenantId/oauth2/token"
$authBody = [Ordered] @{
  resource = "$resourceAppIdUri"
  client_id = "$appId"
  client_secret = "$appSecret"
  grant_type = 'client_credentials'
}
$authResponse = Invoke-RestMethod -Method Post -Uri $oAuthUri -Body $authBody -ErrorAction Stop
$token = $authResponse.access_token
Out-File -FilePath "./Latest-token.txt" -InputObject $token
return $token
```

#### Validate the token

1. Run the script to generate the `Latest-token.txt` file.
2. In a web browser, open https://jwt.ms/, and then copy the token (the contents of the `Latest-token.txt`) in the **Enter token below** box.
3. On the **Decoded token** tab, find the **roles** section, and verify it contains **Alert.Read.All** permissions as shown in the following image:

[![Screenshot of jwt.ms showing a copied token and the decoded token with the Roles section and the Alert.Read.All permission highlighted.](../media/api-jwt-ms.png)](../media/api-jwt-ms.png#lightbox)

### Let's get the Alerts!

- The following script uses `Get-Token.ps1` to access the API and gets alerts for the past 48 hours.
- Save this script in the same folder you saved the previous script `Get-Token.ps1`.
- The script creates two files (json and csv) with the data in the same folder as the scripts.

```powershell
# Returns Alerts created in the past 48 hours.

$token = ./Get-Token.ps1       #run the script Get-Token.ps1  - make sure you are running this script from the same folder of Get-Token.ps1

# Get Alert from the last 48 hours. Make sure you have alerts in that time frame.
$dateTime = (Get-Date).ToUniversalTime().AddHours(-48).ToString("o")

# The URL contains the type of query and the time filter we created previously.
# Learn more about other query options and filters: https://learn.microsoft.com/defender-endpoint/api/get-alerts.
$url = "https://api.security.microsoft.com/api/alerts?`$filter=alertCreationTime ge $dateTime"

# Set the WebRequest headers
$headers = @{
  'Content-Type' = 'application/json'
  Accept = 'application/json'
  Authorization = "Bearer $token"
}

# Send the web request and get the results.
$response = Invoke-WebRequest -Method Get -Uri $url -Headers $headers -ErrorAction Stop

# Extract the alerts from the results.
$alerts =  ($response | ConvertFrom-Json).value | ConvertTo-Json

# Get string with the execution time. We concatenate that string to the output file to avoid overwrite the file.
$dateTimeForFileName = Get-Date -Format o | foreach {$_ -replace ":", "."}

# Save the result as json and as csv.
$outputJsonPath = "./Latest Alerts $dateTimeForFileName.json"
$outputCsvPath = "./Latest Alerts $dateTimeForFileName.csv"

Out-File -FilePath $outputJsonPath -InputObject $alerts
($alerts | ConvertFrom-Json) | Export-CSV $outputCsvPath -NoTypeInformation
```

You're all done! You successfully:

- Created and registered and application.
- Granted permission for that application to read alerts.
- Connected the API.
- Used a PowerShell script to return alerts created in the past 48 hours.