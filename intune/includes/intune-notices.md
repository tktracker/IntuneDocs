---
title: include file
description: include file
author: ErikjeMS  
ms.service: microsoft-intune
ms.topic: include
ms.date: 11/4/2019
ms.author: erikje
ms.custom: include file
---

These notices provide important information that can help you prepare for future Intune changes and features.

### Plan for Change: Updated experience when enrolling Android Enterprise dedicated devices in Intune<!--5198878-->
With the November or 1911 release to Intune, we’re adding support for SCEP device certificate deployment to Android Enterprise dedicated devices to enable certificate-based access to Wi-Fi profiles. This change also involves some minor changes the flow when enrolling Android Enterprise dedicated devices.

#### How does this affect me?
If you manage Android Enterprise dedicated devices in your environment, you will start to see some changes roll out in November.

- For new Android Enterprise dedicated device enrollments: End users will see a different set of steps on devices during enrollment. Enrollment will still start the way it does today (with QR, NFC, Zero-touch, or device identifier) but after the November service release, there will be a mandatory app install step.
- For existing Android devices enrolled as dedicated devices: Intune will start to automatically install the Microsoft Intune app on devices starting in early November. You don't need to take any action. The app will automatically download and install on devices. 

#### What can I do to prepare for this change?
You should plan to update your end user guidance and let your helpdesk know of this change. Click Additional Information for more details and screenshots. We’ll update our What’s New page when this change starts to roll out.

