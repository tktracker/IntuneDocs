---
# required metadata

title: Create Mobile Threat Defense (MTD) app protection policy with Intune
titleSuffix: Microsoft Intune
description: Create Mobile Threat Defense (MTD) app protection policy with Microsoft Intune.
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


# Create Mobile Threat Defense app protection policy with Intune

> [!NOTE] 
> This article applies to all Mobile Threat Defense (MTD) partners that support app protection policies: Better Mobile (Android), Zimperium (iOS), Lookout for Work (Android/iOS).

Intune with MTD helps you detect threats and assess risk on mobile devices. You can create an Intune app protection policy that assesses risk to determine if the device is allowed access to corporate data or not. 

## Before you begin

As part of the MTD setup, in the MTD partner console, you created a policy that classifies various threats as high, medium, and low. You now need to set the Mobile Threat Defense level in the Intune app protection policy.

Prerequisites for app protection policy with MTD:

- Set up MTD integration with Intune. Without this integration, the MTD app protection policy will have no effect.

## To create an MTD app protection policy

1. Go to the [Azure portal](https://portal.azure.com/), and sign in with your Intune credentials.

2. On the **Azure Dashboard**, choose **All services** from the left menu, then type **Intune** in the text box filter.

3. Choose **Intune**, the **Intune Dashboard** opens.

4. On the **Intune Dashboard**, choose **Client apps**, then choose **App protection policies** under the **Manage** section.

5. Choose **Create policy**, enter the **Name**, **Description**, select the **Platform**. 

6. On the **Conditional launch** pane, under the **Device conditions** table, choose the Mobile Threat Level from the drop-down list under the **Max allowed device threat level**.

    a.  **Secured**: This level is the most secure. The device cannot have any threats present and still access company resources. If any threats are found, the device is evaluated as noncompliant.

    b.  **Low**: The device is compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.

    c.  **Medium**: The device is compliant if the threats found on the device are low or medium level. If high-level threats are detected, the device is determined as noncompliant.

    d.  **High**: This level is the least secure. This allows all threat levels, and uses Mobile Threat Defense for reporting purposes only. Devices are required to have the MTD app activated with this setting.

7. Click **Save** twice, then choose **Create**.

## To assign an MTD app protection policy

To assign a device compliance policy to users, choose a policy that you have previously configured. Existing policies can be found in the **Device compliance – policies** pane.

1. Choose the policy you want to assign to users and choose **Assignments**. This action opens the pane where you can select **Azure Active Directory Security Groups** and assign them to the policy.

2. Choose **Select groups to include** to open the pane that displays the Azure AD Security Groups. Choosing **Select** deploys the policy to users.

> [!NOTE] 
> You have applied the policy to users. The devices used by the users who are targeted by the policy are evaluated for access to corporate data on targeted apps via Intune app protection.

## Next steps  

- Learn more about [Mobile Threat Defense](~/protect/mobile-threat-defense.md) in Microsoft Intune.
