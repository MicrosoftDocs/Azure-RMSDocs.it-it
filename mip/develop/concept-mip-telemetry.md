---
title: 'Concetti: i concetti di base del controllo MIP SDK-telemetria'
description: Questo articolo consente di comprendere come rifiutare esplicitamente i dati di telemetria e quali eventi vengono comunque inviati quando vengono esclusi.
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
# <a name="microsoft-information-protection-sdk---telemetry-configuration"></a>Microsoft Information Protection SDK-configurazione della telemetria

## <a name="telemetry"></a>Telemetria

Per impostazione predefinita, Microsoft Information Protection SDK invia i dati di telemetria a Microsoft. Questi dati di telemetria sono utili per la risoluzione dei problemi relativi a bug, qualità e prestazioni nella base di installazione dell'SDK che potrebbero non essere acquisiti nei test interni. Quando si implementa l'applicazione con l'SDK, è importante fornire agli utenti e agli amministratori la possibilità di rifiutare esplicitamente i dati di telemetria, se necessario.

## <a name="telemetry-configuration"></a>Configurazione della telemetria

Le opzioni di telemetria nell'SDK MIP possono essere controllate tramite [TelemetryConfiguration](https://docs.microsoft.com/dotnet/api/microsoft.informationprotection.telemetryconfiguration?view=mipsdk-dotnet). Creare un'istanza di questa classe, quindi impostare **IsTelemetryOptedOut** su true. Fornire l'oggetto della classe **TelemetryConfiguration** alla funzione utilizzata per creare **MipContext**. Questa operazione non elimina completamente i dati di telemetria, ma si riduce a un set minimo con tutte le informazioni identificabili dall'utente finale rimosse.

### <a name="minimum-telemetry-events"></a>Eventi di telemetria minimi

Quando la telemetria è impostata su *opt-out*, un set di dati minimo viene inviato a Microsoft. Tutte le informazioni personali vengono rimosse da queste informazioni. Questi dati includono informazioni sull'heartbeat per comprendere che l'SDK è in uso e i metadati di sistema. **Nessun contenuto utente o informazioni identificabili dall'utente finale è impostato sul servizio.**

Esaminare le tabelle seguenti per visualizzare esattamente gli eventi e i dati inviati con un set di telemetria minimo.

#### <a name="event-heartbeat"></a>Evento: heartbeat

| Nome                                 | Descrizione                                                                            | Pulitura |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| App. ApplicationId                    | Identificatore dell'applicazione fornito tramite MIP:: ApplicationInfo.                          | No       |
| App. ApplicationName                  | Nome dell'applicazione fornito tramite MIP:: ApplicationInfo.                                | No       |
| App. ApplicationVersion               | Versione dell'applicazione profided tramite MIP:: ApplicationInfo.                             | No       |
| ApplicationId                        | Versione dell'applicazione profided tramite MIP:: ApplicationInfo.                             | No       |
| ApplicationName                      | Nome dell'applicazione fornito tramite MIP:: ApplicationInfo.                                | No       |
| CreationTime                         | È stato generato l'evento Time.                                                              | No       |
| DefaultLabel.Id                      | ID etichetta predefinito del tenant.                                                               | No       |
| Motore. TenantId                      | GUID del tenant Home dell'utente autenticato.                                            | No       |
| Motore. UserObjectId                  | ID oggetto utente in Azure Active Directory.                                              | No       |
| Event. CorrelationId                  | ID univoco generato associato all'oggetto che ha attivato l'evento.                   | No       |
| Event. CorrelationIdDescription       | C++nome della classe dell'oggetto che ha attivato l'evento.                                     | No       |
| Event. ParentCorrelationId            | ID di correlazione dell'evento padre.                                                           | No       |
| Event. ParentCorrelationIdDescription | ID univoco generato associato al padre dell'oggetto che ha attivato l'evento. | No       |
| Event. UniqueId                       | ID univoco generato assegnato all'evento.                                             | No       |
| MachineName                          | Nome del sistema che ha generato l'evento.                                           | **Sì**  |
| MIP. Versione                          | Versione di MIP SDK.                                                                | No       |
| Operazione                            | Heartbeat                                                                              | No       |
| OrganizationId                       | GUID del tenant Home dell'utente autenticato.                                            | No       |
| Piattaforma                             | Versione del sistema operativo.                                                              | No       |
| ProcessName                          | Nome del processo che utilizza l'SDK.                                                     | No       |
| ProductVersion                       | Uguale a "app. ApplicationVersion".                                                      | No       |
| SDKVersion                           | Uguale a MIP. Versione.                                                                   | No       |
| UserId                               | Indirizzo di posta elettronica dell'utente.                                                             | **Sì**  |
| UserObjectId                         | Azure AD ID oggetto dell'utente.                                                        | No       |
| Versione                              | Schema della versione di controllo ("1,1").                                                          | No       |

