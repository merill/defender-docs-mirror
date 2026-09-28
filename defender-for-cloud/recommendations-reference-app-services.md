---
layout: Conceptual
title: Reference table for Azure App Service security recommendations - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/recommendations-reference-app-services
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
description: This article lists the Microsoft Defender for Cloud security recommendations for Azure App Service.
ms.topic: reference
ms.date: 2026-06-30T00:00:00.0000000Z
ms.custom: generated
ai-usage: ai-assisted
locale: en-us
document_id: 86e209b4-a680-9c66-ced2-8689522d2319
document_version_independent_id: d6ea34a9-b4ef-00ac-10bb-c3a5b145048b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/recommendations-reference-app-services.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/recommendations-reference-app-services
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/recommendations-reference-app-services.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 2c33bf2a-aedd-1fb8-032e-8483fe810a99
---

# Reference table for Azure App Service security recommendations - Microsoft Defender for Cloud | Microsoft Learn

This article lists all the security recommendations you might see issued by the Microsoft Defender for Cloud plan - Microsoft Defender for Cloud for Azure App Service.

The recommendations that appear in your environment are based on the resources that you're protecting and on your customized configuration. You can [see the recommendations in the portal](https://portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/5) that apply to your resources.

To learn about actions that you can take in response to these recommendations, see [Remediate recommendations in Defender for Cloud](implement-security-recommendations).

Tip

If a recommendation's description says *No related policy*, usually it's because that recommendation is dependent on a different recommendation and *its* policy.

For example, the recommendation *Endpoint protection health failures should be remediated* relies on the recommendation that checks whether an endpoint protection solution is even installed (*Endpoint protection solution should be installed*). The underlying recommendation *does* have a policy. Limiting the policies to only the foundational recommendation simplifies policy management.

## App Services recommendations

### API App should only be accessible over HTTPS

**Description**: Use of HTTPS ensures server/service authentication and protects data in transit from network layer eavesdropping attacks. (Related policy: [API App should only be accessible over HTTPS](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2fb7ddfbdc-1260-477d-91fd-98bd9be789a6)).

**Severity**: Medium

### CORS should not allow every resource to access API Apps

**Description**: Cross-Origin Resource Sharing (CORS) should not allow all domains to access your API app. Allow only required domains to interact with your API app. (Related policy: [CORS should not allow every resource to access your API App](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fmicrosoft.authorization%2fpolicydefinitions%2f358c20a6-3f9e-4f0e-97ff-c6ce485e2aac)).

**Severity**: Low

### CORS should not allow every resource to access Function Apps

**Description**: Cross-Origin Resource Sharing (CORS) should not allow all domains to access your Function app. Allow only required domains to interact with your Function app. (Related policy: [CORS should not allow every resource to access your Function Apps](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fmicrosoft.authorization%2fpolicydefinitions%2f0820b7b9-23aa-4725-a1ce-ae4558f718e5)).

**Severity**: Low

### CORS should not allow every resource to access Web Applications

**Description**: Cross-Origin Resource Sharing (CORS) should not allow all domains to access your web application. Allow only required domains to interact with your web app. (Related policy: [CORS should not allow every resource to access your Web Applications](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fmicrosoft.authorization%2fpolicydefinitions%2f5744710e-cc2f-4ee8-8809-3b11e89f4bc9)).

**Severity**: Low

### Custom service accounts should be configured for App Engine applications

**Description**: Defender for Cloud identified the use of the default App Engine service account for your applications. This poses a risk because default accounts are often granted broad permissions, such as the Editor role, at the project level, which can be exploited if compromised. Custom service accounts restrict permissions to only those needed for operations, minimizing potential exposure and following the principle of least privilege.

**Severity**: Medium

### Diagnostic logs in App Service should be enabled

**Description**: Audit enabling of diagnostic logs on the app. This enables you to recreate activity trails for investigation purposes if a security incident occurs or your network is compromised (No related policy).

**Severity**: Medium

### Ensure API app has Client Certificates Incoming client certificates set to On

