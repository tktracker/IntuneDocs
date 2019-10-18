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

### Apply dark mode in iOS Company Portal <!-- 4911422  -->
Dark mode is planned for iOS Company Portal. You'll be able to download company apps, manage your devices, and get IT support in the color scheme of your choice. For more information about iOS Company Portal, see [How to configure the Microsoft Intune Company Portal app](../apps/company-portal-app.md).

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


<!-- ***********************************************-->
## Device configuration

### New device firmware configuration interface profile for devices that run Windows 10 and later <!-- 2266073  -->
On Windows 10 and later, you can create a device configuration profile to control settings and features: 

1. Select **Device configuration** > **Profiles** > **Create profile**.
1. For the platform, select **Windows 10 and later**. 
 
A new device firmware configuration interface profile type will allow Intune to manage UEFI (BIOS) settings.

For information about the current settings you can configure, see [Apply features and settings on your devices by using device profiles in Microsoft Intune](../configuration/device-profiles.md).

This feature applies to Windows 10 RS5 (1809) and later, on select devices.
 

<!-- ***********************************************-->
## Device enrollment

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

### Target macOS user groups to require Jamf management <!-- 4061739 -->
You'll be able to target specific groups of users to require their macOS devices to be managed by Jamf. This targeting will enable you to apply the Jamf compliance integration to a subset of macOS devices while other devices continue to be managed by Intune. Targeting will also let you gradually migrate users' devices from one mobile device management (MDM) system to the other.

### Deploy software updates to macOS devices <!-- 3194876 -->
You'll be able to deploy software updates to groups of macOS devices. This feature includes critical, firmware, configuration file, and other updates. You can send updates on the next device check-in. Or you can select a weekly schedule to deploy updates in or out of periods that you set. 

This feature helps when you want to update devices outside standard work hours or outside hours when your help desk is fully staffed. You'll also get a detailed report of all macOS devices that have updates deployed. You can drill into the report by device to see the status of a particular update.

<!-- ***********************************************-->
## Monitoring and troubleshooting

### Android report on the Devices overview page <!-- 2984353  -->
We'll add a new report to the **Devices overview** page. The report displays how many Android devices have been enrolled in each device management solution. The chart shows device counts for work profile, fully managed, dedicated, and device-administrator enrolled. 

To see the report, choose **Intune** > **Devices** > **Overview**.

### Updated support experience   <!--  5012398    -->
As part of continuing improvements, we'll update the in-console support experience for Intune.  We'll improve the in-console search and feedback for common issues, and we'll streamline the workflow to contact support.     

<!-- ***********************************************-->
<!--## Security-->


<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also
For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
