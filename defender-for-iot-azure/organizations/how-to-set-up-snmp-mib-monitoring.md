---
layout: Conceptual
title: Set Up SNMP MIB Monitoring on an OT Sensor - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-set-up-snmp-mib-monitoring
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
description: Learn how to set up your OT sensor for health monitoring via SNMP.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: bbe36fc7-0773-9e4a-2bc1-1f2c69e40a36
document_version_independent_id: 84e8a10b-7400-ed97-c5c5-10dcfe9885a6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-set-up-snmp-mib-monitoring.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-set-up-snmp-mib-monitoring
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-set-up-snmp-mib-monitoring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: b17f34b9-ee3e-a1d9-f7a0-40d9d5317a21
---

# Set Up SNMP MIB Monitoring on an OT Sensor - Microsoft Defender for IoT | Microsoft Learn

Configure your OT sensors for health monitoring by using an authorized Simple Network Management Protocol (SNMP) monitoring server. SNMP queries are polled up to 50 times a second, using UDP over port 161.

Setup for SNMP monitoring includes configuring settings on your OT sensor and on your SNMP server. To define Defender for IoT sensors on your SNMP server, either define your settings manually or use a predefined SNMP MIB file downloaded from the Azure portal.

## Prerequisites

Before you configure SNMP monitoring, make sure you have:

- **An SNMP monitoring server**, using SNMP versions 2 or 3.
    - If you're using SNMP version 3 with AES and 3-DES encryption, you also need:
        - A network management station (NMS) that supports SNMP version 3
        - An understanding of SNMP terminology, and the SNMP architecture in your organization
        - The UDP port 161 must be open in your firewall.

**The following SNMP server details:**

- IP address
- Username and password
- Authentication type: MD5 or SHA
- Encryption type: DES or AES
- Secret key
- SNMP v2 community string
- **An OT sensor** with [OT sensor software installed](ot-deploy/install-software-ot-sensor) and [activate and deploy the OT sensor](ot-deploy/activate-deploy-sensor), with access as an **Admin** user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).

To download a predefined SNMP MIB file from the Azure portal, you need access to the Azure portal as a [Security admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) user. For more information, see [Azure user roles and permissions for Defender for IoT](roles-azure).

## Configure SNMP monitoring settings on your OT sensor

1. Sign into your OT sensor and select **System settings &gt; Sensor management &gt; Health and troubleshooting &gt; SNMP MIB monitoring**.
2. In the **SNMP MIB monitoring configuration** pane, select **+ Add host** and enter the following details:

    ![Screenshot of the SNMP MIB monitoring configuration page.](media/how-to-set-up-snmp-mib-monitoring/simple-network-management-protocol-configuration.png)

    - **Host 1**: Enter the IP address of your SNMP monitoring server. Select **+ Add host** again if you have multiple servers, as many times as needed.
    - **SNMP V2**: Select if you're using SNMP version 2, and then enter your SNMP V2 community string. A community string can have up to 32 alphanumeric characters, and no spaces.
    - **SNMP V3**: Select if you're using SNMP version 3, and then enter the following details:

        | Name | Description |
        | --- | --- |
        | **Username** and **Password** | Enter the SNMP v3 credentials used to access the SNMP server. Both usernames and passwords must be configured on both the OT sensor and the SNMP server.Usernames can include up to 32 alphanumeric characters, and no spaces. Passwords are case-sensitive, and can include 8-12 alphanumeric characters. |
        | **Auth Type** | Select the authentication type used to access the SNMP server: **MD5** or **SHA** |
        | **Encryption** | Select the encryption used when communicating with the SNMP server: - **DES (Data Encryption Standard)** (56-bit key size): RFC3414 User-based Security Model (USM) for version 3 of the Simple Network Management Protocol (SNMPv3). - **AES (Advanced Encryption Standard)** (128 bits supported): RFC3826 The AES Cipher Algorithm in the SNMP User-based Security Model. |
        | **Secret Key** | Enter a secret key used when communicating with the SNMP server. The secret key must have exactly eight alphanumeric characters. |
3. Select **Save** to save your changes.

## Download Defender for IoT's SNMP MIB file

Defender for IoT in the Azure portal provides a downloadable SNMP MIB file. Load this SNMP MIB file into your SNMP monitoring system to predefine Defender for IoT sensors.

To download the SNMP MIB file from [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) on the Azure portal, select **Sites and sensors** &gt; **More actions** &gt; **Download SNMP MIB file**.

## Query SNMP configuration on the sensor

Note

- You can query the SNMP configuration on the sensor in version **25.2.1 or later.**