**Description**: Client certificates allow for the app to request a certificate for incoming requests. Only clients that have a valid certificate will be able to reach the app. (Related policy: [Ensure API app has 'Client Certificates (Incoming client certificates)' set to 'On'](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f0c192fe8-9cbb-4516-85b3-0ade8bd03886)).

**Severity**: Medium

### Identity-Aware Proxy protection should be enabled on App Engine applications

**Description**: Defender for Cloud identified that Identity-Aware Proxy (IAP) is disabled in App Engine applications. IAP is a centralized authorization layer for HTTPS that verifies user identities and enforces contextual access controls before requests reach your application. Without IAP, your App Engine may be exposed to unauthorized access, increasing the risk of exploitation. Enabling IAP is recommended to strengthen your application's security.

**Severity**: Medium

### FTPS should be required in API apps

**Description**: Enable FTPS enforcement for enhanced security (Related policy: [FTPS only should be required in your API App](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f9a1b8c48-453a-4044-86c3-d8bfd823e4f5)).

**Severity**: High

### FTPS should be required in function apps

**Description**: Enable FTPS enforcement for enhanced security (Related policy: [FTPS only should be required in your Function App](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f399b2637-a50f-4f95-96f8-3a145476eb15)).

**Severity**: High

### FTPS should be required in web apps

**Description**: Enable FTPS enforcement for enhanced security (Related policy: [FTPS should be required in your Web App](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f4d24b6d4-5e53-4a4f-a7f4-618fa573ee4b)).

**Severity**: High

### Function App should only be accessible over HTTPS

**Description**: Use of HTTPS ensures server/service authentication and protects data in transit from network layer eavesdropping attacks. (Related policy: [Function App should only be accessible over HTTPS](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f6d555dd1-86f2-4f1c-8ed7-5abae7c6cbab)).

**Severity**: Medium

### Function apps should have Client Certificates (Incoming client certificates) enabled

**Description**: Client certificates allow for the app to request a certificate for incoming requests. Only clients with valid certificates will be able to reach the app. (Related policy: [Function apps should have 'Client Certificates (Incoming client certificates)' enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2feaebaea7-8013-4ceb-9d14-7eb32271373c)).

**Severity**: Medium

### Java should be updated to the latest version for API apps

**Description**: Periodically, newer versions are released for Java either due to security flaws or to include additional functionality. Using the latest Python version for API apps is recommended to benefit from security fixes, if any, and/or new functionalities of the latest version. (Related policy: [Ensure that 'Java version' is the latest, if used as a part of the API app](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f88999f4c-376a-45c8-bcb3-4058f713cf39)).

**Severity**: Medium

### Managed identity should be used in API apps

**Description**: For enhanced authentication security, use a managed identity. On Azure, managed identities eliminate the need for developers to have to manage credentials by providing an identity for the Azure resource in Microsoft Entra ID and using it to obtain Microsoft Entra ID (Microsoft Entra ID) tokens. (Related policy: [Managed identity should be used in your API App](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2fc4d441f8-f9d9-4a9e-9cef-e82117cb3eef)).

**Severity**: Medium

### Managed identity should be used in function apps

**Description**: For enhanced authentication security, use a managed identity. On Azure, managed identities eliminate the need for developers to have to manage credentials by providing an identity for the Azure resource in Microsoft Entra ID and using it to obtain Microsoft Entra ID (Microsoft Entra ID) tokens. (Related policy: [Managed identity should be used in your Function App](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f0da106f2-4ca3-48e8-bc85-c638fe6aea8f)).

**Severity**: Medium

### Managed identity should be used in web apps

**Description**: For enhanced authentication security, use a managed identity. On Azure, managed identities eliminate the need for developers to have to manage credentials by providing an identity for the Azure resource in Microsoft Entra ID and using it to obtain Microsoft Entra ID (Microsoft Entra ID) tokens. (Related policy: [Managed identity should be used in your Web App](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f2b9ad585-36bc-4615-b300-fd4435808332)).

**Severity**: Medium

### Microsoft Defender for App Service should be enabled

**Description**: Microsoft Defender for App Service leverages the scale of the cloud, and the visibility that Azure has as a cloud provider, to monitor for common web app attacks. Microsoft Defender for App Service can discover attacks on your applications and identify emerging attacks.

