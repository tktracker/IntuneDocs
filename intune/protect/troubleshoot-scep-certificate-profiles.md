---
# required metadata

title: Troubleshoot use of SCEP certificate profiles to provision certificates with Intune | Microsoft Docs
description: Troubleshoot the use of SCEP by devices to request certificates for use with Intune, including communication from devices to NDES, NDES to certification authorities, and from the Intune Certificate Connector to the Intune service.  
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

# Troubleshoot using SCEP certificate profiles with Microsoft Intune

Use of Simple Certificate Enrollment Protocol (SCEP) certificate profiles can be challenging to troubleshoot in Intune. This article can help you resolve issues by:

- Explaining the architecture and the communication flow of the SCEP process
- Helping you to narrow down where a problem exists in that communication flow
- Explaining key log files and key entries

The information in this article applies to using SCEP certificate profiles with Android, iOS/iPad, and Windows devices.  
To troubleshoot Network Device Enrollment Service (NDES), see [Troubleshooting NDES configuration for use with Microsoft Intune certificate profiles]( https://support.microsoft.com/help/4459540/troubleshoot-ndes-configuration-for-use-with-intune).

## SCEP communication flow overview

The following communication flow describes how Intune uses SCEP to provision devices with certificates.

![SCEP certificate profile flow](../protect/media/troubleshoot-scep-certificate-profiles/scep-certificate-profile-flow.png)

1. [Deploy a SCEP certificate profile](). Intune generates a challenge string, which requires a specific user, certificate purpose, and certificate type.

2. The device uses the URI for NDES from the profile to contact the NDES server so it can present a challenge.

3. NDES forwards the challenge to the Intune Certificate Connector policy module on the server, which validates the request.

4. If valid, NDES passes the request to issue a certificate to the Certification Authority (CA).

5. The certificate is delivered to the device.

6. The Intune Certificate Connector reports the certificate issuance event to Intune.

## Log files

To identify problems for the communication and certificate provisioning workflow, review log files from both the Server infrastructure, and from devices. Later sections for troubleshooting SCEP certificate profiles refer to log files referenced in this section.

[Infrastructure and Server logs](logs-for-on-premises-infrastructure)

Device logs depend on the device platform:  

<!-- Content in progrss 
- [Android](#logs-for-android):  
  ***PENDING*** additional content
- [iOS/iPadOS](#logs-for-ios):  
-->

- [Windows](#logs-for-windows)

### Logs for on-premises infrastructure
  
On-premises infrastructure includes the Microsoft Intune Certificate Connector, NDES that runs on a Windows Server, and the certification authority.

Log files for these roles include Windows Event Viewer, Certificate consoles, and various log files specific to the Intune Certificate Connector, NDES, or other role and operations that are part of the on-premises infrastructure.

The following table includes logs or consoles that are references in the various SCEP troubleshooting articles, and default locations. 

| Log name or console | Location | Details  |
|---------------------|-------------|-------------------------------------|
|NDESConnector_date_time.svclog | On the server that hosts NDES: <br><br>*%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*| This log shows communication from the Microsoft Intune Certificate Connector to the Intune cloud service. <br><br>  Related registry key: *HKLM\SW\Microsoft\MicrosoftIntune\NDESConnector\ConnectionStatus* <br><br> We recommend that you use [Service Trace Viewer Tool](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) to view the log files.|
|CertificateRegistrationPointdate_time.svclog   | On the server that hosts NDES: <br><br>*%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*  |This log shows NDES policy module receiving and verifying certificate requests.<br><br> We recommend that you use [Service Trace Viewer Tool](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) to view the log files. |
|NDESPlugin.log   | On the server that hosts NDES:  <br><br> *%program_files%\Microsoft Intune\NDESPolicyModule\logs*  |This log shows the passing of certificate requests to the Certificate Registration Point, and the resulting verification of those requests. |
|IIS logs    |  On the server that hosts NDES:  <br><br>*c:\inetpub\logs\LogFiles\W3SVC1* | IS logs show the certificate requests from mobile devices entering NDES.  |
Windows Application log |On the server that hosts NDES: <br><br> Run **eventvwr.msc** to open Windows Event Viewer |This log is referenced when investigating IIS issues, like the SCEP application pool.    |

<!-- Content in progress 

### Logs for Android devices
***PENDING*** additional content

### Logs for iOS/iPadOS devices
***PENDING*** additional content
-->

### Logs for Windows devices

For devices that run Windows, use the Windows Event logs to diagnose enrollment or device management issues for devices that you manage with Intune.

On the device, open **Event Viewer** > **Applications and Services Logs** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider**

![Windows event logs](../protect/media/troubleshoot-scep-certificate-profiles/windows-event-log.png)

## Next steps
Review [deployment of SCEP certificate profiles](troublehsoot-scep-certificate-profile-deployment) 