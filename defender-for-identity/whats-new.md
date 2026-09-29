---
layout: Conceptual
title: What's new - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/whats-new
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn about the latest Microsoft Defender for Identity features, sensor updates, security alerts, enhancements, and preview capabilities.
ms.date: 2026-09-23T00:00:00.0000000Z
ms.topic: overview
ms.reviewer: AbbyMSFT
ms.custom: sfi-image-nochange, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: e601dfee-5ce8-ca02-7614-89981fc949a2
document_version_independent_id: e601dfee-5ce8-ca02-7614-89981fc949a2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/whats-new.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: whats-new
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/whats-new.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 40ff3b63-e58a-65f9-679b-e6b024715b88
---

# What's new - Microsoft Defender for Identity | Microsoft Learn

This article is updated frequently to let you know what's new in the latest releases of Microsoft Defender for Identity.

## What's new scope and references

Defender for Identity releases are deployed gradually to customer organizations. If you don't see a feature documented here in your organization yet, check back later for the update.

For more information, see also:

- [What's new in Microsoft Defender XDR](/en-us/microsoft-365/security/defender/whats-new)
- [What's new in Microsoft Defender for Endpoint](/en-us/microsoft-365/security/defender-endpoint/whats-new-in-microsoft-defender-endpoint)
- [What's new in Microsoft Defender for Cloud Apps](/en-us/cloud-app-security/release-notes)

For updates about versions and features released six months ago or earlier, see the [What's new archive for Microsoft Defender for Identity](whats-new-archive).

## September 2026

### Automatic sensor v3.x activation and Windows auditing by default

The rollout differs for new Microsoft Defender for Endpoint customers and existing Defender for Identity customers:

**New Microsoft Defender for Endpoint customers:** If your organization is licensed for Defender for Identity, its first device was onboarded to Defender for Endpoint on or after September 13, 2026, and it doesn't already have a Defender for Identity workspace, Defender for Identity automatically creates a workspace when it identifies an eligible identity-role server. It also enables automatic sensor v3.x activation and Windows auditing by default.

This flow activates the Defender for Identity sensor capability on eligible servers that are already onboarded to Defender for Endpoint. It doesn't add a separate Defender for Identity installation, activate the sensor on other Defender for Endpoint servers, or affect servers that already have a Defender for Identity sensor.

**Existing Defender for Identity customers:** The change becomes available gradually. The Defender portal displays a notice before it enables the settings automatically. After the notice period ends, the portal enables the settings.

While the notice appears, select **Go to Advanced features** to enable the settings or **Opt out** to prevent automatic enablement.

The notice appears on the **Sensor management** tab of the **On-premises** settings page.

For more information, see [Activate the Defender for Identity sensor v3.x](deploy/activate-sensor#control-automatic-activation) and [Configure Windows event auditing](deploy/configure-windows-event-collection#control-automatic-windows-auditing).

### Identity Security dashboard and Coverage & Maturity

The Identity Security dashboard provides a centralized view of identity-related security risks and posture across your organization. Coverage & Maturity helps security teams understand identity protection across on-premises, cloud, SaaS, identity providers, and partner technologies, identify coverage and deployment gaps, and prioritize actions to improve identity security posture. For more information, see [Coverage & Maturity](/en-us/defender-xdr/identity-security/coverage-maturity).

### Sensor v3.x onboarding without Microsoft Defender for Endpoint deployment (Preview)

You can now activate the Defender for Identity sensor v3.x on eligible domain controllers without first onboarding them to Defender for Endpoint. This preview supports only new sensor v3.x deployments on eligible domain controllers running Windows Server 2019 or later. For more information, see [Activate the Defender for Identity sensor](deploy/activate-sensor#onboard-the-domain-controller-preview).

### Sensor v3.x support for additional identity server roles: AD CS, AD FS, and Entra Connect (Preview)

Defender for Identity sensor v3.x now supports eligible AD FS, AD CS, and Microsoft Entra Connect servers that aren't domain controllers and don't have an existing Defender for Identity sensor. For more information, see [Defender for Identity sensor v3.x prerequisites](deploy/deploy-sensor-v3).

### Combined Sensor management tab on the On-premises settings page

The **Onboarding** and **Sensors** tabs on the identity **On-premises** settings page are now combined into a single **Sensor management** tab that lists both installed sensors and servers eligible for activation. Automatic sensor v3.x activation is now configured on the **Advanced features** page. For more information, see [Manage and update Microsoft Defender for Identity sensors](sensor-settings).

## August 2026

### Defender for Identity sensor updates

| Version number | Updates |
| --- | --- |
| 2.255.19347.63719 | This sensor update includes security improvements. |

### Expanded automatic auditing support for AD CS, AD FS, and Entra Connect servers

Automatic Windows event auditing now configures auditing for AD FS, AD CS, and Microsoft Entra Connect. Auditing is configured automatically on any eligible server that runs Defender for Identity sensor v3.x, including servers that aren't domain controllers. For more information, see [Configure Defender for Identity to collect Windows events automatically](deploy/configure-windows-event-collection#configure-defender-for-identity-to-collect-windows-events-automatically).

## July 2026

### Defender for Identity sensor updates

| Version number | Updates |
| --- | --- |
| 2.255.19295.47272 | This sensor update adds support for a new Event Tracing for Windows (ETW) provider and includes other improvements. |

### Sensor v2.x to v3.x migration is now generally available

Migration of Defender for Identity sensors from v2.x to v3.x is now generally available. For more information, see [Migrate to Defender for Identity sensor v3.x](deploy/migrate-to-sensor-v3).

### Migrate Windows Server 2025 domain controllers to sensor v3.x

You can now migrate domain controllers running Windows Server 2025 from sensor v2.x to sensor v3.x. For more information, see [Migrate to Defender for Identity sensor v3.x](deploy/migrate-to-sensor-v3).

### Migration readiness reasons on the Sensors page

When a server is marked **Not ready for migration** on the **Sensors** page, you can now hover over the status to see a tooltip that lists the specific reasons the server doesn't meet the migration prerequisites. For more information, see [Troubleshoot "Not ready for migration" status](deploy/migrate-to-sensor-v3#troubleshoot-not-ready-for-migration-status).

### Expanded SaaS app support in Password protection (Preview)

The Password protection page now includes password risks from SaaS apps connected through Microsoft Defender for Cloud Apps, in addition to Active Directory, Microsoft Entra ID, and Okta. SaaS apps that support SaaS Security Posture Management (SSPM), such as Salesforce and ServiceNow, appear on the Password Hygiene and Password Policies tabs. Each SaaS app requires a Defender for Cloud Apps app connector. For more information, see [Investigate identity password protection](password-protection).

### The **Domain investigation page** is now generally available

The **Domain investigation** page allows you to investigate an Active Directory domain. It shows Active Directory domain security, including domain properties, deployment health, identity summary, service account breakdown, sensitive entities, active recommendations, group policies, and trust relationships. For more information, see [Investigate a domain](investigate-domain).

### Automatic RPC auditing on domain controllers

Defender for Identity now automatically enables RPC auditing on domain controllers when you upgrade to sensor version 3.0.8 or later. You no longer need to apply a tag manually to enable RPC auditing. For more information, see [Configure RPC auditing](deploy/deploy-sensor-v3#configure-rpc-auditing).

## June 2026

### Identity risk score is now generally available

The [identity risk score](/en-us/defender-xdr/investigate-users#risk-score-tab) is now generally available. The score ranges from 0 to 100 and reflects how likely an identity is to be compromised and how much damage a compromise could cause, based on the identity's criticality level and privileged role assignments. The **Risk score** tab on the **Identity** page provides a detailed breakdown of risk factors, percentile comparison, and risk trends.

### New Defender for Identity security alerts

These new alerts were added to the Defender for Identity security alerts:

**New alerts related to Entra ID**:

- [Anomalous activity following Global Administrator elevation](alerts-xdr#anomalous-activity-following-global-administrator-elevation)
- [Reciprocal Temporary Access Pass creation between users](alerts-xdr#reciprocal-temporary-access-pass-creation-between-users)
- [Suspicious service principal sign-in following credential addition](alerts-xdr#suspicious-service-principal-sign-in-following-credential-addition)
- [Suspicious bulk user deletion via scripted activity](alerts-xdr#suspicious-bulk-user-deletion-via-scripted-activity)
- [Suspicious removal of privileged app role assignment through Graph API](alerts-xdr#suspicious-removal-of-privileged-app-role-assignment-through-graph-api)
- [Suspicious sign-in by a user exhibiting a spike in account update activity](alerts-xdr#suspicious-signin-by-a-user-exhibiting-a-spike-in-account-update-activity)
- [User exhibiting spike in distinct application-resource access combinations](alerts-xdr#user-exhibiting-spike-in-distinct-applicationresource-access-combinations)

**New alerts related to Active Directory**:

- [DCSync attack (replication of directory services)](alerts-xdr#dcsync-attack-replication-of-directory-services)
- [Suspicious Entra Connect account authentication](alerts-xdr#suspicious-entra-connect-account-authentication)

**New alerts related to other identity providers**:

- [SailPoint ISC suspected brute-force attack](alerts-xdr#sailpoint-isc-suspected-brute-force-attack)

### NHI inventory enhancements (Preview)

- **Expanded Entra ID inventory**: The non-human identity inventory now includes all Microsoft Entra service principals, not just those with API permissions. For more information, see [View the Identity inventory](identity-inventory).
- **Microsoft Entra roles visibility**: The Permissions tab now shows assigned Microsoft Entra roles alongside API permissions. For more information, see [View your app details with app governance](/en-us/defender-cloud-apps/app-governance-visibility-insights-view-apps).

### Visibility into service principals used by AI agents (Preview)

The non-human identity inventory now identifies which Entra ID service principals are used by AI agents. A new "Used by AI agents" column and insight card help you find and prioritize these identities. For more information, see [View the Identity inventory](identity-inventory).

## May 2026

### Sensor v3.x supports all identity roles on domain controllers

Defender for Identity sensor v3.x now supports domain controllers running all identity roles, including Microsoft Entra Connect, AD FS, and AD CS identity roles. For deployment details, see [Defender for Identity sensor v3.x prerequisites](deploy/deploy-sensor-v3).

### Increased sensor capacity

Defender for Identity now supports up to 1,000 sensors per workspace, increased from the previous limit of 350. To add more than 1,000 sensors, contact Defender for Identity support.

### New Defender for Identity security alerts

These new alerts were added to the Defender for Identity security alerts:

**New alerts related to Entra ID**:

- [Guest user account promoted to member](alerts-xdr#guest-user-account-promoted-to-member)
- [User was created and assigned to Global Administrator role](alerts-xdr#user-was-created-and-assigned-to-global-administrator-role)
- [Failed credential abuse attempt in Entra ID authentication](alerts-xdr#failed-credential-abuse-attempt-in-entra-id-authentication)
- [Malicious sign in from a randomized user agent](alerts-xdr#malicious-sign-in-from-a-randomized-user-agent)
- [Possible use of a stolen session cookie](alerts-xdr#possible-use-of-a-stolen-session-cookie)
- [Suspected Conditional Access bypass via non-compliant device](alerts-xdr#suspected-conditional-access-bypass-via-non-compliant-device)
- [Suspicious addition of default third-party MFA method to user account](alerts-xdr#suspicious-addition-of-default-thirdparty-mfa-method-to-user-account)

### Known limitation: Migration of domain controllers with Windows Server 2025 from sensor v2.x to sensor v3.x is not supported

Migrating domain controllers running Windows Server 2025 to sensor v3.x isn't currently supported. Continue using the v2.x sensor on Windows Server 2025 domain controllers until support for migration to v3.x is available.

### Defender for Identity sensor updates

| Version number | Updates |
| --- | --- |
| 2.255.19247.44775 | This sensor update adds properties to Group Policy (GPO) event collection and includes bug fixes. |

## April 2026

### **Identity Explorer (Preview)**

The Identity page now includes the **Identity Explorer** tab for customers with a Microsoft Sentinel Data Lake license. This tab uses the [hunting graph](/en-us/defender-xdr/advanced-hunting-graph) to visualize identity attack paths and exposure scenarios as interactive graphs. Use predefined identity scenarios to discover lateral movement paths, privilege escalation routes, and credential-access risks. For more information, see [Investigate an identity](/en-us/defender-xdr/investigate-users#identity-explorer-tab-preview).

### **Custom account correlation rules (Preview)**

Custom account correlation rules let you link accounts that belong to the same identity, such as privileged accounts with unique naming conventions. You can correlate accounts that don't share strong identifiers such as account ID, SID, object ID, or UPN by defining rules based on UPN prefix, UPN suffix, or domain UPN. For more information, see [Create custom account correlation rules](custom-account-correlation-rules).

### Automatic Windows event auditing configuration for sensors v3.x is now generally available

The [Automatic Windows event-auditing configuration for sensors v3.x](deploy/configure-windows-event-collection#configure-defender-for-identity-to-collect-windows-events-automatically) is now generally available. Automatic Windows event-auditing streamlines deployment by automatically applying the required auditing settings to new sensors and correcting misconfigurations on existing ones.

## March 2026

### Sensor v3.x support for domain controllers with Microsoft Entra Connect identity roles

Defender for Identity sensor v3.x now supports domain controllers that run Microsoft Entra Connect, including detections and identity security posture management (ISPM) recommendations. Detections and ISPM recommendations for additional identity roles, including AD FS and AD CS, will become available soon. Domain controllers with Microsoft Entra Connect roles and v3.x of the sensor must run Windows Server 2019 or later and include at least the [March 2026 Cumulative Update](https://support.microsoft.com/topic/march-10-2026-kb5078766-os-build-20348-4893-fa3ee26a-0877-47d7-a4b2-9dd632ea8cea). For deployment details, see [Defender for Identity deployment overview](deploy/deploy-defender-identity) and [Sensor v3.x prerequisites](deploy/deploy-sensor-v3).

### Migrate Defender for Identity sensors from v2.x to v3.x

You can now migrate Defender for Identity sensors from v2.x to v3.x directly from the Microsoft Defender portal. The v2.x sensor continues running during the migration until the v3.x sensor is ready, so there's no downtime. Eligible servers appear as **Ready for migration** on the **Sensors** page, and migration takes up to 20 minutes. For more information, see [Migrate to Defender for Identity sensor v3.x](deploy/migrate-to-sensor-v3).

### Identity security enhancements

New identity security capabilities help you monitor and manage identity security for human and non-human identities:

- **Identity Security dashboard (Preview)**: The **Identity Security** dashboard provides summary cards for identity providers, on-premises identities, SaaS identities, PAM and IGA integrations, and non-human identities. Widgets show deployment status, highly privileged identities, users at risk, and domains with unsecured configurations. For more information, see [The Identity Security dashboard](dashboard).

    The **Identity Security** dashboard is being rolled out gradually to customers, and might not yet be available in your organization.
- **Coverage and maturity page (Preview)**: The **Coverage and maturity** page shows your organization's identity security coverage for identity providers, on-premises identities, SaaS identities, and PAM and IGA integrations. Each source displays a maturity level, including Connected, Protected, Fortified, and Resilient, with identity counts, coverage scores, and prioritized setup tasks. For more information, see [Coverage and maturity](/en-us/defender-xdr/identity-security/coverage-maturity).

    The **Coverage and maturity** page is being rolled out gradually to customers, and might not yet be available in your organization. If you don't see this feature in your environment yet, check back soon.
- **Identity inventory**: The **Identity inventory** page now shows human and non-human identities in separate tabs. Insight cards help you classify critical assets, view highly privileged identities, identify critical Active Directory service accounts, and view cloud application accounts. For more information, see [View the Identity inventory](identity-inventory).
- **Non-human identities (Preview)**: The **Non-human identities** tab on the **Identity inventory** page shows non-human identities, including Microsoft Entra ID apps, Active Directory service accounts, Google Workspace apps, and Salesforce apps. The tab includes statistics for risky, highly privileged, overprivileged, unused, and externally published identities. A separate investigation page lets you view details for each identity. For more information, see [Identity inventory](identity-inventory) and [Investigate non-human identities](/en-us/defender-xdr/investigate-non-human-identities).
- **Identity risk score (Preview)**: A new risk score for identities, ranging from 0 to 100, that indicates the likelihood of compromise and the potential impact based on criticality and privileged roles. The risk score is available in Microsoft Entra ID, where it can be used to inform conditional access policies and identity protection workflows. A new **Risk score** tab on the **Identity** page provides a detailed breakdown of the risk factors, including percentile comparison and risk trends. For more information, see [Investigate an identity](/en-us/defender-xdr/investigate-users).
- **Identity security recommendations (Preview)**: View recommendations for Active Directory, Microsoft Entra ID, and SaaS applications such as Microsoft, Atlassian, GitHub, Google Workspace, Salesforce, and ServiceNow. Recommendations are also available for non-Microsoft identity providers such as Okta, PingOne, CyberArk, and SailPoint. For more information, see [Identity security recommendations](/en-us/defender-xdr/identity-security/identity-security-recommendations).
- **Domain investigation page (Preview)**: The **Domain investigation** page shows Active Directory domain security, including domain properties, deployment health, identity summary, service account breakdown, sensitive entities, active recommendations, group policies, and trust relationships. For more information, see [Investigate a domain](investigate-domain).
- **Password protection page (Preview)**: The **Password protection** page shows identity password risk from Active Directory, Microsoft Entra ID, and Okta, with tabs for password hygiene, password policies, leaked credentials, and exposed passwords. For more information, see [Password protection](password-protection).

### Defender for Identity sensor updates

Sensor versions now display the full version number (for example, 2.255.19201.14651) instead of only the major/minor version (for example, 2.255). This makes it easier to identify the exact update installed on each sensor.

When you validate upgrades or troubleshoot, the last two numbers in the version (for example, 19201.14651) show which update is installed.

| Version number | Updates |
| --- | --- |
| 2.255.19243.47944 | This sensor update includes bug fixes. |
| 2.255.19201.14651 | This sensor update includes bug fixes. |

### Migrate Defender for Identity sensors from v2.x to v3.x

You can now migrate Defender for Identity sensors from v2.x to v3.x directly from the Microsoft Defender portal. The v2.x sensor continues running during the migration until the v3.x sensor is ready, so there's no downtime. Eligible servers appear as **Ready for migration** on the **Sensors** page, and migration takes up to 20 minutes. For more information, see [Migrate to Defender for Identity sensor v3.x](deploy/migrate-to-sensor-v3).

### Identity security enhancements

New identity security capabilities help you monitor and manage identity security for human and non-human identities:

- **Identity Security dashboard (Preview)**: The **Identity Security** dashboard provides summary cards for identity providers, on-premises identities, SaaS identities, PAM and IGA integrations, and non-human identities. Widgets show deployment status, highly privileged identities, users at risk, and domains with unsecured configurations. For more information, see [The Identity Security dashboard](dashboard).

    The **Identity Security** dashboard is being rolled out gradually to customers, and might not yet be available in your organization.
- **Coverage and maturity page (Preview)**: The **Coverage and maturity** page shows your organization's identity security coverage for identity providers, on-premises identities, SaaS identities, and PAM and IGA integrations. Each source displays a maturity level, including Connected, Protected, Fortified, and Resilient, with identity counts, coverage scores, and prioritized setup tasks. For more information, see [Coverage and maturity](/en-us/defender-xdr/identity-security/coverage-maturity).

    The **Coverage and maturity** page is being rolled out gradually to customers, and might not yet be available in your organization. If you don't see this feature in your environment yet, check back soon.
- **Identity inventory**: The **Identity inventory** page now shows human and non-human identities in separate tabs. Insight cards help you classify critical assets, view highly privileged identities, identify critical Active Directory service accounts, and view cloud application accounts. For more information, see [View the Identity inventory](identity-inventory).
- **Non-human identities (Preview)**: The **Non-human identities** tab on the **Identity inventory** page shows non-human identities, including Microsoft Entra ID apps, Active Directory service accounts, Google Workspace apps, and Salesforce apps. The tab includes statistics for risky, highly privileged, overprivileged, unused, and externally published identities. A separate investigation page lets you view details for each identity. For more information, see [Identity inventory](identity-inventory) and [Investigate non-human identities](/en-us/defender-xdr/investigate-non-human-identities).
- **Identity risk score (Preview)**: A new risk score for identities, ranging from 0 to 100, that indicates the likelihood of compromise and the potential impact based on criticality and privileged roles. The risk score is available in Microsoft Entra ID, where it can be used to inform conditional access policies and identity protection workflows. A new **Risk score** tab on the **Identity** page provides a detailed breakdown of the risk factors, including percentile comparison and risk trends. For more information, see [Investigate an identity](/en-us/defender-xdr/investigate-users).
- **Identity security recommendations (Preview)**: View recommendations for Active Directory, Microsoft Entra ID, and SaaS applications such as Microsoft, Atlassian, GitHub, Google Workspace, Salesforce, and ServiceNow. Recommendations are also available for non-Microsoft identity providers such as Okta, PingOne, CyberArk, and SailPoint. For more information, see [Identity security recommendations](/en-us/defender-xdr/identity-security/identity-security-recommendations).
- **Domain investigation page (Preview)**: The **Domain investigation** page shows Active Directory domain security, including domain properties, deployment health, identity summary, service account breakdown, sensitive entities, active recommendations, group policies, and trust relationships. For more information, see [Investigate a domain](investigate-domain).
- **Password protection page (Preview)**: The **Password protection** page shows identity password risk from Active Directory, Microsoft Entra ID, and Okta, with tabs for password hygiene, password policies, leaked credentials, and exposed passwords. For more information, see [Password protection](password-protection).

### Defender for Identity sensor updates

Sensor versions now display the full version number (for example, 2.255.19201.14651) instead of only the major/minor version (for example, 2.255). This makes it easier to identify the exact update installed on each sensor.

When you validate upgrades or troubleshoot, the last two numbers in the version (for example, 19201.14651) show which update is installed.

| Version number | Updates |
| --- | --- |
| 2.255.19201.14651 | This sensor update includes bug fixes. |

### New Defender for Identity security alerts

These new alerts were added to the Defender for Identity security alerts:

**New alerts related to Entra ID**:

- [Attempt to disable Defender for Identity service principal observed](alerts-xdr#attempt-to-disable-defender-for-identity-service-principal-observed)
- [Suspicious Entra account enablement after disruption](alerts-xdr#suspicious-entra-account-enablement-after-disruption)
- [Suspicious Intune device registration activity](alerts-xdr#suspicious-intune-device-registration-activity)
- [Suspicious OS switch sign-in](alerts-xdr#suspicious-os-switch-sign-in)
- [User sign-in from shared client infrastructure exhibiting anomalous activity](alerts-xdr#user-signin-from-shared-client-infrastructure-exhibiting-anomalous-activity)
- [Suspicious sign-in from an unusual user agent and IP address using PowerShell](alerts-xdr#suspicious-sign-in-from-an-unusual-user-agent-and-ip-address-using-powershell)
- [Suspicious sign-in from an unusual user agent and IP address using device code flow](alerts-xdr#suspicious-sign-in-from-an-unusual-user-agent-and-ip-address-using-device-code-flow)

**New alerts related to Active Directory**:

- [Suspicious on-premises account enablement after disruption](alerts-xdr#suspicious-on-prem-account-enablement-after-disruption)
- [Suspicious resource-based constrained delegation (RBCD) attribute change](alerts-xdr#suspicious-resource-based-constrained-delegation-rbcd-attribute-change)
- [Suspicious resource-based constrained delegation (RBCD) authentication](alerts-xdr#suspicious-resource-based-constrained-delegation-rbcd-authentication)

### Suspected pass-the-ticket attack alert is now generally available

The [Suspected pass-the-ticket attack](alerts-xdr#suspected-pass-the-ticket-attack) alert is now generally available. This alert was previously available in public preview as *Pass-the-Ticket (PtT) attack*. For more information, see [Lateral movement alerts](alerts-xdr).

### Updates to Secure Score category calculations for increased accuracy

To improve accuracy and better protect organizational identities, some security recommendations categorized as **Cloud apps** recommendations are now considered identity-related and grouped under the **Identity** category. While the total Secure Score remains unchanged, individual identity and app scores may change.

### Continued rollout of new health alert: Sensor v3.x RPC audit misconfigured

The **Sensor v3.x RPC Audit Misconfigured** health alert is continuing to be rolled out gradually to customers. The new health alert helps identify v3.x sensors where Enhanced RPC auditing configuration is either missing or incorrectly applied. Enhanced RPC auditing is required for some Microsoft Defender for Identity advanced identity detections. For more information, see [Configure RPC on sensors v3.x](deploy/deploy-sensor-v3#configure-rpc-auditing).

## February 2026

### Defender for Identity sensor updates

| Version number | Updates |
| --- | --- |
| 2.255 | This sensor update includes bug fixes. |

### New Defender for Identity security alerts

These new alerts were added to the Defender for Identity security alerts:

**New alerts related to Entra ID**:

- [Suspicious user configuration change activity from Entra ID sync application](alerts-xdr#suspicious-user-configuration-change-activity-from-entra-id-sync-application)
- [Anomalous OAuth device code authentication activity](alerts-xdr#anomalous-oauth-device-code-authentication-activity)
- [Suspicious Graph API request made from Entra ID sync application](alerts-xdr#suspicious-graph-api-request-made-from-entra-id-sync-application)
- [Suspicious sign-in observed from Entra ID sync application](alerts-xdr#suspicious-sign-in-observed-from-entra-id-sync-application)
- [Suspicious sign in with CSRF speedbump trigger](alerts-xdr#suspicious-sign-in-with-csrf-speedbump-trigger)

**New alerts related to Active Directory**:

- [Possible golden ticket attack (suspicious ticket)](alerts-xdr#possible-golden-ticket-attack-suspicious-ticket)
- [Possible Kerberos key list attack](alerts-xdr#possible-kerberos-key-list-attack)

## January 2026

### New Defender for Identity security alerts

These new alerts were added to the Defender for Identity security alerts:

**New alerts related to Entra ID**:

- [Suspicious sign-in observed from Entra ID sync application to an uncommon resource app](alerts-xdr#suspicious-sign-in-observed-from-entra-id-sync-application-to-an-uncommon-resource-app)
- [Suspicious sign-in observed to Entra ID sync application using an uncommon user agent](alerts-xdr#suspicious-sign-in-observed-to-entra-id-sync-application-using-an-uncommon-user-agent)
- [Possible OAuth code theft detected through consent abuse](alerts-xdr#possible-oauth-code-theft-detected-through-consent-abuse)
- [Possible adversary-in-the-middle (AiTM) attack detected (ConsentFix)](alerts-xdr#possible-adversary-in-the-middle-aitm-attack-detected-consentfix)
- [Skipped MFA on remembered device from uncommon ISP sign-in](alerts-xdr#skipped-mfa-on-remembered-device-from-uncommon-isp-sign-in)

**New alerts related to Active Directory**:

- [Pass-the-Ticket (PtT) attack](alerts-xdr#suspected-pass-the-ticket-attack)
- [Possible Active Directory Certificate Services enumeration](alerts-xdr#possible-active-directory-certificate-services-enumeration)
- [Possible Active Directory enumeration via ADWS](alerts-xdr#possible-active-directory-enumeration-via-adws)
- [Suspicious NTLM authentication](alerts-xdr#suspicious-ntlm-authentication)
- [Possible Kerberoasting attack using a stealthy LDAP search](alerts-xdr#possible-kerberoasting-attack-using-a-stealthy-ldap-search)
- [Suspicious Kerberos authentication (TGT request using TGS-REQ)](alerts-xdr#suspicious-kerberos-authentication-tgt-request-using-tgs-req)

### Identity inventory enhancements are now generally available

- **Accounts tab in Identity Inventory**: The new \*\*Accounts\*- tab provides a consolidated view of all accounts associated with an identity, including accounts from Active Directory, Microsoft Entra ID, and supported non-Microsoft identity providers. For more information, see [Manage related identities and accounts](manage-related-identities-accounts).
- **Manually link and unlink accounts**: Manually link or unlink accounts from an identity directly in the \*\*Accounts\*- tab. This capability helps you correlate identity components from different directory sources and provides a complete identity context during investigations. For more information, see [Manage related identities and accounts](manage-related-identities-accounts).
- **Identity-level remediation actions**: You can now perform remediation actions such as disabling accounts or resetting passwords on one or more accounts linked to an identity. For more information, see [Remediation actions](remediation-actions#roles-and-permissions).
- **New advanced hunting table**: Advanced hunting in Microsoft Defender now includes the \*\*[IdentityAccountInfo](/en-us/defender-xdr/advanced-hunting-identityaccountinfo-table)\*- table. This table provides account information from various sources, including Microsoft Entra ID, and links to the identity that owns the account.

### New security posture assessments

- [Remove stale Active Directory accounts (Preview)](security-posture-assessments/accounts#remove-stale-active-directory-accounts-preview) lists any user accounts in Active Directory that are stale, meaning they haven't logged in at all during the past 90 days.
- [Microsoft Entra ID privileged user accounts that are also privileged in Active Directory (Preview)](security-posture-assessments/accounts#microsoft-entra-id-privileged-user-accounts-that-are-also-privileged-in-active-directory-preview) lists Microsoft Entra ID privileged user accounts that also have privileged roles in Active Directory.

### New Health Alert: Sensor v3.x RPC Audit Misconfigured

Enhanced RPC auditing is required for some Microsoft Defender for Identity advanced identity detections. A new health alert helps identify v3.x sensors where this configuration is either missing or incorrectly applied. The alert is being rolled out gradually to customers. For more information, see [Configure RPC on sensors v3.x](deploy/deploy-sensor-v3#configure-rpc-auditing).

### New Entra ID user roles to support remediation actions

For some [remediation actions](remediation-actions), Defender for Identity creates an enterprise application in Microsoft Entra ID. The Microsoft Defender for Identity enterprise application is created automatically in the tenant and is used only to execute remediation actions. When a user initiates an action from the Defender portal, the request is authorized based on the user's Entra ID roles and executed by the Defender for Identity application, enforcing Entra ID role-based access control (RBAC) and audit logging. These new Entra ID roles are supported:

- User Administrator
- Authentication Administrator
- Privileged Authentication Administrator
- Directory Writers
- Helpdesk Administrator
- Security Operator

### Automatic Windows event auditing configuration for Defender for Identity sensors v3.x

We're gradually rolling out automatic Windows event-auditing configuration for sensors v3.x, along with related health alerts. Automatic Windows event-auditing streamlines deployment by automatically applying the required auditing settings to new sensors and correcting misconfigurations on existing ones. This update might identify existing auditing configuration gaps that weren't previously detected. To ensure consistent protection, we recommend that you make sure all servers with the v3 sensors are configured with:

- The latest Windows cumulative update.
- Automatic Windows event auditing enabled. For more information, see [Configure automatic windows auditing](deploy/configure-windows-event-collection#configure-defender-for-identity-to-collect-windows-events-automatically).

### Sensor updates

| Version number | Updates |
| --- | --- |
| 2.254 | The sensor now supports a new DNS zone target for \*.atp.gcc.azure.com. Make sure your sensors in GCC can access this zone with your sensor DNS prefix. |

### New security posture assessment: Identify service accounts in privileged groups

This identity security posture assessment lists Active Directory service accounts with direct or nested membership in privileged groups.

You can use this assessment to identify service accounts with elevated permissions and take action when privileged access isn't required.

For more information, see:[Security posture assessment: Identify service accounts in privileged groups](security-posture-assessments/accounts#identify-service-accounts-in-privileged-groups)

### New security posture assessment: Locate accounts in built-in Operator Groups

This identity security posture assessment lists Active Directory accounts that are members of built-in Operator Groups, including direct and indirect membership.

You can use this assessment to review legacy or unnecessary operator access and take action when elevated access isn't required.

For more information, see:[Security posture assessment: Locate accounts in built-in Operator Groups](security-posture-assessments/accounts#locate-accounts-in-built-in-operator-groups)

## December 2025

### New properties for 'sensorCandidate' resource type in Graph-API (preview)

| Property | Type | Description |
| --- | --- | --- |
| domainName | String | The domain name of the sensor. |
| senseClientVersion | String | The version of the Defender for Identity sensor client. |

This capability is currently in preview and available in API preview version. Learn more [here](/en-us/graph/api/resources/security-sensorcandidate?view=graph-rest-beta&amp;preserve-view=true)

### ADWS LDAP search in Advanced Hunting

New ADWS LDAP search activity is now available in the 'IdentityQueryEvents' table in Advanced Hunting. This can provides visibility into directory queries performed through ADWS, helping customers track these operations and create custom detection based on this data.

| Version number | Updates |
| --- | --- |
| 2.253 | Includes bug fixes and stability improvements for the Microsoft Defender for Identity sensor. |
| 2.252 | Includes bug fixes and stability improvements for the Microsoft Defender for Identity sensor. |

## November 2025

| Version number | Updates |
| --- | --- |
| 2.251 | The enhanced ADWS LDAP and legacy password-based LDAP query methods now capture a broader range of unique events at scale. As a result, you might notice an increase in recorded activity. |

### Identity Inventory enhancements: Accounts tab, manual account linking and unlinking, and expanded remediation actions

The following new features are now available in Microsoft Defender for Identity:

**Accounts tab in Identity Inventory**:

A new Accounts tab provides a consolidated view of all accounts associated with an identity, including accounts from Active Directory, Microsoft Entra ID, and supported non-Microsoft identity providers. For more information, see: [Manage related identities and accounts (Preview)](manage-related-identities-accounts)

**Manual link and unlink of accounts**:

You can now manually link or unlink accounts from an identity directly in the Accounts tab. This capability helps you correlate identity components from different directory sources and provides a complete identity context during investigations. For more information, see: [Manage related identities and accounts](manage-related-identities-accounts).

**Identity-level remediation actions**:

You can now perform remediation actions such as disabling accounts or resetting passwords on one or more accounts linked to an identity. For more information, see: [Remediation actions](remediation-actions#roles-and-permissions).

### New security posture assessment: Change password for on-premises account with potentially leaked credentials (Preview)

The new security posture assessment lists users whose valid credentials were leaked. For more information, see: [Change password for on-premises account with potentially leaked credentials (Preview)](/en-us/defender-for-identity/security-posture-assessments/accounts#change-password-for-on-prem-account-with-potentially-leaked-credentials-preview)

### Microsoft Defender for Identity sensor version updates

| Version number | Updates |
| --- | --- |
| 2.250 | The improved event log query method captures a broader range of unique events at scale. As a result, you might notice an increase in captured activities. This update also includes security and performance improvements. |

### Expansion of identity scoping: Support for Organizational units (Preview)

In addition to the GA release of scoping by Active Directory domains a few months ago, you can now scope by \*\*Organizational Units (OUs)\*- as part of XDR user role-based access control (URBAC). This enhancement provides even more granular control over which entities and resources are included in security analysis.

For more information, see [Configure scoped access for Microsoft Defender for Identity](configure-scoped-access).