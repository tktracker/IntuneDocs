---
# required metadata

title: Create and deploy app protection policies 
titleSuffix: Microsoft Intune
description: This topic describes how to create and assign Microsoft Intune app protection policies (APP).
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 10/16/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: f31b2964-e932-4cee-95c4-8d5506966c85

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# How to create and assign app protection policies

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Learn how to create and assign Microsoft Intune app protection policies (APP) for users of your organization. This topic also describes how to make changes to existing policies.

## Before you begin

App protection policies can apply to apps running on devices that may or may not be managed by Intune. For a more detailed description of how app protection policies work and the scenarios that are supported by Intune app protection policies, see [What are Microsoft Intune app protection policies?](app-protection-policy.md)

If you're looking for a list of MAM supported apps, see [MAM apps list](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).

For information about adding your organization's line-of-business (LOB) apps to Microsoft Intune to prepare for app protection policies, see [Add apps to Microsoft Intune](apps-add.md).

Currently, the process flow to create an app protection policy differs based on platform:
- App protection policies for iOS/iPadOS and Android apps
- App protection policies for Windows 10 apps

## App protection policies for iOS/iPadOS and Android apps

When you create an app protection policy for iOS/iPadOS and Android apps, you follow a modern Intune process flow that results in a new app protection policy.

### Create an iOS/iPadOS or Android app protection policy
1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
2. In Intune portal, choose **Client apps** > **App protection policies**. This selection opens the **App protection policies** details, where you create new policies and edit existing policies.
3. Select **Create policy** and select either **iOS/iPadOS** or **Android**. The **Create policy** blade is displayed.
4. On the **Basics** page, add the following values:

    | Value | Description |
    |--------------|------------------------------------------------|
    | Name | The name of this app protection policy. |
    | Description | [Optional] The description of this app protection policy. |


    The **Platform** value is set based on your above choice.

    ![Screenshot of the Basics page of the Create policy blade](~/apps/media/app-protection-policies/app-protection-add-policies-01.png)

5. Click **Next** to display the **Apps** page.<br>
    The **Apps** page allows you to choose how you want to apply this policy to apps on different devices. You must add at least one app.<p>
    
    | Value/Option | Description |
    |-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Target to apps on all devices types | Use this option to target your policy to apps on devices of any management state. Choose **No**  to target apps on specific devices types. |
    |     Device types | Use this option to specify whether this policy applies to MDM managed devices or unmanaged devices. For iOS APP policies, select from **Unmanaged** and **Managed** devices. For Android APP policies, select from **Unmanaged**, **Android device administrator**, and **Android Enterprise**.  |
    | Public apps | Click **Select public apps** to choose the apps to target. |
    | Custom apps | Click **Select custom apps** to select custom apps to target based on a Bundle ID. |
    
    The app(s) you have selected will appear in the public and custom apps list. 
