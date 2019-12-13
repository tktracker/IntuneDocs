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

Use the following information to determine if a device that received and processed an Intune SCEP certificate profile can successfully contact NDES to present a challenge.

This article references Step 2 of the [SCEP communication flow overview](troubleshoot-scep-certificate-profiles.md), and makes reference to log files that are introduced in that article.

To connect to NDES, the device uses the URI from the SCEP certificate profile to contact IIS on the NDES server. 
This article applies to the step 2 of the [SCEP communication workflow](../troubleshoot-scep-communication.md); communication from the device to the NDES server that hosts your Microsoft Intune Certificate Connector.

<!-- Platforms? Just WIndows currently...  
with Android, iOS/iPad, and Windows devices.  
-->

<!-- DO we need this:
Relevant log files:
- IIS log
- Windows Event log - deviceManagement-Enterprise-Diagnostics-Provider log
-->

## Review IIS logs on the NDES server for a connection from the device

1. On the NDES server, open the most recent IIS log file found in the following folder:   *%SystemDrive%\inetpub\logs\logfiles\w3svc1*

2. Search the log for entries similar to the following. These example both contain a status **200**, which appears near the end:

   `fe80::f53d:89b8:c3e8:5fec%13 GET /certsrv/mscep/mscep.dll/pkiclient.exe operation=GetCACaps&message=default 80 - fe80::f53d:89b8:c3e8:5fec%13 Mozilla/4.0+(compatible;+Win32;+NDES+client) - 200 0 0 186 0.`
   
   And

   `fe80::f53d:89b8:c3e8:5fec%13 GET /certsrv/mscep/mscep.dll/pkiclient.exe operation=GetCACert&message=default 80 - fe80::f53d:89b8:c3e8:5fec%13 Mozilla/4.0+(compatible;+Win32;+NDES+client) - 200 0 0 3567 0`

3. When the device contacts IIS, an HTTP GET request for mscep.dll is logged.

   Review the status code near the end of this request:
   - **Status code of 200**: This indicates the connection with the NDES server is successful.
   - **Status code of 500**: The IIS_IURS group might lack correct permissions. See [Status code 500](#status-code-500), later in this article.
   - If the status code is not 200 or 500:

     - See [Test the SCEP server URL](#test-the-scep-server-url) later in this article to help validate the configuration.

     - See [The HTTP status code in IIS 7 and later versions](https://support.microsoft.com/help/943891) for information about less common error codes.

   If the connection request isn’t logged at all, the contact from the device might be blocked by on the network between the device and the NDES server.

## Review Event Logs on the device for the connection to the NDES server

You can view the Windows Event Viewer on the device that is making the connection to NDES, for indications of a successful connection. This is logged as an event ID 36 in the devices *DeviceManagement-Enterprise-Diagnostics-Provide* > **Admin** log.

To open the log:

1. On the device, run **eventvwr.msc** to open Windows Event Viewer.

2. Expand **Applications and Services Logs** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostic-Provider** > **Admin**.

3. Look for Event **36**, which resembles the following example, with the key line of **SCEP: Certificate request generated successfully.**:
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

The following sections can help you resolve the more common connection issues between devices and NDES.

### Status code 500

Connections that resemble the following example, with a status code of 500, indicate the Impersonate a client after authentication user right isn’t assigned to the IIS_IURS group on the NDES server. The status value of **500** appears at the end: 

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

2. Open a web browser, and then brows to that SCEP server URL. The result should be: **HTTP Error 403.0 – Forbidden**. This result indicates the URL is functioning correctly.

   If you don’t receive that error, select the link that resembles the error you see to view issue specific guidance:.  
   - [I receive a general Network Device Enrollment Service message](#general-ndes-message)
   - [I receive "HTTP Error 503. The service is unavailable"](#https-error-503)
   - [I receive the "GatewayTimeout" error](#gatewaytimeout)    
   - [I receive "HTTP 414 Request-URI Too Long"](#http-414-request-uri-too-long)
   - [I receive "This page can't be displayed"](#this-page-cant-be-displayed)
   - [I receive "500 - Internal server error"](#intenral-server-error)

#### General NDES message

When you browse to the SCEP server URL, you receive the following Network Device Enrollment Service message:

![SCEP server URL](../protect/media/troubleshoot-scep-certificate-device-to-ndes/ndes-server-url-message.png) 

This problem is usually caused by an issue with the Microsoft Intune Connector installation.

Mscep.dll is an ISAPI extension that intercepts incoming request and displays the HTTP 403 error if it's installed correctly. Examine the *SetupMsi.log* file to determine whether Microsoft Intune Connector is successfully installed. In the following example, **Installation completed successfully** and **Installation success or error status: 0** indicate a successful installation:

`MSI (c) (28:54) [16:13:11:905]: Product: Microsoft Intune Connector -- Installation completed successfully.`

`MSI (c) (28:54) [16:13:11:999]: Windows Installer installed the product. Product Name: Microsoft Intune Connector. Product Version: 6.1711.4.0. Product Language: 1033. Manufacturer: Microsoft Corporation. Installation success or error status: 0.`

If the installation fails, remove the Microsoft Intune Connector and then reinstall it.

#### HTTP Error 503

When you browse to the SCEP server URL, you receive the following error:

![HTTP Error 503. The service is unavailable](../protect/media/troubleshoot-scep-certificate-device-to-ndes/service-unavailable.png)

This issue is usually because the **SCEP** application pool in IIS isn’t started. On the NDES server, open **IIS Manager** and go to **Application Pools**. Locate the **SCEP** application pool and confirm it’s started.

If the SCEP application pool isn’t started, check the application event log on the server:

1. On the device, open **Event Viewer** > **Applications and Services Logs** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider**.

2. Look for an event that is similar to the following, which means that the application pool crashes when a request is received:

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





#### GatewayTimeout



#### HTTP 414 Request-URI Too Long


#### This page can't be displayed


##### 500 - Internal server error


