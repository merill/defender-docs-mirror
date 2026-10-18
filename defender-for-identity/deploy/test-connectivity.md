---
layout: Conceptual
title: Test connectivity for Microsoft Defender for Identity sensor servers - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/test-connectivity
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
description: Learn how to test whether the server where you're installing your Microsoft Defender for Identity sensor can access the Defender for Identity cloud service.
ms.date: 2026-10-18T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: rlitinsky
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 28102fcb-e02b-79c4-6de7-06686e6947bc
document_version_independent_id: 28102fcb-e02b-79c4-6de7-06686e6947bc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/test-connectivity.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/test-connectivity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/test-connectivity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/486161dc-fa28-4625-9b1c-1a21d690bc8d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5dd28c86-729c-4723-ab5a-57e26fcec2a8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: f28aac24-5233-b0d8-9c4f-2306cfec5c58
---

# Test connectivity for Microsoft Defender for Identity sensor servers - Microsoft Defender for Identity | Microsoft Learn

The Defender for Identity sensor requires network connectivity to the Defender for Identity service. Depending on which version of the sensor you deployed, see [Sensor v2.x prerequisites](prerequisites-sensor-version-2) or [Sensor v3.x prerequisites](deploy-sensor-v3).

Test connectivity before deployment to verify that the sensor server can reach the Defender for Identity cloud service. Use the browser connectivity test or PowerShell connectivity test. You can also use these tests to troubleshoot connectivity after deployment.

For more information, see [v2.x required ports](prerequisites-sensor-version-2#required-ports).

Note

To get the name and other important details about your Defender for Identity workspace, see the [About page](../settings-about) in the [Microsoft Defender XDR](https://security.microsoft.com/) portal.

## Test connectivity using a browser

Use this procedure to test v2.x sensor connectivity from a browser:

1. Open a browser. If you're using a proxy, make sure that your browser uses the same proxy settings being used by the sensor.

    For example, if the proxy settings are defined for **Local System**, you'll need to use PSExec to open a session as **Local System** and open the browser from that session.
2. Browse to the following URL: `https://<your_workspace_name>sensorapi.atp.azure.com/tri/sensor/api/ping`. Replace `<your_workspace_name>` with the name of your Defender for Identity workspace.

    Important

    You must specify `HTTPS`, not `HTTP`, to properly test connectivity.

    **Expected result**: The response shows the latest sensor version number, confirming that the server can reach the Defender for Identity HTTPS endpoint.

    For some older workspaces, the message returned could be *Error 503 The service is unavailable*. This is a temporary state that still indicates success. For example:

    ![Screenshot of an HTTP 200 status code (OK).](../media/configure-proxy/test-proxy.png)

    Other results might include the following scenarios:

    - If you don't get *Ok* message, then you may have a problem with your proxy configuration. Check your network and proxy settings.
    - If you get a certificate error, ensure that you have the required trusted root certificates installed before continuing. For more information, see [Proxy authentication problem presents as a connection error](../troubleshooting-known-issues#proxy-authentication-problem-presents-as-a-connection-error). The certificate details should look like this:

        ![Screenshot of the required certificate path.](../media/configure-proxy/certificate.png)

## Test service connectivity using PowerShell

These commands test v2.x connectivity to the workspace sensor API.

**Prerequisites**: Before running Defender for Identity PowerShell commands, make sure that you downloaded the [Defender for Identity PowerShell module](https://www.powershellgallery.com/packages/DefenderForIdentity/).

Sign in to your server and run one of the following commands:

- To use the current server's settings, run:

    ```powershell
    Test-MDISensorApiConnection
    ```
- To test settings that you're planning on using, but aren't currently configured on the server, run the command using the following syntax:

    ```powershell
    Test-MDISensorApiConnection -BypassConfiguration -SensorApiUrl 'https://contososensorapi.atp.azure.com' -ProxyUrl 'https://myproxy.contoso.com:8080' -ProxyCredential $credential
    ```

    Where:

    - `https://contososensorapi.atp.azure.com` is an example of your sensor URL, where *contoso* is the name of your workspace.
    - `https://myproxy.contoso.com:8080` is an example of your proxy URL

For more information, see the [MDI PowerShell documentation](/en-us/powershell/module/defenderforidentity/test-mdisensorapiconnection).

## Check v3.x connectivity requirements

The v3.x sensor uses Microsoft Defender for Endpoint service endpoints. Follow the [v3.x network requirements](deploy-sensor-v3#network-requirements) for the applicable Defender for Endpoint connectivity guidance.