---
layout: Conceptual
title: Advanced multistage attack detection in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/fusion
breadcrumb_path: breadcrumb/toc.json
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
description: Use Fusion technology in Microsoft Sentinel to reduce alert fatigue and create actionable incidents that are based on advanced multistage attack detection.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: concept-article
ms.date: 2024-11-26T00:00:00.0000000Z
locale: en-us
document_id: 00866ed7-92de-5bcc-0812-d6a3167e8a30
document_version_independent_id: 9e1f54b8-9ab7-ed03-97a7-2f5fa96e6b7e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/fusion.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/fusion
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/fusion.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: aa44b5ec-f2e5-d797-223d-bb2cdf4691c3
---

# Advanced multistage attack detection in Microsoft Sentinel | Microsoft Learn

Important

[**Custom detections**](/en-us/defender-xdr/custom-detections-overview?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) is now the best way to create new rules across Microsoft Sentinel SIEM Microsoft Defender XDR. With custom detections, you can reduce ingestion costs, get unlimited real-time detections, and benefit from seamless integration with Defender XDR data, functions, and remediation actions with automatic entity mapping. For more information, read [this blog](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/custom-detections-are-now-the-unified-experience-for-creating-detections-in-micr/4463875).

Microsoft Sentinel uses Fusion, a correlation engine based on scalable machine learning algorithms, to automatically detect multistage attacks (also known as advanced persistent threats or APT) by identifying combinations of anomalous behaviors and suspicious activities that are observed at various stages of the kill chain. Based on these discoveries, Microsoft Sentinel generates incidents that would otherwise be difficult to catch. These incidents comprise two or more alerts or activities. By design, these incidents are low-volume, high-fidelity, and high-severity.

Customized for your environment, this detection technology not only reduces [false positive](false-positives) rates but can also detect attacks with limited or missing information.

Since Fusion correlates multiple signals from various products to detect advanced multistage attacks, successful Fusion detections are presented as **Fusion incidents** on the Microsoft Sentinel **Incidents** page and not as **alerts**, and are stored in the *SecurityIncident* table in **Logs** and not in the *SecurityAlert* table.

### Configure Fusion

Fusion is enabled by default in Microsoft Sentinel, as an [analytics rule](detect-threats-built-in) called **Advanced multistage attack detection**. You can view and change the status of the rule, configure source signals to be included in the Fusion ML model, or exclude specific detection patterns that may not be applicable to your environment from Fusion detection. Learn how to [configure the Fusion rule](configure-fusion-rules).

Note

Microsoft Sentinel currently uses 30 days of historical data to train the Fusion engine's machine learning algorithms. This data is always encrypted using Microsoft’s keys as it passes through the machine learning pipeline. However, the training data is not encrypted using [Customer-Managed Keys (CMK)](customer-managed-keys) if you enabled CMK in your Microsoft Sentinel workspace. To opt out of Fusion, navigate to **Microsoft Sentinel** &gt; **Configuration** &gt; **Analytics &gt; Active rules**, right-click on the **Advanced Multistage Attack Detection** rule, and select **Disable.**

For Microsoft Sentinel workspaces that are onboarded to the Microsoft Defender portal, Fusion is disabled. Its functionality is replaced by the Microsoft Defender XDR correlation engine.

## Fusion for emerging threats

Important