#### Additional information
[https://aka.ms/Dedicated_devices_enrollment](https://aka.ms/Dedicated_devices_enrollment)

### Plan for Change: The 'Server-side Logging for Siri commands' setting will be removed from the Intune console <!-- 5468501-->

We plan to remove the setting “Server-side logging for Siri commands” from the Intune console with the November update to the Intune service. This change aligns with Apple already having removed the setting on their side.

#### How does this affect me?
When the November update or 1911 rolls out around mid-November, you’ll see that this setting has been removed from the Device restrictions menu (Built-in Apps) for iOS configuration profiles, in the Intune console. It may appear in your policies and the targeted device’s management profile but the setting has no effect on your device. We do not anticipate much impact to functionality since it currently doesn’t work on devices even though you see it in the management profile.

You can choose one of two paths:
- If you wish to delete this setting from your policies, you can go to the profile that has this setting, make a minor edit and save the policy. The policy will recompute in the backend and the setting will be deleted from your policy.
- If you choose not to take this action, end users will see this setting in the management profile of their device but the setting will have no effect.

#### What can I do to prepare for this change?
You can take action according to the section above or leave your policy as is. We’ll update our What’s New page and documentation when this change rolls out.

### End of support for legacy PC management

Legacy PC management is going out of support on October 15, 2020. Upgrade devices to Windows 10 and reenroll them as MDM devices to keep them managed by Intune.

[Learn more](https://go.microsoft.com/fwlink/?linkid=2107122)

### Decreasing support for Android device administrator 
Android device administrator (sometimes referred to "legacy" Android management and released with Android 2.2) is a way to manage Android devices. However, improved management functionality is now available with [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (released with Android 5.0). In an effort to move to modern, richer, and more secure device management, Google is decreasing device administrator support in new Android releases.

#### How does this affect me?
Because of these changes by Google, Intune users will be impacted in the following ways:  
- Intune will only be able to provide support for device administrator-managed Android devices running Android 10 and later (also known as Android Q) through the summer of 2020. This date is when the next major version of Android is expected to be released.   
- Device administrator-managed devices that are running Android 10 or later after the summer of 2020 will no longer be able to be entirely managed.       
- Device administrator-managed Android devices that remain on Android versions below Android 10 will not be impacted and can continue to be entirely managed with device administrator.    
- For all devices running Android 10 and later, Google has restricted the ability for device administrator management agents like Company Portal to access device identifier information. This impacts the following Intune features after a device updates to Android 10 or later:  
    - Network access control for VPN will no longer work.   
    - Identifying devices as corporate-owned with an IMEI or serial number will not automatically mark devices as corporate-owned.  
    - The IMEI and serial number will no longer be visible to IT admins in Intune. 
        > [!NOTE]
        > This only impacts device administrator-managed devices on Android 10 and later and does not affect devices being managed as Android Enterprise. 

#### What do I need to do to prepare for this change?
To avoid the reduction in functionality coming in the summer of 2020, we recommend the following:
- Don't onboard new devices into device administrator management.
- If a device is expected to receive an update to Android 10, migrate it off of device administrator management to Android Enterprise management and/or app protection policies.

#### Additional information
- [Google's guidance for migration from device administrator to Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Google's documentation on the plan to deprecate the device administrator API](https://developers.google.com/android/work/device-admin-deprecation)

### Update your Android Company Portal app to the latest version <!--4536963-->
Intune periodically releases updates to the Android Company Portal app. In November 2018 we released a company portal update, which included a back-end switch to prepare for Google's change from their existing notification platform to Google's Firebase Cloud Messaging (FCM). When Google retires their existing notification platform and moves to FCM, end users will need to have updated their Company Portal app to at least the November 2018 release to continue communicating with the Google Play store.

#### How does this affect me?
Our telemetry indicates you have devices with a Company Portal version earlier than 5.0.4269.0. If this version or later of the Company Portal app is not installed, IT-pro-initiated device actions like wipe, reset password, available and required app installs, and certificate enrollment may not work as expected. If your devices are MDM-enrolled in Intune, then you can see the Company Portal versions and users by going to Client apps – Discovered apps. Selecting earlier versions of the Company Portal app will allow you to see which end users have the devices that haven't updated the Company Portal app.

#### What do I need to do to prepare for this change?
Ask end users of Android devices that have not updated to update the Company Portal app through Google Play. Notify your help desk in case a user has not kept auto-updating the Company Portal app. See the link in *Additional information* for more on Google's FCM platform and change.

#### Additional information
https://firebase.google.com/docs/cloud-messaging/


### New full-screen experience coming to Intune <!--4593669-->
We're rolling out updated create and edit UI experiences to Intune in the Azure portal. This new experience will simplify the existing workflows by using a wizard-style format condensed within one blade. This update will do away with "blade sprawl" or any create and edit flows that require you to drill down into deep blade journeys. The create workflows will also be updated to include assignments (except for app assignment).

#### How does this affect me?
The full-screen experience will be rolled out to Intune both at portal.azure.com and devicemanagement.microsoft.com over the next few months. This update to the UI will not impact functionality of your existing policies and profiles, but you will see a slightly modified workflow. When you create new policies, for example, you will be able to set some assignments as part of this flow instead of doing so after creating the policy. See the blog post at *Additional information* for screenshots of what the new experience will look like in the console.

#### What can I do to prepare for this change?
You do not need to take any action but can consider updating your IT-pro guidance if necessary. We'll update our documentation as this experience rolls out to various blades in Intune on the Azure portal.

#### Additional information 
https://aka.ms/intune_fullscreen

### Plan for change: Intune App SDK and app protection policies for Android moving to support Android 5.0 and higher in an upcoming release <!--4911065 -->
Intune will be moving to support Android 5.x (Lollipop) and higher in an upcoming release. Update any wrapped apps with the latest Intune App SDK and update your devices.

#### How does this affect me?
If you're not using or plan to use either the SDK or APP for Android, this change won't affect you. If you are using the Intune App SDK, be sure to update to the latest version and also update your devices to Android 5.x and higher. If you don't update, apps will not receive updates, and the quality of their experience will diminish over time.

Below find a list of common devices enrolled in Intune that run Android version 4.x. If you have one of these devices, take the appropriate steps to make sure that this device will support Android version 5.0 or higher or that it will be replaced with a device that supports Android version 5.0 or higher. This list is not exhaustive of all devices that may need to be evaluated:

- Samsung SM-T561  
- Samsung SM-T365
- Samsung GT-I9195
- Samsung SM-G800F
- Samsung SM-G357FZ
- Motorola XT1080
- Samsung GT-I9305
- Samsung SM-T231

#### What do I need to do to prepare for this change?
Wrap your apps with the latest Intune App SDK. You may also set the "Require minimum OS version (Warning only)" conditional launch setting to notify end users on personal devices to upgrade.

### Intune plan for change: Nearing end of support for Windows 7<!-- 3042987 -->
As we messaged in MC148476, posted last September 2018, and again in MC176794 back in March 2019, Windows 7 reaches its end of extended support on January 14, 2020. At that time, Intune will retire support for devices running Windows 7 so we can focus our investment on supporting newer technologies and providing great new end-user experiences. After that date, technical assistance and automatic updates that help protect your Windows 7 PC will no longer be available through Intune. Microsoft strongly recommends that you move to Windows 10 before January 2020 to avoid a scenario where you need service or support that is no longer available. Read more about the Windows support lifecycle [here](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

#### How does this affect me?
You are receiving this message because you are currently managing Windows 7 PCs using the legacy Intune PC software agent. Because less than a year remains before the end of Windows 7 extended support, we strongly encourage your organization to begin upgrading to Windows 10 as soon as possible.  

PC management capabilities are built directly into the Windows 10 operating system, and you no longer need to install a client agent such as the Intune software client for Windows 7. Starting with Windows 8.1, Microsoft uses the Mobile Device Management (MDM) architecture to provision, configure, update, and manage Windows PCs. When you have set up Intune, you can simplify Windows enrollment by [enrolling Windows 10 PCs into Intune](..\windows-enroll.md) through the MDM channel. We recommend that you use this "agentless" MDM management solution to manage your Windows 10 PCs.

#### What do I need to do to prepare for this change?
We encourage your organization to immediately consider this action plan:

- Plan and upgrade the Windows 7 fleet to Windows 10 before January 14, 2020.
- Explore [Windows 10 deployment support](https://docs.microsoft.com/windows/deployment/) to learn more about how to upgrade your existing fleet of Windows 7 PCs to Windows 10.
- Review the [Desktop App Assure](https://www.microsoft.com/fasttrack/microsoft-365/desktop-app-assure?rtc=1) offer through FastTrack, which will assist with the Microsoft application compatibility promise.
- Transition existing legacy Intune software client managed devices to the Microsoft-recommended solution to manage Windows 10 using MDM management. Enroll all new Windows 10 PCs using MDM management for Intune in the Azure portal.

See the [blog post here](https://aka.ms/Windows7_Intune) for more information.
