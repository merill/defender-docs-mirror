---
layout: Conceptual
title: Offensive Security Testing for Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/security-testing-best-practices
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
description: Learn about best practices for Offensive Security Testing for Microsoft Defender for Identity.
ms.date: 2026-09-29T00:00:00.0000000Z
ms.topic: article
ms.reviewer: martin77s
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 14e58f10-a76f-dffc-302b-7812bf222291
document_version_independent_id: 14e58f10-a76f-dffc-302b-7812bf222291
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/security-testing-best-practices.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-testing-best-practices
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/security-testing-best-practices.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 424fd10d-357e-e0f9-1900-87c1474ef7ad
---

# Offensive Security Testing for Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn

This article summarizes the best practices and items to review before you begin Offensive Security Testing for Microsoft Defender for Identity.

## Common issues that affect testing

Here are some common issues that can affect your offensive security testing:

### Infrastructure protection issues

- **Incomplete infrastructure protection**: Deploy Microsoft Defender for Identity sensors on all domain controllers.
- **Missing Microsoft Defender for Endpoint**: Endpoint protection adds detection capabilities for activities on identity infrastructure that may not be covered by identity-based detections alone.

### Detection accuracy issues

- **Insufficient learning period**: The learning period for alerts is used to tune alert detections. Without this learning period, detections won't be as accurate.
- **Using accounts with established admin patterns**: Avoid using users or computers that regularly run administrative tasks, as the system learns these as normal behavior. Instead, use:
    - **Existing computer**: Use a computer that doesn't regularly run admin or attack simulation activities.
    - **Existing standard user**: Use a user that doesn't regularly run admin or attack simulation activities.

### Configuration issues

