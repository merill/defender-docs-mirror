---
layout: FAQ
title: Microsoft Defender for Identity frequently asked questions - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/technical-faq
summary: >
  <p>This article provides a list of frequently asked questions and answers about Microsoft Defender for Identity divided into the following categories:</p>
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
description: Provides a list of frequently asked questions about Microsoft Defender for Identity and the associated answers
ms.date: 2024-06-10T00:00:00.0000000Z
ms.topic: article
locale: en-us
document_id: e97ffd97-fe32-11a6-80d9-7dd69b100b38
document_version_independent_id: e97ffd97-fe32-11a6-80d9-7dd69b100b38
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/technical-faq.yml
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: technical-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/technical-faq.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/58f888a4-3847-4473-ba35-882e789f0dbe
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/314a9abc-91dd-4683-8691-43005e929bb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: 1a4fb64f-5fda-ff05-c8a6-2394416c67fd
---

# Microsoft Defender for Identity frequently asked questions - Microsoft Defender for Identity | Microsoft Learn

This article provides a list of frequently asked questions and answers about Microsoft Defender for Identity divided into the following categories:

## What is Defender for Identity?

### What can Defender for Identity detect?

Defender for Identity detects known malicious attacks and techniques, security issues, and risks against your network. For the full list of Defender for Identity detections, see [Defender for Identity Security Alerts](/en-us/defender-for-identity/alerts-overview).

### What data does Defender for Identity collect?

Defender for Identity collects and stores information from your configured servers, such as domain controllers, member servers, and so on. Data is stored in a database specific to the service for administration, tracking, and reporting purposes.

Information collected includes:

- Network traffic to and from domain controllers, such as Kerberos authentication, NTLM authentication, or DNS queries.
- Security logs, such as Windows security events.
- Active Directory information, such as structure, subnets, or sites.
- Entity information, such as names, email addresses, and phone numbers.

Microsoft uses this data to:

- Proactively identify indicators of attack (IOAs) in your organization.
- Generate alerts if a possible attack was detected.
- Provide your security operations with a view into entities related to threat signals from your network, enabling you to investigate and explore the presence of security threats on the network.

Microsoft doesn't mine your data for advertising or for any other purpose other than providing you with the service.

### How many Directory Service credentials does Defender for Identity support?

Defender for Identity currently supports adding up to 30 different Directory Service credentials to support Active Directory environments with untrusted forests. If you require more accounts, open a support ticket.

### Does Defender for Identity only use traffic from Active Directory?

In addition to analyzing Active Directory traffic using deep packet inspection technology, Defender for Identity also collects relevant Windows Events from your domain controller and creates entity profiles based on information from Active Directory Domain Services. Defender for Identity also supports receiving RADIUS accounting of VPN logs from various vendors (Microsoft, Cisco, F5, and Checkpoint).

### Does Defender for Identity monitor only domain-joined devices?

No. Defender for Identity monitors all devices in the network performing authentication and authorization requests against Active Directory, including non-Windows and mobile devices.

### Does Defender for Identity monitor computer accounts and user accounts?

Yes. Since computer accounts, and other entities, can be used to perform malicious activities, Defender for Identity monitors all computer accounts behavior and all other entities in the environment.

### What is the difference between Advanced Threat Analytics (ATA) and Defender for Identity?

ATA is a standalone on-premises solution with multiple components, such as the ATA Center that requires dedicated hardware on-premises.

Defender for Identity is a cloud-based security solution that uses your on-premises Active Directory signals. The solution is highly scalable and is frequently updated.

ATA has reached end of life. The final release of ATA is [Update 3 for ATA 1.9](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9). ATA ended mainstream support on January 12, 2021, and extended support ended on January 13, 2026. ATA no longer receives updates of any kind, including security updates. For more information, see [Advanced Threat Analytics 1.X lifecycle](/en-us/lifecycle/products/advanced-threat-analytics-1x). We strongly recommend migrating to Defender for Identity. For migration guidance, see [Migrate from ATA to Defender for Identity](/en-us/defender-for-identity/migrate-from-ata-overview).

In contrast to the ATA sensor, the Defender for Identity sensor also uses data sources such as Event Tracing for Windows (ETW) enabling Defender for Identity to deliver extra detections.

Defender for Identity's frequent updates include the following features and capabilities:

