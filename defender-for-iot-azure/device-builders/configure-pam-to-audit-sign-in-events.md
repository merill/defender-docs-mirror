---
layout: Conceptual
title: Configure Pluggable Authentication Modules (PAM) to Audit Sign-in Events (Preview) - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/configure-pam-to-audit-sign-in-events
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
ms.subservice: device-builders
description: Learn how to configure Pluggable Authentication Modules (PAM) to audit sign-in events when syslog isn't configured for your device.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: f238b383-fb4b-0d10-58bf-bff105ee7fe2
document_version_independent_id: a2d748f2-7a68-d02f-3c37-dc57df29df16
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/configure-pam-to-audit-sign-in-events.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/configure-pam-to-audit-sign-in-events
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/configure-pam-to-audit-sign-in-events.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: ef94eae4-f82a-b1f4-9006-22e8dd08673a
---

# Configure Pluggable Authentication Modules (PAM) to Audit Sign-in Events (Preview) - Microsoft Defender for IoT | Microsoft Learn

This article provides a sample process for configuring Pluggable Authentication Modules (PAM) to audit SSH, Telnet, and terminal sign-in events on an unmodified Ubuntu 20.04 or 18.04 installation.

PAM configurations might vary between devices and Linux distributions.

For more information, see [Login collector (event-based collector)](concept-event-aggregation#login-collector-event-based-collector).

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Prerequisites

Before you get started, make sure that you have a Defender for IoT Micro Agent.

Configuring PAM requires technical knowledge.

For more information, see [Tutorial: Install the Defender for IoT micro agent](tutorial-standalone-agent-binary-installation).

## Modify PAM configuration to report sign-in and sign-out events

This procedure provides a sample process for configuring the collection of successful sign-in events.

Our example is based on an unmodified Ubuntu 20.04 or 18.04 installation, and the steps in this process might differ for your system.

1. Locate the following files:

    - `/etc/pam.d/sshd`
    - `/etc/pam.d/login`
2. Append the following lines to the end of each file:

    ```txt
    // report login
    session [default=ignore] pam_exec.so type=open_session /usr/libexec/defender_iot_micro_agent/pam/pam_audit.sh 0
    
    // report logout
    session [default=ignore] pam_exec.so type=close_session /usr/libexec/defender_iot_micro_agent/pam/pam_audit.sh 1
    ```

## Modify the PAM configuration to report sign-in failures

This procedure provides a sample process for configuring the collection of failed sign-in attempts.

This example in this procedure is based on an unmodified Ubuntu 18.04 or 20.04 installation. The following files and commands might differ per configuration or as a result of modifications.

1. Locate the `/etc/pam.d/common-auth` file and look for the following lines:

    ```txt
    # here are the per-package modules (the "Primary" block)
    auth    [success=1 default=ignore]  pam_unix.so nullok_secure
    # here's the fallback if no module succeeds
    auth    requisite           pam_deny.so
    ```

    The `common-auth` configuration shown here authenticates via the `pam_unix.so` module. In case of authentication failure, the configuration continues to the `pam_deny.so` module to prevent access.
2. Replace the indicated lines of code with the following:

    ```txt
    # here are the per-package modules (the "Primary" block)
    auth	[success=1 default=ignore]	pam_unix.so nullok_secure
    auth	[success=1 default=ignore]	pam_exec.so quiet /usr/libexec/defender_iot_micro_agent/pam/pam_audit.sh 2
    auth	[success=1 default=ignore]	pam_echo.so
    # here's the fallback if no module succeeds
    auth	requisite			pam_deny.so
    ```

    In the modified `/etc/pam.d/common-auth` configuration shown here, PAM skips one module to the `pam_echo.so` module, and then skips the `pam_deny.so` module and authenticates successfully.

    In case of failure, PAM continues to report the sign-in failure to the agent log file, and then skips one module to the `pam_deny.so` module, which blocks access.

## Validate your configuration

This procedure describes how to verify that you've configured PAM correctly to audit sign-in events.

1. Sign in to the device using SSH, and then sign-out.
2. Sign in to the device using SSH, using incorrect credentials to create a failed sign-in event.
3. Access your device and run the following command:

    ```bash
    cat /var/lib/defender_iot_micro_agent/pam.log
    ```
4. Verify that lines similar to the following are logged, for a successful sign-in (`open_session`), sign-out (`close_session`), and a sign-in failure (`auth`):

    ```txt
    2021-10-31T18:10:31+02:00,16356631,2589842,open_session,sshd,user,192.168.0.101,ssh,0
    2021-10-31T18:26:19+02:00,16356719,199164,close_session,sshd, user,192.168.0.201,ssh,1
    2021-10-28T17:44:13+03:00,163543223,3572596,auth,sshd,user,143.24.20.36,ssh,2
    ```
5. Repeat the verification procedure with Telnet and terminal connections.