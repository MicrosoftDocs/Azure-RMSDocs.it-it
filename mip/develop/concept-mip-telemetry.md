---
title: Concepts - The core concepts in the MIP SDK - Telemetry Control
description: This article will help you understand how to opt out of telemetry and which events are still sent when opted out.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 10/01/2019
ms.author: tommos
ms.openlocfilehash: 3d97bdbf5307d7f0faefe6b6434b1df1ebc67798
ms.sourcegitcommit: 487e681c9683b8adb7ae6fcfb374830bf0e5ad72
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2019
ms.locfileid: "74484854"
---
# <a name="microsoft-information-protection-sdk---telemetry-configuration"></a>Microsoft Information Protection SDK - Telemetry Configuration

## <a name="telemetry"></a>Telemetria

By default, the Microsoft Information Protection SDK sends telemetry data to Microsoft. This telemetry data is useful for troubleshooting bugs, quality, and performance issues across the SDK install base that we may not capture in our internal testing. When implementing your application with the SDK, it's important to give users and admins the ability to opt out of telemetry if required.

## <a name="telemetry-configuration"></a>Telemetry Configuration

Telemetry options in the MIP SDK can be controlled via [TelemetryConfiguration](https://docs.microsoft.com/dotnet/api/microsoft.informationprotection.telemetryconfiguration?view=mipsdk-dotnet). Create an instance of this class, then set **IsTelemetryOptedOut** to true. Provide the object of class **TelemetryConfiguration** to the function used to create **MipContext**. This doesn't completely eliminate telemetry data, but reduces to a minimum set with all end-user identifiable information scrubbed.

### <a name="minimum-telemetry-events"></a>Minimum Telemetry Events

When telemetry is set to *opted out*, a minimum set of data is sent to Microsoft. All personally identifiable information is scrubbed from this information. This data includes heartbeat information to understand that the SDK is being used, and system metadata. **No user content or end user identifiable information is set to the service.**

Review the tables below to see exactly what events and data are sent with minimum telemetry set.

#### <a name="event-heartbeat"></a>Event: Heartbeat

| Name                                 | Description                                                                            | Scrubbed |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| App.ApplicationId                    | The application identifier provided via mip::ApplicationInfo.                          | No       |
| App.ApplicationName                  | The application name provided via mip::ApplicationInfo.                                | No       |
| App.ApplicationVersion               | The application version profided via mip::ApplicationInfo.                             | No       |
| ApplicationId                        | The application version profided via mip::ApplicationInfo.                             | No       |
| ApplicationName                      | The application name provided via mip::ApplicationInfo.                                | No       |
| CreationTime                         | Time event was generated.                                                              | No       |
| DefaultLabel.Id                      | Tenant default label ID.                                                               | No       |
| Engine.TenantId                      | Home tenant GUID of the authenticated user.                                            | No       |
| Engine.UserObjectId                  | User object ID in Azure Active Directory.                                              | No       |
| Event.CorrelationId                  | Generated unique ID associated with object that triggered the event.                   | No       |
| Event.CorrelationIdDescription       | C++ class name of object that triggered the event.                                     | No       |
| Event.ParentCorrelationId            | Parent event correlation ID.                                                           | No       |
| Event.ParentCorrelationIdDescription | Generated Unique ID associated with the parent of the object that triggered the event. | No       |
| Event.UniqueId                       | Generated unique ID assigned to the event.                                             | No       |
| MachineName                          | Name of the system that generated the event.                                           | **Sì**  |
| MIP.Version                          | Version of the MIP SDK.                                                                | No       |
| Operazione                            | Heartbeat                                                                              | No       |
| OrganizationId                       | Home tenant GUID of the authenticated user.                                            | No       |
| Piattaforma                             | Operating system version.                                                              | No       |
| ProcessName                          | Name of the process using the SDK.                                                     | No       |
| ProductVersion                       | Same as “App.ApplicationVersion”.                                                      | No       |
| SDKVersion                           | Same as MIP.Version.                                                                   | No       |
| UserId                               | Indirizzo di posta elettronica dell'utente.                                                             | **Sì**  |
| UserObjectId                         | Azure AD object ID of the user.                                                        | No       |
| Versione                              | Audit version schema (“1.1”).                                                          | No       |

#### <a name="event-discovery"></a>Event: Discovery

| Name                                 | Description                                                                            | Scrubbed |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | Unique action ID for this event, used for event correlation.                           | No       |
| App.ApplicationId                    | The application identifier provided via mip::ApplicationInfo.                          | No       |
| App.ApplicationName                  | The application name provided via mip::ApplicationInfo.                                | No       |
| App.ApplicationVersion               | The application version profided via mip::ApplicationInfo.                             | No       |
| ApplicationId                        | The application version profided via mip::ApplicationInfo.                             | No       |
| ApplicationName                      | The application name provided via mip::ApplicationInfo.                                | No       |
| CreationTime                         | Time event was generated.                                                              | No       |
| DataState                            | The state of the data as the application acts on it “REST”, “MOTION”, “USE”.           | No       |
| DefaultLabel.Id                      | Tenant default label identifier.                                                       | No       |
| Engine.TenantId                      | Home tenant GUID of the authenticated user.                                            | No       |
| Engine.UserObjectId                  | User object identifier in Azure Active Directory.                                      | No       |
| Event.CorrelationId                  | Generated unique ID associated with object that triggered the event.                   | No       |
| Event.CorrelationIdDescription       | C++ class name of object that triggered the event.                                     | No       |
| Event.ParentCorrelationId            | Parent event correlation ID.                                                           | No       |
| Event.ParentCorrelationIdDescription | Generated Unique ID associated with the parent of the object that triggered the event. | No       |
| Event.UniqueId                       | Generated unique ID assigned to the event.                                             | No       |
| LabelId                              | Content label identifier on the opened file or data.                                   | No       |
| MachineName                          | Name of the system that generated the event.                                           | **Sì**  |
| MIP.Version                          | Version of the MIP SDK.                                                                | No       |
| ObjectId                             | File path/description of the file or data.                                             | **Sì**  |
| Operazione                            | "Discovery".                                                                           | No       |
| OrganizationId                       | Home tenant GUID of the authenticated user.                                            | No       |
| Piattaforma                             | Operating system version.                                                              | No       |
| ProcessName                          | Name of the process using the SDK.                                                     | No       |
| Protetto                            | Bool indicating if the file is protected or not.                                       | No       |
| Protection                           | The protection template identifier.                                                    | **Sì**  |
| ProtectionOwner                      | Email address of the protection owner.                                                 | **Sì**  |
| SDKVersion                           | Same as MIP.Version.                                                                   | No       |
| UserId                               | Indirizzo di posta elettronica dell'utente.                                                             | **Sì**  |
| UserObjectId                         | Azure AD object ID of the user.                                                        | No       |
| Versione                              | Audit version schema (“1.1”).                                                          | No       |

#### <a name="event-label-change"></a>Event: Label Change

| Name                                 | Description                                                                            | Scrubbed |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | Unique action ID for this event, used for event correlation.                           | No       |
| ActionIdBefore                       | Previous action ID. Used to chain to new action ID.                                    | No       |
| ActionSource                         | Value of MIP::ActionSource.                                                            | No       |
| App.ApplicationId                    | The application ID provided via mip::ApplicationInfo.                                  | No       |
| App.ApplicationName                  | The application name provided via mip::ApplicationInfo.                                | No       |
| App.ApplicationVersion               | The application version profided via mip::ApplicationInfo.                             | No       |
| ApplicationId                        | The application ID provided via mip::ApplicationInfo.                                  | No       |
| ApplicationName                      | The application name provided via mip::ApplicationInfo.                                | No       |
| CreationTime                         | Time the event was generated.                                                          | No       |
| DataState                            | The state of the data as the application acts on it “REST”, “MOTION”, “USE”.           | No       |
| DefaultLabel.Id                      | Tenant default label identifier.                                                       | No       |
| Engine.TenantId                      | Home tenant GUID of the authenticated user.                                            | No       |
| Engine.UserObjectId                  | User object identifier in Azure Active Directory.                                      | No       |
| Event.CorrelationId                  | Generated unique ID associated with object that triggered the event.                   | No       |
| Event.CorrelationIdDescription       | C++ class name of object that triggered the event.                                     | No       |
| Event.ParentCorrelationId            | Parent event correlation ID.                                                           | No       |
| Event.ParentCorrelationIdDescription | Generated Unique ID associated with the parent of the object that triggered the event. | No       |
| Event.UniqueId                       | Generated unique ID assigned to the event.                                             | No       |
| IsLabelChanged                       | Bool indicating if the label changed.                                                  | No       |
| IsProtectionChanged                  | Bool indicating if protection changed.                                                 | No       |
| LabelId                              | Label ID that is to be applied to the file or data.                                    | No       |
| LabelIdBefore                        | Previous label ID that was on the file or data.                                        | No       |
| MachineName                          | Name of the system that generated the event.                                           | **Sì**  |
| MIP.Version                          | Version of the MIP SDK.                                                                | No       |
| ObjectId                             | File path/description of the file or data.                                             | **Sì**  |
| Operazione                            | "Change".                                                                              | No       |
| OrganizationId                       | Home tenant GUID of the authenticated user.                                            | No       |
| Piattaforma                             | Operating system version.                                                              | No       |
| ProcessName                          | Name of the process using the SDK.                                                     | No       |
| Product Version                      |                                                                                        | No       |
| Protetto                            | Bool indicating if the file is protected or not.                                       | No       |
| Protected Before                     | Bool indicating if the file was previously protected or not.                           | No       |
| Protection                           | The protection template identifier.                                                    | No       |
| Protection Before                    | The previous protection template identifier.                                           | No       |
| ProtectionContentId                  | The new content identifier (GUID).                                                     | No       |
| ProtectionContentIdBefore            | The previous content identifier (GUID).                                                | No       |
| ProtectionOwner                      | Email address of the protection owner.                                                 | **Sì**  |
| ProtectionOwnerBefore                | Previous email address of the protection owner.                                        | **Sì**  |
| SDKVersion                           | Same as MIP.Version.                                                                   | No       |
| UserId                               | Indirizzo di posta elettronica dell'utente.                                                             | **Sì**  |
| UserObjectId                         | Azure AD object ID of the user.                                                        | No       |
| Versione                              | Audit version schema (“1.1”).                                                          | No       |


### <a name="opting-out-in-c"></a>Opting out in C++

To set telemetry to minimum only, create a shared pointer of **mip::TelemetryConfiguration()** and set **isTelemetryOptedOut** to true. Pass the configuration object in to **MipContent::Create()** .

```cpp
auto telemetryConfig = std::make_shared<mip::TelemetryConfiguration>();                                     
telemetryConfig->isTelemetryOptedOut = true;
                       
// Create MipContext, passing in mip::TelemetryConfiguration object.
mMipContext = mip::MipContext::Create(
    mAppInfo,
    "mip_data",
    mip::LogLevel::Trace,
    false,
    nullptr /*loggerDelegateOverride*/,
    telemetryConfig /*telemetryOverride*/
);
```

### <a name="opting-out-in-net"></a>Opting out in .NET

To set telemetry to minimum only, create a **TelemetryConfiguration()** object and set **isTelemetryOptedOut** to true. Pass the configuration object in to **MIP.CreateMipContext()** .

```csharp
TelemetryConfiguration telemetryConfiguration = new TelemetryConfiguration();
telemetryConfiguration.IsTelemetryOptedOut = true;

// Create MipContext, passing in TelemetryConfiguration object.
mipContext = MIP.CreateMipContext(appInfo, 
    "mip_data", 
    LogLevel.Trace, 
    null, 
    telemetryConfiguration);
```