6. Click **Next** to display the **Data protection** page.<br>
    This page provides settings for data loss prevention (DLP) controls, including cut, copy, paste, and save-as restrictions. These settings determine how users interact with data in the apps that this app protection policy applies.​

    **Data protection settings**:<br>
    - **iOS/iPadOS data protection** - For information, see [iOS app protection policy settings - Data protection](~/apps/app-protection-policy-settings-ios.md#data-protection).
    - **Android data protection** - For information, see [Android app protection policy settings - Data protection](~/apps/app-protection-policy-settings-android.md#data-protection).

7. Click **Next** to display the **Access requirements** page.<br>
    This page provides settings to allow you to configure the PIN and credential requirements that users must meet to access apps in a work context. 
 
    **Access requirements settings**:<br>
    - **iOS/iPadOS access requirements** - For information, see [iOS app protection policy settings - Access requirements](~/apps/app-protection-policy-settings-ios.md#access-requirements).
    - **Android access requirements** - For information, see [Android app protection policy settings - Access requirements](~/apps/app-protection-policy-settings-android.md#access-requirements).

8. Click **Next** to display the **Conditional launch** page.<br>
    This page provides settings to set the sign-in security requirements for your app protection policy. Select a **Setting** and enter the **Value** that users must meet to sign in to your company app. Then select the **Action** you want to take if users do not meet your requirements. In some cases, multiple actions can be configured for a single setting.

    **Conditional launch settings**:<br>
    - **iOS/iPadOS conditional launch** - For information, see [iOS app protection policy settings - Conditional launch](~/apps/app-protection-policy-settings-ios.md#conditional-launch).
    - **Android conditional launch** - For information, see [Android app protection policy settings - Conditional launch](~/apps/app-protection-policy-settings-android.md#conditional-launch).

7. Click **Next** to display the **Assignments** page.<br>
   The **Assignments** page allows you can assign the app protection policy to groups of users. 
8. Click **Next: Review + create** to review the values and settings you entered for this app protection policy.
9. When you are done, click **Create** to create the app protection policy in Intune. 

## App protection policies for Windows 10 apps

When you create an app protection policy for Windows 10 apps, you will following a classic Intune process flow.

### Create a Windows 10 app protection policy
1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
2. In Intune portal,choose **Client apps** > **App protection policies**. This selection opens the **App protection policies** details, where you create new policies and edit existing policies.
3. Select **Create policy**.

    <img alt="Screenshot of the 'Create policy' blade for Windows 10" src="~/apps/media/app-protection-policies/app-protection-add-policy.png" width="350">

4. Specify a name for the policy, add a brief description, and select the platform type for your policy. You can create more than one policy for each platform.

4. You can choose to **Target to all app types**. This option allows you to target your policy to apps on devices of any management state. During policy conflict resolution, this setting will be superseded if a user has a policy targeted for a specific management state. For more information, see [Target app protection policies based on device management state](~/apps/app-protection-policies.md#target-app-protection-policies-based-on-device-management-state).

5. Select **Apps** to open the **Apps** blade, where a list of available apps is displayed. Select one or more apps from the list that you want to associate with the policy that you're creating. Select at least one app to create a policy.  

6. Once you've selected the apps, choose **Select** to save your selection.

7. On the **Add a policy** blade, select **Configure required settings** to open **Settings**.

   There are three categories of policy settings:
   - **Data protection** - This group includes the data loss prevention (DLP) controls, like cut, copy, paste, and save-as restrictions. These settings determine how users interact with data in the apps.
   - **Access requirements** - This group contains the per-app PIN options that determine how the end user accesses the apps in a work context.  
   - **Conditional launch** - This group holds settings like the minimum OS settings, jailbreak and rooted device detection, and offline grace periods.

   To get you started, the policy settings have default values. If the default values meet your requirements, you don't have to make any changes.

   > [!TIP]
   > These policy settings are enforced only when using apps in the work context. When end users use the app to do a personal task, they aren't affected by these policies. Note that when you create a new file it is considered a personal file. 

8. Select **OK** to save this configuration. You're now back in the **Add a policy** blade.
9. Select **Create** to create the policy and save your settings.

New Windows 10 policies that you create aren't assigned to any users until you explicitly do so. To assign a Windows 10 policy, see [Assign a Windows 10 policy to users](~/apps/app-protection-policies.md#assign-a-windows-10-policy-to-users)

### Assign a Windows 10 policy to users 

1. In the **App protection policies** pane, select a policy.

2. In the ***Intune App Protection** pane, select **Assignments** to open the **Intune App Protection - Assignments** pane. On the *Include* tab, select **Select groups to include**. 

   ![Screenshot of the Assignments pane with Select groups to include menu](./media/app-protection-policies/app-protection-policy-add-users.png)

3. A list of all the security groups in your **Azure Active Directory** is displayed. Select the user groups that you want this policy to apply to, and then choose **Select**. 

    ![Screenshot of the Add user group pane with list of Azure AD users](./media/app-protection-policies/azure-ad-user-group-list.png)

4. After you include and exclude groups, select **Save** to save the configuration and deploy the policy to users. If you select **Discard** before you save your configuration, you will discard all changes you've made to the *Include* and *Exclude* tabs.   
 
     ![Screenshot showing the save and discard options](./media/app-protection-policies/save-assignment.png)
  
You've now created a policy and deployed it to users.

Only users with assigned Microsoft Intune licenses are affected by the policy. Users in the selected security group that don’t have an assigned Intune license aren't affected.

>[!IMPORTANT]
> If you're using Intune with Configuration Manager to manage your devices, the policy is only applied to the users directly in the group that you selected. Members of child groups nested within the group you selected aren't affected.

End users can download the apps from the App store or Google Play. For more information, see:
* [What to expect when your Android app is managed by app protection policies](../fundamentals/end-user-mam-apps-android.md)
* [What to expect when your iOS app is managed by app protection policies](../fundamentals/end-user-mam-apps-ios.md)

### Change existing Windows 10 policies
You can edit an existing policy and apply it to the targeted users. However, when you change existing policies, users who are already signed in to the apps won’t see the changes for an eight-hour period.

To see the effect of the changes immediately, the end user must sign out of the app, and then sign back in.

### To change the list of apps associated with the policy

1. In the **App protection policies** pane, select the policy you want to change.

2. In the *Intune App Protection* pane, select **Targeted apps** to open the list of apps.

3. Remove or add apps from the list and then select the **Save** icon to save your changes.

#### To change the list of user groups

1. In  the **App protection policies** pane, select the policy you want to change.

2. In the *Intune App Protection* pane, select **Assignments** to open the **Intune App Protection - Assignments** pane that shows the list of current user groups who have this policy.

3. To add a new user group to the policy, on the *Include* tab choose **Select groups to include**, and select the user group. Choose **Select** to add the group. 

4. To exclude a user group, on the *Exclude* tab choose **Select groups to exclude**, and select the user group. Choose **Select** to remove the user group.  

5. To delete groups that were added previously, on either the *Include* or *Exclude* tabs, select the ellipsis (...) and select **Delete**. 

5. After your changes to the assignments are ready, select **Save** to save the configuration and deploy the policy to the new set of users. If you select **Discard** before you save your configuration, you will discard all changes you've made to the *Include* and *Exclude* tabs.

### To change Windows 10 policy settings

1. In the **App protection policies** pane, choose the policy you want to change.

2. In the *Intune App Protection* pane, select **Properties** to open the list of settings areas you can edit. 

3. Select the settings area with the settings you want to change, like **Data relocation** or **Access requirements**. Then change the settings to new values.

4. Select the **Save** icon to save your changes. Repeat the process to select a settings area and modify and then save your changes, until all your changes are complete. You can then close the *Intune App Protection - Properties* pane. 

## Target app protection policies based on device management state
In many organizations, it’s common to allow end users to use both Intune Mobile Device Management (MDM) managed devices, such as corporate owned devices, and un-managed devices protected with only Intune app protection policies. Unmanaged devices are often known as Bring Your Own Devices (BYOD).

Because Intune app protection policies target a user’s identity, the protection settings for a user can apply to both enrolled (MDM managed) and non-enrolled devices (no MDM). Therefore, you can target an Intune app protection policy to either Intune enrolled or unenrolled iOS and Android devices. You can have one protection policy for unmanaged devices in which strict data loss prevention (DLP) controls are in place, and a separate protection policy for MDM managed devices, where the DLP controls may be a little more relaxed. For more information how this works on personal Android Enterprise devices, see [App protection policies and work profiles](android-deployment-scenarios-app-protection-work-profiles.md).

To create these policies, browse to **Client apps** > **App protection policies** in the Intune console, and then select **Create Policy**. You can also edit an existing app protection policy. To have the app protection policy apply to both managed and un-managed devices, navigate to the **Apps** page and confirm that **Target to apps on all device types** is set to **Yes**, the default value. If you want to granularly assign based on management state, set **Target to apps on all device types**  to **No**. 

![Screenshot of the Add a policy blade with Target to all app types](./media/app-protection-policies/app-protection-policies-target-all.png)

### App types

- **Apps on unmanaged devices**: Unmanaged devices are devices where Intune MDM management has not been detected. This includes 3rd party MDM vendors.
- **Apps on Intune managed devices**: Managed devices are managed by Intune MDM.
- **Apps in Android Work Profile**: Managed devices that have been enrolled as Android Enterprise work profile devices.

> Note
> Android devices will prompt to install the Intune Company Portal app regardless of which App type is chosen. For example, if you select 'Apps on Intune managed devices' then users with unmanaged Android devices will still be prompted.

For iOS, additional app configuration settings are required to target app protection policy (APP) settings to apps on Intune enrolled devices:

- **IntuneMAMUPN** must be configured for all MDM managed applications. For more information, see [How to manage data transfer between iOS apps in Microsoft Intune](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).
- **IntuneMAMDeviceID** must be configured for all Third-party and LOB MDM managed applications. The **IntuneMAMDeviceID** should be configured to the device ID token. For example, `key=IntuneMAMDeviceID, value={{deviceID}}`. For more information, see [Add app configuration policies for managed iOS devices](app-configuration-policies-use-ios.md).
- If only the **IntuneMAMDeviceID** is configured, the Intune APP will consider the device as unmanaged.

> [!NOTE]
> For specific iOS support information about app protection policies based on device management state, see [MAM protection policies targeted based on management state](../fundamentals/whats-new-archive.md#mam-protection-policies-targeted-based-on-management-state-).

## Policy settings
To see a full list of the policy settings for iOS and Android, select one of the following links:

- [iOS policies](app-protection-policy-settings-ios.md)
- [Android policies](app-protection-policy-settings-android.md)

## Next steps
[Monitor compliance and user status](app-protection-policies-monitor.md)

## See also
* [What to expect when your Android app is managed by app protection policies](../fundamentals/end-user-mam-apps-android.md)
* [What to expect when your iOS app is managed by app protection policies](../fundamentals/end-user-mam-apps-ios.md)