Remediating this recommendation will result in charges for protecting your App Service plans. If you don't have any App Service plans in this subscription, no charges will be incurred. If you create any App Service plans on this subscription in the future, they will automatically be protected and charges will begin at that time. Learn more in [Protect your web apps and APIs](defender-for-app-service-introduction). (Related policy: [Azure Defender for App Service should be enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fmicrosoft.authorization%2fpolicyDefinitions%2f2913021d-f2fd-4f3d-b958-22354e2bdbcb)).

**Severity**: High

### PHP should be updated to the latest version for API apps

**Description**: Periodically, newer versions are released for PHP software either due to security flaws or to include additional functionality. Using the latest PHP version for API apps is recommended to benefit from security fixes, if any, and/or new functionalities of the latest version. (Related policy: [Ensure that 'PHP version' is the latest, if used as a part of the API app](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f1bc1795e-d44a-4d48-9b3b-6fff0fd5f9ba)).

**Severity**: Medium

### Python should be updated to the latest version for API apps

**Description**: Periodically, newer versions are released for Python software either due to security flaws or to include additional functionality. Using the latest Python version for API apps is recommended to benefit from security fixes, if any, and/or new functionalities of the latest version. (Related policy: [Ensure that 'Python version' is the latest, if used as a part of the API app](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f74c3584d-afae-46f7-a20a-6f8adba71a16)).

**Severity**: Medium

### Remote debugging should be turned off for API App

**Description**: Remote debugging requires inbound ports to be opened on an API app. Remote debugging should be turned off. (Related policy: [Remote debugging should be turned off for API Apps](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fmicrosoft.authorization%2fpolicydefinitions%2fe9c8d085-d9cc-4b17-9cdc-059f1f01f19e)).

**Severity**: Low

### Remote debugging should be turned off for Function App

**Description**: Remote debugging requires inbound ports to be opened on an Azure Function app. Remote debugging should be turned off. (Related policy: [Remote debugging should be turned off for Function Apps](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fmicrosoft.authorization%2fpolicydefinitions%2f0e60b895-3786-45da-8377-9c6b4b6ac5f9)).

**Severity**: Low

### Remote debugging should be turned off for Web Applications

**Description**: Remote debugging requires inbound ports to be opened on a web application. Remote debugging is currently enabled. If you no longer need to use remote debugging, it should be turned off. (Related policy: [Remote debugging should be turned off for Web Applications](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fmicrosoft.authorization%2fpolicydefinitions%2fcb510bfd-1cba-4d9f-a230-cb0976f4bb71)).

**Severity**: Low

### TLS should be updated to the latest version for API apps

**Description**: Upgrade to the latest TLS version. (Related policy: [Latest TLS version should be used in your API App](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f8cb6aa8b-9e41-4f4e-aa25-089a7ac2581e)).

**Severity**: High

### TLS should be updated to the latest version for function apps

**Description**: Upgrade to the latest TLS version. (Related policy: [Latest TLS version should be used in your Function App](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2ff9d614c5-c173-4d56-95a7-b4437057d193)).

**Severity**: High

### TLS should be updated to the latest version for web apps

**Description**: Upgrade to the latest TLS version. (Related policy: [Latest TLS version should be used in your Web App](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2ff0e6e85b-9b9f-4a4b-b67b-f730d42f1b0b)).

**Severity**: High

### Web Application should only be accessible over HTTPS

**Description**: Use of HTTPS ensures server/service authentication and protects data in transit from network layer eavesdropping attacks. (Related policy: [Web Application should only be accessible over HTTPS](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2fa4af4a39-4135-47fb-b175-47fbdf85311d)).

**Severity**: Medium

### Web apps should request an SSL certificate for all incoming requests

**Description**: Client certificates allow for the app to request a certificate for incoming requests. Only clients that have a valid certificate will be able to reach the app. (Related policy: [Ensure WEB app has 'Client Certificates (Incoming client certificates)' set to 'On'](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f5bb220d9-2698-4ee4-8404-b9c30c9df609)).

**Severity**: Medium