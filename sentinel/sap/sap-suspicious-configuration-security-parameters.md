---
layout: Conceptual
title: SAP security parameters monitored by the Microsoft Sentinel solution for SAP to detect suspicious configuration changes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/sap-suspicious-configuration-security-parameters
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
ms.reviewer: mapankra
description: Learn about the security parameters in the SAP system that the Microsoft Sentinel solution for SAP applications monitors for suspicious configuration changes.
ms.author: monaberdugo
author: mberdugo
ms.topic: reference
ms.date: 2026-08-04T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
locale: en-us
document_id: d0bec8e9-6363-d56a-c5e8-4d5a750a0164
document_version_independent_id: 04e9a7e0-6240-20e0-5c38-240eff615b09
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/sap-suspicious-configuration-security-parameters.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/sap-suspicious-configuration-security-parameters
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/sap-suspicious-configuration-security-parameters.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 19e7f1e6-1331-75a0-a9fa-cec5a0ae26f5
---

# SAP security parameters monitored by the Microsoft Sentinel solution for SAP to detect suspicious configuration changes | Microsoft Learn

This article lists the static security parameters in the SAP system that the Microsoft Sentinel solution for SAP applications monitors as part of the [*SAP - (Preview) Sensitive Static Parameter has Changed* analytics rule](sap-solution-security-content).

The Microsoft Sentinel solution for SAP applications provides updates for this content according to SAP best practice changes. Add parameters to watch for by changing values according to your organization's needs, and turn off specific parameters in the [*SAPSystemParameters* watchlist](sap-solution-security-content).

This article doesn't describe the parameters, and isn't a recommendation to configuring the parameters. For configuration considerations, consult your SAP admins. For parameter descriptions, see the SAP documentation.

Content in this article is intended for your **SAP BASIS** teams.

## Prerequisites

For the Microsoft Sentinel solution for SAP applications to successfully monitor the SAP security parameters, the solution needs to successfully monitor the SAP PAHI table at regular intervals. Confirm with your SAP BASIS team that the `SAP_COLLECTOR_FOR_PERFMONITOR` job is scheduled to run hourly so that the PAHI table stays current.

### Authentication parameters

| Parameter | Security value/considerations |
| --- | --- |
| auth/no\_check\_in\_some\_cases | While this parameter might improve performance, it can also pose a security risk by allowing users to perform actions they might not have permission for. |
| auth/object\_disabling\_active | Can help improve security by reducing the number of inactive accounts with unnecessary permissions. |
| auth/rfc\_authority\_check | High. Enabling this parameter helps prevent unauthorized access to sensitive data and functions via RFCs. |

### Gateway parameters

| Parameter | Security value/considerations |
| --- | --- |
| gw/accept\_remote\_trace\_level | The parameter can be configured to restrict the trace level accepted from external systems. Setting a lower trace level might reduce the amount of information that external systems can obtain about the internal workings of the SAP system. |
| gw/acl\_mode | High. This parameter controls access to the gateway and helps prevent unauthorized access to the SAP system. |
| gw/logging | High. This parameter can be used to monitor and detect suspicious activity or potential security breaches. |
| gw/monitor |  |
| gw/sim\_mode | Enabling this parameter can be useful for testing purposes and can help prevent any unintended changes to the target system. |

### Internet Communication Manager (ICM) parameters

| Parameter | Security value/considerations |
| --- | --- |
| icm/accept\_remote\_trace\_level | Medium Allowing remote trace level changes can provide valuable diagnostic information to attackers and potentially compromise system security. |

### Sign-in parameters

| Parameter | Security value/considerations |
| --- | --- |
| login/accept\_sso2\_ticket | Enabling SSO2 can provide a more streamlined and convenient user experience, but also introduces extra security risks. If an attacker gains access to a valid SSO2 ticket, they might be able to impersonate a legitimate user and gain unauthorized access to sensitive data or perform malicious actions. |
| login/create\_sso2\_ticket |  |
| login/disable\_multi\_gui\_login | This parameter can help improve security by ensuring that users are only logged in to one session at a time. |
| login/failed\_user\_auto\_unlock |  |
| login/fails\_to\_session\_end | High. This parameter helps prevent brute-force attacks on user accounts. |
| login/fails\_to\_user\_lock | Helps prevent unauthorized access to the system and helps protect user accounts from being compromised. |
| login/min\_password\_diff | High. Requiring a minimum number of character differences can help prevent users from choosing weak passwords that can easily be guessed. |
| login/min\_password\_digits | High. This parameter increases the complexity of passwords and makes them harder to guess or crack. |
| login/min\_password\_letters | Specifies the minimum number of letters that must be included in a user's password. Setting a higher value helps increase password strength and security. |
| login/min\_password\_lng | Specifies the minimum length that a password can be. Setting a higher value for this parameter can improve security by ensuring that passwords aren't easily guessed. |
| login/min\_password\_lowercase |  |
| login/min\_password\_specials |  |
| login/min\_password\_uppercase |  |
| login/multi\_login\_users | Enabling this parameter can help prevent unauthorized access to SAP systems by limiting the number of concurrent logins for a single user. When this parameter is set to `0`, only one login session is allowed per user, and other login attempts are rejected. This can help prevent unauthorized access to SAP systems in case a user's login credentials are compromised or shared with others. |
| login/no\_automatic\_user\_sapstar | High. This parameter helps prevent unauthorized access to the SAP system via the default SAP\* account. |
| login/password\_change\_for\_SSO | High. Enforcing password changes can help prevent unauthorized access to the system by attackers who might have obtained valid credentials through phishing or other means. |
| login/password\_change\_waittime | Setting an appropriate value for this parameter can help ensure that users change their passwords regularly enough to maintain the security of the SAP system. At the same time, setting the wait time too short can be counterproductive because users might be more likely to reuse passwords or choose weak passwords that are easier to remember. |
| login/password\_compliance\_to\_current\_policy | High. Enabling this parameter can help ensure that users comply with the current password policy when changing passwords, which reduces the risk of unauthorized access to SAP systems. When this parameter is set to `1`, users are prompted to comply with the current password policy when changing their passwords. |
| login/password\_downwards\_compatibility |  |
| login/password\_expiration\_time | Setting this parameter to a lower value can improve security by ensuring that passwords are changed frequently. |
| login/password\_history\_size | This parameter prevents users from repeatedly using the same passwords, which can improve security. |
| login/password\_max\_idle\_initial | Setting a lower value for this parameter can improve security by ensuring that idle sessions aren't left open for extended periods of time. |
| login/ticket\_only\_by\_https | High. Using HTTPS for ticket transmission encrypts the data in transit, making it more secure. |