#### <a name="event-discovery"></a>Evento: individuazione

| Nome                                 | Descrizione                                                                            | Pulitura |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | ID di azione univoco per questo evento, usato per la correlazione degli eventi.                           | No       |
| App. ApplicationId                    | Identificatore dell'applicazione fornito tramite MIP:: ApplicationInfo.                          | No       |
| App. ApplicationName                  | Nome dell'applicazione fornito tramite MIP:: ApplicationInfo.                                | No       |
| App. ApplicationVersion               | Versione dell'applicazione profided tramite MIP:: ApplicationInfo.                             | No       |
| ApplicationId                        | Versione dell'applicazione profided tramite MIP:: ApplicationInfo.                             | No       |
| ApplicationName                      | Nome dell'applicazione fornito tramite MIP:: ApplicationInfo.                                | No       |
| CreationTime                         | È stato generato l'evento Time.                                                              | No       |
| dataState                            | Lo stato dei dati quando l'applicazione agisce su "REST", "MOTION", "USE".           | No       |
| DefaultLabel.Id                      | Identificatore di etichetta predefinito del tenant.                                                       | No       |
| Motore. TenantId                      | GUID del tenant Home dell'utente autenticato.                                            | No       |
| Motore. UserObjectId                  | Identificatore dell'oggetto utente in Azure Active Directory.                                      | No       |
| Event. CorrelationId                  | ID univoco generato associato all'oggetto che ha attivato l'evento.                   | No       |
| Event. CorrelationIdDescription       | C++nome della classe dell'oggetto che ha attivato l'evento.                                     | No       |
| Event. ParentCorrelationId            | ID di correlazione dell'evento padre.                                                           | No       |
| Event. ParentCorrelationIdDescription | ID univoco generato associato al padre dell'oggetto che ha attivato l'evento. | No       |
| Event. UniqueId                       | ID univoco generato assegnato all'evento.                                             | No       |
| LabelId                              | Identificatore dell'etichetta del contenuto nel file o nei dati aperti.                                   | No       |
| MachineName                          | Nome del sistema che ha generato l'evento.                                           | **Sì**  |
| MIP. Versione                          | Versione di MIP SDK.                                                                | No       |
| ObjectId                             | Percorso/Descrizione del file o dei dati.                                             | **Sì**  |
| Operazione                            | "Individuazione".                                                                           | No       |
| OrganizationId                       | GUID del tenant Home dell'utente autenticato.                                            | No       |
| Piattaforma                             | Versione del sistema operativo.                                                              | No       |
| ProcessName                          | Nome del processo che utilizza l'SDK.                                                     | No       |
| Protetto                            | Bool che indica se il file è protetto o meno.                                       | No       |
| Protection                           | Identificatore del modello di protezione.                                                    | **Sì**  |
| ProtectionOwner                      | Indirizzo di posta elettronica del proprietario della protezione.                                                 | **Sì**  |
| SDKVersion                           | Uguale a MIP. Versione.                                                                   | No       |
| UserId                               | Indirizzo di posta elettronica dell'utente.                                                             | **Sì**  |
| UserObjectId                         | Azure AD ID oggetto dell'utente.                                                        | No       |
| Versione                              | Schema della versione di controllo ("1,1").                                                          | No       |

#### <a name="event-label-change"></a>Evento: modifica dell'etichetta

