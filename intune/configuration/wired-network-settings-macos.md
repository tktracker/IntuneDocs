---
# required metadata

title: Configure wired network settings for macOS devices in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Create or add a wired network device configuration profile for macOS devices. See the different settings, including adding certificates, choosing an EAP type, and selecting an authentication method in Microsoft Intune. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/10/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add wired network settings for macOS devices in Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

You can create a profile with specific wired network settings, and then deploy this profile to your macOS devices. Microsoft Intune offers many features, including authenticating to your network, adding a PKCS or SCEP certificate, and more. 

## Before you begin

[Create a device profile](device-profile-create.md).

> [!NOTE]
> These settings are available for all enrollment types. For more information on the enrollment types, see [macOS enrollment](../enrollment/macos-enroll.md).

## Profiles

- **Profile type**: Choose **Wired network**.
- **Network Interface**: Choose which of the network interfaces on the device the profile applies to, based on service-order priority. Options that include active in the title will use interfaces that are actively working on the device. If there are no active interfaces, the next interface in service-order priority will be configured. First active Ethernet is selected by default, which is also the default setting configured by macOS itself.

  Your options:
  
  - **First active Ethernet**
  - **Second active Ethernet**
  - **Third active Ethernet**
  - **First Ethernet**
  - **Second Ethernet**
  - **Third Ethernet**
  - **Any Ethernet**

- **EAP type**: Choose the Extensible Authentication Protocol (EAP) type used to authenticate secured wireless connections. Your options:
  - **EAP-FAST**: Enter the **Protected Access Credential (PAC) Settings**. This option uses protected access credentials to create an authenticated tunnel between the client and the authentication server. Your options:
    - **Do not use (PAC)**
    - **Use (PAC)**: If an existing PAC file exists, use it.
    - **Use and Provision PAC**: Create and add the PAC file to your devices.
    - **Use and Provision PAC Anonymously**: Create and add the PAC file to your devices without authenticating to the server.
  - **EAP-TLS**: Also enter:
    - **Server Trust** - **Certificate server names**: **Add** one or more common names used in the certificates issued by your trusted certificate authority (CA). When you enter this information, you can bypass the dynamic trust window displayed on user's devices when they connect to this network.
    - **Root certificate for server validation**: Choose an existing trusted root certificate profile. This certificate is presented to the server when the client connects to the network, and is used to authenticate the connection.
    - **Client Authentication** - **Client certificate for client authentication (Identity certificate)**: Choose the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.
    - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.
  - **EAP-TTLS**: Also enter:
    - **Server Trust** - **Certificate server names**: **Add** one or more common names used in the certificates issued by your trusted certificate authority (CA). When you enter this information, you can bypass the dynamic trust window displayed on user's devices when they connect to this network.
    - **Root certificate for server validation**: Choose an existing trusted root certificate profile. This certificate is presented to the server when the client connects to the network, and is used to authenticate the connection.
    - **Client Authentication** - Choose an **Authentication method**. Your options:
      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method (inner identity)**: Choose how you authenticate the connection. Be sure you choose the same protocol that's configured on your network. Your options: 
          - **Unencrypted password (PAP)**
          - **Challenge Handshake Authentication Protocol (CHAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP Version 2 (MS-CHAP v2)**
      - **Certificates**: Choose the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.
      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.
  - **LEAP**
  - **PEAP**: Also enter:
    - **Server Trust** - **Certificate server names**: **Add** one or more common names used in the certificates issued by your trusted certificate authority (CA). When you enter this information, you can bypass the dynamic trust window displayed on user's devices when they connect to this network.
    - **Root certificate for server validation**: Choose an existing trusted root certificate profile. This certificate is presented to the server when the client connects to the network, and is used to authenticate the connection.
    - **Client Authentication** - Choose an **Authentication method**. Your options:
      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. 
      - **Certificates**: Choose the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.
      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

## Next steps

The profile is created, but it's not doing anything. Next, [assign this profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