### Remote dispatcher parameters

| Parameter | Security value/considerations |
| --- | --- |
| rdisp/gui\_auto\_logout | High. automatically logging out inactive users can help prevent unauthorized access to the system by attackers who might have access to a user's workstation. |
| rfc/ext\_debugging |  |
| rfc/reject\_expired\_passwd | Enabling this parameter can be helpful when enforcing password policies and preventing unauthorized access to SAP systems. When this parameter is set to `1`, RFC connections are rejected if the user's password expired, and the user is prompted to change their password before they can connect. This helps ensure that only authorized users with valid passwords can access the system. |
| rsau/enable | High. This Security Audit log can provide valuable information for detecting and investigating security incidents. |
| rsau/max\_diskspace/local | Setting an appropriate value for this parameter helps prevent the local audit logs from consuming too much disk space, which could lead to system performance issues or even denial of service attacks. On the other hand, setting a value that's too low might result in the loss of audit log data, which might be required for compliance and auditing. |
| rsau/max\_diskspace/per\_day |  |
| rsau/max\_diskspace/per\_file | Setting an appropriate value helps manage the size of audit files and avoid storage issues. |
| rsau/selection\_slots | Helps ensure that audit files are retained for a longer period of time, which can be useful in a security breach. |
| rspo/auth/pagelimit | This parameter doesn't directly affect the security of the SAP system, but can help to prevent unauthorized access to sensitive authorization data. By limiting the number of entries displayed per page, it can reduce the risk of unauthorized individuals viewing sensitive authorization information. |

### Secure network communications (SNC) parameters

| Parameter | Security value/considerations |
| --- | --- |
| snc/accept\_insecure\_cpic | Enabling this parameter can increase the risk of data interception or manipulation, because it accepts SNC-protected connections that don't meet the minimum security standards. Therefore, the recommended security value for this parameter is to set it to `0`, which means that only SNC connections that meet the minimum security requirements are accepted. |
| snc/accept\_insecure\_gui | Setting the value of this parameter to `0` is recommended to ensure that SNC connections made through the SAP GUI are secure, and to reduce the risk of unauthorized access or interception of sensitive data. Allowing insecure SNC connections might increase the risk of unauthorized access to sensitive information or data interception, and should only be done when there's a specific need and the risks are properly assessed. |
| snc/accept\_insecure\_r3int\_rfc | Enabling this parameter can increase the risk of data interception or manipulation, because it accepts SNC-protected connections that don't meet the minimum security standards. Therefore, the recommended security value for this parameter is to set it to `0`, which means that only SNC connections that meet the minimum security requirements are accepted. |
| snc/accept\_insecure\_rfc | Enabling this parameter can increase the risk of data interception or manipulation, because it accepts SNC-protected connections that don't meet the minimum security standards. Therefore, the recommended security value for this parameter is to set it to `0`, which means that only SNC connections that meet the minimum security requirements are accepted. |
| snc/data\_protection/max | Setting a high value for this parameter can increase the level of data protection and reduce the risk of data interception or manipulation. The recommended security value for this parameter depends on the organization's specific security requirements and risk management strategy. |
| snc/data\_protection/min | Setting an appropriate value for this parameter helps ensure that SNC-protected connections provide a minimum level of data protection. This setting helps prevent sensitive information from being intercepted or manipulated by attackers. The value of this parameter should be set based on the security requirements of the SAP system and the sensitivity of the data transmitted over SNC-protected connections. |
| snc/data\_protection/use |  |
| snc/enable | When enabled, SNC provides an extra layer of security by encrypting data transmitted between systems. |
| snc/extid\_login\_diag | Enabling this parameter can be helpful for troubleshooting SNC-related issues, because it provides extra diagnostic information. However, the parameter might also expose sensitive information about the external security products used by the system, which could be a potential security risk if that information falls into the wrong hands. |
| snc/extid\_login\_rfc |  |

### Web dispatcher parameters

| Parameter | Security value/considerations |
| --- | --- |
| wdisp/ssl\_encrypt | High. This parameter ensures that data transmitted over HTTP is encrypted, which helps prevent eavesdropping and data tampering. |