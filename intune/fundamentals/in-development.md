---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 10/07/2019
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

# In development for Microsoft Intune - October 2019

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

### Include another app configuration variable <!-- 4969237  -->
When creating an app configuration policy, you'll be able to include the `AAD Device ID` configuration variable as part of your configuration settings. 

To add the `AAD Device ID` configuration variable:
1. In Intune, select **Client apps** > **App configuration policies** > **Add**. 
1. Enter your configuration policy details.
1. To view the **Configuration settings** blade, select **Configuration settings**.

### Apply dark mode in iOS Company Portal <!-- 4911422  -->
Dark mode is planned for iOS Company Portal. You'll be able to download company apps, manage your devices, and get IT support in the color scheme of your choice. For more information about iOS Company Portal, see [How to configure the Microsoft Intune Company Portal app](../apps/company-portal-app.md).

### Prevent installation of apps from unknown sources on Android Enterprise devices <!-- 4760025  -->
On Android Enterprise work profile devices, end users can never install apps from unknown sources on the work profile. You'll be able to choose to extend this restriction to the personal profile as well. If you enable this restriction, end users on Android Enterprise work profile devices won't be able to side-load apps from unknown sources onto the personal side of their device. 

### Use an updated app protection UI and iOS app provisioning UI <!-- 4102027, 4102029  -->
We'll update the UI to create and edit app protection policies (APP) and iOS app provisioning profiles in Intune. The UI changes include:
- A simplified experience that uses a wizard-style format on one blade. 
- An update to the create flow to include assignments.
- A summary. When you view properties before you create a new policy or when you edit a property, you'll see a summary page of all settings. Also, when you edit properties, the summary will list only items from the category of properties you're editing.

### Create groups of management objects called policy sets <!-- 3762880  -->
You'll be able to use *policy sets* to create a bundle of references to existing management entities that need to be identified, targeted, and monitored as a single conceptual unit. Policy sets don't replace existing concepts or objects. Admins can continue to assign individual objects as they do today. Policy sets reference individual objects. Therefore, any changes to those individual objects will be reflected in the policy set. 

To create a policy set in Intune, you'll select **Policy sets** > **Create**. 

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

### Assign the Microsoft Edge beta for macOS <!-- 4678761  -->
You'll be able to add and assign the latest version of the Microsoft Edge beta to Intune for macOS devices. 

To assign the Microsoft Edge beta for macOS devices:
1. In Intune, select **Client apps** > **Apps** > **Add app** > **Microsoft Edge - macOS**. 
1. Assign the Microsoft Edge beta to the intended groups. Microsoft AutoUpdate (MAU) keeps Microsoft Edge up to date. 
 
For more information about Microsoft Edge, see [Manage web access by using Microsoft Edge with Microsoft Intune](../apps/manage-microsoft-edge.md).

### Configure app notification content for organization accounts <!-- 2576686 -->
Intune APP on Android and iOS devices will allow you to control app notification content for organization accounts. This feature will require support from applications and might not be available for all APP-enabled applications. For more information about APP, see [What are app protection policies?](../apps/app-protection-policy.md)

