---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 11/19/2019
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

# In development for Microsoft Intune - December 2019

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

### iOS user-licensed VPP apps<!-- 5619268 idready -->
For User Enrollment iOS devices, end-users will no longer be presented with device-licensed VPP applications deployed as available. However, end-users will continue to see all user-licensed VPP apps within the Company Portal. For more information about VPP apps, see [How to manage iOS and macOS apps purchased through Apple Volume Purchase Program with Microsoft Intune](~/apps/vpp-apps-ios.md).

### Retrieve personal recovery key from MEM encrypted macOS devices<!-- 4851745 idready -->
End-users will be able to retrieve their personal recovery key (FileVault key) using the iOS Company Portal app. The device that has the personal recovery key must be enrolled with Intune and encrypted with FileVault through Intune. Using the iOS Company Portal app, an end-user can open the Safari web view and retrieve their personal recovery key. In Intune, select **Devices** > *the encrypted and enrolled macOS device* > **Get recovery key**. For more information about FileVault, see [FileVault encryption for macOS](~/protect/encrypt-devices.md#filevault-encryption-for-macos).

### Microsoft app icons update<!--4677605-->
The icons used for Microsoft apps in the app targeting pane for App protection policies and App configuration policies will be updated.

### S/MIME support for Microsoft Outlook Mobile<!-- 2669398  -->
Intune will support delivering S/MIME signing and encryption certificates that can be used with Outlook Mobile on iOS and Android. For related information, see [email settings for iOS devices](~/configuration/email-settings-ios.md) and [e-mail settings for Android devices](~/configuration/email-settings-android.md).

### Custom settings support for macOS applications<!-- 4736278  -->
Intune will support custom settings, allowing you to add specific keys and values to an existing preferences property list (.plist) file to configure macOS apps and the device. Not all apps support managed preferences, and in some cases only specific settings can be managed. The settings are deployed via the device channel only. You should only upload property list files or .xml files that target device channel settings.

### Display notifications for the Company Portal app on Windows<!-- 1808082  -->
We'll update the Company Portal app on Windows devices to display toast notifications to users, even when the application is closed. The update will show notifications for available apps only when the installation status is completed or failed. The Company Portal app won't show notifications for required applications.

### Display installation status messages for the Company Portal app<!-- 2514416  -->
The Company Portal app will show additional app installation status messages to end users. The following conditions will apply to new Win32 dependency features:
- App failed to install. Dependencies defined by the admin were not met.

### Configure app notification content for organization accounts<!-- 2576686 -->
Intune APP on Android and iOS devices will allow you to control app notification content for organization accounts. This feature will require support from applications and might not be available for all APP-enabled applications. For more information about APP, see [What are app protection policies?](../apps/app-protection-policy.md)

<!-- ***********************************************-->
## Device configuration

### Block users from configuring certificate credentials in the managed keystore on Android Enterprise device owner devices<!-- 3311998 idready -->
On Android Enterprise device owner devices, there'll be a new setting to block users from configuring their certificate credentials in the managed keystore (**Device configuration** > **Profiles** > **Create profile** > **Android Enterprise** for platform > **Device Owner Only > Device Restrictions** for profile type > **Users + Accounts**).

To see the current settings, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android Enterprise device owner, including dedicated and fully managed devices

### Wired network device configuration profiles for macOS devices<!-- 3508686 idready -->
On macOS devices, a future update will include a new device configuration profile that configures wired networks (**Device configuration** > **Profiles** > **Create profile** > **macOS** for platform > **Wired Network** for profile type). Use this feature to create 802.1x profiles to manage wired networks, and deploy these wired networks to your macOS devices.

Applies to:
- macOS

### Add automatic proxy settings to Wi-Fi profiles for Android Enterprise work profiles<!-- 4490822 idready -->
On Android Enterprise Work Profile devices, you can create Wi-Fi profiles. When you choose the Wi-Fi Enterprise type, you can also enter the Extensible Authentication Protocol (EAP) type used on your Wi-Fi network.

In a future update, when you choose the Enterprise type, you'll be able to enter automatic proxy settings, including a proxy server URL, such as `proxy.contoso.com`.

To see the current Wi-Fi settings you can configure, go to [Add Wi-Fi settings for devices running Android Enterprise and Android kiosk in Microsoft Intune](../configuration/wi-fi-settings-android-enterprise.md).

Applies to:
- Android Enterprise work profile

### Enable network access control (NAC) with Cisco AnyConnect VPN on iOS devices<!-- 4860111 idready -->
On iOS devices, you can create a VPN profile, and use different connection types, including Cisco AnyConnect (**Device configuration** > **Profiles** > **Create profile** > **iOS** for platform > **VPN** for profile type > **Cisco AnyConnect** for connection type). 

In a future update, you'll be able to enable network access control (NAC) with Cisco AnyConnect. To use this feature:

1. At [Cisco Identity Services Engine Administrator Guide](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html), use the steps in **Configuring Microsoft Intune as an MDM Server** to configure the Cisco Identity Services Engine (ISE) in Azure.
2. In the Intune device configuration profile, select the **Enable Network Access Control (NAC)** setting.

To see all the available VPN settings, go to [Configure VPN settings on iOS devices](../configuration/vpn-settings-ios.md).

Applies to:
- iOS

### Updated single sign-on experience for apps and websites on your iOS, iPadOS, and macOS devices<!-- 4999578 idready -->
Intune is adding more single sign-on settings for iOS, iPadOS, and macOS devices. Currently, you can configure credential SSO app extensions and Apple's built-in Kerberos extension in Intune. In a future update, you'll be able to configure redirect SSO app extensions written by your organization or by your identity provider. 

Use these settings to configure a seamless single sign-on experience for apps and websites that use modern authentication methods, such as OAuth and SAML2. 

To see the SSO app extension settings you can configure, go to [SSO on iOS](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) and [SSO on macOS](../configuration/macos-device-features-settings.md#single-sign-on-app-extension).

Applies to:
- iOS/iPadOS
- macOS

### Require use of approved keyboards on Android<!--4761794 IDready -->
You'll be able to specify a list of approved keyboards for use in managed Android apps. From the managed app, the user will be prompted to switch to one of the approved keyboards already installed on their device or, if needed, they will be directed to the Google Play Store to download and set-up one of the approved keyboards. The user will only be able to edit text fields in a managed app if their active keyboard is one of the approved keyboards.

### Use PKCS certificates with Wi-Fi profiles on Windows 10 and later devices<!-- 3246388  -->
Currently, you can authenticate Windows Wi-Fi profiles with SCEP certificates (**Device configuration** > **Profiles** > **Create profile** > **Windows 10 and later** for platform > **Wi-Fi** for profile type > **Enterprise** > **EAP type**). You'll be able use PKCS certificates with your Windows Wi-Fi profiles. This feature allows users to authenticate Wi-Fi profiles using new or existing PKCS certificate profiles in your tenant. 

For more information on Wi-Fi profiles, see [Add Wi-Fi settings for Windows 10 and later devices in Intune](../configuration/wi-fi-settings-windows.md).

Applies to:
- Windows 10 and later

### New ExchangeActiveSync settings when creating an Email device configuration profile on iOS devices<!-- 4892824  --> 
On iOS/iPadOS devices, you can configure email connectivity in a device configuration profile (**Device configuration** > **Profiles** > **Create profile** > **iOS/iPadOS** for platform > **Email** for profile type). 

There will be new ExchangeActiveSync settings available, including:
- Choose the services to sync (or block syncing), such as email, calendar, and contacts.
- Allow (or block) users to change the sync settings for these services on their devices. 

To see the current settings, go to [Email profile settings for iOS devices in Intune](../configuration/email-settings-ios.md).

Applies to:
- iOS 13.0 and newer
- iPadOS 13.0 and newer

### Prevent users from adding personal Google accounts to Android Enterprise device owner and dedicated devices<!-- 5353228  -->
You'll be able to prevent users from creating personal Google accounts on Android Enterprise device owner and dedicated devices (**Device configuration** > **Profiles** > **Create profile** > **Android Enterprise** for platform > **Device Owner Only > Device Restrictions** for profile type > **Users and Accounts settings**).

To see the current settings you can configure, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android Enterprise device owner
- Android Enterprise dedicated devices

### Server-side logging for Siri commands setting is removed in iOS device restrictions profile<!-- 5468501  -->
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

### Target macOS user groups to require Jamf management<!-- 4061739 -->
You'll be able to target specific groups of users to require their macOS devices to be managed by Jamf. This targeting will enable you to apply the Jamf compliance integration to a subset of macOS devices while other devices continue to be managed by Intune. Targeting will also let you gradually migrate users' devices from one mobile device management (MDM) system to the other.

<!-- ***********************************************-->
## Intune apps

### Improved macOS enrollment experience in Company Portal<!-- 5074349  -->
The Company Portal for macOS enrollment experience will have a simpler enrollment process that will align more closely with the Company Portal for iOS enrollment experience. Device users will see:  

* A sleeker user interface.  
* An improved enrollment checklist.  
* Clearer instructions about how to enroll their devices.  
* Improved troubleshooting options.  

<!-- ***********************************************-->
## Monitoring and troubleshooting

### Centralized audit logs<!--5603185, 5697164-->
A new centralized audit log experience will collect audit logs for all categories into one page. You'l be able to filter the logs to get the data you're looking for. To see the audit logs, go to **Tenant administration** > **Audit logs**. For more information, see [Upcoming change to Audit logs in Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Upcoming-change-to-Audit-logs-in-Intune/ba-p/1015858).

<!-- ***********************************************-->
## Role-based access control

### Duplicate custom or built-in roles<!-- 1081938 -->
You'll be able to copy built-in and custom roles. To do so, go to **Intune** > **Roles** > **All roles** > choose a role in the list > **Duplicate**. Make sure to enter a new Name that is unique.

<!-- ***********************************************-->

## Security

### Use PKCS certificate profiles to provision devices with certificates<!-- 2317124, 2317130, 2317139, 2340517, 2340528, 2340529 IDready -->
You’ll be able to use a PKCS certificate profile to issue certificates to devices, expanding on our current support for user-based certificates. Device-based certificates will be supported the Android, iOS, and Windows platforms, and can be used for Wi-Fi and VPN profiles.

<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also
For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).


