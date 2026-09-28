---
layout: Conceptual
title: Forward on-premises OT alert information to partners - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-forward-alert-information-to-partners
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
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
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
description: Configure your OT sensor to forward alert details to partner services, syslog servers, email recipients, and other external destinations.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 0513e9c3-7edf-5695-e64d-d237d686a0fd
document_version_independent_id: ea995143-604c-5b9d-f528-7d50b468a515
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-forward-alert-information-to-partners.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-forward-alert-information-to-partners
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-forward-alert-information-to-partners.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: e977274b-20c9-83b0-9794-8c598bfe08b7
---

# Forward on-premises OT alert information to partners - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT alerts enhance your network security and operations with real-time details about events logged in your network. OT alerts are triggered when OT network sensors detect changes or suspicious activity in network traffic that needs your attention.

This article describes how to configure your OT sensor to forward alerts to partner services, syslog servers, email addresses, and more. Forwarded alert information includes details like:

- Date and time of the alert
- Engine that detected the event
- Alert title and descriptive message
- Alert severity

- Source and destination name and IP address
- Suspicious traffic detected
- Disconnected sensors
- Remote backup failures

Note

Forwarding alert rules run only on alerts triggered after the forwarding rule is created. Alerts already in the system from before the forwarding rule was created are not affected by the rule.

## Prerequisites

Before you create forwarding rules, make sure the following prerequisites are met:

- Depending on where you want to create your forwarding alert rules, you need to have either an [OT network sensor installed](how-to-install-software), with access as an **Admin** user.

    For more information, see [Install OT agentless monitoring software](how-to-install-software) and [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).
