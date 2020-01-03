---
# required metadata

title: Troubleshoot managed device to NDES communication in Microsoft Intune | Microsoft Docs
description: Troubleshoot managed device to NDES server communication when using SCEP certificate profiles to deploy certificates with Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/15/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Troubleshoot device to NDES server communication for SCEP certificate profiles in Microsoft Intune

Use the following information to determine if a device that received and processed an Intune Simple Certificate Enrollment Protocol (SCEP) certificate profile can successfully contact Network Device Enrollment Service (NDES) to present a challenge. To contact the NDES server, the device uses the URI from the SCEP certificate profile.

This article references Step 2 of the [SCEP communication flow overview](troubleshoot-scep-certificate-profiles.md).

## Review IIS logs for a connection from the device

1. On the NDES server, open the most recent IIS log file found in the following folder:   *%SystemDrive%\inetpub\logs\logfiles\w3svc1*

2. Search the log for entries similar to the following examples. Both examples contain a status **200**, which appears near the end:

   `fe80::f53d:89b8:c3e8:5fec%13 GET /certsrv/mscep/mscep.dll/pkiclient.exe operation=GetCACaps&message=default 80 - fe80::f53d:89b8:c3e8:5fec%13 Mozilla/4.0+(compatible;+Win32;+NDES+client) - 200 0 0 186 0.`

   And

   `fe80::f53d:89b8:c3e8:5fec%13 GET /certsrv/mscep/mscep.dll/pkiclient.exe operation=GetCACert&message=default 80 - fe80::f53d:89b8:c3e8:5fec%13 Mozilla/4.0+(compatible;+Win32;+NDES+client) - 200 0 0 3567 0`

