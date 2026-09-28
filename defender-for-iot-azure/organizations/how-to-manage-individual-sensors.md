---
layout: Conceptual
title: Maintain Defender for IoT OT network sensors from the GUI - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-manage-individual-sensors
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
description: Learn how to perform maintenance activities on individual OT network sensors using the OT sensor console.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 680e7e4a-1914-6012-b38e-7e23472a3f63
document_version_independent_id: 8ebc2495-ea12-b883-dcdc-8e97302e6103
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-manage-individual-sensors.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-manage-individual-sensors
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-manage-individual-sensors.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 8057eb7b-2d93-ee08-2018-68e1a13fc6c8
---

# Maintain Defender for IoT OT network sensors from the GUI - Microsoft Defender for IoT | Microsoft Learn

This article describes extra Operational Technology (OT) sensor maintenance activities that you might perform outside of a larger deployment process.

OT sensors can also be maintained from the [OT sensor CLI](cli-ot-sensor) or the [Azure portal](how-to-manage-sensors-on-the-cloud). Before you begin, make sure you meet the prerequisites.

Caution

Only documented configuration parameters on the OT network sensor are supported for customer configuration. Do not change any undocumented configuration parameters or system properties, as changes may cause unexpected behavior and system failures.

Removing packages from your sensor without Microsoft approval can cause unexpected results. All packages installed on the sensor are required for correct sensor functionality.

## Prerequisites

Before performing the procedures in this article, make sure that you have:

- An OT network sensor with [OT sensor software installed](ot-deploy/install-software-ot-sensor), [configured, and activated](ot-deploy/activate-deploy-sensor) and [onboarded to Defender for IoT](onboard-sensors) in the Azure portal.
- Access to the OT sensor as an **Admin** user. Selected procedures and CLI access also requires a privileged user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).
- To download software for OT sensors, you need access to the Azure portal as a [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) user.
- An [SSL/TLS certificate prepared](ot-deploy/create-ssl-certificates) if you need to update your sensor's certificate.

## View overall OT sensor status

When you sign into your OT sensor, the first page shown is the **Overview** page.

For example:

[![Screenshot of the overview page.](media/how-to-manage-individual-sensors/screenshot-of-overview-page.png)](media/how-to-manage-individual-sensors/screenshot-of-overview-page.png#lightbox)

The **Overview** page shows the following widgets:

| Name | Description |
| --- | --- |
| **General Settings** | Displays a list of the sensor's basic configuration settings and connectivity status. |
| **Traffic Monitoring** | Displays a graph detailing traffic in the sensor. The graph shows traffic as units of Mbps per hour on the day of viewing. |
| **Top 5 OT Protocols** | Displays a bar graph that details the top five most used OT protocols. The bar graph also provides the number of devices that are using each of those protocols. |
| **Traffic By Port** | Displays a pie chart showing the types of ports in your network, with the amount of traffic detected in each type of port. |
| **Top open alerts** | Displays a table listing any currently open alerts with high severity levels, including critical details about each alert. |

Select the link in each widget to drill down for more information in your sensor.

### Validate connectivity status

Verify that your OT sensor is successfully connected to the Azure portal directly from the OT sensor's **Overview** page.

If there are any connection issues, a disconnection message is shown in the **General Settings** area on the **Overview** page, and a **Service connection error** warning appears at the top of the page in the ![](media/how-to-manage-individual-sensors/bell-icon.png)**System Messages** area. For example:

[![Screenshot of a sensor page showing the connectivity status as disconnected.](media/how-to-manage-individual-sensors/connectivity-status.png)](media/how-to-manage-individual-sensors/connectivity-status.png#lightbox)

Find more information about the issue by hovering over the ![](media/how-to-manage-individual-sensors/information-icon.png) information icon. For example:

[![Screenshot of a connectivity error message.](media/how-to-manage-individual-sensors/connectivity-message.png)](media/how-to-manage-individual-sensors/connectivity-message.png#lightbox)

Take action by selecting the **Learn more** option under ![](media/how-to-manage-individual-sensors/bell-icon.png)**System Messages**. For example:

[![Screenshot of the system messages pane.](media/how-to-manage-individual-sensors/system-messages.png)](media/how-to-manage-individual-sensors/system-messages.png#lightbox)

## Download software for OT sensors

You might need to download software for your OT sensor if you're [installing Defender for IoT software](ot-deploy/install-software-ot-sensor) on your own appliances, or [updating software versions](update-ot-software).

In [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) in the Azure portal, use one of the following options:

- For a new installation, select **Getting started** &gt; **Sensor**. Select a version in the **Purchase an appliance and install software** area, and then select **Download**.
- If you're updating your OT sensor, use the options in the **Sites and sensors** page &gt; **Sensor update (Preview)** menu.

All files downloaded from the Azure portal are signed by root of trust so that your machines use signed assets only.

For more information, see [Update Defender for IoT OT monitoring software](update-ot-software).

## Upload a new activation file

Each OT sensor is onboarded as a cloud-connected or locally managed OT sensor and activated using a unique activation file. For cloud-connected sensors, the activation file is used to ensure the connection between the sensor and Azure.

You need to upload a new activation file to your sensor if you want to switch sensor management modes, such as moving from a locally managed sensor to a cloud-connected sensor, or if you're [updating from a recent software version](update-ot-software?tabs=portal#update-ot-sensors-with-the-latest-ot-monitoring-software). Uploading a new activation file to your sensor includes deleting your sensor from the Azure portal and onboarding it again.

**To add a new activation file:**

1. Do one of the following:

    - **Onboard your sensor from scratch**:

        1. In [Defender for IoT on the Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/Getting_Started) &gt; **Sites and sensors**, locate and [delete your OT sensor](how-to-manage-sensors-on-the-cloud#sensor-maintenance-and-troubleshooting).
        2. Select **Onboard OT sensor &gt; OT** to onboard the sensor again from scratch and download the new activation file. For more information, see [Onboard OT sensors](onboard-sensors).
    - **Download the current sensor's activation file**: On the **Sites and sensors** page, locate the sensor you just added. Select the three dots (...) on the sensor's row and select **Download activation file**. Save the file in a location accessible to your sensor.

    All files downloaded from the Azure portal are signed by root of trust so that your machines use signed assets only.
2. Sign in to the Defender for IoT sensor console and select **System Settings** &gt; **Sensor management** &gt; **Subscription & Activation Mode**.
3. Select **Upload** and browse to the file that you downloaded from the Azure portal.
4. Select **Activate** to upload your new activation file.

### Troubleshoot activation file upload

You'll receive an error message if the activation file couldn't be uploaded. The following events might have occurred:

- **The sensor can't connect to the internet:** Check the sensor's network configuration. If your sensor needs to connect through a web proxy to access the internet, verify that your proxy server is configured correctly on the **Sensor Network Configuration** screen. Verify that the required endpoints are allowed in the firewall and/or proxy.

    For OT sensors version 22.x, download the list of required endpoints from the **Sites and sensors** page on the Azure portal. Select an OT sensor with a supported software version, or a site with one or more supported sensors. And then select **More actions** &gt; **Download endpoint details**. For sensors with earlier versions, see [Sensor access to Azure portal](networking-requirements#sensor-access-to-azure-portal).
- **The activation file is valid but Defender for IoT rejected it:** If you can't resolve this problem, you can download another activation from the **Sites and sensors** page in the [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/Getting_Started). If downloading another activation file doesn't work, contact Microsoft Support.

Note

Activation files expire 14 days after creation. If you onboarded your sensor but didn't upload the activation file before it expired, download a new activation file.

## Manage SSL/TLS certificates

If you're working with a production environment, you'd deployed a CA-signed SSL/TLS certificate as part of your [OT sensor deployment](ot-deploy/activate-deploy-sensor#define-ssltls-certificate-settings). We recommend using self-signed certificates only for testing purposes.

The following procedures describe how to deploy updated SSL/TLS certificates, such as if the certificate has expired.

# [Deploy a CA-signed certificate](#tab/ca-signed)
**To deploy a CA-signed SSL/TLS certificate:**

1. Sign into your OT sensor and select **System Settings** &gt; **Basic** &gt; **SSL/TLS Certificate**.
2. In the **SSL/TLS Certificates** pane, select the **Import trusted CA certificate (recommended)** option. For example:

    [![Screenshot of importing a trusted CA certificate.](media/how-to-deploy-certificates/recommended-ssl.png)](media/how-to-deploy-certificates/recommended-ssl.png#lightbox)
3. Enter the following parameters:

    | Parameter | Description |
    | --- | --- |
    | **Certificate Name** | Enter your certificate name. |
    | **Passphrase** - *Optional* | Enter a [passphrase](best-practices/certificate-requirements#supported-characters-for-keys-and-passphrases). |
    | **Private Key (KEY file)** | Upload a Private Key (KEY file). |
    | **Certificate (CRT file)** | Upload a Certificate (CRT file). |
    | **Certificate Chain (PEM file)** - *Optional* | Upload a Certificate Chain (PEM file). |

    Select **Use CRL (Certificate Revocation List) to check certificate status** to validate the certificate against a [CRL server](ot-deploy/create-ssl-certificates#verify-crl-server-access). The certificate is checked once during the import process.

    If an upload fails, contact your security or IT administrator. For more information, see [SSL/TLS certificate requirements for on-premises resources](best-practices/certificate-requirements) and [Create SSL/TLS certificates for OT appliances](ot-deploy/create-ssl-certificates).
4. In the **Validation of OT sensor certificate** area, select **Mandatory** if SSL/TLS certificate validation is required. Otherwise, select **None**.

    If you've selected **Mandatory** and validation fails, communication between relevant components is halted, and a validation error is shown on the sensor. For more information, see [CRT file requirements](best-practices/certificate-requirements#crt-file-requirements).
5. Select **Save** to save your certificate settings.

# [Create and deploy a self-signed certificate](#tab/self-signed)
Each OT sensor is installed with a self-signed certificate that we recommend you use only for testing purposes. In production environments, we recommend that you always use a CA-signed certificate.

Self-signed certificates lead to a less secure environment, as the owner of the certificate can't be validated and the security of your system can't be maintained.

To create a self-signed certificate, download the certificate file from your OT sensor and then use a certificate management platform to create the certificate files you'll need to upload back to the OT sensor.

**To create a self-signed certificate**:

Go to the OT sensor's IP address in a browser, and then:

1. Select the ![](media/how-to-deploy-certificates/warning-icon.png)**Not secure** alert in the address bar of your web browser, then select the **&gt;** icon next to the warning message **"Your connection to this site isn't secure"**. For example:

    [![Screenshot of web page with a Not secure warning in the address bar.](media/how-to-deploy-certificates/connection-is-not-secure.png)](media/how-to-deploy-certificates/connection-is-not-secure.png#lightbox)
2. Select the ![](media/how-to-deploy-certificates/show-certificate-icon.png)**Show certificate** icon to view the security certificate for this website.
3. In the **Certificate viewer** pane, select the **Details** tab, then select **Export** to enter a name for your exported file and save it on your local machine.
4. Use a certificate management platform to create the following types of SSL/TLS certificate files:

    | File type | Description |
    | --- | --- |
    | **.crt – certificate container file** | A `.pem`, or `.der` file, with a different extension for support in Windows Explorer. |
    | **.key – Private key file** | A key file is in the same format as a `.pem` file, with a different extension for support in Windows Explorer. |
    | **.pem – certificate container file (optional)** | Optional. A text file with a Base64-encoding of the certificate text, and a plain-text header and footer to mark the beginning and end of the certificate. |

    For example:

    1. Open the downloaded certificate file and select the **Details** tab &gt; **Copy to file** to run the **Certificate Export Wizard**.
    2. In the **Certificate Export Wizard**, select **Next** &gt; **DER encoded binary X.509 (.CER)** &gt; and then select **Next** again.
    3. In the **File to Export** screen, select **Browse**, choose a location to store the certificate, and then select **Next**.
    4. Select **Finish** to export the certificate.

Note

You may need to convert existing files types to supported types.

When you're done, use the following procedures to validate your certificate files:

- [Verify CRL server access](ot-deploy/create-ssl-certificates#verify-crl-server-access)
- [Import the SSL/TLS certificate to a trusted store](ot-deploy/create-ssl-certificates#import-the-ssltls-certificate-to-a-trusted-store)
- [Test your SSL/TLS certificates](ot-deploy/create-ssl-certificates#test-your-ssltls-certificates)

**To deploy a self-signed certificate**:

1. Sign into your OT sensor and select **System Settings** &gt; **Basic** &gt; **SSL/TLS Certificate**.
2. In the **SSL/TLS Certificates** pane, keep the default **Use Locally generated self-signed certificate (Not recommended)** option selected.
3. Select the **Confirm** option to confirm the warning.
4. In the **Validation of OT sensor certificate** area, select **Mandatory** if SSL/TLS certificate validation is required. Otherwise, select **None**.

    If the **Mandatory** validation option is toggled on and validation fails, communication between relevant components is halted, and a validation error is shown on the sensor. For more information, see [CRT file requirements](best-practices/certificate-requirements#crt-file-requirements).
5. Select **Save** to save your certificate settings.

---

### Troubleshoot certificate upload errors

You won't be able to upload certificates to your OT sensors if the certificates aren't created properly or are invalid. Use the following table to understand how to take action if your certificate upload fails and an error message is shown:

| **Certificate validation error** | **Recommendation** |
| --- | --- |
| **Passphrase does not match to the key** | Make sure you have the correct passphrase. If the problem continues, try recreating the certificate using the correct passphrase. For more information, see [Supported characters for keys and passphrases](best-practices/certificate-requirements#supported-characters-for-keys-and-passphrases). |
| **Cannot validate chain of trust. The provided Certificate and Root CA don't match.** | Make sure a `.pem` file correlates to the `.crt` file.  If the problem continues, try recreating the certificate using the correct chain of trust, as defined by the `.pem` file. |
| **This SSL certificate has expired and isn't considered valid.** | Create a new certificate with valid dates. |
| **This certificate has been revoked by the CRL and can't be trusted for a secure connection** | Create a new unrevoked certificate. |
| **The CRL (Certificate Revocation List) location is not reachable. Verify the URL can be accessed from this appliance** | Make sure that your network configuration allows the sensor to reach the CRL server defined in the certificate.  For more information, see [Verify CRL server access](ot-deploy/create-ssl-certificates#verify-crl-server-access). |
| **Certificate validation failed** | This indicates a general error in the appliance.  Contact [Microsoft Support](https://support.microsoft.com/supportforbusiness/productselection?sapId=82c8f35-1b8e-f274-ec11-c6efdd6dd099). |

## Update the OT sensor network configuration

After configuring your OT sensor network during [OT sensor installation](ot-deploy/install-software-ot-sensor), you might need to make changes as part of OT sensor maintenance, such as modifying network values or setting up a proxy configuration.

**To update the OT sensor configuration:**

1. Sign into the OT sensor and select **System Settings** &gt; **Basic** &gt; **Sensor network settings**.
2. In the **Sensor network settings** pane, update the following details for your OT sensor as needed:

    - **IP address**. Changing the IP address might require users to sign into your OT sensor again.
    - **Subnet mask**
    - **Default gateway**
    - **DNS**. Make sure to use the same hostname that's configured in your organization's DNS server.
    - **Hostname** (optional)
3. Toggle the **Enable Proxy** option on or off if needed. If you're using a proxy, enter following values:

    - **Proxy host**
    - **Proxy port**
    - **Proxy username** (optional)
    - **Proxy password** (optional)
4. Select **Save** to save your changes.

## Turn off learning mode manually

An OT network sensor starts monitoring your network automatically as soon as it connects to your network and you [sign in to the sensor console](ot-deploy/activate-deploy-sensor#sign-in-to-the-sensor-console-and-change-the-default-password). Network devices start appearing in your [device inventory](device-inventory), and [alerts](alerts) are triggered for any security or operational incidents that occur in your network.

There are three stages to the monitoring process. For more information, see [overview of the multi stage monitoring process](ot-deploy/create-learned-baseline).

Two to six weeks after deploying your sensor the detection levels should accurately reflect your network activity. At this stage we recommend turning off learning mode.

**To turn off learning mode**:

1. Sign into your OT network sensor and select **System settings &gt; Network monitoring &gt; Detection engines and network modeling**.
2. In **Network modeling**, toggle off **Learning**.
3. Select **OK** in the confirmation message, and then select **Close** to save your changes.

Once learning mode is turned off, the sensor starts to generate **Policy Violation** alerts and this setting is now available by selecting **Support** in the side menu. We recommend leaving the mode settings for each alert to automatically update from dynamic to operational. For testing or other reasons, you could manually change the mode setting, however, this isn't recommended as it can produce a large number of alerts.

**Manually change a Policy Violations setting**:

1. In the main sensor menu, select **Support**. The **Engines** table shows the list of all the Defender for IoT alerts.
2. In the **Learning Mode** column, change the mode for any **Policy Violation** alert by selecting **Learning**, **Dynamic** or **Operational** from the dropdown box.

    When selecting **Learning**, you must enter the length of time, in hours, to maintain this setting. Select **Submit**.

## Update a sensor's monitoring interfaces (configure ERSPAN)

You might want to change the interfaces used by your sensor to monitor traffic. You originally configured these details as part of your [initial sensor setup](ot-deploy/activate-deploy-sensor#define-the-interfaces-you-want-to-monitor), but might need to modify the settings as part of system maintenance, such as configuring ERSPAN monitoring.

For more information, see [ERSPAN ports](best-practices/traffic-mirroring-methods#erspan-ports).

Note

Updating your sensor's monitoring interfaces restarts the sensor software to implement any changes made.

Defender for IoT ERSPAN monitoring is tested, certified, and supported **only when the ERSPAN tunnel originates from Cisco equipment.**

ERSPAN tunnels from non-Cisco vendors are **not supported** and might fail due to differences in ERSPAN implementations.

**To update your sensor's monitoring interfaces**:

1. Sign into your OT sensor and select **System settings** &gt; **Basic** &gt; **Interface connections**.
2. In the grid, locate the interface you want to configure. Do any of the following:

    - Select the **Enable/Disable** toggle for any interfaces you want the sensor to monitor. You must have at least one interface enabled for each sensor.

        If you're not sure about which interface to use, select the ![](media/install-software-ot-sensor/blink-interface.png)**Blink physical interface LED** button to have the selected port blink on your machine.

        Tip

        We recommend that you optimize performance on your sensor by configuring your settings to monitor only the interfaces that are actively in use.
    - For each interface you select to monitor, select the ![](media/install-software-ot-sensor/advanced-settings-icon.png)**Advanced settings** button to modify any of the following settings:

        | Name | Description |
        | --- | --- |
        | **Mode** | Select one of the following: - **SPAN Traffic (no encapsulation)** to use the default SPAN port mirroring. - **Tunneling** if you're using ERSPAN mirroring. For more information, see [Choose a traffic mirroring method for OT sensors](best-practices/traffic-mirroring-methods). |
        | **Description** | Enter an optional description for the interface. You'll see the description later on in the sensor's **System settings &gt; Interface configurations** page, and descriptions might be helpful in understanding the purpose of each interface. |
        | **Interface IP** | The ERSPAN IP on the sensor side.  - The management interface IP and the ERSPAN interface IP must be configured on separate network subnets.  - Configuring both the management and ERSPAN IP addresses on the same subnet might lead to asymmetric routing issues. |
        | **Subnet** | The subnet mask of the ERSPAN interface IP. |
        | **Name** | Enter a unique name for the virtual ERSPAN interface. |
        | **ID** - ERSPAN tunnel ID | The ID value must be identical to the `erspan-id` value on the Cisco side.  In case of an ID mismatch, the sensor will discard all incoming tunnel traffic. |
        | **Source IP** | The IP address of the ERSPAN interface on the Cisco side that sends the tunnel traffic. |
        | **Add tunneling** | The sensor supports adding multiple tunnels. Each tunnel must have a unique name and ID. |
        | **Auto negotiation** | Relevant for physical machines only. Use this option to determine which sort of communication methods are used, or if the communication methods are automatically defined between components. **Important**: We recommend that you change this setting only on the advice of your networking team. |

    For example:

    [![Screenshot of how to configure Tunneling for ERSPAN on the Interface configurations page.](media/how-to-manage-individual-sensors/tunneling-advanced-settings.png)](media/how-to-manage-individual-sensors/tunneling-advanced-settings.png#lightbox)
3. Select **Save** to save your changes. Your sensor software restarts to implement your changes.

## Synchronize time zones on an OT sensor

You might want to configure your OT sensor with a specific time zone so that all users see the same times regardless of the user's location.

Time zones are used in [alerts](how-to-view-alerts), [trends and statistics widgets](how-to-create-trends-and-statistics-reports), [data mining reports](how-to-create-data-mining-queries), [risk assessment reports](how-to-create-risk-assessment-reports), and [attack vector reports](how-to-create-attack-vector-reports).

**To configure an OT sensor's time zone**:

1. Sign into your OT sensor and select **System settings** &gt; **Basic** &gt; **Time & Region**.
2. In the **Time & Region** pane, enter the following details:

    - **Time Zone**: Select the time zone you want to use
    - **Date Format**: Select the time and date format you want to use. Supported formats include:

        - `dd/MM/yyyy HH:mm:ss`
        - `MM/dd/yyyy HH:mm:ss`
        - `yyyy/MM/dd HH:mm:ss`

    The **Date & Time** field is automatically updated with the current time in the format you'd selected.
3. Select **Save** to save your changes.

## Configure SMTP mail server settings

Define SMTP mail server settings on your OT sensor so that you configure the OT sensor to send data to other servers and partner services.

You need an SMTP mail server configured to enable email alerts about disconnected sensors, failed sensor backup retrievals, and SPAN monitoring port failures from the OT sensor, and to set up mail forwarding and configure [forwarding alert rules](how-to-forward-alert-information-to-partners).

**Prerequisites**:

Make sure you can reach the SMTP server from the [sensor's management port](best-practices/understand-network-architecture).

**To configure an SMTP server on your OT sensor**:

1. Sign in to the OT sensor and select **System settings** &gt; **Integrations** &gt; **Mail server**.
2. In the **Edit Mail Server Configuration** pane that appears, define the values for your SMTP server as follows:

    | Parameter | Description |
    | --- | --- |
    | **SMTP Server Address** | Enter the IP address or domain address of your SMTP server. |
    | **SMTP Server Port** | Default = 25. Adjust the value as needed. |
    | **Outgoing Mail Account** | Enter an email address to use as the outgoing mail account from your sensor. |
    | **SSL** | Toggle on for secure connections from your sensor. |
    | **Authentication** | Toggle on and then enter a username and password for your email account. |
    | **Use NTLM** | Toggle on to enable [NTLM](/en-us/windows-server/security/kerberos/ntlm-overview). This option only appears when you have the **Authentication** option toggled on. |
3. Select **Save** when you're done.

## Upload and play PCAP files

When troubleshooting your OT sensor, you might want to examine data recorded by a specific PCAP file. To do so, you can upload a PCAP file to your OT sensor and replay the data recorded.

The **Play PCAP** option is enabled by default in the sensor console's settings.

Maximum size for uploaded files is 2 GB.

**To show the PCAP player in your sensor console**:

1. On your sensor console, go to **System settings &gt; Sensor management &gt; Advanced Configurations**.
2. In the **Advanced configurations** pane, select the **Pcaps** category.
3. In the configurations displayed, change `enabled=0` to `enabled=1`, and select **Save**.

The **Play PCAP** option is now available in the sensor console's settings, under: **System settings &gt; Basic &gt; Play PCAP**.

**To upload and play a PCAP file**:

1. On your sensor console, select **System settings &gt; Basic &gt; Play PCAP**.
2. In the **PCAP PLAYER** pane, select **Upload** and then navigate to and select the file or multiple files you want to upload.

    [![Screenshot of uploading PCAP files on the PCAP PLAYER pane in the sensor console.](media/how-to-manage-individual-sensors/upload-and-play-pcaps.png)](media/how-to-manage-individual-sensors/upload-and-play-pcaps.png#lightbox)
3. Select **Play** to play your PCAP file, or **Play All** to play all PCAP files currently loaded.

Tip

Select **Clear All** to clear the sensor of all PCAP files loaded.

## Turn off specific analytics engines

By default, each OT network sensor analyzes ingested data using [built-in analytics engines](architecture#defender-for-iot-analytics-engines), and triggers alerts based on both real-time and prerecorded traffic.

We recommend that you keep all analytics engines on. However, you might want to turn off specific analytics engines on your OT sensors to limit the type of anomalies and risks that the OT sensor monitors.

Important

When you disable a policy engine, information that the engine generates won't be available to the sensor. For example, if you disable the Anomaly engine, you won't receive alerts on network anomalies. If you'd created a [forwarding alert rule](how-to-forward-alert-information-to-partners), anomalies that the engine learns won't be sent.

**To manage an OT sensor's analytics engines**:

1. Sign into your OT sensor and select **System settings &gt; Network monitoring &gt; Customization &gt; Detection engines and network modeling**.
2. In the **Detection engines and network modeling** pane, in the **Engines** area, toggle off one or more of the following engines:

    - **Protocol Violation**
    - **Policy Violation**
    - **Malware**
    - **Anomaly**
    - **Operational**

    Toggle the engine back on to start tracking related anomalies and activities again.

    For more information, see [Defender for IoT analytics engines](architecture#defender-for-iot-analytics-engines).
3. Select **Close** to save your changes.

**To manage analytics engines from an OT sensor**:

1. Sign into your OT sensor and select **System Settings**.
2. In the **Sensor Engine Configuration** section, select one or more OT sensors where you want to apply settings, and clear any of the following options:

    - **Protocol Violation**
    - **Policy Violation**
    - **Malware**
    - **Anomaly**
    - **Operational**
3. Select **SAVE CHANGES** to save your changes.

## Clear OT sensor data

If you need to relocate or erase your OT sensor, reset it to clear all detected or learned data on the OT sensor.

Warning

Clearing sensor data permanently removes all learned data, allowlists, policies, and configuration settings from the sensor. This action cannot be undone.

After clearing data on a cloud-connected sensor:

- The device inventory on the Azure portal is updated in parallel.
- Some actions on corresponding alerts in the Azure portal are no longer supported, such as downloading PCAP files or learning alerts.

Note

Network settings such as IP/DNS/GATEWAY won't be changed by clearing system data.

**To clear system data**:

1. Sign into the OT sensor as the *admin* user. For more information, see [Default privileged on-premises users](roles-on-premises#default-privileged-on-premises-users).
2. Select **Support** &gt; **Clear data**.
3. In the confirmation dialog box, select **Yes** to confirm that you do want to clear all data from the sensor and reset it. For example:

    [![Screenshot of clearing system data on the support page in the sensor console.](media/how-to-manage-individual-sensors/clear-system-data.png)](media/how-to-manage-individual-sensors/clear-system-data.png#lightbox)

A confirmation message appears that the action was successful. All learned data, allowlists, policies, and configuration settings are cleared from the sensor.

## Manage sensor plugins and monitor plugin performance

Horizon Plugins are protocol analysis plugins that use Deep Packet Inspection (DPI) to inspect monitored traffic and expose protocol-specific performance and error data. View data for each protocol monitored by your sensor using the **Protocols DPI (Horizon Plugins)** page in the sensor console.

1. Sign into your OT sensor console and select **System settings &gt; Network monitoring &gt; Protocols DPI (Horizon Plugins)**.
2. Do one of the following:

    - To limit the protocols monitored by your sensor, select the **Enable/Disable** toggle for each plugin as needed.
    - To monitor plugin performance, view the data shown on the **Protocols DPI (Horizon Plugins)** page for each plugin. To help locate a specific plugin, use the **Search** box to enter part or all of a plugin name.

The **Protocols DPI (Horizon Plugins)** lists the following data per plugin:

| Column name | Description |
| --- | --- |
| **Plugin** | Defines the plugin name. |
| **Type** | The plugin type, including APPLICATION or INFRASTRUCTURE. |
| **Time** | The time that data was last analyzed using the plugin. The time stamp is updated every five seconds. |
| **PPS** | The number of packets analyzed per second by the plugin. |
| **Bandwidth** | The average bandwidth detected by the plugin within the last five seconds. |
| **Malforms** | The number of malform errors detected in the last five seconds. Malformed validations are used after the protocol has been positively validated. If there's a failure to process the packets based on the protocol, a failure response is returned. |
| **Warnings** | The number of warnings detected, such as when packets match the structure and specifications, but unexpected behavior is detected, based on the plugin warning configuration. |
| **Errors** | The number of errors detected in the last five seconds for packets that failed basic protocol validations for the packets that match protocol definitions. |

Log data is available for export in the **Dissection statistics** and **Dissection Logs**, log files. For more information, see [Export troubleshooting logs](how-to-troubleshoot-sensor).