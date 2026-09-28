---
layout: Conceptual
title: Deploy Defender for IoT for OT monitoring - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/ot-deploy/ot-deploy-path
breadcrumb_path: ../../breadcrumb/toc.json
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
description: Learn about the steps involved in deploying a Microsoft Defender for IoT system for OT monitoring.
ms.topic: install-set-up-deploy
ms.date: 2023-07-04T00:00:00.0000000Z
locale: en-us
document_id: 4e12f554-e8b1-e3ee-ae27-8ef96b15b5ce
document_version_independent_id: 857582d9-5385-8003-d72a-23a6a445cff5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/ot-deploy/ot-deploy-path.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/ot-deploy/ot-deploy-path
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/ot-deploy/ot-deploy-path.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: e89ad35f-3865-1d09-df79-a37ebb1e992a
---

# Deploy Defender for IoT for OT monitoring - Microsoft Defender for IoT | Microsoft Learn

This article describes the high-level steps required to deploy Defender for IoT for OT monitoring. Learn more about each deployment step in the sections below, including relevant cross-references for more details.

The following image shows the phases in an end-to-end OT monitoring deployment path, together with the team responsible for each phase.

While teams and job titles differ across different organizations, all Defender for IoT deployments require communication between the people responsible for the different areas of your network and infrastructure.