- **Support for [multi-forest environments](deploy/multi-forest)**: Provides organizations visibility across AD forests.
- **[Microsoft Secure Score posture assessments](/en-us/defender-for-identity/security-assessment)**: Identifies common misconfigurations and exploitable components and provides remediation paths to reduce the attack surface.
- **Native integrations**: Integrates with Microsoft Defender for Cloud Apps and Microsoft Entra ID Protection to provide a hybrid view of what's taking place in both on-premises and hybrid environments.
- **Contributes to Microsoft Defender XDR**: Contributes alert and threat data to Microsoft Defender XDR. Microsoft Defender XDR uses the Microsoft 365 security portfolio (identities, endpoints, data, and applications) to automatically analyze cross-domain threat data, building a complete picture of each attack in a single dashboard.

    With this breadth and depth of clarity, Defenders can focus on critical threats and hunt for sophisticated breaches. Defenders can trust that Microsoft Defender XDR's powerful automation stops attacks anywhere in the kill chain and returns the organization to a secure state.

## Licensing and privacy

### Where can I get a license for Microsoft Defender for Identity?

Defender for Identity is available as part of Enterprise Mobility + Security 5 suite (EMS E5), and as a standalone license. You can acquire a license directly from the [Microsoft 365 portal](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) or through the Cloud Solution Partner (CSP) licensing model.

### Does Defender for Identity need only a single license or does it require a license for every user I want to protect?

