---
# required metadata

title: Intune actions and options supported with Apple User Enrollment
titleSuffix: Microsoft Intune
description: Learn which Intune actions and options are supported with Apple User Enrollment
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/2/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Intune actions and options supported with Apple User Enrollment

User Enrollment supports a subset of device management options. If a pre-existing configuration profile is applied to a User Enrollment device, only settings supported by User Enrollment will be applied to that device.

## Password settings

On User Enrollment devices, if you configure any password setting, then the **Simple passwords** settings is automatically set to **Block**, and a 6 digit PIN is enforced.

For example, you configure the **Password expiration** setting, and push this policy to user-enrolled devices. On the devices, the following happens:
- The **Password expiration** setting is ignored.
- Simple passwords, such as `1111` or `1234`, aren't allowed.
- A 6 digit pin is enforced.

## Administrator remote device actions and options
Admins can perform the following actions and options on User Enrollment devices:
- Retire
- Delete
- Remote Lock
- Sync

All other actions aren't supported.

## End-user actions
On User Enrollment devices, end users can perform these actions on their devices from the Company Portal application and website:
- Rename. This action applies only to the user-facing name within the Company Portal. It won’t fully rename the device outside of that context.
- Remove
- Remote Lock
- Check Status

## Other supported options

The following options are supported in Intune for devices enrolled by using Apple User enrollment:
- Per-App VPN. This support excludes Safari Domains as User Enrollment doesn't support configuring Safari settings.
- WiFi 
- Corporate app removal upon unenrollment
- App deployment via User-licensed Volume Purchasing Plan (VPP )
- Jailbreak Detection

The following restrictions are supported:
- View corporate documents in unmanaged apps
- Viewing non-corporate documents in corporate apps
- Allow unmanaged apps to read from managed contacts accounts
- AirDrop as an unmanaged destination
- Required encrypted backup
- Managed apps sync to cloud
- Control Center access while device locked
- Notification Center access while device locked
- Today view while device locked
- Block screenshots
- Block Enterprise Book backup
- Block Enterprise Book metadata sync
- Require encrypted backup
- Require watch wrist detection
- Block Siri
- Block Siri while device is locked
- Require Safari fraud warnings
- Block diagnostics submission to Apple


## Options not supported
The following options aren't supported on devices enrolled with User Enrollment. If you need these options, check out Device Enrollment for personally-owned devices or Automated Device Enrollment for corporate devices.
- Collect app inventory for apps outside of the managed APFS volume.
- Collect inventory of certificates and provisioning profiles outside of the managed APFS volume.
- Collect UDID and other persistent device identifiers.
- User Enrollment supports a unique enrollment ID for each device enrolled, but this ID doesn't persist after unenrollment.
- The following Intune features aren't supported because of this limitation:
- SCEP User profiles with Subject Name Format of Serial Numbe.r
- Device-level VPN.
- Device-licensed VPP app deployment.
- MDM control of applications outside of the managed APFS volume.
- Application Protection Policies will still apply to these apps. However, you won’t be able to take over management or deploy a managed version of these apps unless the user deletes them from their device.
- Actions, configurations, settings, and commands requiring supervision. 

## Next steps

[Set up iOS and iPadOS User Enrollment](ios-user-enrollment.md)