[![Diagram of an OT monitoring deployment path.](../media/deployment-paths/ot-deploy.png)](../media/deployment-paths/ot-deploy.png#lightbox)

Tip

Each step in the process can take a different amount of time. For example, downloading an OT sensor activation file may take five minutes, while configuring traffic monitoring may take days or even weeks, depending on your organization's processes.

We recommend that you start the process for each step without waiting for it to be completed before moving on to the next step. Make sure to continue following up on any steps still in process to ensure their completion.

## Prerequisites

Before you start planning your OT monitoring deployment, make sure that you have an Azure subscription and an OT plan onboarded to Defender for IoT.

For more information, see [Manage Defender for IoT plans for OT monitoring](../how-to-manage-subscriptions).

## Planning and preparing

The following image shows the steps included in the planning and preparing phase. Planning and preparing steps are handled by your architecture teams.

![Diagram of the steps included in the planning and preparing stage.](../media/deployment-paths/plan-prepare.png)

### Plan your OT monitoring system

Plan basic details about your monitoring system, such as:

- **Sites and zones**: Decide how you'll segment the network you want to monitor using *sites* and *zones* that can represent locations all around the world.
- **Sensor management**: Decide on whether you'll be using cloud-connected or air-gapped, locally managed OT sensors, or a hybrid system of both. If you're using cloud-connected sensors, select a connection method, such as connecting directly or via a proxy.
- **Users and roles**: List of the types of users you'll need on each sensor, and the roles that they'll need for each activity.

For more information, see [Plan your OT monitoring system with Defender for IoT](../best-practices/plan-corporate-monitoring).

### Prepare for an OT site deployment

Define additional details for each site planned in your system, including:

- **A network diagram**. Identify all of the devices you want to monitor and create a well-defined list of subnets. After you've deployed your sensors, use this list to verify that all the subnets you want to monitor are covered by Defender for IoT.
- **A list of sensors**: Use the list of traffic, subnets, and devices you want to monitor to create a list of the OT sensors you'll need and where they'll be placed in your network.
- **Traffic mirroring methods**: Choose a traffic mirroring method for each OT sensor, such as a SPAN port or TAP.
- **Appliances**: Prepare a deployment workstation and any hardware or VM appliances you'll be using for each of the OT sensors you've planned. If you're using pre-configured appliances, make sure to order them.

For more information, see [Prepare an OT site deployment](../best-practices/plan-prepare-deploy).

## Onboard sensors to Azure

The following image shows the step included in the onboard sensors phase. Sensors are onboarded to Azure by your deployment teams.

![Diagram of the onboard sensors phase.](../media/deployment-paths/onboard-sensors.png)

### Onboard OT sensors on the Azure portal

Onboard as many OT sensors to Defender for IoT as you've planned. Make sure to download the activation files provided for each OT sensor and save them in a location that will be accessible from your sensor machines.

For more information, see [Onboard OT sensors to Defender for IoT](../onboard-sensors).

## Site networking setup

The following image shows the steps included in the site networking setup phrase. Site networking steps are handled by your connectivity teams.

![Diagram of the site networking setup phase.](../media/deployment-paths/site-networking-setup.png)

### Configure traffic mirroring in your network

Use the plans you'd created earlier to configure traffic mirroring at the places in your network where you'll be deploying OT sensors and mirroring traffic to Defender for IoT.

A brief summary of the information needed to choose the best location for your OT sensor and deploy it on your network is available in [traffic mirroring set up overview](../traffic-mirroring/set-up-traffic-mirroring).

For more information, see:

- [Configure mirroring with a switch SPAN port](../traffic-mirroring/configure-mirror-span)
- [Configure traffic mirroring with a Remote SPAN (RSPAN) port](../traffic-mirroring/configure-mirror-rspan)
- [Configure active or passive aggregation (TAP)](../best-practices/traffic-mirroring-methods#active-or-passive-aggregation-tap)
- [Update a sensor's monitoring interfaces (configure ERSPAN)](../how-to-manage-individual-sensors#update-a-sensors-monitoring-interfaces-configure-erspan)
- [Configure traffic mirroring with a ESXi vSwitch](../traffic-mirroring/configure-mirror-esxi)
- [Configure traffic mirroring with a Hyper-V vSwitch](../traffic-mirroring/configure-mirror-hyper-v)

### Provision for cloud management

Configure any firewall rules to ensure that your OT sensor appliances will be able to access Defender for IoT on the Azure cloud. If you're planning to connect via a proxy, you'll configure those settings only after installing your sensor.

Skip this step for any OT sensor that is planned to be air-gapped and managed locally directly on the sensor console.

For more information, see [Provision OT sensors for cloud management](provision-cloud-management).

## Deploy your OT sensors

The following image shows the steps included in the sensor deployment phase. OT sensors are deployed and activated by your deployment team.

![Diagram of the OT sensor deployment phase.](../media/deployment-paths/deploy-sensors.png)

### Install your OT sensors

If you're installing Defender for IoT software on your own appliances, download installation software from the Azure portal and install it on your OT sensor appliance.

After installing your OT sensor software, run several checks to validate the installation and configuration.

For more information, see:

- [Install OT monitoring software on OT sensors](install-software-ot-sensor)
- [Validate an OT sensor software installation](post-install-validation-ot-software)

Skip these steps if you're purchasing [pre-configured appliances](../ot-pre-configured-appliances).

### Activate your OT sensors and initial setup

Use an initial setup wizard to confirm network settings, activate the sensor, and apply SSH/TLS certificates.

For more information, see [Configure and activate your OT sensor](activate-deploy-sensor).

### Configure proxy connections

If you've decided to use a proxy to connect your sensors to the cloud, set up your proxy and configure settings on your sensor. For more information, see [Configure proxy settings on an OT sensor](../connect-sensors).

Skip this step in the following situations:

- For any OT sensor where you're connecting directly to Azure, without a proxy
- For any sensor that is planned to be air-gapped and managed locally directly on the sensor console.

### Configure optional settings

We recommend that you configure an Active Directory connection for managing on-premises users on your OT sensor, and also setting up sensor health monitoring via SNMP.

If you don't configure these settings during deployment, you can also return and configure them later on.

For more information, see:

- [Set up SNMP MIB monitoring on an OT sensor](../how-to-set-up-snmp-mib-monitoring)
- [Configure an Active Directory connection](../manage-users-sensor#configure-an-active-directory-connection)

## Calibrate and fine-tune OT monitoring

The following image shows the steps involved in calibrating and fine-tuning OT monitoring with your newly deployed sensor. Calibration and fine-tuning activities are done by your deployment team.

![Diagram of the calibrate and fine-tuning phase.](../media/deployment-paths/calibrate-fine-tune.png)

### Control OT monitoring on your sensor

By default, your OT sensor may not detect the exact networks that you want to monitor, or identify them in precisely the way you'd like to see them displayed. Use the lists you'd created earlier to verify and manually configure the subnets, customize port and VLAN names, and configure DHCP address ranges as needed.

For more information, see [Control the OT traffic monitored by Microsoft Defender for IoT](../how-to-control-what-traffic-is-monitored).

### Verify and update your detected device inventory

After your devices are fully detected, review the device inventory and modify the device details as needed. For example, you might identify device types or other properties to modify, and more.

For more information, see [Verify and update your detected device inventory](update-device-inventory).

### Learn OT alerts to create a network baseline

The alerts triggered by your OT sensor may include several alerts that you'll want to regularly ignore, or *Learn*, as authorized traffic.

Review all the alerts in your system as an initial triage. This step creates a network traffic baseline for Defender for IoT to work with moving forward.

For more information, see [Create a learned baseline of OT alerts](create-learned-baseline).

## Baseline learning ends

Your OT sensors will remain in *Learning mode* for as long as new traffic is detected and you have unhandled alerts.

![Diagram of the deployment phase where baseline learning ends.](../media/deployment-paths/baseline-learning-ends.png)

When baseline learning ends, the OT monitoring deployment process is complete, and you'll continue on in operational mode for ongoing monitoring. In operational mode, any activity that differs from your baseline data will trigger an alert.

Tip

[Turn off learning mode manually](../how-to-manage-individual-sensors#turn-off-learning-mode-manually) when the current alerts in Defender for IoT reflect your network traffic accurately.

## Connect Defender for IoT data to your SIEM

Once Defender for IoT has been deployed, send security alerts and manage OT/IoT incidents by integrating Defender for IoT with your security information and event management (SIEM) platform and existing SOC workflows and tools. Integrate Defender for IoT alerts with your organizational SIEM by [integrating with Microsoft Sentinel](../iot-advanced-threat-monitoring) and leveraging the out-of-the-box Microsoft Defender for IoT solution, or by [creating forwarding rules](../how-to-forward-alert-information-to-partners) to other SIEM systems. Defender for IoT integrates out-of-the-box with Microsoft Sentinel, as well as [a broad range of SIEM systems](../integrate-overview), such as Splunk, IBM QRadar, LogRhythm, Fortinet, and more.

A brief summary of the information needed to choose the best location for your OT sensor and deploy it on your network is available in [traffic mirroring set up overview](../traffic-mirroring/set-up-traffic-mirroring).

For more information, see:

- [OT threat monitoring in enterprise SOCs](../concept-sentinel-integration)
- [Tutorial: Connect Microsoft Defender for IoT with Microsoft Sentinel](../iot-solution)
- [Connect on-premises OT network sensors to Microsoft Sentinel](../integrations/on-premises-sentinel)
- [Integrations with Microsoft and partner services](../integrate-overview)
- [Stream Defender for IoT cloud alerts to a partner SIEM](../integrations/send-cloud-data-to-partners)

After integrating Defender for IoT alerts with a SIEM, we recommend the following next steps to operationalize OT/IoT alerts and fully integrate them with your existing SOC workflows and tools:

- Identify and define relevant IoT/OT security threats and SOC incidents you would like to monitor based on your specific OT needs and environment.
- Create detection rules and severity levels in the SIEM. Only relevant incidents will be triggered, thus reducing unnecessary noise. For example, you would define PLC code changes performed from unauthorized devices, or outside of work hours, as a high severity incident due to the high fidelity of this specific alert.

    In Microsoft Sentinel, the Microsoft Defender for IoT solution includes [a set of out-of-the-box detection rules](../iot-advanced-threat-monitoring#detect-threats-out-of-the-box-with-defender-for-iot-data), which are built specifically for Defender for IoT data, and help you fine-tune the incidents created in Sentinel.
- Define the appropriate workflow for mitigation, and create automated investigation playbooks for each use case. In Microsoft Sentinel, the Microsoft Defender for IoT solution includes [out-of-the-box playbooks for automated response to Defender for IoT alerts](../iot-advanced-threat-monitoring#automate-response-to-defender-for-iot-alerts).