For information about Defender for Identity licensing requirements, see [Defender for Identity licensing guidance](/en-us/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance#microsoft-defender-for-identity).

### Is my data isolated from other customer data?

Yes, your data is isolated through access authentication and logical segregation based on customer identifiers. Each customer can only access data collected from their own organization and generic data that Microsoft provides.

### Do I have the flexibility to select where to store my data?

No. When your Defender for Identity workspace is created, it's stored automatically in the Azure region that's closest to your Microsoft Entra tenant's geographical location. Once your Defender for Identity workspace is created, Defender for Identity data can't be moved to a different region.

### How does Microsoft prevent malicious insider activities and abuse of high privilege roles?

Microsoft developers and administrators have, by design, been given sufficient privileges to carry out their assigned duties to operate and evolve the service. Microsoft deploys combinations of preventive, detective, and reactive controls including the following mechanisms to help protect against unauthorized developer and/or administrative activity:

- Tight access control to sensitive data
- Combinations of controls that greatly enhance independent detection of malicious activity
- Multiple levels of monitoring, logging, and reporting

In addition, Microsoft conducts background verification checks on certain operations personnel, and limits access to applications, systems, and network infrastructure in proportion to the level of background verification. Operations personnel follow a formal process when they're required to access a customer's account or related information in the performance of their duties.

## Deployment

### How many Defender for Identity sensors do I need?

We recommend that you have a Defender for Identity sensor or standalone sensor for each one of your domain controllers. For more information, see [Defender for Identity sensor sizing](capacity-planning#sizing).

### Does Defender for Identity work with encrypted traffic?

While network protocols with encrypted traffic, such as AtSvc and WMI, aren't decrypted, sensors do still analyze the traffic.

### Does Defender for Identity work with Kerberos Armoring?

Defender for Identity supports Kerberos Armoring, also known as Flexible Authentication Secure Tunneling (FAST). The exception to this support is the over-pass the hash detection, which doesn't work with Kerberos Armoring.

### How do I monitor a virtual domain controller using Defender for Identity?

The Defender for Identity sensor can cover most virtual domain controllers. For more information, see [Defender for Identity Capacity Planning](deploy/capacity-planning).

If the Defender for Identity sensor can't cover a virtual domain controller, use either a virtual or physical Defender for Identity standalone sensor instead. For more information, see [Configure port mirroring](deploy/configure-port-mirroring).

The easiest way is to have a virtual Defender for Identity standalone sensor on every host where a virtual domain controller exists.

If your virtual domain controllers move between hosts, you need to perform one of the following steps:

- When the virtual domain controller moves to another host, preconfigure the Defender for Identity standalone sensor in that host to receive the traffic from the recently moved virtual domain controller.
- Make sure that you affiliate the virtual Defender for Identity standalone sensor with the virtual domain controller so that if it's moved, the Defender for Identity standalone sensor moves with it.
- There are some virtual switches that can send traffic between hosts.

### How do I configure the Defender for Identity sensors to communicate with Defender for Identity cloud service when I have a proxy?

For your domain controllers to communicate with the cloud service, you must open: \*.atp.azure.com port 443 in your firewall/proxy. For more information, see [Configure your proxy or firewall to enable communication with Defender for Identity sensors](configure-proxy).

### Can Defender for Identity monitored domain controllers be virtualized on your IaaS solution?

Yes, you can use the Defender for Identity sensor to monitor domain controllers that are in any IaaS solution.

### Can Defender for Identity support multi-domain and multi-forest?

Defender for Identity supports multi-domain environments and multiple forests. For more information and trust requirements, see [Multi-forest support](deploy/multi-forest).

### Can you see the overall health of the deployment?

Yes, you can view the overall deployment health and any specific issues related to configuration, connectivity, and so on. You're alerted as these events occur with Defender for Identity health issues.

### Does Microsoft Defender for Identity require synchronizing users to Microsoft Entra ID?

Microsoft Defender for Identity provides security value for all Active Directory accounts including those that are not synced to Microsoft Entra ID. User accounts that are synced to Microsoft Entra ID benefit from the security value provided by Microsoft Entra ID based on license level. For more detailse see: [Identity inventory](/en-us/defender-for-identity/identity-inventory).

## WinPcap and Npcap drivers

### What recommendations about WinPcap and Npcap drivers are changing?

The Microsoft Defender for Identity team recommends that all customers use the Npcap driver instead of the WinPcap drivers. Starting with Defender for Identity version 2.184, the installation package installs Npcap 1.0 OEM instead of the WinPcap 4.1.3 drivers.

### Why are we moving away from WinPcap?

WinPcap is no longer supported and since it's no longer being developed, the driver can't be optimized any longer for the Defender for Identity sensor. Additionally, if there's an issue in the future with the WinPcap driver, there are no options for a fix.

### Why Npcap?

Npcap is supported, while WinPcap is no longer a supported product.

### What version of Npcap is supported?

The MDI Sensor requires Npcap 1.0 or later. The Sensor installation package will install version 1.0 if no other version of Npcap is installed. If you have Npcap already installed (because of other software requirements, or any other reason) it is important to ensure it version 1.0 or later, and that it has been installed with the required settings for MDI.

### Do I need to manually remove and reinstall the Sensor, or will the automatic update service handle this as part of its normal updating?

Yes. It is required to manually remove the Sensor to remove the WinPcap drivers. The reinstallation using the latest package will install the Npcap drivers.

### How can I check whether my current installation of Defender for Identity uses Npcap or WinPcap?

You can see that 'Npcap OEM' is installed through the Add/Remove programs (appwiz.cpl), and if there was an open [health issue](health-alerts) for this, it will be automatically closed.

### I have more than five domain controllers in my organization. Do I need to purchase an Npcap license if I'm using Npcap on these domain controllers?

No, Npcap has an exemption from the usual limit of five installs. You can install it on unlimited systems where it's only used with the Defender for Identity sensor.

See the Npcap license agreement [here](https://github.com/nmap/Npcap/blob/master/LICENSE), and search for Microsoft Defender for Identity.

### Is Npcap also relevant for ATA?

No, only the Microsoft Defender for Identity sensor supports Npcap version 1.00.

### I would like to script the deployment of Npcap, do I need to purchase the OEM version?

No, you don't need to purchase the OEM version. Download the sensor installation package version 2.156 and above from the Defender for Identity console, which includes the OEM version of Npcap.

### How do I download and install or upgrade the Npcap driver?

- You can obtain the Npcap executables by [downloading the latest deployment package of the Defender for Identity sensor](download-sensor).
- **If you haven't yet installed the sensor**, install the sensor using version 2.184 or higher.
- **If you already installed the sensor** with WinPcap and need to update to use Npcap:

    1. Uninstall the sensor. Use either **Add/Remove programs** from the Windows control panel (*appwiz.cpl*), or run the following [uninstall command](uninstall-sensor#uninstall-the-defender-for-identity-sensor-silently): `".\Azure ATP Sensor Setup.exe" /uninstall /quiet`
    2. Uninstall WinPcap if needed. This step is relevant only if WinPcap was manually installed prior to the sensor installation. In this case, you would need to manually remove WinPcap.
    3. Reinstall the sensor using version 2.184 or higher.
- **If you want to manually install Npcap**: Install Npcap with the following options:

    - If you're using the GUI installer, clear the **loopback support** option and select **WinPcap** mode. Make sure the **Restrict Npcap driver's access to Administrators only** option is cleared.
    - If you're using the command line, run: `npcap-1.00-oem.exe /loopback_support=no /winpcap_mode=yes /admin_only=no /S`
- **If you want to manually upgrade Npcap**:

    1. Stop the Defender for Identity sensor services, *AATPSensorUpdater* and *AATPSensor*. Run: `Stop-Service -Name AATPSensorUpdater -Force; Stop-Service -Name AATPSensor -Force`
    2. Remove Npcap using **Add/Remove programs** in the Windows control panel (*appwiz.cpl*).
    3. Install Npcap with the following options:

        - If you're using the GUI installer, clear the **loopback support** option and select **WinPcap** mode. Make sure the **Restrict Npcap driver's access to Administrators only** option is cleared.
        - If you're using the command line, run: `npcap-1.00-oem.exe /loopback_support=no /winpcap_mode=yes /admin_only=no /S`
    4. Start the Defender for Identity sensor services, *AATPSensorUpdater* and *AATPSensor*. Run: `Start-Service -Name AATPSensorUpdater; Start-Service -Name AATPSensor`

## Operation

### What kind of integration does Defender for Identity have with SIEMs?

Defender for Identity can be configured to send a Syslog alert, to any SIEM server using the CEF format, for health issues and when a security alert is detected. For more information, see the [SIEM log reference](cef-format-sa).

### Why are certain accounts considered sensitive?

Accounts are considered as sensitive when an account is a member of groups that are designated as sensitive (for example: "Domain Admins").

To understand why an account is sensitive you can review its group membership to understand which sensitive groups it belongs to. The group that it belongs to can also be sensitive due to another group, so the same process should be performed until you locate the highest level sensitive group. Alternately, manually [tag accounts as sensitive](/en-us/defender-for-identity/entity-tags).

### Do you have to write your own rules and create a threshold/baseline?

With Defender for Identity, there's no need to create rules, thresholds, or baselines and then fine-tune. Defender for Identity analyzes the behaviors among users, devices, and resources, as well as their relationship to one another, and can detect suspicious activity and known attacks quickly. Three weeks after deployment, Defender for Identity starts to detect behavioral suspicious activities. On the other hand, Defender for Identity will start detecting known malicious attacks and security issues immediately after deployment.

### Which traffic does Defender for Identity generate in the network from domain controllers, and why?

Defender for Identity generates traffic from domain controllers to computers in the organization in one of three scenarios:

- **Network Name resolution** Defender for Identity captures traffic and events, learning and profiling users and computer activities in the network. To learn and profile activities according to computers in the organization, Defender for Identity needs to resolve IPs to computer accounts. To resolve IPs to computer names Defender for Identity sensors, request the IP address for the computer name *behind* the IP address.

    Requests are made using one of four methods:

    - NTLM over RPC (TCP Port 135)
    - NetBIOS (UDP port 137)
    - RDP (TCP port 3389)
    - Query the DNS server using reverse DNS lookup of the IP address (UDP 53)

    After getting the computer name, Defender for Identity sensors cross check the details in Active Directory to see if there's a correlated computer object with the same computer name. If a match is found, an association is made between the IP address and the matched computer object.
- **Querying Active Directory using LDAP** for entity data Defender for Identity sensors query the domain controller from the domain where the entity belongs. It can be the same sensor, or another domain controller from that domain.

| Protocol | Service | Port | Source | Direction |
| --- | --- | --- | --- | --- |
| LDAP | TCP and UDP | 389 | Domain controllers | Outbound |
| Secure LDAP (LDAPS) | TCP | 636 | Domain controllers | Outbound |
| LDAP to Global Catalog | TCP | 3268 | Domain controllers | Outbound |
| LDAPS to Global Catalog | TCP | 3269 | Domain controllers | Outbound |

### Why don't activities always show both the source user and computer?

Defender for Identity captures activities over many different protocols. In some cases, Defender for Identity doesn't receive the data of the source user in the traffic. Defender for Identity attempts to correlate the session of the user to the activity, and when the attempt is successful, the source user of the activity is displayed. When user correlation attempts fail, only the source computer is displayed.

### Why do I see DNS queries to aatp.dns.detection.local?

Defender for Identity sensor might trigger a DNS call to "aatp.dns.detection.local" in response to certain incoming DNS activities to the MDI monitored machine.

## Personal data management

### Can personal user data be updated in Defender for Identity?

Personal user data in Defender for Identity is derived from the user's object in the organization's Active Directory, and can't be updated directly in Defender for Identity.

### How can I export personal data from Defender for Identity?

You can export personal data from Defender for Identity using the same method as exporting security alert information. For more information, see [Review security alerts](manage-security-alerts#review-security-alerts).

### How can I locate personal data stored in Defender for Identity?

Use the [Microsoft Defender portal](https://security.microsoft.com) search bar to search for identifiable personal data, such as a specific user or computer. For more information, see [Investigate assets](investigate-assets).

### What sort of auditing does Defender for Identity run on personal data?

Defender for Identity implements the audit of personal data changes, including the deleting and exporting of personal data records. Audit trail retention time is 90 days. Auditing in Defender for Identity is a back-end feature and not accessible to customers.

### What happens in Defender for Identity when a user is deleted from the organization's Active Directory?

After a user is deleted from the organization's Active Directory, Defender for Identity automatically deletes the user profile and any related network activity in alignment with Defender for Identity's [general data retention policy](privacy-compliance#data-retention), unless the data is part of an active incident. We recommend adding **Read-only** permissions on the **Deleted Objects** container. For more information, see [Grant required DSA permissions](directory-service-accounts#grant-required-dsa-permissions).

## Troubleshooting

### What should I do if the Defender for Identity sensor or standalone sensor doesn't start?

Look at the most recent error in the current error [log](troubleshooting-using-logs) (Where Defender for Identity is installed under the "Logs" folder).