- You also need to define SMTP settings on the OT sensor.

    For more information, see [Configure SMTP mail server settings on an OT sensor](how-to-manage-individual-sensors#configure-smtp-mail-server-settings).

## Create forwarding rules on an OT sensor

1. Sign into the OT sensor and select **Forwarding** on the left-hand menu &gt; **+ Create new rule**.
2. In the **Add forwarding rule** pane, enter a meaningful rule name, and then define rule conditions and actions as follows:

    | Name | Description |
    | --- | --- |
    | **Minimal alert level** | Select the minimum [alert severity level](alert-engine-messages#alert-severities) you want to forward.  For example, if you select **Minor**, minor alerts and any alert above this severity level are forwarded. |
    | **Any protocol detected** | Toggle on to forward alerts from all protocol traffic or toggle off and select the specific protocols you want to include. |
    | **Traffic detected by any engine** | Toggle on to forward alerts from all [analytics engines](architecture#defender-for-iot-analytics-engines), or toggle off and select the specific engines you want to include. |
    | **Actions** | Select the type of server you want to forward alerts to, and then define any other required information for that server type. To add multiple servers to the same rule, select **+ Add server** and add more details. For more information, see Configure alert forwarding rule actions. |
3. When you're done configuring the rule, select **Save**. The rule is listed on the **Forwarding** page.
4. Test the rule you've created:

    1. Select the options menu (**...**) for your rule &gt; **Send Test Message**.
    2. Go to the target service to verify that the information sent by the sensor was received.

### Edit or delete forwarding rules on an OT sensor

Warning

Deleting a forwarding rule is irreversible.

To edit or delete an existing rule:

1. Sign into your OT sensor and select **Forwarding** on the left-hand menu.
2. Select the options menu (**...**) for your rule, and then do one of the following:

    - Select **Edit** and update the fields as needed. For field descriptions, see Create forwarding rules on an OT sensor. When you're done, select **Save**.
    - Select **Delete** &gt; **Yes** to confirm the deletion.

## Configure alert forwarding rule actions

OT sensor alert forwarding rules support these action types: Email, Syslog server, and NetWitness.

### Configure the email address action

Configure an **Email** action to forward alert data to the configured email address.

In the **Actions** area, enter the following details:

| Name | Description |
| --- | --- |
| **Server** | Select **Email**. |
| **Email** | Enter the email address you want to forward the alerts to. Each rule supports a single email address. |
| **Timezone** | Select the time zone you want to use for the alert detection in the target system. |

### Configure syslog server actions

Configure a Syslog server action to forward alert data to the selected type of Syslog server.

In the **Actions** area, enter the following details:

| Name | Description |
| --- | --- |
| **Server** | Select one of the following types of syslog formats: - **SYSLOG Server (CEF format)**- **SYSLOG Server (LEEF format)**- **SYSLOG Server (Object)**- **SYSLOG Server (Text Message)** |
| **Host** / **Port** | Enter the syslog server's host name and port |
| **Timezone** | Select the time zone you want to use for the alert detection in the target system. |
| **Protocol** | Supported for text messages only. Select **TCP** or **UDP**. |
| **Enable encryption** | Supported for CEF format only. Toggle on to configure a TLS encryption certificate file, key file, and passphrase. |

For syslog output syntax details, see Syslog text message output fields, Syslog object output fields, Syslog CEF output fields, and Syslog LEEF output fields.

#### Syslog text message output fields

The following table describes the fields included in syslog text message output.

| Name | Description |
| --- | --- |
| Priority | User. Alert |
| Message | CyberX platform name: The sensor name. Microsoft Defender for IoT Alert: The title of the alert. Type: The type of the alert. Can be **Protocol Violation**, **Policy Violation**, **Malware**, **Anomaly**, or **Operational**. Severity: The severity of the alert. Can be **Warning**, **Minor**, **Major**, or **Critical**. Source: The source device name. Source IP: The source device IP address. Protocol (Optional): The detected source protocol. Address (Optional): Source protocol address. Destination: The destination device name. Destination IP: The IP address of the destination device. Protocol (Optional): The detected destination protocol. Address (Optional): The destination protocol address. Message: The message of the alert. Alert group: The alert group associated with the alert.  UUID (Optional): The UUID the alert. |

#### Syslog object output fields

The following table lists the fields included in syslog object output.

| Name | Description |
| --- | --- |
| Priority | `User.Alert` |
| Date and Time | Date and time that the syslog server machine received the information. |
| Hostname | Sensor IP |
| Message | Sensor name: The name of the appliance.  Alert time: The time that the alert was detected: Can vary from the time of the syslog server machine, and depends on the time-zone configuration of the forwarding rule.  Alert title: The title of the alert.  Alert message: The message of the alert.  Alert severity: The severity of the alert: **Warning**, **Minor**, **Major**, or **Critical**.  Alert type: **Protocol Violation**, **Policy Violation**, **Malware**, **Anomaly**, or **Operational**.  Protocol: The protocol of the alert. **Source\_MAC**: IP address, name, vendor, or OS of the source device.  Destination\_MAC: IP address, name, vendor, or OS of the destination. If data is missing, the value is **N/A**.  alert\_group: The alert group associated with the alert. |

#### Syslog CEF output fields

The following table describes the fields included in syslog CEF output.

| Name | Description |
| --- | --- |
| Priority | `User.Alert` |
| Date and time | Date and time that the sensor sent the information, in UTC format |
| Hostname | Sensor hostname |
| Message | *CEF:0*Microsoft Defender for IoT/CyberX Sensor name Sensor version Microsoft Defender for IoT Alert Alert title Integer indication of severity. 1=**Warning**, 4=**Minor**, 8=**Major**, or 10=**Critical**.msg= The message of the alert. protocol= The protocol of the alert. severity= **Warning**, **Minor**, **Major**, or **Critical**. type= **Protocol Violation**, **Policy Violation**, **Malware**, **Anomaly**, or **Operational**. UUID= UUID of the alert (Optional)  start= The time that the alert was detected. Might vary from the time of the syslog server machine, and depends on the time-zone configuration of the forwarding rule. src\_ip= IP address of the source device. (Optional) src\_mac= MAC address of the source device. (Optional) dst\_ip= IP address of the destination device. (Optional)dst\_mac= MAC address of the destination device. (Optional)cat= The alert group associated with the alert. |

#### Syslog LEEF output fields

The following table describes the fields included in syslog LEEF output.

| Name | Description |
| --- | --- |
| Priority | `User.Alert` |
| Date and time | Date and time that the sensor sent the information, in UTC format |
| Hostname | Sensor IP |
| Message | Sensor name: The name of the Microsoft Defender for IoT appliance. *LEEF:1.0*Microsoft Defender for IoT Sensor Sensor version Microsoft Defender for IoT Alert title: The title of the alert. msg: The message of the alert. protocol: The protocol of the alert.severity: **Warning**, **Minor**, **Major**, or **Critical**. type: The type of the alert: **Protocol Violation**, **Policy Violation**, **Malware**, **Anomaly**, or **Operational**. start: The time of the alert. It might be different from the time of the syslog server machine, and depends on the time-zone configuration. src\_ip: IP address of the source device.dst\_ip: IP address of the destination device. cat: The alert group associated with the alert. |

### Configure the NetWitness action

Configure a **NetWitness** action to send alert information to a NetWitness server.

In the **Actions** area, enter the following details:

| Name | Description |
| --- | --- |
| **Server** | Select **NetWitness**. |
| **Hostname / Port** | Enter the NetWitness server's hostname and port. |
| **Time zone** | Enter the time zone you want to use in the time stamp for the alert detection at the SIEM. |

## Configure forwarding rules for partner integrations

You might be integrating Defender for IoT with a partner service to send alert or device inventory information to another security or device management system, or to communicate with partner-side firewalls.

[Partner integrations](integrate-overview) can help to bridge previously siloed security solutions, enhance device visibility, and accelerate system-wide response to more rapidly mitigate risks.

In such cases, use supported **Actions** to enter credentials and other information required to communicate with integrated partner services.

For more information, see:

- [Integrate Fortinet with Microsoft Defender for IoT](tutorial-fortinet)
- [Integrate Qradar with Microsoft Defender for IoT](tutorial-qradar)

### Configure alert groups in partner services

When you configure forwarding rules to send alert data to Syslog servers, QRadar, and ArcSight, *alert groups* are automatically applied and are available in those partner servers.

*Alert groups* help SOC teams using those partner solutions to manage alerts based on enterprise security policies and business priorities. For example, alerts about new detections are organized into a *discovery* group, which includes any alerts about new devices, VLANs, user accounts, MAC addresses, and more.

Alert groups appear in partner services with the following prefixes:

| Prefix | Partner service |
| --- | --- |
| `cat` | [QRadar](tutorial-qradar), [ArcSight](integrations/arcsight), Syslog CEF, Syslog LEEF |
| `Alert Group` | Syslog text messages |
| `alert_group` | Syslog objects |

To use alert groups in your integration, make sure to configure your partner services to display the alert group name.

By default, alerts are grouped as follows:

- Abnormal communication behavior
- Custom alerts
- Remote access
- Abnormal HTTP communication behavior
- Discovery
- Restart and stop commands
- Authentication
- Firmware change
- Scan
- Unauthorized communication behavior
- Illegal commands

- Sensor traffic
- Bandwidth anomalies
- Internet access
- Suspicion of malware
- Buffer overflow
- Operation failures
- Suspicion of malicious activity
- Command failures
- Operational issues
- Configuration changes
- Programming

For more information and to create custom alert groups, contact [Microsoft Support](https://support.microsoft.com/supportforbusiness/productselection?sapId=82c8f35-1b8e-f274-ec11-c6efdd6dd099).

## Troubleshoot forwarding rules

If your forwarding alert rules aren't working as expected, check the following details.

### Troubleshoot certificate validation for forwarded alerts

**Certificate validation**. Forwarding rules for Syslog CEF, [Microsoft Sentinel](integrate-overview#microsoft-sentinel), and [QRadar](tutorial-qradar) support encryption and certificate validation.

If your OT sensors are configured to [verify CRL server access for SSL certificates](ot-deploy/create-ssl-certificates#verify-crl-server-access) and the certificate can't be verified, the alerts aren't forwarded.

In these cases, the sensor is the session's client and initiator. Certificates are typically received from the server or use asymmetric encryption, where a specific certificate is provided to set up the integration.