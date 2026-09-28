---
layout: Conceptual
title: Create SSL/TLS certificates for OT appliances - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/ot-deploy/create-ssl-certificates
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
description: Learn how to create SSL/TLS certificates for use with Microsoft Defender for IOT OT sensors.
ms.date: 2023-01-17T00:00:00.0000000Z
ms.topic: install-set-up-deploy
ms.custom: sfi-image-nochange
locale: en-us
document_id: 62c012ae-802c-bac0-fd61-9dd09f0d0b36
document_version_independent_id: 436566da-ef36-09f7-82f7-17b0c685c095
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/ot-deploy/create-ssl-certificates.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/ot-deploy/create-ssl-certificates
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/ot-deploy/create-ssl-certificates.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 4a325fa7-1f6f-0935-5da8-b6fa1555d8e7
---

# Create SSL/TLS certificates for OT appliances - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](ot-deploy-path) for OT monitoring with Microsoft Defender for IoT, and describes how to create CA-signed certificates to use with Defender for IoT on-premises OT sensor appliances.

[![Diagram of a progress bar with Plan and prepare highlighted.](../media/deployment-paths/progress-plan-and-prepare.png)](../media/deployment-paths/progress-plan-and-prepare.png#lightbox)

Each certificate authority (CA)-signed certificate must have both a `.key` file and a `.crt` file, which are uploaded to Defender for IoT appliances after the first sign-in. While some organizations may also require a `.pem` file, a `.pem` file isn't required for Defender for IoT.

Important

You must create a unique certificate for each Defender for IoT appliance, where each certificate meets required criteria.

## Prerequisites

To perform the procedures described in this article, make sure that you have a security, PKI or certificate specialist available to oversee the certificate creation.

Make sure that you've also familiarized yourself with [SSL/TLS certificate requirements for Defender for IoT](../best-practices/certificate-requirements).

## Create a CA-signed SSL/TLS certificate

We recommend that you always use CA-signed certificates on production environments, and only use self-signed certificates on testing environments.

Use a certificate management platform, such as an automated PKI management platform, to create a certificate that meets Defender for IoT requirements.

If you don't have an application that can automatically create certificates, consult a security, PKI, or other qualified certificate lead for help. You can also convert existing certificate files if you don't want to create new ones.

Make sure to create a unique certificate for each Defender for IoT appliance, where each certificate meets required [parameter criteria](../best-practices/certificate-requirements).

**For example**:

1. Open the downloaded certificate file and select the **Details** tab &gt; **Copy to file** to run the **Certificate Export Wizard**.
2. In the **Certificate Export Wizard**, select **Next** &gt; **DER encoded binary X.509 (.CER)** &gt; and then select **Next** again.
3. In the **File to Export** screen, select **Browse**, choose a location to store the certificate, and then select **Next**.
4. Select **Finish** to export the certificate.

Note

You may need to convert existing files types to supported types.

Verify that the certificate meets [certificate file requirements](../best-practices/certificate-requirements#crt-file-requirements), and then test the certificate file you created when you're done.

If you aren't using certificate validation, remove the CRL URL reference in the certificate. For more information, see [certificate file requirements](../best-practices/certificate-requirements#crt-file-requirements).

Tip

(Optional) Create a certificate chain, which is a `.pem` file that contains the certificates of all the certificate authorities in the chain of trust that led to your certificate.

## Verify CRL server access

If your organization validates certificates, your Defender for IoT appliances must be able to access the CRL server defined by the certificate. By default, certificates access the CRL server URL via HTTP port 80. However, some organizational security policies block access to this port.

If your appliances can't access your CRL server on port 80, you can use one of the following workarounds:

- **Define another URL and port in the certificate**:

    - The URL you define must be configured as `http: //` and not `https://`
    - Make sure that the destination CRL server can listen on the port you define
- **Use a proxy server that can access the CRL on port 80**

    For more information, see [Forward OT alert information].

If validation fails, communication between the relevant components is halted and a validation error is presented in the console.

## Import the SSL/TLS certificate to a trusted store

After creating your certificate, import it to a trusted storage location. For example:

1. Open the security certificate file and, in the **General** tab, select **Install Certificate** to start the **Certificate Import Wizard**.
2. In **Store Location**, select **Local Machine**, then select **Next**.
3. If a **User Allow Control** prompt appears, select **Yes** to allow the app to make changes to your device.
4. In the **Certificate Store** screen, select **Automatically select the certificate store based on the type of certificate**, then select **Next**.
5. Select **Place all certificates in the following store**, then **Browse**, and then select the **Trusted Root Certification Authorities** store. When you're done, select **Next**. For example:

    [![Screenshot of the certificate store screen where you can browse to the trusted root folder.](../media/how-to-deploy-certificates/certificate-store-trusted-root.png)](../media/how-to-activate-and-set-up-your-sensor/certificate-store-trusted-root.png#lightbox)
6. Select **Finish** to complete the import.

## Test your SSL/TLS certificates

Use the following procedures to test certificates before deploying them to your Defender for IoT appliances.

### Check your certificate against a sample

Use the following sample certificate to compare to the certificate you've created, making sure that the same fields exist in the same order.

```Sample
Bag Attributes: <No Attributes>
subject=C = US, S = Illinois, L = Springfield, O = Contoso Ltd, OU= Contoso Labs, CN= sensor.contoso.com, E 
= support@contoso.com
issuer C=US, S = Illinois, L = Springfield, O = Contoso Ltd, OU= Contoso Labs, CN= Cert-ssl-root-da2e22f7-24af-4398-be51-
e4e11f006383, E = support@contoso.com
-----BEGIN CERTIFICATE-----
MIIESDCCAZCgAwIBAgIIEZK00815Dp4wDQYJKoZIhvcNAQELBQAwgaQxCzAJBgNV 
BAYTAIVTMREwDwYDVQQIDAhJbGxpbm9pczEUMBIGA1UEBwwLU3ByaW5nZmllbGQx
FDASBgNVBAoMCONvbnRvc28gTHRKMRUWEwYDVQQLDAXDb250b3NvIExhYnMxGzAZ
BgNVBAMMEnNlbnNvci5jb250b3NvLmNvbTEIMCAGCSqGSIb3DQEJARYTc3VwcG9y
dEBjb250b3NvLmNvbTAeFw0yMDEyMTcxODQwMzhaFw0yMjEyMTcxODQwMzhaMIGK
MQswCQYDVQQGEwJVUzERMA8GA1UECAwISWxsaW5vaXMxFDASBgNVBAcMC1Nwcmlu 
Z2ZpZWxkMRQwEgYDVQQKDAtDb250b3NvIEX0ZDEVMBMGA1UECwwMQ29udG9zbyBM 
YWJzMRswGQYDVQQDDBJzZW5zb3luY29udG9zby5jb20xljAgBgkqhkiG9w0BCQEW 
E3N1cHBvcnRAY29udG9zby5jb20wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEK 
AoIBAQDRGXBNJSGJTfP/K5ThK8vGOPzh/N8AjFtLvQiiSfkJ4cxU/6d1hNFEMRYG
GU+jY1Vknr0|A2nq7qPB1BVenW3 MwsuJZe Floo123rC5ekzZ7oe85Bww6+6eRbAT 
WyqpvGVVpfcsloDznBzfp5UM9SVI5UEybllod31MRR/LQUEIKLWILHLW0eR5pcLW 
pPLtOW7wsK60u+X3tqFo1AjzsNbXbEZ5pnVpCMqURKSNmxYpcrjnVCzyQA0C0eyq
GXePs9PL5DXfHy1x4WBFTd98X83 pmh/vyydFtA+F/imUKMJ8iuOEWUtuDsaVSX0X
kwv2+emz8CMDLsbWvUmo8Sg0OwfzAgMBAAGjfDB6MB0GA1UdDgQWBBQ27hu11E/w 
21Nx3dwjp0keRPuTsTAfBgNVHSMEGDAWgBQ27hu1lE/w21Nx3dwjp0keRPUTSTAM
BgNVHRMEBTADAQH/MAsGA1UdDwQEAwIDqDAdBgNVHSUEFjAUBggrBgEFBQcDAgYI
KwYBBQUHAwEwDQYJKoZIhvcNAQELBQADggEBADLsn1ZXYsbGJLLzsGegYv7jmmLh
nfBFQqucORSQ8tqb2CHFME7LnAMfzFGpYYV0h1RAR+1ZL1DVtm+IKGHdU9GLnuyv
9x9hu7R4yBh3K99ILjX9H+KACvfDUehxR/ljvthoOZLalsqZIPnRD/ri/UtbpWtB 
cfvmYleYA/zq3xdk4vfOI0YTOW11qjNuBIHh0d5S5sn+VhhjHL/s3MFaScWOQU3G 
9ju6mQSo0R1F989aWd+44+8WhtOEjxBvr+17CLqHsmbCmqBI7qVnj5dHvkh0Bplw 
zhJp150DfUzXY+2sV7Uqnel9aEU2Hlc/63EnaoSrxx6TEYYT/rPKSYL+++8=
-----END CERTIFICATE-----
```

### Test certificates without a `.csr` or private key file

If you want to check the information within the certificate `.csr` file or private key file, use the following CLI commands:

- **Check a Certificate Signing Request (CSR)**: Run `openssl req -text -noout -verify -in CSR.csr`
- **Check a private key**: Run `openssl rsa -in privateKey.key -check`
- **Check a certificate**: Run `openssl x509 -in certificate.crt -text -noout`

If these tests fail, review [certificate file requirements](../best-practices/certificate-requirements#crt-file-requirements) to verify that your file parameters are accurate, or consult your certificate specialist.

### Validate the certificate's common name

1. To view the certificate's common name, open the certificate file and select the Details tab, and then select the **Subject** field.

    The certificate's common name appears next to **CN**.
2. Sign-in to your sensor console without a secure connection. In the **Your connection isn't private** warning screen, you might see a **NET::ERR\_CERT\_COMMON\_NAME\_INVALID** error message.
3. Select the error message to expand it, and then copy the string next to **Subject**. For example:

    [![Screenshot of the connection isn't private screen with the details expanded.](../media/how-to-deploy-certificates/connection-is-not-private-subject.png)](../media/how-to-deploy-certificates/connection-is-not-private-subject.png#lightbox)

    The subject string should match the **CN** string in the security certificate's details.
4. In your local file explorer, browse to the hosts file, such as at **This PC &gt; Local Disk (C:) &gt; Windows &gt; System32 &gt; drivers &gt; etc**, and open the **hosts** file.
5. In the hosts file, add in a line at the end of document with the sensor's IP address and the SSL certificate's common name that you copied in the previous steps. When you're done, save the changes. For example:

    [![Screenshot of the hosts file.](../media/how-to-deploy-certificates/hosts-file.png)](../media/how-to-activate-and-set-up-your-sensor/hosts-file.png#lightbox)

### Self-signed certificates

Self-signed certificates are available for use in testing environments after installing Defender for IoT OT monitoring software. For more information, see:

- [Create and deploy self-signed certificates on OT sensors](../how-to-manage-individual-sensors#manage-ssltls-certificates)