### Available Google Play app reporting for Android work profiles <!-- 3041956  -->
For available app installations on Android work profile devices, you can view the app installation status and the installed version of managed Google Play apps. For more information, see [How to monitor app protection policies](../apps/app-protection-policies-monitor.md), [Manage Android work profile devices with Intune](../enrollment/android-enterprise-overview.md), and [Managed Google Play app types](../apps/apps-add-android-for-work.md#managed-google-play-app-types).

<!-- ***********************************************-->
## Device configuration


### New device configuration settings for supervised iOS and iPadOS devices <!-- 5199328  -->
On iOS and iPadOS devices, you can create a profile to restrict features and settings on devices:

1. Select **Device configuration** > **Profiles** > **Create profile**.
1. For the platform, select **iOS/iPadOS**.
1. For the profile type, select **Device restrictions**.

You'll be able to control new settings: 
- Access the network drive in the Files app.  
- Access the USB drive in the Files app. 
- Keep Wi-Fi on. 

For information about the current settings, see [iOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-ios.md).

The new settings apply to:
- iOS 13.0 and newer.
- iPadOS 13.0 and newer.

### Removal of automatic connection in Wi-Fi profiles on Android and Android Enterprise <!-- 5021055  -->
On Android and Android Enterprise devices, you can create a Wi-Fi profile to configure different settings: 

1. Select **Device configuration** > **Profiles** > **Create profile**.
1. For the platform, select **Android** or **Android Enterprise**.
1. For the profile type, select **Wi-Fi**. 

The **Connect automatically** setting will be removed because it's [not supported by Android](https://developer.android.com/reference/android/net/wifi/WifiManager.html#enableNetwork%28int%2c%20boolean%29).

If you use this setting in a Wi-Fi profile, you might notice that **Connect automatically** doesn't work. You don't need to take any action, but be aware that this setting will be removed from the Intune user interface.

For information about the current settings, go to [Android Wi-Fi settings](../configuration/wi-fi-settings-android.md) or [Android Enterprise Wi-Fi settings](../configuration/wi-fi-settings-android-enterprise.md).

The removal of this setting applies to:
- Android.
- Android Enterprise.

### Global HTTP proxy on Android Enterprise devices <!-- 4816339  -->
On Android Enterprise devices, you'll be able to configure a global HTTP proxy to meet your organization's web browsing standards:

1. Select **Device configuration** > **Profiles** > **Create profile**.
1. For the platform, select **Android Enterprise**.
1. Select **Device owner**.
1. For the profile type, select **Device restrictions**. 
1. Select **Connectivity**. 
 
After you configure the proxy, all HTTP traffic will use it. This feature applies to Android Enterprise devices that are in device-owner mode.

### New device firmware configuration interface profile for devices that run Windows 10 and later <!-- 2266073  -->
On Windows 10 and later, you can create a device configuration profile to control settings and features: 

1. Select **Device configuration** > **Profiles** > **Create profile**.
1. For the platform, select **Windows 10 and later**. 
 
A new device firmware configuration interface profile type will allow Intune to manage UEFI (BIOS) settings.

For information about the current settings you can configure, see [Apply features and settings on your devices by using device profiles in Microsoft Intune](../configuration/device-profiles.md).

This feature applies to Windows 10 RS5 (1809) and later, on select devices.

### PKCS certificates for macOS  <!-- 1333650                -->
We'll add full support for Public Key Cryptography Standards (PKCS) certificates on devices that run macOS. Users will be able to deploy user and device certificates with fields for **Customization subject** and **Subject alternative name**. 

We'll also have a new setting called **Allow All Apps Access**. Enable this setting to give all associated apps access to the private key. For more information about this setting, see [Configuration profile reference](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf) on Developer.Apple.com.

### Derived credentials to provision mobile devices with certificates      <!--  1736036, 1736037, 1772050      --> 
We'll add support for derived credentials, which support the *National Institute of Standards and Technology (NIST) 800-157* standard for deploying certificates to devices.  Derived credentials rely on the use of a personal identity verification (PIV) or common access card (CAC), like a smart card. Users authenticate by using their smart card on a computer. They then request a certificate for their managed device by following the process that the derived credential provider requires.   

The process to use derived credentials to get a certificate is different from processes that use SCEP or PKCS certificate profiles. But the result is the same: mobile devices that have authentication certificates that can be used for app authentication, VPN, Wi-Fi, or email profiles. For more information, see [Derived PIV credentials](https://www.nccoe.nist.gov/projects/building-blocks/piv-credentials) on NCCOE.NIST.gov.

The initial release of derived credentials will support Entrust Datacard, Intercede, and DISA Purebred on iOS. Additional platforms and derived credential providers will be supported in later releases.   

<!-- ***********************************************-->
## Device enrollment

### Specify which Android device OS versions enroll through the work profile and which enroll through the device administrator <!-- 4350697 -->
By using Intune device type restrictions, you'll be able to use a device's OS version to specify whether it will use Android Enterprise work profile enrollment or Android device administrator enrollment. To do so, in Intune, select **Device enrollment** > **Enrollment restrictions** > **Create restriction** > **Device type restriction** > **Platform settings**.

### Edit the device name value for Autopilot devices <!-- 4816775 -->
You'll be able to edit the **Device Name** value for Azure AD Joined Autopilot devices:

1. Select **Intune** > **Device enrollment** > **Windows enrollment** > **Windows Autopilot** > **Devices**.
1. Choose the device.
1. In the pane on the right, change the **Device Name** value.
1. Select **Save**.

### For iOS devices, customize the enrollment privacy window of Company Portal <!-- 4394993  -->
By using Markdown, you'll be able to customize the Company Portal privacy window that end users see during iOS enrollment. Specifically, you can customize the list of things that your organization can't see or do on the device.

<!-- ***********************************************-->
## Device management


### Edit the Group Tag value for Autopilot devices<!-- 4816775 -->
You'll be able to edit the **Group Tag** value for Autopilot devices:

1. Select **Intune** > **Device enrollment** > **Windows enrollment** > **Windows Autopilot** > **Devices**.
1. Choose the device.
1. In the pane on the right, change the **Group Tag** value.
1. Select **Save**.

### UI update for creating and editing Windows 10 update rings  <!-- 4099089          -->   
We'll roll out updated create and edit UI experiences for Windows 10 update rings. The new UI will:  
- Simplify the existing experience by using a wizard-style format on one blade. This UI update will eliminate blade sprawl that requires IT pros to take deep blade journeys.   
- Revise the create flow to include assignments.  
- Add a summary page. The summary will include all settings when you're viewing properties, when you're preparing to create an update ring, and when you're editing a property. When you're editing, the summary will list only the items within the category of properties you're editing.

### UI update for creating and editing iOS software updates  <!-- 4099090        -->   
We'll roll out updated create and edit UI experiences for iOS software updates to Intune. The new UI will:
- Simplify the existing experience by using a wizard-style format on one blade. This UI update will eliminate blade sprawl that requires IT pros to take deep blade journeys.  
- Include assignments in the iOS software update policy create flow. 
- Include a summary page in the iOS software update policy. The summary will include all settings when you're viewing properties, when you're preparing to create a policy, and when you're editing a property. When you're editing, the summary will list only the items within the category of properties you're editing.

### Target macOS user groups to require Jamf management <!-- 4061739 -->
You'll be able to target specific groups of users to require their macOS devices to be managed by Jamf. This targeting will enable you to apply the Jamf compliance integration to a subset of macOS devices while other devices continue to be managed by Intune. Targeting will also let you gradually migrate users' devices from one mobile device management (MDM) system to the other.

### New restrictions for renaming Windows devices <!-- 3478938 -->
Device names will have to follow these rules:
- 15 characters or fewer (fewer than or equal to 63 bytes, not including a trailing NULL)
- No null or empty strings
- Allowed ASCII: letters (a-z, A-Z), numbers (0-9), and hyphens
- Allowed Unicode: characters >= 0x80, valid UTF8, mappable by IDN (RtlIdnToNameprepUnicode succeeds; see RFC 3492)
- Names must not contain only numbers or start with a number
- No spaces in the name
- Disallowed characters: { | } ~ [ \ ] ^ ' : ; < = > ? & @ ! " # $ % ` ( ) + / , . _ *

### Deploy software updates to macOS devices <!-- 3194876 -->
You'll be able to deploy software updates to groups of macOS devices. This feature includes critical, firmware, configuration file, and other updates. You can send updates on the next device check-in. Or you can select a weekly schedule to deploy updates in or out of periods that you set. 

This feature helps when you want to update devices outside standard work hours or outside hours when your help desk is fully staffed. You'll also get a detailed report of all macOS devices that have updates deployed. You can drill into the report by device to see the status of a particular update.

<!-- ***********************************************-->
## Monitoring and troubleshooting

### Android report on the Devices overview page <!-- 2984353  -->
We'll add a new report to the **Devices overview** page. The report displays how many Android devices have been enrolled in each device management solution. The chart shows device counts for work profile, fully managed, dedicated, and device-administrator enrolled. 

To see the report, choose **Intune** > **Devices** > **Overview**.

### Windows Autopilot deployment reports <!-- 3856172  -->
A new report will detail each device deployed through Windows Autopilot. This data will be available for 30 days after deployment. 

To see the report, go to **Intune** > **Device enrollment** > **Monitor** > **Autopilot deployments**.

### Updated support experience   <!--  5012398    -->
As part of continuing improvements, we'll update the in-console support experience for Intune.  We'll improve the in-console search and feedback for common issues, and we'll streamline the workflow to contact support.     

<!-- ***********************************************-->
<!--## Security-->


<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also
For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
