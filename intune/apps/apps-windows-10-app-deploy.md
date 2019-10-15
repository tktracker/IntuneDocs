---
# required metadata

title: Windows 10 app deployment by using Microsoft Intune
titleSuffix: 
description: Learn about Windows 10 app deployment scenarios available with Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 10/02/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology:
ms.assetid: abebfb5e-054b-435a-903d-d1c31767bcf2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Windows 10 app deployment by using Microsoft Intune 

Microsoft Intune supports a variety of app types and deployment scenarios on Windows 10 devices. After you've added an app to Intune, you can assign the app to users and devices. This article provides more details on the supported Windows 10 scenarios, and also covers key details to note when you're deploying apps to Windows. 

Line-of-business (LOB) apps and Microsoft Store for Business apps are the app types supported on Windows 10 devices. The file extensions for Windows apps include .msi, .appx, and .appxbundle.  

> [!Note]
> To deploy modern apps, you need at least:
> - For Windows 10 1803, [May 23, 2018—KB4100403 (OS Build 17134.81)](https://support.microsoft.com/help/4100403/windows-10-update-kb4100403).
> - For Windows 10 1709, [June 21, 2018—KB4284822 (OS Build 16299.522)](https://support.microsoft.com/help/4284822).
>
> Only Windows 10 1803 and later support installing apps when there is no primary user associated.
>
> LOB app deployment isn't supported on devices running Windows 10 Home editions.

## Windows 10 LOB apps

You can sign and upload Windows 10 LOB apps to the Intune admin console. These can include modern apps, such as Universal Windows Platform (UWP) apps and Windows App Packages (AppX), as well as Win 32 apps, such as simple Microsoft Installer package files (MSI). The admin must manually upload and deploy updates of LOB apps. These updates are automatically installed on user devices that have installed the app. No user intervention is required, and the user has no control over the updates. 

## Microsoft Store for Business apps

Microsoft Store for Business apps are modern apps, purchased from the Microsoft Store for Business admin portal. They are then synced over to Microsoft Intune for management. The apps can either be online licensed or offline licensed. The Microsoft Store directly manages updates, with no additional action required by the admin. You can also prevent updates to specific apps by using a custom Uniform Resource Identifier (URI). For more information, see [Enterprise app management - Prevent app from automatic updates](https://docs.microsoft.com/windows/client-management/mdm/enterprise-app-management#prevent-app-from-automatic-updates). The user can also disable updates for all Microsoft Store for Business apps on the device. 

### Categorize Microsoft Store for Business apps 
To categorize Microsoft Store for Business apps: 

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
2. Select **Client apps** > **Apps**. Select a Microsoft Store for Business app. Then select **App Information** > **Category**. 
3. Select a category.

## Install apps on Windows 10 devices
Depending on the app type, you can install the app on a Windows 10 device in one of two ways:

- **User Context**: When an app is deployed in user context, the managed app is installed for that user on the device when the user signs in to the device. Note that the app installation doesn't succeed until the user signs in to the device. 
  - Modern line-of-business apps and Microsoft Store for Business apps (both online and offline) can be deployed in user context. The apps support both the Required and Available intents.
  - Win32 apps built as User Mode or Dual Mode can be deployed in user context, and support both the Required and Available intents. 
- **Device Context**: When an app is deployed in device context, the managed app is installed directly to the device by Intune.
  - Only modern line-of-business apps and offline licensed Microsoft Store for Business apps can be deployed in device context. These apps only support the Required intent.
  - Win32 apps built as Machine Mode or Dual Mode can be deployed in device context, and support only the Required intent.

> [!NOTE]
> For Win32 apps built as Dual Mode apps, the admin must choose if the app will function as a User Mode or Machine Mode app for all assignments associated with that instance. The deployment context can't be changed per assignment.  

When an app is deployed in device context, the installation only succeeds when targeted to a device that supports device context. In addition, deploying in device context supports the following conditions:
- If an app is deployed in device context and targeted to a user, the installation fails. The following status and error appears in the admin console:
  - Status: Failed.
  - Error: A user can’t be targeted with a device context install.
- If an app is deployed in device context, but is targeted to a device that doesn't support device context, the installation fails. The following status and error appears in the admin console:
  - Status: Failed.
  - Error: This platform does not support device context installs. 

> [!Note]
> After you save an app assignment with a specific deployment, you can't change the context for that assignment, except for modern apps. For modern apps, you can change the context from user context to device context. 

If there's a conflict in policies on a single user or device, the following priorities apply:
- A device context policy is a higher priority than a user context policy. 
- An install policy is a higher priority than an uninstall policy.

For more information, see [Include and exclude app assignments in Microsoft Intune](apps-inc-exl-assignments.md). For more information about app types in Intune, see [Add apps to Microsoft Intune](apps-add.md).

## Next steps

- [Assign apps to groups with Microsoft Intune](apps-deploy.md)
- [How to monitor apps](apps-monitor.md)
