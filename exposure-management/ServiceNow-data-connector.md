---
layout: Conceptual
title: ServiceNow data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/servicenow-data-connector
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to the ServiceNow data connector in Microsoft Security Exposure Management.
ms.topic: overview
ms.date: 2025-10-23T00:00:00.0000000Z
locale: en-us
document_id: b42c0796-c501-e557-f6b5-10e0b319da48
document_version_independent_id: b42c0796-c501-e557-f6b5-10e0b319da48
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/ServiceNow-data-connector.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: servicenow-data-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/ServiceNow-data-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
platformId: 2ac4c556-4117-2503-2baa-b37c8404c896
---

# ServiceNow data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

To set up the ServiceNow CMDB integration, you need to provide the hostname of your ServiceNow instance and valid credentials. The connector supports both Basic Authentication and OAuth 2.0 as authentication options for read only access. Basic Authentication requires username and password to connect, and OAuth 2.0 is based on granting client credentials.

Note

The ServiceNow connector supports Basic Authentication and OAuth 2.0 (client credentials grant). We recommend creating a dedicated user for use with data connectors in Exposure Management with least-privilege (cmdb\_read) role assignment.

## Configure ServiceNow with Basic Authentication

1. Find the hostname of your ServiceNow instance. For example, "contoso.service-now.com".
2. Create a New ServiceNow user:
    1. Follow [these steps] (https://docs.servicenow.com/en-US/bundle/vancouver-platform-administration/page/administer/users-and-groups/task/t_CreateAUser.html) to create a new user.
    2. Keep the **username (User Id) and password** you provided for future use.
    3. If there’s no password field, submit the form to create the user. Afterwards, when you select the new user, you'll receive the **Set Password** option.
    4. As you create the user, check the **Web service access only** box so that the user will be of dedicated use only for this integration.
3. Assign a **cmdb\_read** role to the user you've created. See these [detailed instructions](https://docs.servicenow.com/bundle/vancouver-platform-administration/page/administer/users-and-groups/task/t_AssignARoleToAUser.html).

## Configure OAuth 2.0 authentication (client credentials flow)

Use OAuth 2.0 client credentials to avoid storing a long‑lived password and to align with modern authentication standards.

### Prerequisites

1. Create (or identify) a ServiceNow user with at minimum the cmdb\_read role. For detailed instructions on creating a ServiceNow user and assigning roles, see the Configure ServiceNow with Basic Authentication section. We recommend a dedicated integration user; admin is only required temporarily if needed to install plugins.
2. Verify these plugins are installed (navigate to `sys_plugins.list`):
    - OAuth 2.0 (`com.snc.platform.security.oauth`)
    - REST API Provider (`com.glide.rest`)
    - Authentication scope (`com.glide.auth.scope`)
    - REST API Auth Scope Plugin (`com.glide.rest.auth.scope`)
3. Enable the client credentials grant:
    - Navigate to `sys_properties.list`
    - Property name: `glide.oauth.inbound.client.credential.grant_type.enabled`
    - Value: `true`
    - This property toggles support for the client credentials flow.

### Create the OAuth client (Application Registry)

1. Go to: System OAuth &gt; Application Registry.
2. Select: Create an OAuth API endpoint for external clients.
3. Fill mandatory fields (Name, etc.). Leave Redirect URL and Login URL blank (not used for client credentials).
4. Ensure Public Client remains unchecked (must be a confidential client).
5. Save the record.
6. In the Application Registries list view, customize the view (gear icon) to add the "OAuth Application User" column.
7. Set the OAuth Application User to the dedicated integration user (the token assumes this user's roles).
8. Open the record to copy the Client ID and generate/view the Client Secret.

### Token endpoint and grant details

- Token URL format: `https://<your-instance>.service-now.com/oauth_token.do`
- Grant type: `client_credentials`
- No redirect or authorization code is involved.
- Scopes: Not typically required; access is determined by the roles of the OAuth Application User.
- Required role on the integration user: `cmdb_read` (plus any additional roles needed for specific CI access, if applicable).

### Differences vs Basic Authentication

- Credentials rotate easily (regenerate client secret without changing the integration user password).
- Authentication is scoped to the roles of the OAuth Application User.
- Rate limits and data scope are unchanged; ensure a dedicated user to avoid API contention.
- No interactive login or redirect URLs are required.

### Troubleshooting OAuth

| Issue | Action |
| --- | --- |
| 401 Unauthorized | Confirm client ID/secret are correct; verify OAuth Application User is set; ensure `cmdb_read` role assigned; confirm property `glide.oauth.inbound.client.credential.grant_type.enabled = true`. |
| 403 Forbidden | User lacks required CMDB read role; add `cmdb_read`. |
| Invalid client | Regenerate client secret; verify you used "OAuth API endpoint for external clients". |
| Token endpoint failure | Verify plugins installed; confirm instance hostname correctness. |
| Empty or missing CMDB data | Validate the integration user can view CIs in the CMDB directly; check roles. |

For more background on ServiceNow OAuth, see ServiceNow documentation.

## Establish ServiceNow connection in Exposure Management

To establish a connection with ServiceNow in Exposure Management, follow these steps:

1. Open the [Data Connectors](https://security.microsoft.com/exposure-data-connectors) from the Exposure Management navigation and select **Connect** in the ServiceNow CMDB tile.
2. Choose your authentication method and enter the required information:
    - **For Basic Authentication**: Enter your ServiceNow instance hostname and the username and password created in the Basic Authentication configuration.
    - **For OAuth 2.0**: Choose the OAuth 2.0 authentication option and enter your instance hostname, Client ID, and Client Secret created in the OAuth configuration.
3. Select **Connect**. The system will authenticate using your chosen method and retrieve CMDB data.

[![Screenshot of connecting ServiceNow connector](media/service-now/oauth.png)](media/service-now/oauth.png#lightbox)

## Retrieved data

Exposure Management currently retrieves data on devices, their business application association, and business criticality. Additional data is also retrieved that helps identify the device, such as network adapter information and OS data.

The following fields are ingested via the connector:

| **Category** | **Properties** |
| --- | --- |
| **Devices** | - os- osVersion- osServicePack- cpuType- category- assetTag- virtual- serviceNowCriticality- usedFor- networkAdapters (see details below)- lastLoggedOnUser- mostFrequentUser- sysClassName- uPrimaryBusinessApplication (see details below) |
| **Network Adapter** | - name- sysId- macAddress- ipAddress- ipDefaultGateway |
| **Business Application** | - sysId- number- uCriticality- businessCriticality |

## Troubleshooting the connector

Here are some common issues that might arise when configuring the ServiceNow Connector, and suggestions for how to resolve them.

| **Error Type** | **Troubleshooting Action** |
| --- | --- |
| 'The remote server name couldn't be resolved' error message | Verify ServiceNow Instance hostname. Learn more about authentication to ServiceNow here: [Authentication (servicenow.com)](https://docs.servicenow.com/bundle/vancouver-platform-security/page/integrate/single-sign-on/concept/c_Authentication.html) |
| **Error code 401**: Authorization failure | An authorization failure indicates that credentials might not be correct, or there might not be sufficient permissions to access the ServiceNow data. Check your credentials and make sure they're correct and valid. Also check that your credentials have the required permissions. See the Configure ServiceNow with Basic Authentication section for details on how to ensure the cmdb\_read role is assigned. Another possible reason for this failure is the that your ServiceNow instance is configured to accept connections only from a limited range of IP addresses. In this case, see the guidance for adding the right set of IPs to your allowlist here: [Allowlist IP addresses](configure-data-connectors#allowlist-ip-addresses) |
| **Error code 403:** Access forbidden error | This error indicates that the provided credentials lack the necessary permissions to run the requested APIs. Update your credentials with the proper permissions as described in the Configure ServiceNow with Basic Authentication section, and make sure they have at minimum cmdb\_read role assigned. |
| **Error code 404:** Not found error | This error indicates that the requested endpoint wasn't found to be reachable. Verify that your ServiceNow Instance hostname is correct. |
| **Error code 429** 'Too many requests" | The system periodically pulls data from the configured external providers, which might have a limit on the number of concurrent requests. We recommend creating a dedicated user or account for the connector to avoid reaching this limit. |
| Bad URL error message | This error indicates that the requested endpoint wasn't found to be reachable. Verify that your ServiceNow Instance hostname is correct. |
| 'Temporary disconnected' or 'Temporary failure' error | In the case where this error message appears without any additional information, verify the connector configuration (hostname and credentials). If these are valid and the issue doesn't resolve on its own, contact Support. |
| Not seeing some ServiceNow CMDB CIs or assets in the ingested data | See Retrieved data for a description of the data expected to be retrieved by the ServiceNow CMDB connector. If there's still missing data, contact Support. |
| Not seeing any data ingested from ServiceNow CMDB | Review your connection status to ensure there are no errors. Validate that there are valid entries in your ServiceNow CMDB that correspond with the data we're retrieving. Run the sample [Advanced Hunting query](value-data-connectors#advanced-hunting) to check if any ServiceNow assets can be found in the Exposure Graph tables. If you're still unable to find your ServiceNow CMDB data, contact Support. |
| ServiceNow allowed IPs need to be configured to enable Exposure Management connectors to access ServiceNow | Read how to add the set of IPs to add to your allowlist here: [Allowlist IP addresses](configure-data-connectors#allowlist-ip-addresses) |