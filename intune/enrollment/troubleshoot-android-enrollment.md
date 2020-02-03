---
title: Troubleshoot Android enterprise devices in Microsoft Intune
description: Suggestions for troubleshooting some of the most common problems when you enroll Android devices in Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/04/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: mghadial
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Troubleshoot Android device enrollment problems in Microsoft Intune

This article helps Intune administrators understand and troubleshoot problems when enrolling Android devices in Intune.

## Apps on Android devices

### Why are apps that I unapproved from the Google Play for Work store not being removed from the Mobile Apps page in the Intune Admin Portal?

  **Answer**: This is expected behavior.

### Why are managed Google Play apps not reporting under the Discovered Apps blade in the Intune portal?

  **Answer**: This is expected behavior.

###  Why are managed Google Play apps that aren't deployed through Intune displayed in the work profile?

  **Answer**: System apps can be enabled in the work profile by the device OEM at the time that the work profile is created. This isn't controlled by the MDM provider.

  To troubleshoot, follow these steps:

  1. Collect Company Portal logs.
  2. Note apps that appear in the work profile unexpectedly.
  3. Unenroll device from Intune and uninstall Company Portal.
  4. Install the [Test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc) app which allows creation of a work profile without an EMM for testing.
  5. Follow the instructions in [Test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc) to create a work profile on the device.
  6. Review apps that appear in the work profile. 
  7. If the same applications show in the Test DPC app, the apps are expected by the OEM for that device.

### Are Web Applications supported for work profile enrolled devices?

  **Answer**: Not currently.

## Remote actions

### Why is the Wipe (Factory Reset) option not available for my work profile enrolled device?

  **Answer**: This is expected behavior. In the work profile scenario, the MDM provider doesn't have full control over the device. The only option available is Retire (Remove Company Data) which removes the whole work profile and all its contents.

### Is device passcode reset supported?

  **Answer**: For work profile enrolled devices, you can only reset the work profile passcode on devices running Android 8.0+ when the work profile passcode is managed and the end-user has allowed you to reset it. For Dedicated devices (COSU), device passcode reset is supported.


## Device management

### Why can't I find file path Internal storage/Android/Data.com.microsoft.windowsintune.companyportal/files on my work profile enrolled device to manually collect Company Portal Logs?

  **Answer**: This is expected behavior. This path is only created for the Device Admin (Legacy Android Enrollment) scenario.

  To collect logs, follow these steps:

  1. In the Company Portal app with the badge, tap **Menu** > **Help** > **Email Support**, and then tap **Send Email & Upload logs**. 
  2. When you are prompted **Send help request with**, select one of the Email apps.
  3. An email is generated to your IT admin with an incident ID that can be provided to Microsoft product support.

### I checked the Managed Google Play Last Sync time and it hasn't been updated in days. Why?

  **Answer**: This is expected behavior. The sync is only triggered when you manually do so.


### Is System Center Configuration Manager hybrid supported?

  **Answer**: It's supported with Configuration Manager 1702 and later versions for work profile management. Dedicated devices (COSU) aren't supported in a hybrid scenario.

### My device is required to be encrypted upon enrollment, is there an option to turn it off?

  **Answer**: No, encryption is required from Google for the work profile. 

### Why are Samsung devices blocking the use of third-party keyboards like SwiftKey?

  **Answer**: Samsung began enforcing this on Android 8.0+ devices. Microsoft is currently working with Samsung on this issue and will post new information when it's available.

</details>

## Next steps

- [Troubleshoot device enrollment in Intune](../troubleshoot-device-enrollment-in-intune.md)
- [Ask a question on the Intune forum](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [Check the Microsoft Intune Support Team Blog](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Check the Microsoft Enterprise Mobility and Security Blog](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210)