| Nome                                 | Descrizione                                                                            | Pulitura |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | ID di azione univoco per questo evento, usato per la correlazione degli eventi.                           | No       |
| ActionIdBefore                       | ID azione precedente. Utilizzato per concatenare al nuovo ID di azione.                                    | No       |
| ActionSource                         | Valore di MIP:: ActionSource.                                                            | No       |
| App. ApplicationId                    | ID applicazione fornito tramite MIP:: ApplicationInfo.                                  | No       |
| App. ApplicationName                  | Nome dell'applicazione fornito tramite MIP:: ApplicationInfo.                                | No       |
| App. ApplicationVersion               | Versione dell'applicazione profided tramite MIP:: ApplicationInfo.                             | No       |
| ApplicationId                        | ID applicazione fornito tramite MIP:: ApplicationInfo.                                  | No       |
| ApplicationName                      | Nome dell'applicazione fornito tramite MIP:: ApplicationInfo.                                | No       |
| CreationTime                         | Ora di generazione dell'evento.                                                          | No       |
| dataState                            | Lo stato dei dati quando l'applicazione agisce su "REST", "MOTION", "USE".           | No       |
| DefaultLabel.Id                      | Identificatore di etichetta predefinito del tenant.                                                       | No       |
| Motore. TenantId                      | GUID del tenant Home dell'utente autenticato.                                            | No       |
| Motore. UserObjectId                  | Identificatore dell'oggetto utente in Azure Active Directory.                                      | No       |
| Event. CorrelationId                  | ID univoco generato associato all'oggetto che ha attivato l'evento.                   | No       |
| Event. CorrelationIdDescription       | C++nome della classe dell'oggetto che ha attivato l'evento.                                     | No       |
| Event. ParentCorrelationId            | ID di correlazione dell'evento padre.                                                           | No       |
| Event. ParentCorrelationIdDescription | ID univoco generato associato al padre dell'oggetto che ha attivato l'evento. | No       |
| Event. UniqueId                       | ID univoco generato assegnato all'evento.                                             | No       |
| IsLabelChanged                       | Bool che indica se l'etichetta è stata modificata.                                                  | No       |
| IsProtectionChanged                  | Bool che indica se la protezione è cambiata.                                                 | No       |
| LabelId                              | ID dell'etichetta da applicare al file o ai dati.                                    | No       |
| LabelIdBefore                        | ID etichetta precedente che si trovava nel file o nei dati.                                        | No       |
| MachineName                          | Nome del sistema che ha generato l'evento.                                           | **Sì**  |
| MIP. Versione                          | Versione di MIP SDK.                                                                | No       |
| ObjectId                             | Percorso/Descrizione del file o dei dati.                                             | **Sì**  |
| Operazione                            | "Modifica".                                                                              | No       |
| OrganizationId                       | GUID del tenant Home dell'utente autenticato.                                            | No       |
| Piattaforma                             | Versione del sistema operativo.                                                              | No       |
| ProcessName                          | Nome del processo che utilizza l'SDK.                                                     | No       |
| Versione prodotto                      |                                                                                        | No       |
| Protetto                            | Bool che indica se il file è protetto o meno.                                       | No       |
| Protetto prima                     | Bool che indica se il file è stato precedentemente protetto o meno.                           | No       |
| Protection                           | Identificatore del modello di protezione.                                                    | No       |
| Protezione prima                    | Identificatore del modello di protezione precedente.                                           | No       |
| ProtectionContentId                  | Nuovo identificatore di contenuto (GUID).                                                     | No       |
| ProtectionContentIdBefore            | Identificatore del contenuto precedente (GUID).                                                | No       |
| ProtectionOwner                      | Indirizzo di posta elettronica del proprietario della protezione.                                                 | **Sì**  |
| ProtectionOwnerBefore                | Indirizzo di posta elettronica precedente del proprietario della protezione.                                        | **Sì**  |
| SDKVersion                           | Uguale a MIP. Versione.                                                                   | No       |
| UserId                               | Indirizzo di posta elettronica dell'utente.                                                             | **Sì**  |
| UserObjectId                         | Azure AD ID oggetto dell'utente.                                                        | No       |
| Versione                              | Schema della versione di controllo ("1,1").                                                          | No       |


### <a name="opting-out-in-c"></a>Opt-out inC++

Per impostare la telemetria solo sul valore minimo, creare un puntatore condiviso di **MIP:: TelemetryConfiguration ()** e impostare **isTelemetryOptedOut** su true. Passare l'oggetto di configurazione in a **MipContent:: Create ()** .

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

### <a name="opting-out-in-net"></a>Rifiuto esplicito in .NET

Per impostare la telemetria solo sul valore minimo, creare un oggetto **TelemetryConfiguration ()** e impostare **isTelemetryOptedOut** su true. Passare l'oggetto di configurazione in **MIP. CreateMipContext ()** .

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