Before you begin, make sure you can [access the Defender for IoT CLI](references-work-with-defender-for-iot-cli-commands#defender-for-iot-cli-access) over SSH as the *cyberx* user, using a terminal emulator.

To validate and query the SNMP MIB monitoring configuration in the OT sensor:

1. In the OT sensor, go to **System settings &gt; Sensor management**
2. To [access the Defender for IoT CLI](references-work-with-defender-for-iot-cli-commands#defender-for-iot-cli-access), sign in to your OT or Enterprise IoT sensor as the *cyberx* user, using a terminal emulator and SSH.
3. Run the appropriate query for the SNMP version you configured, and update the variables accordingly:

- For version 2 type: `snmpwalk -v 2c -c<community-string> <sensor-ip> isa`
- For version 3 type: `snmpwalk -v 3 -aMD5|SHA -xDES|AES -A<password> -X<secret-key> -u<username> -|autoPriv <sensor-ip> isa`

## OT sensor OIDs for manual SNMP configurations

If you're configuring Defender for IoT sensors on your SNMP monitoring system manually, use the following table for reference regarding sensor object identifier values (OIDs):

| OT sensor | OID | Format | Description |
| --- | --- | --- | --- |
| **sysDescr** | 1.3.6.1.2.1.1.1 | DISPLAYSTRING | Returns `Microsoft Defender for IoT` |
| **Platform** | 1.3.6.1.2.1.1.1.0 | STRING | Sensor |
| **sysObjectID** | 1.3.6.1.2.1.1.2 | DISPLAYSTRING | Returns the private MIB allocation, for example `1.3.6.1.4.1.53313.1.1` is the private OID root for 1.3.6.1.4.1.53313 |
| **sysUpTime** | 1.3.6.1.2.1.1.3 | DISPLAYSTRING | Returns the sensor uptime in hundredths of a second |
| **sysContact** | 1.3.6.1.2.1.1.4 | DISPLAYSTRING | Returns the textual name of the admin user for this sensor |
| **Vendor** | 1.3.6.1.2.1.1.4.0 | STRING | Microsoft Support (support.microsoft.com) |
| **sysName** | 1.3.6.1.2.1.1.5 | DISPLAYSTRING | Returns the appliance name |
| **Appliance name** | 1.3.6.1.2.1.1.5.0 | STRING | Appliance name for the sensor |
| **sysLocation** | 1.3.6.1.2.1.1.6 | DISPLAYSTRING | Returns the default location Portal.azure.com |
| **sysServices** | 1.3.6.1.2.1.1.7 | INTEGER | Returns a value indicating the service this entity offers, for example, `7` signifies “applications” |
| **ifIndex** | 1.3.6.1.2.1.2.2.1.1 | GAUGE32 | Returns the sequential ID numbers for each network card |
| **ifDescription** | 1.3.6.1.2.1.2.2.1.2 | DISPLAYSTRING | Returns a string of the hardware description for each network interface card |
| **ifType** | 1.3.6.1.2.1.2.2.1.3 | INTEGER | Returns the type of network adapter, for example `1.3.6.1.2.1.2.2.1.3.117` signifies Gigabit Ethernet |
| **ifMtu** | 1.3.6.1.2.1.2.2.1.4 | GAUGE32 | Returns the MTU value for this network adapter. **Note** monitoring interfaces don't show an MTU value |
| **ifspeed** | 1.3.6.1.2.1.2.2.1.5 | GAUGE32 | Returns the interface speed for this network adapter |
| **Serial number** | 1.3.6.1.4.1.53313.1 | STRING | String that the license uses |
| **Software version** | 1.3.6.1.4.1.53313.2 | STRING | Xsense full-version string and management full-version string |
| **CPU usage** | 1.3.6.1.4.1.53313.3.1 | GAUGE32 | Indication for zero to 100 |
| **CPU temperature** | 1.3.6.1.4.1.53313.3.2 | STRING | Celsius indication for zero to 100 based on Linux input.  Any machine that has no actual physical temperature sensor (for example VMs) returns "No sensors found" |
| **Memory usage** | 1.3.6.1.4.1.53313.3.3 | GAUGE32 | Indication for zero to 100 |
| **Disk Usage** | 1.3.6.1.4.1.53313.3.4 | GAUGE32 | Indication for zero to 100 |
| **Service Status** | 1.3.6.1.4.1.53313.5 | STRING | Online or offline if one of the four crucial components failed |
| **Locally/cloud connected** | 1.3.6.1.4.1.53313.6 | STRING | Activation mode of this appliance: Cloud Connected / Locally Connected |
| **License status** | 1.3.6.1.4.1.53313.7 | STRING | Activation period of this appliance: Active / Expiration Date / Expired |

Note

- Nonexisting keys respond with null, HTTP 200.
- You should test Hardware-related MIBs (CPU usage, CPU temperature, memory usage, disk usage) on all architectures and physical sensors. CPU temperature on virtual machines is expected to be non applicable.