Indicated Fusion detections are currently in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](overview#changes-for-new-customers-starting-july-2025).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

## Configure Fusion

Fusion is enabled by default in Microsoft Sentinel, as an [analytics rule](detect-threats-built-in) called **Advanced multistage attack detection**. You can view and change the status of the rule, configure source signals to be included in the Fusion ML model, or exclude specific detection patterns that might not be applicable to your environment from Fusion detection. Learn how to [configure the Fusion rule](configure-fusion-rules).

You might want to opt out of Fusion if you've enabled [Customer-Managed Keys (CMK)](customer-managed-keys) in your workspace. Microsoft Sentinel currently uses 30 days of historical data to train the Fusion engine's machine learning algorithms, and this data is always encrypted using Microsoft’s keys as it passes through the machine learning pipeline. However, the training data is not encrypted using CMK. To opt out of Fusion, disable the **Advanced Multistage Attack Detection** analytics rule in Microsoft Sentinel. For more information, see [Configure Fusion rules](configure-fusion-rules#configure-fusion-rules).

Fusion is disabled when Microsoft Sentinel is [onboarded to the Defender portal](https://aka.ms/unified-soc-announcement). Instead, when working in the Defender portal, functionality provided by Fusion is replaced by the Microsoft Defender XDR correlation engine.

## Fusion for emerging threats (Preview)

The volume of security events continues to grow, and the scope and sophistication of attacks are ever increasing. We can define the known attack scenarios, but how about the emerging and unknown threats in your environment?

Microsoft Sentinel's ML-powered Fusion engine can help you find the **emerging and unknown threats** in your environment by applying **extended ML analysis** and by correlating **a broader scope of anomalous signals**, while keeping the alert fatigue low.

The Fusion engine's ML algorithms constantly learn from existing attacks and apply analysis based on how security analysts think. It can therefore discover previously undetected threats from millions of anomalous behaviors across the kill-chain throughout your environment, which helps you stay one step ahead of the attackers.

**Fusion for emerging threats** supports data collection and analysis from the following sources:

- [Out-of-the-box anomaly detections](soc-ml-anomalies)
- Alerts from Microsoft services:

    - Microsoft Entra ID Protection
    - Microsoft Defender for Cloud
    - Microsoft Defender for IoT
    - Microsoft Defender XDR
    - Microsoft Defender for Cloud Apps
    - Microsoft Defender for Endpoint
    - Microsoft Defender for Identity
    - Microsoft Defender for Office 365
- [Alerts from scheduled analytics rules](configure-fusion-rules#configure-scheduled-analytics-rules-for-fusion-detections). [Analytics rules](scheduled-rules-overview) must contain kill-chain (tactics) and entity mapping information in order to be used by Fusion.

You don't need to have connected all the data sources listed above in order to make Fusion for emerging threats work. However, the more data sources you have connected, the broader the coverage, and the more threats Fusion will find.

When the Fusion engine's correlations result in the detection of an emerging threat, Microsoft Sentinel generates a high-severity incident titled **Possible multistage attack activities detected by Fusion**.

## Fusion for ransomware

Microsoft Sentinel's Fusion engine generates an incident when it detects multiple alerts of different types from the following data sources, and determines that they might be related to ransomware activity:

- [Microsoft Defender for Cloud](connect-defender-for-cloud)
- [Microsoft Defender for Endpoint](data-connectors-reference#microsoft-defender-for-endpoint)
- [Microsoft Defender for Identity connector](data-connectors-reference#microsoft-defender-for-identity)
- [Microsoft Defender for Cloud Apps](data-connectors-reference#microsoft-defender-for-cloud-apps)
- [Microsoft Sentinel scheduled analytics rules](scheduled-rules-overview). Fusion only considers scheduled analytics rules with tactics information and mapped entities.

Such Fusion incidents are named **Multiple alerts possibly related to Ransomware activity detected**, and are generated when relevant alerts are detected during a specific time-frame and are associated with the **Execution** and **Defense Evasion** stages of an attack.

For example, Microsoft Sentinel would generate an incident for possible ransomware activities if the following alerts are triggered on the same host within a specific timeframe:

| Alert | Source | Severity |
| --- | --- | --- |
| **Windows Error and Warning Events** | Microsoft Sentinel scheduled analytics rules | informational |
| **'GandCrab' ransomware was prevented** | Microsoft Defender for Cloud | medium |
| **'Emotet' malware was detected** | Microsoft Defender for Endpoint | informational |
| **'Tofsee' backdoor was detected** | Microsoft Defender for Cloud | low |
| **'Parite' malware was detected** | Microsoft Defender for Endpoint | informational |

## Scenario-based Fusion detections

The following section lists the types of [scenario-based multistage attacks](fusion-scenario-reference), grouped by threat classification, that Microsoft Sentinel detects using the Fusion correlation engine.

In order to enable these Fusion-powered attack detection scenarios, their associated data sources must be ingested to your Log Analytics workspace. Select the links in the table below to learn about each scenario and its associated data sources.

| Threat classification | Scenarios |
| --- | --- |
| **Compute resource abuse** | - (PREVIEW) [Multiple VM creation activities *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#multiple-vm-creation-activities-following-suspicious-azure-active-directory-sign-in) |
| **Credential access** | - (PREVIEW) [Multiple passwords reset by user *following* suspicious sign-in](fusion-scenario-reference#multiple-passwords-reset-by-user-following-suspicious-sign-in)<br>- (PREVIEW) [Suspicious sign-in *coinciding with* successful sign-in to Palo Alto VPN by IP with multiple failed Microsoft Entra sign-ins](fusion-scenario-reference#suspicious-sign-in-coinciding-with-successful-sign-in-to-palo-alto-vpn-by-ip-with-multiple-failed-azure-ad-sign-ins) |
| **Credential harvesting** | - [Malicious credential theft tool execution *following* suspicious sign-in](fusion-scenario-reference#malicious-credential-theft-tool-execution-following-suspicious-sign-in)<br>- [Suspected credential theft activity *following* suspicious sign-in](fusion-scenario-reference#suspected-credential-theft-activity-following-suspicious-sign-in) |
| **Crypto-mining** | - [Crypto-mining activity *following* suspicious sign-in](fusion-scenario-reference#crypto-mining-activity-following-suspicious-sign-in) |
| **Data destruction** | - [Mass file deletion *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#mass-file-deletion-following-suspicious-azure-ad-sign-in)<br>- (PREVIEW) [Mass file deletion *following* successful Microsoft Entra sign-in from IP blocked by a Cisco firewall appliance](fusion-scenario-reference#mass-file-deletion-following-successful-azure-ad-sign-in-from-ip-blocked-by-a-cisco-firewall-appliance)<br>- (PREVIEW) [Mass file deletion *following* successful sign-in to Palo Alto VPN by IP with multiple failed Microsoft Entra sign-ins](fusion-scenario-reference#mass-file-deletion-following-successful-sign-in-to-palo-alto-vpn-by-ip-with-multiple-failed-azure-ad-sign-ins)<br>- (PREVIEW) [Suspicious email deletion activity *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#suspicious-email-deletion-activity-following-suspicious-azure-ad-sign-in) |
| **Data exfiltration** | - (PREVIEW) [Mail forwarding activities *following* new admin-account activity not seen recently](fusion-scenario-reference#mail-forwarding-activities-following-new-admin-account-activity-not-seen-recently)<br>- [Mass file download *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#mass-file-download-following-suspicious-azure-ad-sign-in)<br>- (PREVIEW) [Mass file download *following* successful Microsoft Entra sign-in from IP blocked by a Cisco firewall appliance](fusion-scenario-reference#mass-file-download-following-successful-azure-ad-sign-in-from-ip-blocked-by-a-cisco-firewall-appliance)<br>- (PREVIEW) [Mass file download *coinciding with* SharePoint file operation from previously unseen IP](fusion-scenario-reference#mass-file-download-coinciding-with-sharepoint-file-operation-from-previously-unseen-ip)<br>- [Mass file sharing *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#mass-file-sharing-following-suspicious-azure-ad-sign-in)<br>- (PREVIEW) [Multiple Power BI report sharing activities *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#multiple-power-bi-report-sharing-activities-following-suspicious-azure-ad-sign-in)<br>- [Office 365 mailbox exfiltration *following* a suspicious Microsoft Entra sign-in](fusion-scenario-reference#office-365-mailbox-exfiltration-following-a-suspicious-azure-ad-sign-in)<br>- (PREVIEW) [SharePoint file operation from previously unseen IP *following* malware detection](fusion-scenario-reference#sharepoint-file-operation-from-previously-unseen-ip-following-malware-detection)<br>- (PREVIEW) [Suspicious inbox manipulation rules set *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#suspicious-inbox-manipulation-rules-set-following-suspicious-azure-ad-sign-in)<br>- (PREVIEW) [Suspicious Power BI report sharing *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#suspicious-power-bi-report-sharing-following-suspicious-azure-ad-sign-in) |
| **Denial of service** | - (PREVIEW) [Multiple VM deletion activities *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#multiple-vm-deletion-activities-following-suspicious-azure-ad-sign-in) |
| **Lateral movement** | - [Office 365 impersonation *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#office-365-impersonation-following-suspicious-azure-ad-sign-in)<br>- (PREVIEW) [Suspicious inbox manipulation rules set *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#suspicious-inbox-manipulation-rules-set-following-suspicious-azure-ad-sign-in) |
| **Malicious administrative activity** | - [Suspicious cloud app administrative activity *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#suspicious-cloud-app-administrative-activity-following-suspicious-azure-ad-sign-in)<br>- (PREVIEW) [Mail forwarding activities *following* new admin-account activity not seen recently](fusion-scenario-reference#mail-forwarding-activities-following-new-admin-account-activity-not-seen-recently-1) |
| **Malicious execution with legitimate process** | - (PREVIEW) [PowerShell made a suspicious network connection, *followed by*anomalous traffic flagged by Palo Alto Networks firewall](fusion-scenario-reference#powershell-made-a-suspicious-network-connection-followed-by-anomalous-traffic-flagged-by-palo-alto-networks-firewall)<br>- (PREVIEW) [Suspicious remote WMI execution *followed by*anomalous traffic flagged by Palo Alto Networks firewall](fusion-scenario-reference#suspicious-remote-wmi-execution-followed-by-anomalous-traffic-flagged-by-palo-alto-networks-firewall)<br>- [Suspicious PowerShell command line *following* suspicious sign-in](fusion-scenario-reference#suspicious-powershell-command-line-following-suspicious-sign-in) |
| **Malware C2 or download** | - (PREVIEW) [Beacon pattern detected by Fortinet following multiple failed user sign-ins to a service](fusion-scenario-reference#beacon-pattern-detected-by-fortinet-following-multiple-failed-user-sign-ins-to-a-service)<br>- (PREVIEW) [Beacon pattern detected by Fortinet *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#beacon-pattern-detected-by-fortinet-following-suspicious-azure-ad-sign-in)<br>- (PREVIEW) [Network request to TOR anonymization service *followed by*anomalous traffic flagged by Palo Alto Networks firewall](fusion-scenario-reference#network-request-to-tor-anonymization-service-followed-by-anomalous-traffic-flagged-by-palo-alto-networks-firewall)<br>- (PREVIEW) [Outbound connection to IP with a history of unauthorized access attempts *followed by*anomalous traffic flagged by Palo Alto Networks firewall](fusion-scenario-reference#outbound-connection-to-ip-with-a-history-of-unauthorized-access-attempts-followed-by-anomalous-traffic-flagged-by-palo-alto-networks-firewall) |
| **Persistence** | - (PREVIEW) [Rare application consent *following* suspicious sign-in](fusion-scenario-reference#rare-application-consent-following-suspicious-sign-in) |
| **Ransomware** | - [Ransomware execution *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#ransomware-execution-following-suspicious-azure-ad-sign-in) |
| **Remote exploitation** | - (PREVIEW) [Suspected use of attack framework *followed by*anomalous traffic flagged by Palo Alto Networks firewall](fusion-scenario-reference#suspected-use-of-attack-framework-followed-by-anomalous-traffic-flagged-by-palo-alto-networks-firewall) |
| **Resource hijacking** | - (PREVIEW) [Suspicious resource / resource group deployment by a previously unseen caller *following* suspicious Microsoft Entra sign-in](fusion-scenario-reference#suspicious-resource--resource-group-deployment-by-a-previously-unseen-caller-following-suspicious-azure-ad-sign-in) |