3. When the device contacts IIS, an HTTP GET request for mscep.dll is logged.

   Review the status code near the end of this request:
   - **Status code of 200**: This status indicates the connection with the NDES server is successful.
   - **Status code of 500**: The IIS_IURS group might lack correct permissions. See [Status code 500](#status-code-500), later in this article.
   - If the status code isn't 200 or 500:

     - See [Test the SCEP server URL](#test-the-scep-server-url) later in this article to help validate the configuration.

     - See [The HTTP status code in IIS 7 and later versions](https://support.microsoft.com/help/943891) for information about less common error codes.

   If the connection request isn’t logged at all, the contact from the device might be blocked on the network between the device and the NDES server.

## Review Event Logs for the connection to NDES

View the Windows Event Viewer on the device that is making the connection to NDES, and look for indications of a successful connection. Connections are logged as an event ID **36** in the devices *DeviceManagement-Enterprise-Diagnostics-Provide* > **Admin** log.

To open the log:

1. On the device, run **eventvwr.msc** to open Windows Event Viewer.

2. Expand **Applications and Services Logs** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostic-Provider** > **Admin**.

3. Look for Event **36**, which resembles the following example, with the key line of **SCEP: Certificate request generated successfully**:

   ```
   Event ID:      36
   Task Category: None
   Level:         Information
   Keywords:
   User:          <UserSid>
   Computer:      <Computer Name>
   Description:
   SCEP: Certificate request generated successfully. Enhanced Key Usage: (1.3.6.1.5.5.7.3.2), NDES URL: (https://<Server>/certsrv/mscep/mscep.dll/pkiclient.exe), Container Name: (), KSP Setting: (0x2), Store Location: (0x1).
   ```

## Troubleshoot common errors

The following sections can help with common connection issues between devices and NDES.

### Status code 500

Connections that resemble the following example, with a status code of 500, indicate the *Impersonate a client after authentication* user right isn’t assigned to the IIS_IURS group on the NDES server. The status value of **500** appears at the end:

`2017-08-08 20:22:16 IP_address GET /certsrv/mscep/mscep.dll operation=GetCACert&message=SCEP%20Authority 443 - 10.5.14.22 profiled/1.0+CFNetwork/811.5.4+Darwin/16.6.0 - 500 0 1346 31`

**To fix this issue**:

1. On the NDES server, run **secpol.msc** to open the Local Security Policy.

2. Expand **Local Policies**, and then click **User Rights Assignment**.

3. Double-click **Impersonate a client after authentication** in the right pane.

4. Click **Add User or Group…**, enter **IIS_IURS** in the **Enter the object names to select box**, and then click **OK**.

5. Click **OK**.

6. Restart the computer, and then try the connection from the device again.

### Test the SCEP server URL

Use the following steps to test the URL that is specified in the SCEP certificate profile.

1. In Intune, edit your SCEP certificate profile and copy the Server URL. The URL should resemble *https://contoso.com/certsrv/mscep/msecp.dll*.

2. Open a web browser, and then browse to that SCEP server URL. The result should be: **HTTP Error 403.0 – Forbidden**. This result indicates the URL is functioning correctly.

   If you don’t receive that error, select the link that resembles the error you see to view issue-specific guidance:
   - [I receive a general Network Device Enrollment Service message](#general-ndes-message)
   - [I receive "HTTP Error 503. The service is unavailable"](#http-error-503)
   - [I receive the "GatewayTimeout" error](#gatewaytimeout)
   - [I receive "HTTP 414 Request-URI Too Long"](#http-414-request-uri-too-long)
   - [I receive "This page can't be displayed"](#this-page-cant-be-displayed)
   - [I receive "500 - Internal server error"](#internal-server-error)

#### General NDES message

When you browse to the SCEP server URL, you receive the following Network Device Enrollment Service message:

![SCEP server URL](../protect/media/troubleshoot-scep-certificate-device-to-ndes/ndes-server-url-message.png)

- **Cause**: This problem is usually an issue with the Microsoft Intune Connector installation.

  Mscep.dll is an ISAPI extension that intercepts incoming request and displays the HTTP 403 error if it's installed correctly.
  
  **Resolution**: Examine the *SetupMsi.log* file to determine whether Microsoft Intune Connector is successfully installed. In the following example, *Installation completed successfully* and *Installation success or error status: 0* indicate a successful installation:

  `MSI (c) (28:54) [16:13:11:905]: Product: Microsoft Intune Connector -- Installation completed successfully.`

  `MSI (c) (28:54) [16:13:11:999]: Windows Installer installed the product. Product Name: Microsoft Intune Connector. Product Version: 6.1711.4.0. Product Language: 1033. Manufacturer: Microsoft Corporation. Installation success or error status: 0.`

  If the installation fails, remove the Microsoft Intune Connector and then reinstall it.

#### HTTP Error 503

When you browse to the SCEP server URL, you receive the following error:

![HTTP Error 503. The service is unavailable](../protect/media/troubleshoot-scep-certificate-device-to-ndes/service-unavailable.png)

This issue is usually because the **SCEP** application pool in IIS isn’t started. On the NDES server, open **IIS Manager** and go to **Application Pools**. Locate the **SCEP** application pool and confirm it’s started.

If the SCEP application pool isn’t started, check the application event log on the server:

1. On the device, run **eventvwr.msc** to open **Event Viewer** and go to **Windows Logs** > **Application**.

2. Look for an event that is similar to the following example, which means that the application pool crashes when a request is received:

   ```
   Log Name:      Application
   Source:        Application Error
   Event ID:      1000
   Task Category: Application Crashing Events
   Level:         Error
   Keywords:      Classic
   Description: Faulting application name: w3wp.exe, version: 8.5.9600.16384, time stamp: 0x5215df96
   Faulting module name: ntdll.dll, version: 6.3.9600.18821, time stamp: 0x59ba86db
   Exception code: 0xc0000005
   ```

**Common causes for an application pool crash**:

- **Cause 1**: There are intermediate CA certificates (not self-signed) in the NDES server's Trusted Root Certification Authorities certificate store.

  **Resolution**: Remove intermediate certificates from the Trusted Root Certification Authorities certificate store, and then restart the NDES server.
  
  To identify all intermediate certificates in the Trusted Root Certification Authorities certificate store, run the following PowerShell cmdlet: `Get-Childitem -Path cert:\LocalMachine\root -Recurse | Where-Object {$_.Issuer -ne $_.Subject}`

  A certificate that has the same **Issued to** and **Issued by** values, is a root certificate. Otherwise, it's an intermediate certificate.

  After removing certificates and restarting the server, run the PowerShell cmdlet again to confirm there are no intermediate certificates. If there are, check whether a Group Policy pushes the intermediate certificates to the NDES server. If so, exclude the NDES server from the Group Policy and remove the intermediate certificates again.

- **Cause 2**: The URLs in the Certificate Revocation List (CRL) are blocked or unreachable for the certificates that are used by the Intune Certificate Connector.

  **Resolution**: Enable additional logging to collect more information:
  1. Open Event Viewer, click **View**, make sure that **Show Analytic and Debug Logs** option is checked.
  2. Go to **Applications and Services Logs** > **Microsoft** > **Windows** > **CAPI2** > **Operational**, right-click **Operational**, then click **Enable Log**.
  3. After CAPI2 logging is enabled, reproduce the problem, and examine the event log to troubleshoot the issue.

- **Cause 3**: IIS permission on **CertificateRegistrationSvc** has **Windows Authentication** enabled.

  **Resolution**: Enable **Anonymous Authentication** and disable **Windows Authentication**, and then restart the NDES server.

  ![IIS permissions](../protect/media/troubleshoot-scep-certificate-device-to-ndes/iis-permissions.png)

#### GatewayTimeout

When you browse to the SCEP server URL, you receive the following error:
![Gatewaytimeout error](../protect/media/troubleshoot-scep-certificate-device-to-ndes/gateway-timeout.png)

- **Cause**: The **Microsoft AAD Application Proxy Connector** service isn’t started.

  **Resolution**:  Run **services.msc**, and then make sure that the **Microsoft AAD Application Proxy Connector** service is running and **Startup Type** is set to **Automatic**.

#### HTTP 414 Request-URI Too Long

When you browse to the SCEP server URL, you receive the following error: `HTTP 414 Request-URI Too Long`

- **Cause**: IIS request filtering isn't configured to support the long URLs (queries) that the NDES service receives. This support is configured when you [configure the NDES service](certificates-scep-configure.md#configure-the-ndes-service) for use with your infrastructure for SCEP.

- **Resolution**: Configure support for long URLs.

  1. On the NDES server, open IIS manager, select **Default Web Site** > **Request Filtering** > **Edit Feature Setting** to open the **Edit Request Filtering Settings** page.

  2. Configure the following settings:
     - **Maximum URL length (Bytes)** = 65534
     - **Maximum query string (Bytes)** = 65534

  3. Select **OK** to save this configuration and close IIS manager.

  4. Validate this configuration by locating the following registry key to confirm that it has the indicated values:

     HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HTTP\Parameters

     The following values are set as DWORD entries:
     - Name: **MaxFieldLength**, with a decimal value of **65534**
     - Name: **MaxRequestBytes**, with a decimal value of **65534**

  5. Restart the NDES server.

#### This page can't be displayed

You have Azure AD Application Proxy configured. When you browse to the SCEP server URL, you receive the following error: `This page can't be displayed`

- **Cause**: This issue occurs when the SCEP external URL is incorrect in the Application Proxy configuration. An example of this URL is https://contoso.com/certsrv/mscep/mscep.dll.

  **Resolution**: Use the default domain of *yourtenant.msappproxy.net* for the SCEP external URL in the Application Proxy configuration.

#### 500 - Internal server error

When you browse to the SCEP server URL, you receive the following error:

![500 - Internal server error](../protect/media/troubleshoot-scep-certificate-device-to-ndes/500-internal-server-error.png)

- **Cause 1**: The NDES service account is locked or its password is expired.

  **Resolution**: Unlock the account or reset the password.

- **Cause 2**: The MSCEP-RA certificates are expired.

  **Resolution**: If the MSCEP-RA certificates are expired, reinstall the NDES role or request new CEP Encryption and Exchange Enrollment Agent (Offline request) certificates.

  To request new certificates, follow these steps:

  1. On the Certificate Authority (CA) or issuing CA, open the Certificate Templates MMC. Make sure that the logged in user and the NDES server have **Read** and **Enroll** permissions to the CEP Encryption and Exchange Enrollment Agent (Offline request) certificate templates.

  2. Check the expired certificates on the NDES server, copy the **Subject** information from the certificate.

  3. Open the Certificates MMC for **Computer account**.

  4. Expand **Personal**, right-click **Certificates**, then select **All Tasks** > **Request New Certificate**.

  5. On the **Request Certificate** page, select **CEP Encryption**, then click **More information is required to enroll for this certificate. Click here to configure settings**.

     ![Select CEP Encryption](../protect/media/troubleshoot-scep-certificate-device-to-ndes/select-scep-encryption.png)

  6. In **Certificate Properties**, click the **Subject** tab, fill the **Subject name** with the information that you collected during step 2, click **Add**, then click **OK**.

  7. Complete the certificate enrollment.

  8. Open the Certificates MMC for **My user account**.

     When you enroll for the Exchange Enrollment Agent (Offline request) certificate, it must be done in the user context. Because the **Subject Type** of this certificate template is set to **User**.

  9. Expand **Personal**, right-click **Certificates**, then select **All Tasks** > **Request New Certificate**.

  10. On the **Request Certificate** page, select **Exchange Enrollment Agent (Offline request)**, then click **More information is required to enroll for this certificate. Click here to configure settings**.

      ![Select Exchange Enrollment Agent](../protect/media/troubleshoot-scep-certificate-device-to-ndes/select-exchange-enrollment-agent.png)

  11. In **Certificate Properties**, click the **Subject** tab, fill the **Subject name** with the information that you collected during step 2, click **Add**.

      ![Certificate properties](../protect/media/troubleshoot-scep-certificate-device-to-ndes/certificate-properties.png)

      Select the **Private Key** tab, select **Make private key exportable**, then click **OK**.

      ![Private key](../protect/media/troubleshoot-scep-certificate-device-to-ndes/private-key.png)

  12. Complete the certificate enrollment.

  13. Export the Exchange Enrollment Agent (Offline request) certificate from the current user certificate store. In the Certificate Export Wizard, select **Yes, export the private key**.

  14. Import the certificate to the local machine certificate store.

  15. In the Certificates MMC, do the following action for each of the new certificates:

      Right-click the certificate, click **All Tasks** > **Manage Private Keys**, add **Read** permission to the NDES service account.

  16. Run the **iisreset** command to restart IIS.

## Next steps

If the device successfully reaches the NDES server to present the certificate request, the next step is to review the [Intune Certificate Connectors policy module](troubleshoot-scep-certificate-ndes-policy-module.md).
