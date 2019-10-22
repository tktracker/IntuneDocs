---
# required metadata

title: Enable the Mobile Threat Defense connector for unenrolled devices
titleSuffix: Microsoft Intune
description: Enable the Mobile Threat Defense connector in Microsoft Intune for unenrolled devices.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: M365-identity-device-management
---

# Enable the Mobile Threat Defense connector in Intune for unenrolled devices

During Mobile Threat Defense (MTD) setup, you've configured a policy for classifying threats in your Mobile Threat Defense partner console and you've created the app protection policy in Intune. If you've already configured the Intune connector in the MTD partner console, you can now enable the MTD connection for MTD partner applications.

> [!NOTE] 
> This article applies to all Mobile Threat Defense partners that support app protection policies: Better Mobile (Android), Zimperium (iOS), Lookout for Work (Android/iOS).

## To enable the MTD connector

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).

2. On the **Intune Dashboard**, choose **Device compliance**, then choose **Mobile Threat Defense** under the **Setup** section.

3. On the **Mobile Threat Defense** pane, choose **Add**.

4. Choose your MTD solution as the **Mobile Threat Defense connector to setup** from the drop-down list.

    <!-- ![MTD setup in Intune](PLACEHOLDER, need a new screenshot of this page) -->

5. Enable the toggle options according to your organization's requirements. Toggle options visible will vary depending on the MTD partner.

## MTD toggle options

You can decide which MTD toggle options you need to enable according to your organization's requirements. Here are more details:

**App Protection Policy Settings**
- **Connect Android devices of version 4.1 and above to *\<MTD partner name>* for app protection policy evaluation**: When you enable this option, app protection policies using the Device Threat Level rule will evaluate devices including data from this connector.
- **Connect iOS devices version 8.0 and above to *\<MTD partner name>* for app protection policy evaluation**: When you enable this option, app protection policies using the Device Threat Level rule will evaluate devices including data from this connector.

**Common Shared Settings**
- **Number of days until partner is unresponsive**: Number of days of inactivity before Intune considers the partner to be unresponsive because the connection is lost. Intune ignores compliance state for unresponsive MTD partners.

> [!TIP]
> You can see the **Connection status** and the **Last synchronized** time between Intune and the MTD partner from the Mobile Threat Defense pane.

> [!NOTE] 
> When you enable the Mobile Threat Defense connection to Intune, Intune creates a classic conditional access policy in Azure Active Directory. Each MTD app you integrate, including [Defender ATP](advanced-threat-protection.md) or any of our additional [MTD partners](mobile-threat-defense.md#mobile-threat-defense-partners), creates a new classic conditional access policy. **These policies can be ignored, but should not be edited, deleted, or disabled.**
> 
> Classic conditional access policies for MTD apps: 
> - Are used by Intune MTD to require that devices are registered in Azure AD so that they have a device ID before communicating to MTD partners. The ID is required so that devices and can successfully report their status to Intune.  
> - Have no effect on any other Cloud apps or Resources.  
> - Are distinct from conditional access policies you might create to help manage MTD, or for Require App Protection CA
> - By default, don’t interact with other conditional access policies you use for evaluation.  
>
> To view classic conditional access policies, in [Azure](https://portal.azure.com/#home), go to **Azure Active Directory** > **Conditional Access** > **Classic policies**.

## Next Steps

- [Create Mobile Threat Defense (MTD) app protection policy with Intune](~/protect/mtd-app-protection-policy.md).