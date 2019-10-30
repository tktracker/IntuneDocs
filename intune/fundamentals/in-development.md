---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 10/28/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1

# optional metadata

#audience:
#ms.devlang:
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# In development for Microsoft Intune - November 2019

To help in your readiness and planning, this page lists Intune UI updates and features that are in development but not yet released. In addition to the information on this page:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in Office message center.
- When a feature enters production, whether it's a preview or generally available, the feature description will move from this page to [What's new](whats-new.md).
- This page and the [What's new](whats-new.md) page are updated periodically. Check back for additional updates.
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

> [!NOTE]
> This page reflects our current expectations about Intune capabilities in a future release. Dates and individual features might change. This page doesn't describe all features in development.

**RSS feed**: Find out when this page is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## App management

### S/MIME support for Microsoft Outlook Mobile <!-- 2669398  -->
Intune will support delivering S/MIME signing and encryption certificates that can be used with Outlook Mobile on iOS and Android. For related information, see [email settings for iOS devices](~/configuration/email-settings-ios.md) and [e-mail settings for Android devices](~/configuration/email-settings-android.md).

### Custom settings support for macOS applications <!-- 4736278  -->
Intune will support custom settings, allowing you to add specific keys and values to an existing preferences property list (.plist) file to configure macOS apps and the device. Not all apps support managed preferences, and in some cases only specific settings can be managed. The settings are deployed via the device channel only. You should only upload property list files or .xml files that target device channel settings.

### Assignment type value in Windows Company Portal <!-- 5459950  -->
The **Installed Apps** page of the Windows Company Portal app will be updated. The **Assignment type** column of the **Installed Apps** page has been updated to be called "Required by your organization". Possible values are **Yes** or **No** to designate required vs. available apps. This change is being made in response to some end user confusion. For more information about the Windows Company portal, see [How to configure the Microsoft Intune Company Portal app](~/apps/company-portal-app.md).

### Run Win32 apps on Windows 10 S-mode devices <!-- 3747604  --> 
You'll be able to install and run Win32 apps on devices that are managed in Windows 10 S mode. Create one or more supplemental policies for S mode by using the Windows Defender Application Control (WDAC) PowerShell tools. Use the Device Guard signing portal to sign the supplemental policies. Then upload and distribute the policies through Intune. 

In Intune, you'll find this capability by selecting **Client apps** > **Windows 10 S supplemental policies**. 

### Set app availability based on a date and time <!-- 3510685  -->
As an admin, you'll be able to configure the start time and deadline for a required app. At the start time, the Intune management extension will download the app content and cache it. The app will be installed at the deadline time. For available apps, the start time will dictate when the app is visible in Company Portal. 

To set app availability based on date and time:

1. In Intune, select **Client apps** > **Apps**. 
1. Select an app from the list or add a new one by selecting **Add**. 
1. From the app blade, select **Assignments** > **Add group**. 
1. Set the **Assignment type** to **Required** and then select **Included Groups**. 
1. Set **Make this app required for all users** to **Yes**. 
1. Select **Edit** to modify the **End user experience** options. 
1. On the **End user experience** blade, set the **Software available time** as needed. 

For more information, see [Add apps to Microsoft Intune](../apps/apps-add.md).

### Require Win32 apps to restart <!-- 3136567  -->
You'll be able to require a Win32 app to restart after a successful installation. You can choose the amount of time (the grace period) before the restart.

### Display notifications for the Company Portal app on Windows <!-- 1808082  -->
We'll update the Company Portal app on Windows devices to display toast notifications to users, even when the application is closed. The update will show notifications for available apps only when the installation status is completed or failed. The Company Portal app won't show notifications for required applications.

### Display installation status messages for the Company Portal app <!-- 2514416  -->
The Company Portal app will show additional app installation status messages to end users. The following conditions will apply to new Win32 dependency features:
- App failed to install. Dependencies defined by the admin were not met.
- App installed successfully but requires a restart.
- App is in the process of installing but requires a restart to continue.

### Configure app notification content for organization accounts <!-- 2576686 -->
Intune APP on Android and iOS devices will allow you to control app notification content for organization accounts. This feature will require support from applications and might not be available for all APP-enabled applications. For more information about APP, see [What are app protection policies?](../apps/app-protection-policy.md)


<!-- ***********************************************-->
## Device configuration

### Use PKCS certificates with Wi-Fi profiles on Windows 10 and later devices <!-- 3246388  -->
Currently, you can authenticate Windows Wi-Fi profiles with SCEP certificates (**Device configuration** > **Profiles** > **Create profile** > **Windows 10 and later** for platform > **Wi-Fi** for profile type > **Enterprise** > **EAP type**). You'll be able use PKCS certificates with your Windows Wi-Fi profiles. This feature allows users to authenticate Wi-Fi profiles using new or existing PKCS certificate profiles in your tenant. 

For more information on Wi-Fi profiles, see [Add Wi-Fi settings for Windows 10 and later devices in Intune](../configuration/wi-fi-settings-windows.md).

Applies to:
- Windows 10 and later

### New ExchangeActiveSync settings when creating an Email device configuration profile on iOS devices <!-- 4892824  --> 
On iOS/iPadOS devices, you can configure email connectivity in a device configuration profile (**Device configuration** > **Profiles** > **Create profile** > **iOS/iPadOS** for platform > **Email** for profile type). 

There will be new ExchangeActiveSync settings available, including:
- Choose the services to sync (or block syncing), such as email, calendar, and contacts.
- Allow (or block) users to change the sync settings for these services on their devices. 

To see the current settings, go to [Email profile settings for iOS devices in Intune](../configuration/email-settings-ios.md).

Applies to:
- iOS 13.0 and newer
- iPadOS 13.0 and newer

### Prevent users from adding personal Google accounts to Android Enterprise device owner and dedicated devices <!-- 5353228  -->
You'll be able to prevent users from creating personal Google accounts on Android Enterprise device owner and dedicated devices (**Device configuration** > **Profiles** > **Create profile** > **Android Enterprise** for platform > **Device Owner Only > Device Restrictions** for profile type > **Users and Accounts settings**).

To see the current settings you can configure, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android Enterprise device owner
- Android Enterprise dedicated devices

### Server-side logging for Siri commands setting is removed in iOS device restrictions profile <!-- 5468501  -->
On iOS devices, you can create a device restrictions profiles that configures server-side logging for Siri commands (**Device configuration** > **Profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile type > **Built-in apps**). The **Server-side logging for Siri commands** setting will be removed.

This setting will be removed from the Intune admin console. This setting has no effect on the device even though existing policies that have this setting configured will continue to show the setting. If you want to remove the setting from existing policies, go to the policy, make a minor edit, save it, and the policy will be updated.

To see the settings you can configure, see [iOS and iPadOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-ios.md).

Applies to:
- iOS


<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## Device management

### Edit device name value for Autopilot devices<!-- 2640074  -->
You'll be able to edit the Device Name value for Azure AD Joined Autopilot devices. To do so, go to **Intune** > **Device enrollment** > **Windows enrollment** > **Windows Autopilot** > **Devices** > choose the device > change the **Device Name** value in the right pane > **Save**.


### Edit the Group Tag value for Autopilot devices<!-- 4816775 -->
You'll be able to edit the **Group Tag** value for Autopilot devices:

1. Select **Intune** > **Device enrollment** > **Windows enrollment** > **Windows Autopilot** > **Devices**.
1. Choose the device.
1. In the pane on the right, change the **Group Tag** value.
1. Select **Save**.

### Target macOS user groups to require Jamf management <!-- 4061739 -->
You'll be able to target specific groups of users to require their macOS devices to be managed by Jamf. This targeting will enable you to apply the Jamf compliance integration to a subset of macOS devices while other devices continue to be managed by Intune. Targeting will also let you gradually migrate users' devices from one mobile device management (MDM) system to the other.

<!-- ***********************************************-->
## Intune apps

### Improved macOS enrollment experience in Company Portal <!-- 5074349  -->
The Company Portal for macOS enrollment experience will have a simpler enrollment process that will align more closely with the Company Portal for iOS enrollment experience. Device users will see:  

* A sleeker user interface.  
* An improved enrollment checklist.  
* Clearer instructions about how to enroll their devices.  
* Improved troubleshooting options.  

### Improved checklist design in Company Portal app for Android<!-- 5550857  -->
The setup checklist in the Company Portal app for Android will be updated with a lightweight design and new icons. The changes will align with the recent updates made to the Company Portal app for iOS.

<!-- ***********************************************-->
## Monitoring and troubleshooting

### Updated support experience   <!--  5012398    -->
As part of continuing improvements, we'll update the in-console support experience for Intune.  We'll improve the in-console search and feedback for common issues, and we'll streamline the workflow to contact support.     

<!-- ***********************************************-->
## Role-based access control

### Duplicate custom or built-in roles <!-- 1081938 -->
You'll be able to copy built-in and custom roles. To do so, go to **Intune** > **Roles** > **All roles** > choose a role in the list > **Duplicate**. Make sure to enter a new Name that is unique.

<!-- ***********************************************-->

## Security

### BitLocker key rotation     <!-- 2564951      -->
You'll be able to use Intune to rotate the BitLocker recovery keys for managed devices that run Windows version 1909 or later. 

<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also
For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