- **Network configuration mismatch**: Sensors running on VMware might experience Microsoft Defender for Identity health issues. See [VMware virtual machine sensor issue](troubleshooting-known-issues#vmware-virtual-machine-sensor-issue).
- **Unhealthy Network Name Resolution (NNR)**: This issue can lead to problems with certain detections.
- **Incomplete attack simulation**: Test with actual attack scenarios rather than single TTPs. Defender for Identity detections focus on complete attack stories. Performing only one segment of a kill chain without other steps yields incomplete results and decreased detection outcomes.
- **Incompatible penetration testing tools**: Some tools might return false results. Cross-check relevant audit logs to confirm successful attacks.

## Best practices checklist

| Recommendation | Description | Links to Documentation for related tasks |
| --- | --- | --- |
| Check that Defender for Identity is deployed on all domain controllers | Deployment on all domain controllers ensures that you're getting all of the signals for threat detection. Not having full protection can lead to missed detections or false positives. | [Microsoft Defender for Identity deployment overview](deploy/deploy-defender-identity) |
| Check that Defender for Identity is deployed on all AD FS, AD CS, and Microsoft Entra Connect servers | Deployment on all these servers ensures that you're getting all of the signals for threat detection. Not having full protection can lead to missed detections or false positives. | [Configure sensors for AD FS, AD CS, and Microsoft Entra Connect](deploy/active-directory-federation-services) |
| Check the health of your Defender for Identity sensors | It's critical that your sensor is healthy and reporting as expected to ensure optimal performance. Having an unhealthy sensor can lead to missed detections. Review all health alerts before running any tests. | [Microsoft Defender for Identity health issues](health-alerts) |
| Consider integrating with Microsoft Defender | Defender for Identity provides alerting on identity-based threats. Integrating with Microsoft Defender lets you correlate these alerts with other signals for a more comprehensive view of threats and potential solutions.Microsoft Defender is a unified pre-breach and post-breach enterprise defense suite that natively coordinates detection, prevention, investigation, and response in endpoints, identities, email, and applications to provide integrated protection against sophisticated attacks. | [Microsoft Defender](/en-us/defender-xdr/microsoft-365-defender-train-security-staff). |
| Check Windows event collection configuration | Optimal event collection is essential for Defender for Identity to analyze and detect threats effectively. Check your configuration before running any tests. | - [Configure Windows event collection for domain controllers](deploy/configure-windows-event-collection) - [Configure Windows event collection for AD CS](deploy/configure-windows-event-collection#configure-auditing-on-an-ad-cs-server) - [Configure Windows event collection for AD FS](deploy/configure-windows-event-collection#configure-auditing-on-an-ad-fs-server) - [Configure Windows event collection for Microsoft Entra Connect](deploy/configure-windows-event-collection#configure-auditing-on-microsoft-entra-connect) - [Use PowerShell to check your configuration](https://www.powershellgallery.com/packages/DefenderForIdentity/1.0.0.4) |
| Check that NNR is configured correctly | NNR is a critical component of Defender for Identity. Defender for Identity uses NNR to correlate between raw activities containing IP addresses and the computers involved in each activity. Defender for Identity profiles entities, including computers, and generates security alerts for suspicious activities. It's important for NNR to be configured correctly for a successful deployment and to help detect advanced threats. | [Configure Network Name Resolution (NNR) for Microsoft Defender for Identity](nnr-policy) |
| Check directory access requirements for your sensor version | For sensor v2.x deployments, configure a Directory Service Account (DSA) for full security coverage. A DSA is required to access the *DeletedObjects* container and for specific cross-domain and non-domain-controller scenarios.The sensor v3.x uses LocalSystem for Active Directory interactions. On domain controllers, the sensor v3.x collects information about deleted users and computers without a DSA or additional *DeletedObjects* container permission configuration. | [Directory Service Accounts for Microsoft Defender for Identity](deploy/directory-service-accounts) |
| Check the alert learning periods | Alerts rely on learning periods to build a profile of patterns and then distinguish between legitimate and suspicious activities. Each alert incorporates specific conditions within the detection logic, such as thresholds and filtering of popular activities. Check these alerts to make sure that they meet the required learning periods. | [Alerts overview](alerts-overview) |
| Check the alert thresholds | The threshold level of an alert influences the number of alerts you receive for that trigger. The default threshold for all alerts is **High**. You can customize the threshold level for individual alerts to **High**, **Medium**, or **Low**. Lowering the threshold of an alert increases the number of alerts generated by Microsoft Defender for Identity. Alerts that are triggered when threshold is set to **Medium** or **Low** contain text that indicates the alert threshold.When you enable the **Recommended Test Mode** button, all alert threshold levels are set to **Low**. When the threshold is low, you get more alerts, including some related to legitimate traffic and activities. This setting can be useful to get more data into a nonproduction environment that doesn't have enough entity historical data or profiles.Lowering the threshold to **Low** also leads to more false positives and isn't recommended for production environments. | [Adjust alert threshold settings or enable recommended test mode](advanced-settings#adjust-alert-thresholds) |
| Review the Secure Score recommendations for Defender for Identity | Following Secure Score recommendations helps improve your security posture and enhances the effectiveness of Defender for Identity in detecting threats. | [Microsoft Secure Score](https://security.microsoft.com/securescore?viewid=actions) |

### Security alert learning periods

Make sure that the learning periods for the alerts listed below have been met before you begin your offensive security testing.

| Alert | Learning Period |
| --- | --- |
| [Network-mapping reconnaissance (DNS) (External ID 2007)](alerts-mdi-classic#network-mapping-reconnaissance-dns) | Eight days from the start of domain controller monitoring |
| [User and Group membership reconnaissance (SAMR) (External ID 2021)](alerts-mdi-classic#user-and-group-membership-reconnaissance-samr) | Four weeks per domain controller starting from the first network activity of SAMR against the specific DC |
| [Suspected Golden Ticket usage (encryption downgrade) (External ID 2009)](alerts-mdi-classic#suspected-golden-ticket-usage-encryption-downgrade) | Five days from the start of domain controller monitoring |
| [Suspicious additions to sensitive groups (External ID 2024)](alerts-mdi-classic#suspicious-additions-to-sensitive-groups) | Four weeks per domain controller, starting from the first event |
| [Suspected Brute Force attack (Kerberos, NTLM) (External ID 2023)](alerts-mdi-classic#suspected-brute-force-attack-kerberos-ntlm) | One week |
| [Security principal reconnaissance (LDAP) (External ID 2038)](alerts-mdi-classic#security-principal-reconnaissance-ldap) | 15 days per computer, starting from the day of the first event, observed from the machine |
| [Suspected over-pass-the-hash attack (forced encryption type) (External ID 2008)](alerts-mdi-classic#suspected-over-pass-the-hash-attack-forced-encryption-type) | One month |
| [Suspicious VPN connection (External ID 2025)](alerts-mdi-classic#suspicious-vpn-connection) | 30 days from the first VPN connection, and at least 5 VPN connections in the last 30 days, per user |